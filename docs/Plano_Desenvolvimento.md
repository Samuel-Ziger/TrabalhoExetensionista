# Plano de Desenvolvimento – Rede Profissional para Veteranos

**Documento:** Plano completo de desenvolvimento do aplicativo  
**Base:** [Relatorio_Projeto.md](Relatorio_Projeto.md), [Correlacao_PC_AC_LinkedIn.md](Correlacao_PC_AC_LinkedIn.md), README e documentação do projeto  
**Objetivo:** Definir arquitetura, fases, ordem de implementação e critérios de entrega.

---

## 1. Visão geral do plano

O desenvolvimento segue uma abordagem **incremental e por fases**, priorizando:

1. **Fundação técnica** – ambiente, autenticação e perfil (base de todos os fluxos).
2. **Valor central** – vagas (candidato e empresa), que é o diferencial PC + AC.
3. **Engajamento** – networking, feed e chat (estilo LinkedIn).
4. **Complementos** – aprendizado, páginas de empresas, comunidades, estatísticas.

Requisitos transversais em todas as fases: **segurança (API, criptografia, LGPD)**, **uso mínimo de bateria e memória**, **responsividade** e **aviso de conectividade**.

---

## 2. Stack e arquitetura técnica

### 2.1 Visão geral

```
┌─────────────────────────────────────────────────────────────────┐
│                    APLICATIVO (React Native)                     │
│  Android (prioridade) │ Código preparado para iOS                │
└───────────────────────────────┬─────────────────────────────────┘
                                │ HTTPS / REST (e/ou WebSocket para chat)
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API (Node.js)                              │
│  Autenticação (JWT) │ Validação │ Rate limit │ Logs              │
└───────────────────────────────┬─────────────────────────────────┘
                                │
                ┌───────────────┼───────────────┐
                ▼               ▼               ▼
        ┌───────────┐   ┌───────────┐   ┌───────────┐
        │  Banco    │   │  Storage  │   │  Cache    │
        │  (SQL ou  │   │  (arquivos│   │  (opcional│
        │  NoSQL)   │   │  docs/img)│   │  Redis)   │
        └───────────┘   └───────────┘   └───────────┘
```

### 2.2 Frontend (obrigatório)

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

### 2.3 Backend

| Item | Escolha | Observação |
|------|---------|------------|
| Runtime | Node.js | Exigência do projeto |
| Framework HTTP | Express ou Fastify | Rotas, middleware, tratamento de erros |
| Linguagem | JavaScript ou TypeScript | Consistência com o app |
| Autenticação | JWT (access + refresh opcional) | Login/registro; renovação sem re-login |
| Validação | Joi ou Zod | Body, query, params em todas as rotas |
| Banco de dados | PostgreSQL ou MongoDB | PostgreSQL recomendado para relações (perfil, vagas, conexões); definir modelo de dados cedo |
| ORM/Query | Prisma ou TypeORM (SQL) / Mongoose (NoSQL) | Migrações e modelo único |
| Armazenamento de arquivos | Disco local ou S3-compatible (MinIO, AWS S3) | Documentos e imagens; política de retenção e LGPD |
| Chat em tempo real | WebSockets (Socket.io ou ws) ou serviço (Firebase, Pusher) | Definir na fase de chat |
| Filas (opcional) | Bull (Redis) ou similar | Envio de e-mail, processamento de documentos, alertas |

### 2.4 Segurança (transversal)

- **HTTPS** em produção.
- **Senhas:** hash com bcrypt (ou argon2); nunca em texto puro.
- **Dados sensíveis:** criptografia em repouso para documentos e campos críticos; alinhado à LGPD.
- **API:** rate limiting, CORS restrito, headers de segurança.
- **Token:** tempo de vida curto para access token; refresh token opcional com rotação.
- **LGPD:** consentimento, finalidade, mínimo de dados; documentação de base legal e retenção.

### 2.5 Requisitos não funcionais (do projeto)

- **Bateria e memória:** evitar polling; usar WebSocket ou push para notificações; otimizar listas (virtualização) e imagens.
- **Responsividade:** layouts flexíveis (Dimensions, percentuais, breakpoints se necessário); testar em vários tamanhos de tela.
- **Conectividade:** detectar estado da rede (NetInfo); tela ou aviso “É necessária conexão com a internet”; desabilitar ações que dependem da API quando offline.
- **Usabilidade:** navegação clara, feedback visual (loading, sucesso/erro), acessibilidade básica.

---

## 3. Estrutura de pastas sugerida

### 3.1 Repositório (monorepo ou separado)

**Opção A – Monorepo (recomendado para trabalho acadêmico):**

```
TrabalhoExetensionista/
├── README.md
├── docs/                    # documentação (já existente)
├── app/                     # React Native
│   ├── src/
│   │   ├── api/
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
├── api/                     # Node.js
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

**Opção B – Dois repositórios:** `app-veteranos` (React Native) e `api-veteranos` (Node.js). Útil se backend e frontend forem entregues por times ou prazos diferentes.

### 3.2 App (React Native)

- **screens:** uma pasta por fluxo (auth, perfil, vagas, feed, chat, etc.).
- **components:** reutilizáveis (botões, cards, inputs, listas).
- **api:** cliente HTTP (baseURL, interceptors, funções por domínio).
- **navigation:** stacks e tabs definidos em um lugar só.
- **contexts/store:** usuário logado, perfil resumido, preferências.

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

**Objetivo:** Projeto rodando (app + API + BD), autenticação mínima e deploy local.

| # | Tarefa | Responsável técnico | Entregável |
|---|--------|---------------------|------------|
| 0.1 | Criar projeto React Native (Android); configurar Android Studio e SDK | Frontend | App abre em emulador/dispositivo |
| 0.2 | Configurar navegação (stack + tab ou drawer inicial) e tema básico | Frontend | Navegação e tela placeholder |
| 0.3 | Criar projeto Node.js (Express/Fastify); estrutura de pastas (routes, controllers, services, models) | Backend | API responde em localhost |
| 0.4 | Escolher e configurar banco (PostgreSQL ou MongoDB); definir primeiras entidades (User, Profile básico) | Backend | Migrações/schemas iniciais |
| 0.5 | Implementar registro e login (e-mail/senha); emissão de JWT; rota de “me” | Backend | Post /auth/register, /auth/login, GET /me |
| 0.6 | Tela de login/registro no app; salvar token (AsyncStorage); cliente API com interceptor de token | Frontend | Fluxo login → tela inicial |
| 0.7 | Detecção de rede (NetInfo); aviso “conexão necessária” quando offline | Frontend | Componente ou tela de “sem internet” |
| 0.8 | Documentar ambiente (README no app e na API): como rodar, variáveis de ambiente | Todos | README atualizado |

**Critério de conclusão:** Usuário se registra e faz login no app; API valida JWT e retorna dados do usuário.

---

### Fase 1: Perfil profissional unificado (prioridade alta)

**Objetivo:** Perfil completo (currículo online) no app, alinhado ao PC + LinkedIn.

| # | Tarefa | Entregável |
|---|--------|------------|
| 1.1 | Modelar e implementar entidade Perfil no backend (foto, banner, headline, sobre, experiência, educação, skills, links); CRUD e GET público por ID | API de perfil; perfil editável |
| 1.2 | Tela “Meu perfil” (visualização) e “Editar perfil” (formulários por seção) | Telas de perfil e edição |
| 1.3 | Upload de foto de perfil e banner; armazenamento no servidor; exibição no app | Fotos no perfil |
| 1.4 | Seções: Experiência profissional, Educação, Soft/Hard Skills, Área/Cargo pretendido, Informações complementares, Links | Todas as seções do perfil no app e na API |
| 1.5 | Documentos: modelo de dados (tipo, arquivo, usuário); upload e listagem; tipos conforme PC (CT, reservista, atestado, etc.) | API e telas de documentos |
| 1.6 | Testes: modelo (lógica, interpretação, personalidade); persistir respostas e resultado; exibir no perfil (resumo ou “realizou testes”) | Fluxo de testes no app e na API |

**Critério de conclusão:** Candidato preenche perfil completo, envia documentos e realiza pelo menos um tipo de teste; perfil visível (próprio e, se aplicável, público).

---

### Fase 2: Sistema de vagas – candidato e empresa (prioridade alta)

**Objetivo:** Buscar vagas, candidatar, salvar e alertas (candidato); publicar vagas e ver candidatos com filtros (empresa).

| # | Tarefa | Entregável |
|---|--------|------------|
| 2.1 | Modelar Vagas (empresa, título, descrição, área, cargo, cidade, estado, requisitos, data); CRUD para empresa | API de vagas |
| 2.2 | Candidaturas: vínculo usuário–vaga, status, data; evitar duplicidade | API de candidaturas |
| 2.3 | Listar vagas com filtros (área, cargo, cidade, estado); paginação | Busca de vagas no app |
| 2.4 | Tela “Minhas candidaturas”; candidatura rápida (um toque) e detalhe da vaga/empresa | Fluxo candidato |
| 2.5 | Salvar vagas (favoritos) e alertas (preferências por área/cargo/região); notificação ou lista “Vagas para você” | Salvos e alertas |
| 2.6 | Lado empresa: listar “Veteranos em destaque” (perfis públicos) com filtros (área, cargo, cidade, estado) | API e tela de busca de candidatos |
| 2.7 | Empresa: criar e editar vagas; listar candidatos por vaga (perfil resumido + link para perfil completo) | Fluxo empresa no app |

**Critério de conclusão:** Candidato busca vagas, candidata-se e vê candidaturas; empresa publica vagas e visualiza candidatos com filtros.

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
| Integração com PC/AC reais | Definir cedo se haverá API oficial ou importação; senão, app standalone com dados próprios |
| Escopo grande | Manter MVP nas fases 0–5; fases 6–7 com escopo reduzido se necessário |
| Chat em tempo real complexo | Começar com polling ou Firebase; migrar para WebSocket próprio depois se precisar |
| Armazenamento de documentos (LGPD) | Política de retenção e exclusão; criptografia; acesso apenas autorizado |
| Performance em listas longas | Virtualização (FlatList com windowSize); paginação em todas as listas |

---

## 8. Referências internas

- Escopo e backlog: [Relatorio_Projeto.md](Relatorio_Projeto.md)
- Correlação PC × AC × LinkedIn: [Correlacao_PC_AC_LinkedIn.md](Correlacao_PC_AC_LinkedIn.md)
- Ideia principal e requisitos: [IdeiaPrincipalDotrabalho.md](IdeiaPrincipalDotrabalho.md)
- Visão geral do projeto: [README.md](../README.md) (raiz do repositório)

---

*Este plano deve ser revisado ao início de cada fase e ajustado conforme progresso e mudança de prioridades.*
