# Plano de Desenvolvimento – Rede Profissional para Veteranos

**Documento:** Plano completo de desenvolvimento do aplicativo  
**Base:** [Relatorio_Projeto.md](Relatorio_Projeto.md) (inclui correlação PC × AC × LinkedIn em anexo), README e documentação do projeto  
**Objetivo:** Definir arquitetura, fases, ordem de implementação e critérios de entrega.

---

## 1. Visão geral do plano

### 1.1 Fluxo de entrada: login com dois tipos de usuário

O aplicativo **inicia na tela de login**. Nela o usuário escolhe como deseja entrar:

- **Entrar como candidato** – acessa a interface voltada ao veterano/candidato (perfil, vagas, candidaturas, documentos, testes, cursos – dados da API do PC).
- **Entrar como empresa** – acessa a interface voltada ao recrutador/empresa (veteranos em destaque, Minhas Vagas, candidatos – dados da API do AC).

Ou seja: **duas interfaces dentro do mesmo app**, definidas pelo tipo de login. Após autenticação, o app redireciona para a interface correspondente (candidato ou empresa). A navegação, abas e telas são diferentes conforme o tipo de usuário.

### 1.2 Fases do desenvolvimento

O desenvolvimento segue uma abordagem **incremental e por fases**, priorizando:

1. **Fundação técnica** – tela de login com opção candidato/empresa; ambiente e integração com as APIs (PC e AC).
2. **Valor central** – vagas (interface candidato e interface empresa), que é o diferencial PC + AC.
3. **Engajamento** – networking, feed e chat (estilo LinkedIn).
4. **Complementos** – aprendizado, páginas de empresas, comunidades, estatísticas.

Requisitos transversais em todas as fases: **segurança (API, criptografia, LGPD)**, **uso mínimo de bateria e memória**, **responsividade** e **aviso de conectividade**.

---

## 2. Stack e arquitetura técnica

### 2.1 Fonte dos dados: APIs do PC e do AC

**Os dados do aplicativo vêm das APIs das plataformas existentes:**

- **API do Plano de Chamadas (PC)** – planodechamadas.com.br  
  Perfil do candidato, documentos, testes, cursos, workshops, oportunidades (vagas) e candidaturas.

- **API do Ache um Veterano (AC)** – acheumveterano.com.br  
  Veteranos em destaque, filtros de busca (área, cargo, cidade, estado), vagas publicadas pelas empresas (Minhas Vagas).

O app **não possui banco de dados próprio** para esses domínios: ele **consome as APIs do PC e do AC**. A autenticação do usuário (login/sessão) dependerá do que essas APIs oferecerem (ex.: token único ou tokens separados por plataforma).

Funcionalidades que **não** existem hoje no PC nem no AC (feed, chat, networking, comunidades, estatísticas) podem exigir:
- **Opção A:** uma **API complementar em Node.js** (backend do projeto) com banco próprio apenas para esses recursos; ou  
- **Opção B:** futura expansão das APIs do PC/AC, se houver parceria.

Este plano considera **Opção A** para feed, chat e networking, mantendo **perfil, vagas, documentos, testes e aprendizado** sempre via **APIs do PC e do AC**.

### 2.2 Visão geral da arquitetura

```
┌─────────────────────────────────────────────────────────────────┐
│                    APLICATIVO (React Native)                     │
│  Android (prioridade) │ Código preparado para iOS                 │
└───────┬─────────────────────────────┬───────────────────────────┘
        │ HTTPS / REST                 │ HTTPS / REST (e WebSocket)
        ▼                             ▼
┌───────────────────┐         ┌───────────────────────────────────┐
│   API Plano de    │         │  API Ache um Veterano (AC)         │
│   Chamadas (PC)   │         │  Vagas, veteranos em destaque,     │
│   Perfil, docs,   │         │  filtros (área, cargo, cidade,      │
│   testes, cursos, │         │  estado), Minhas Vagas (empresa)   │
│   vagas/candidat. │         │                                    │
└───────────────────┘         └───────────────────────────────────┘
        │
        │  (dados oficiais; fonte primária)
        │
        └──────────────────────┬──────────────────────────────────┘
                               │
        ┌──────────────────────┴──────────────────────────────────┐
        │  API complementar (Node.js) – apenas se necessário      │
        │  Para: chat, feed, networking, grupos (não existem no     │
        │  PC/AC). Autenticação pode ser delegada ao PC ou própria │
        └──────────────────────┬──────────────────────────────────┘
                               │
                               ▼
                    ┌───────────────────┐
                    │  Banco próprio    │
                    │  (só para chat,    │
                    │   feed, conexões) │
                    └───────────────────┘
```

### 2.3 Frontend (obrigatório)

| Item | Escolha | Observação |
|------|---------|------------|
| Framework | React Native | Exigência do projeto; permite futuro iOS |
| Linguagem | JavaScript ou TypeScript | TypeScript recomendado para tipagem e manutenção |
| Navegação | React Navigation | Padrão para RN; suporta stack, tab, drawer |
| Estado global | Context API / Zustand / Redux (um deles) | Definir no início; útil para auth e perfil |
| Requisições HTTP | axios ou fetch + camada de API | Centralizar baseURL e interceptors (token, erro de rede) |
| Formulários | React Hook Form + validação (ex.: Zod/Yup) | Perfil, vagas, postagens |
| Armazenamento local | AsyncStorage | Token, preferências, cache leve |
| Upload de arquivos | react-native-document-picker + multipart | Documentos e fotos do perfil |

### 2.4 Consumo das APIs do PC e do AC (fonte principal dos dados)

| Aspecto | Observação |
|--------|------------|
| **Documentação** | Obter documentação oficial das APIs do PC e do AC (endpoints, autenticação, formatos). |
| **Autenticação** | Tela de login com opção **candidato** (API do PC) e **empresa** (API do AC). Verificar se existe login unificado (um token para ambas) ou dois fluxos (PC para candidato, AC para empresa). O tipo de usuário define qual interface exibir após o login. |
| **Cliente HTTP no app** | Um módulo por API (ex.: `api/pc.js`, `api/ac.js`) ou camada unificada; tratar erros e timeout. Candidato usa predominantemente PC; empresa usa predominantemente AC. |
| **Cache local** | AsyncStorage ou cache em memória para reduzir chamadas e melhorar performance (perfil, lista de vagas). |
| **Segurança** | Usar HTTPS; não armazenar senhas no app; seguir recomendações das APIs (tokens, refresh). |

O **banco de dados** de perfil, vagas, documentos, testes e cursos **vem das APIs do PC e do AC**, não é criado nem mantido pelo projeto.

### 2.5 Backend complementar (Node.js) – apenas para o que PC/AC não oferecem

Se o projeto implementar feed, chat e networking, será necessário um backend próprio **apenas** para esses recursos:

| Item | Escolha | Observação |
|------|---------|------------|
| Runtime | Node.js | Exigência do projeto |
| Uso | Chat, feed, conexões, grupos | Perfil, vagas, documentos, testes, cursos = APIs PC e AC |
| Banco de dados | PostgreSQL ou MongoDB | Apenas para mensagens, posts, conexões, grupos |
| Autenticação | Pode delegar ao PC (token) ou manter sessão própria vinculada ao usuário do PC/AC | Definir com a disponibilidade das APIs |
| Chat em tempo real | WebSockets (Socket.io ou ws) ou Firebase/Pusher | Só para mensagens do app |

### 2.6 Segurança (transversal)

- **HTTPS** em produção.
- **Senhas:** hash com bcrypt (ou argon2); nunca em texto puro.
- **Dados sensíveis:** criptografia em repouso para documentos e campos críticos; alinhado à LGPD.
- **API:** rate limiting, CORS restrito, headers de segurança.
- **Token:** tempo de vida curto para access token; refresh token opcional com rotação.
- **LGPD:** consentimento, finalidade, mínimo de dados; documentação de base legal e retenção.

### 2.7 Requisitos não funcionais (do projeto)

- **Bateria e memória:** evitar polling; usar WebSocket ou push para notificações; otimizar listas (virtualização) e imagens.
- **Responsividade:** layouts flexíveis (Dimensions, percentuais, breakpoints se necessário); testar em vários tamanhos de tela.
- **Conectividade:** detectar estado da rede (NetInfo); tela ou aviso “É necessária conexão com a internet”; desabilitar ações que dependem da API quando offline.
- **Usabilidade:** navegação clara, feedback visual (loading, sucesso/erro), acessibilidade básica.

---

## 3. Estrutura de pastas sugerida

### 3.1 Repositório (monorepo ou separado)

**Opção A – Monorepo (recomendado):**

```
TrabalhoExetensionista/
├── README.md
├── docs/                    # documentação (já existente)
├── app/                     # React Native (obrigatório)
│   ├── src/
│   │   ├── api/             # clientes para API do PC e API do AC (+ complementar se houver)
│   │   ├── components/
│   │   ├── contexts/
│   │   ├── navigation/
│   │   ├── screens/
│   │   ├── hooks/
│   │   ├── store/
│   │   ├── theme/
│   │   └── utils/
│   ├── App.tsx
│   └── package.json
├── api/                     # Node.js (opcional – só para feed, chat, networking se não vierem do PC/AC)
│   ├── src/
│   │   ├── controllers/
│   │   ├── middlewares/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   │   └── config/
│   ├── server.js
│   └── package.json
└── package.json             # scripts raiz (opcional)
```

**Fonte dos dados:** Perfil, vagas, documentos, testes e cursos vêm das **APIs do PC e do AC**; o app consome essas APIs. A pasta `api/` só é necessária para funcionalidades que as APIs do PC/AC não oferecem (ex.: feed, chat, conexões).

### 3.2 App (React Native)

- **Fluxo de entrada:** tela de login (raiz) com opção **candidato** ou **empresa**; após login, navegação diferente para cada tipo (duas interfaces no mesmo app).
- **screens:** organizar por contexto: `auth/` (login), `candidato/` (perfil, vagas, candidaturas, documentos, etc.), `empresa/` (veteranos em destaque, Minhas Vagas, candidatos); telas comuns (ex.: feed, chat) podem ficar em pasta compartilhada.
- **components:** reutilizáveis (botões, cards, inputs, listas); alguns específicos por interface (ex.: card de vaga para candidato vs card de candidato para empresa).
- **api:** cliente HTTP para API do PC e API do AC (baseURL, interceptors, funções por domínio).
- **navigation:** login → roteamento condicional (navigator candidato ou navigator empresa); stacks e tabs definidos por tipo de usuário.
- **contexts/store:** usuário logado, **tipo de usuário (candidato | empresa)**, perfil resumido, preferências.

### 3.3 API (Node.js)

- **routes:** agrupar por domínio (auth, users, profile, jobs, posts, messages, etc.).
- **controllers:** orquestram request/response e chamam services.
- **services:** regras de negócio e acesso a dados.
- **models:** entidades (User, Profile, Job, Application, Post, Message, etc.).
- **middlewares:** auth, validação, erro global, rate limit.

---

## 4. Fases do desenvolvimento

As fases estão ordenadas por **dependência lógica** e **prioridade de negócio** (conforme [Relatorio_Projeto.md](Relatorio_Projeto.md)).

---

### Fase 0: Fundação e ambiente (sprint 0)

**Objetivo:** App rodando; integração com as **APIs do PC e do AC** (fonte dos dados); autenticação conforme ofertada por essas APIs.

| # | Tarefa | Responsável técnico | Entregável |
|---|--------|---------------------|------------|
| 0.1 | Criar projeto React Native (Android); configurar Android Studio e SDK | Frontend | App abre em emulador/dispositivo |
| 0.2 | Configurar navegação: **tela de login** (raiz) e, após login, **duas estruturas de navegação** (stack + tab ou drawer) – uma para candidato, outra para empresa; tema básico | Frontend | Login como raiz; duas interfaces (candidato e empresa) após autenticação |
| 0.3 | Obter documentação das APIs do **PC** e do **AC** (endpoints, autenticação, formatos) | Todos | Documento ou links das APIs |
| 0.4 | Implementar clientes HTTP no app para **API do PC** e **API do AC** (baseURL, headers, tratamento de erro) | Frontend | Módulos `api/pc` e `api/ac` (ou equivalente) |
| 0.5 | **Tela de login inicial:** opção “Entrar como **candidato**” e “Entrar como **empresa**”; integrar com API do PC (candidato) e API do AC (empresa); salvar token/sessão e **tipo de usuário** (AsyncStorage); após login, redirecionar para a **interface candidato** ou **interface empresa** | Frontend | Login com duas opções → duas interfaces no mesmo app |
| 0.6 | Detecção de rede (NetInfo); aviso “conexão necessária” quando offline | Frontend | Componente ou tela de “sem internet” |
| 0.7 | *(Opcional)* Se houver backend complementar (feed/chat): criar projeto Node.js e estrutura; senão, pular para as fases de consumo | Backend | API complementar só se necessário |
| 0.8 | Documentar ambiente (README): como rodar o app, URLs das APIs PC e AC, variáveis de ambiente | Todos | README atualizado |

**Critério de conclusão:** Usuário vê a tela de login com opção “Entrar como candidato” e “Entrar como empresa”; após login, é levado à interface correspondente (candidato ou empresa); app consome as APIs do PC e do AC conforme o tipo; aviso de conectividade funcionando.

---

### Fase 1: Perfil profissional unificado (prioridade alta)

**Objetivo:** Perfil completo (currículo online) no app, consumindo a **API do PC** (perfil, documentos, testes). Dados vêm do PC; o app não possui banco próprio para perfil.

| # | Tarefa | Entregável |
|---|--------|------------|
| 1.1 | Consumir endpoints da **API do PC** para perfil (GET/atualização); mapear campos: foto, banner, headline, sobre, experiência, educação, skills, links | App exibe e edita perfil via API do PC |
| 1.2 | Tela “Meu perfil” (visualização) e “Editar perfil” (formulários por seção); enviar alterações para a API do PC | Telas de perfil e edição no app |
| 1.3 | Upload de foto de perfil e banner via **API do PC** (conforme contrato da API); exibição no app | Fotos no perfil |
| 1.4 | Seções: Experiência profissional, Educação, Soft/Hard Skills, Área/Cargo pretendido, Informações complementares, Links – todos via API do PC | Todas as seções do perfil no app |
| 1.5 | Documentos: consumir upload e listagem da **API do PC** (tipos: CT, reservista, atestado, etc.); telas de envio e listagem no app | Telas de documentos no app |
| 1.6 | Testes (lógica, interpretação, personalidade): consumir endpoints da **API do PC** para realizar e exibir resultado; resumo no perfil | Fluxo de testes no app via API do PC |

**Critério de conclusão:** Candidato vê e edita perfil completo, envia documentos e realiza testes via API do PC; perfil visível no app (dados do PC).

---

### Fase 2: Sistema de vagas – candidato e empresa (prioridade alta)

**Objetivo:** Vagas e candidaturas consumindo **API do PC** (candidato) e **API do AC** (empresa). Dados vêm das APIs; o app não possui banco próprio para vagas.

| # | Tarefa | Entregável |
|---|--------|------------|
| 2.1 | **Candidato:** consumir **API do PC** para listar oportunidades (vagas) e “minhas candidaturas”; mapear filtros se a API oferecer | Busca de vagas e candidaturas no app via PC |
| 2.2 | Candidatura rápida e detalhe da vaga/empresa; enviar candidatura via **API do PC** | Fluxo candidato no app |
| 2.3 | Salvar vagas (favoritos) e alertas: implementar no app (AsyncStorage) ou consumir endpoint do PC se existir | Salvos e alertas no app |
| 2.4 | **Empresa:** consumir **API do AC** para “Veteranos em destaque” com filtros (área, cargo, cidade, estado) | Tela de busca de candidatos no app via AC |
| 2.5 | **Empresa:** consumir **API do AC** para criar/editar “Minhas Vagas” e listar candidatos por vaga | Fluxo empresa no app via AC |
| 2.6 | Unificar experiência no app: mesma navegação para candidato (dados do PC) e empresa (dados do AC), com troca de contexto se necessário | App integrado PC + AC para vagas |

**Critério de conclusão:** Candidato busca vagas e candidata-se via API do PC; empresa publica vagas e vê candidatos via API do AC; dados vêm apenas das APIs.

---

### Fase 3: Networking – conexões e seguir (prioridade alta)

**Objetivo:** Conexões entre usuários, seguir profissionais/empresas, sugestões e conexões em comum.

| # | Tarefa | Entregável |
|---|--------|------------|
| 3.1 | Modelar Conexão (usuário A, usuário B, status: pendente/aceito); Follow (seguir usuário ou empresa) | Tabelas e APIs |
| 3.2 | Ações: enviar pedido de conexão, aceitar/rejeitar, listar conexões e seguidores | Fluxo de conexões no app |
| 3.3 | Sugestões de conexão (ex.: mesma área, conexões em comum); endpoint e tela “Conectar” | Sugestões no feed ou tela dedicada |
| 3.4 | Conexões em comum (ex.: “X conexões em comum com Y”) | Exibição no perfil ou em listas |
| 3.5 | Diferenciar “perfil pessoa” e “perfil empresa” (entidade Company); seguir empresa | Seguir empresas e listar “seguindo” |

**Critério de conclusão:** Usuário envia/aceita conexões, segue pessoas e empresas e vê sugestões e conexões em comum.

---

### Fase 4: Feed de conteúdo (prioridade alta)

**Objetivo:** Postar conteúdo (texto, imagem, vídeo/documento); curtir, comentar, compartilhar e repost.

| # | Tarefa | Entregável |
|---|--------|------------|
| 4.1 | Modelar Post (autor, tipo, conteúdo, mídia, data); Comment e Like; relação repost (post original) | API de posts |
| 4.2 | Criar post (texto + opcional mídia); listar feed (timeline: conexões + próprio); paginação | Feed no app |
| 4.3 | Curtir e descurtir; contagem de curtidas | Interação curtir |
| 4.4 | Comentários: adicionar e listar por post | Comentários no app |
| 4.5 | Compartilhar (repost) e exibir “repostado por” | Repost no feed |
| 4.6 | Notificações leves (ex.: “X curtiu seu post”) – pode ser lista em app primeiro, push depois | Notificações in-app |

**Critério de conclusão:** Usuário publica posts, vê feed, curte, comenta e reposta.

---

### Fase 5: Chat (prioridade alta)

**Objetivo:** Mensagens privadas e em grupo.

| # | Tarefa | Entregável |
|---|--------|------------|
| 5.1 | Definir solução de tempo real (WebSocket na API ou Firebase/Pusher) | Arquitetura de chat documentada |
| 5.2 | Modelar Conversation (1:1 ou grupo), Message (remetente, conteúdo, data); histórico persistido | API de conversas e mensagens |
| 5.3 | Listar conversas (última mensagem, não lida); tela de conversa com histórico e envio | Chat 1:1 no app |
| 5.4 | Criar grupo, adicionar participantes, enviar mensagem no grupo | Chat em grupo no app |
| 5.5 | Indicador de “digitando” e entrega/lida (opcional) | UX de chat |

**Critério de conclusão:** Usuário envia e recebe mensagens em conversas privadas e em grupos.

---

### Fase 6: Cursos e workshops (prioridade média)

**Objetivo:** Sistema de aprendizado (cursos, workshops, certificações).

| # | Tarefa | Entregável |
|---|--------|------------|
| 6.1 | Modelar Course/Workshop (título, descrição, conteúdo ou link, tipo, carga horária); inscrição usuário–curso | API de cursos |
| 6.2 | Listar cursos e workshops; tela de detalhe; “Inscrever-se” e “Meus cursos” | Telas de aprendizado no app |
| 6.3 | Certificado ou conclusão (marcar como concluído); exibir no perfil (badge ou seção) | Certificados no perfil |

**Critério de conclusão:** Usuário vê oferta, se inscreve e conclui cursos; certificação aparece no perfil.

---

### Fase 7: Páginas de empresas, comunidades e estatísticas (prioridade média)

**Objetivo:** Páginas de empresas completas, grupos e analytics básico.

| # | Tarefa | Entregável |
|---|--------|------------|
| 7.1 | Página empresa: perfil institucional, cultura, vagas da empresa, seguidores; edição pelo dono da empresa | Páginas de empresas no app |
| 7.2 | Comunidades/grupos: modelo Group, membros, posts no grupo; listar grupos e entrar/sair | Grupos no app |
| 7.3 | Estatísticas: visualizações de perfil, alcance de posts, crescimento de seguidores; endpoints e tela “Estatísticas” | Analytics básico no app |
| 7.4 | Recomendações: pedir e exibir recomendações no perfil (texto + autor) | Recomendações no perfil |

**Critério de conclusão:** Empresas têm página completa; usuários participam de grupos e veem estatísticas e recomendações.

---

### Fase 8: Ajustes finais, testes e documentação

**Objetivo:** Qualidade, segurança, documentação e preparação para entrega/iOS.

| # | Tarefa | Entregável |
|---|--------|------------|
| 8.1 | Revisão de segurança: HTTPS, criptografia, LGPD (política de privacidade, consentimento) | Checklist de segurança atendido |
| 8.2 | Otimização: listas virtualizadas, redução de chamadas à API, cache de perfil/feed onde fizer sentido | App estável em dispositivos médios |
| 8.3 | Testes manuais (fluxos críticos: login, perfil, vagas, feed, chat); correção de bugs | Lista de testes executada |
| 8.4 | Documentação técnica (ABNT): arquitetura, como rodar, decisões principais; README e docs/ atualizados | Documento final do projeto |
| 8.5 | Preparação para iOS: verificar dependências nativas e configurações (certificado, splash); build de teste se possível | Código pronto para build iOS |

**Critério de conclusão:** Projeto documentado, revisado em segurança e performance e pronto para apresentação e, se aplicável, deploy.

---

## 5. Ordem sugerida e dependências

```
Fase 0 (Fundação) ─────────────────────────────────────────────────────────┐
       │                                                                   │
       ▼                                                                   │
Fase 1 (Perfil) ──────► Fase 2 (Vagas) ───────────────────────────────────┤
       │                     │                                             │
       │                     │  (perfil necessário para candidaturas       │
       │                     │   e “veteranos em destaque”)                 │
       ▼                     ▼                                             │
Fase 3 (Networking) ──► Fase 4 (Feed) ──► Fase 5 (Chat)                    │
       │                     │                 │                           │
       ▼                     ▼                 ▼                           │
Fase 6 (Cursos) ──────► Fase 7 (Empresas, Grupos, Stats) ──► Fase 8 (Polish)│
                                                                           │
Segurança, performance, LGPD e conectividade em todas as fases ◄───────────┘
```

- **Fase 0** é pré-requisito de tudo.
- **Fase 1** é pré-requisito de vagas (candidaturas e busca de candidatos) e de networking/feed (autor de post, perfil na rede).
- **Fase 2** pode ser desenvolvida em paralelo a partes da **Fase 3** após o perfil estável.
- **Fase 3** (conexões) alimenta **Fase 4** (feed da rede) e **Fase 5** (chat entre conexões).
- **Fases 6 e 7** podem ser em paralelo após o núcleo (vagas, networking, feed, chat).
- **Fase 8** ao final de todas as funcionalidades planejadas.

---

## 6. Entregas por fase (resumo)

| Fase | Nome | Entregável principal |
|------|------|----------------------|
| 0 | Fundação | App + API + BD; login/registro; aviso de conectividade |
| 1 | Perfil | Perfil completo, documentos, testes no app |
| 2 | Vagas | Buscar/candidatar/salvar/alertas (candidato); publicar e ver candidatos (empresa) |
| 3 | Networking | Conexões, seguir, sugestões, conexões em comum |
| 4 | Feed | Posts, curtir, comentar, compartilhar, repost |
| 5 | Chat | Mensagens privadas e em grupo |
| 6 | Aprendizado | Cursos, workshops, certificados no perfil |
| 7 | Empresas e mais | Páginas de empresas, grupos, estatísticas, recomendações |
| 8 | Finalização | Segurança, performance, testes, documentação, preparação iOS |

---

## 7. Riscos e atenções

| Risco | Mitigação |
|-------|-----------|
| **Dependência das APIs do PC e do AC** | Garantir documentação e ambiente de homologação; definir fallback (mensagem ao usuário, cache) se API estiver indisponível; tratar erros e timeout no app. |
| Disponibilidade/contrato das APIs | Confirmar com PC e AC acesso às APIs (chaves, CORS, limites); se não houver API pública, considerar mock ou dados demonstração para o trabalho. |
| Escopo grande | Manter MVP nas fases 0–5; fases 6–7 com escopo reduzido se necessário. |
| Chat em tempo real (backend complementar) | Começar com polling ou Firebase; migrar para WebSocket próprio depois se precisar. |
| Documentos sensíveis (LGPD) | Dados e documentos ficam no PC/AC; app apenas exibe/envia; seguir políticas das plataformas e consentimento. |
| Performance em listas longas | Virtualização (FlatList com windowSize); paginação; cache local das respostas das APIs quando fizer sentido. |

---

## 8. Referências internas

- Escopo, backlog e correlação PC × AC × LinkedIn: [Relatorio_Projeto.md](Relatorio_Projeto.md)
- Visão geral do projeto: [README.md](../../README.md) (raiz do repositório)

---

*Este plano deve ser revisado ao início de cada fase e ajustado conforme progresso e mudança de prioridades.*
