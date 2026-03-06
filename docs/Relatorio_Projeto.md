# Relatório do Projeto – Rede Profissional para Veteranos

**Data:** Março de 2025  
**Status:** Em desenvolvimento  
**Tipo:** Trabalho extensionista acadêmico

---

## 1. Resumo Executivo

O projeto consiste no desenvolvimento de um **aplicativo mobile para Android** que funciona como uma **rede social profissional inspirada no LinkedIn**, com foco na **transição de militares e veteranos para o mercado civil**. O app integra e unifica as funcionalidades das plataformas existentes **Plano de Chamadas** (planodechamadas.com.br) e **Ache um Veterano** (acheumveterano.com.br), oferecendo perfil profissional, vagas, networking, feed de conteúdo, chat e aprendizado em um único ambiente.

**Fluxo de entrada:** O aplicativo **inicia com uma tela de login**, na qual o usuário escolhe **entrar como candidato** ou **entrar como empresa**. A partir daí, o app exibe **duas interfaces distintas dentro do mesmo aplicativo**: uma para o candidato (veterano) e outra para a empresa (recrutador), cada uma com suas telas e fluxos específicos.

---

## 2. Contexto e Plataformas de Referência

### 2.1 Plano de Chamadas (PC)

- **Público:** Militares da reserva e veteranos em transição para o mercado civil; empresas parceiras.
- **Foco:** Preparação do candidato (currículo, capacitação, testes, documentos).
- **Já oferece:** Criação de perfil (sobre mim, experiência, educação, soft/hard skills, área/cargo pretendido), upload de documentos (diplomas, certificados, CT, reservista, atestado de conduta, etc.), testes (lógica, interpretação, personalidade), cursos de capacitação, workshops, visualização de oportunidades e de minhas candidaturas, edição de perfil, fotos e links.

### 2.2 Ache um Veterano (AC)

- **Público:** Recrutadores e empresas que buscam veteranos; veteranos que querem ser encontrados.
- **Foco:** Vitrine de talentos e busca especializada.
- **Já oferece:** Veteranos em destaque, filtros (área, cargo, cidade, estado), criação e gestão de “Minhas Vagas” para empresas.

### 2.3 LinkedIn (referência de funcionalidades)

O app deve replicar o conceito de: perfil profissional, networking, vagas, criação de conteúdo (feed), páginas de empresas, comunidades/grupos, estatísticas e sistema de aprendizado, adaptado ao ecossistema PC + AC.

---

## 3. Objetivos do Aplicativo

- Conectar **candidatos (veteranos)** e **empresas/recrutadores** em uma única plataforma.
- Oferecer **perfil profissional unificado** (currículo online) que sirva tanto ao PC quanto ao AC.
- Integrar **busca e publicação de vagas** (lado candidato e lado empresa).
- Incluir **networking** (conexões, seguir, chat, sugestões).
- Permitir **criação de conteúdo** (feed com postagens, curtir, comentar, compartilhar, repost).
- Manter **documentos e testes** como diferencial de verificação para empresas.
- Incluir **cursos e workshops** (sistema de aprendizado).
- Preparar o código para **futura expansão para iOS** (React Native).

---

## 4. Requisitos Técnicos e Restrições

| Aspecto | Requisito |
|--------|-----------|
| **Plataforma** | Android (prioridade); código preparado para iOS |
| **Frontend** | React Native (obrigatório) |
| **Fonte dos dados** | APIs do **Plano de Chamadas (PC)** e do **Ache um Veterano (AC)** – o app consome essas APIs; não há banco de dados próprio para perfil, vagas, documentos, testes e cursos |
| **Backend** | Node.js (opcional; apenas para recursos não oferecidos pelo PC/AC, ex.: feed, chat) |
| **IDE** | Android Studio; Java SDK |
| **Bateria** | Uso mínimo possível |
| **Memória** | Uso mínimo possível |
| **Responsividade** | Interface adaptável a diferentes resoluções |
| **Conectividade** | App sempre conectado; avisar usuário quando internet for necessária |
| **Usabilidade** | Interface intuitiva e fácil de usar |
| **Segurança** | Foco em consumo de dados via API; criptografia |
| **Documentação** | Normas ABNT |
| **Repositório** | GitHub público até apresentação; depois pode ser privado/transferido |
| **Nome do app** | Ainda não definido |

---

## 5. O Que Já Existe (mapeado no PC e no AC)

Com base nos documentos do projeto, o seguinte já está coberto pelas plataformas atuais e deve ser **replicado, unificado ou integrado** no app:

- **Perfil profissional:** foto, banner, headline, sobre mim, experiência, educação, certificações/documentos, habilidades (soft/hard), links, edição de perfil.
- **Documentos e testes:** upload de documentos (incl. certificado de reservista, atestado de conduta, etc.); testes de lógica, interpretação e personalidade.
- **Vagas (candidato):** ver oportunidades, ver minhas candidaturas.
- **Vagas (empresa):** ver veteranos em destaque, filtros (área, cargo, cidade, estado), criar e gerenciar “Minhas Vagas”.
- **Aprendizado:** cursos de capacitação, participação em workshops.

---

## 6. O Que Será Feito (a ser criado no aplicativo)

Resumo do que **não** está descrito no PC/AC e precisa ser **implementado no app**, com base no LinkedIn e no README:

### 6.1 A implementar (prioridade alta)

1. **Perfil profissional unificado**  
   Unificar modelo de perfil (foto, banner, headline, sobre, experiência, educação, skills, links) em um perfil único que sirva ao PC e ao AC.

2. **Upload de documentos e testes**  
   Manter e integrar no app: documentos (diplomas, certificados, CT, reservista, atestado de conduta, etc.) e testes (lógica, interpretação, personalidade).

3. **Sistema de vagas – lado candidato**  
   Buscar vagas, candidatura (incl. candidatura rápida), salvar vagas, alertas de vagas, ver empresa contratante.

4. **Sistema de vagas – lado empresa**  
   Publicar vagas, ver candidatos, filtros (área, cargo, cidade, estado).

5. **Chat**  
   Mensagens privadas e mensagens em grupo.

6. **Feed de conteúdo**  
   Postar texto, imagens, vídeos, documentos; curtir, comentar, compartilhar, repost.

7. **Networking**  
   Adicionar conexões, seguir profissionais e empresas, sugestões de conexão, ver conexões em comum.

### 6.2 A implementar (prioridade média)

8. **Cursos de capacitação e workshops**  
   Integrar oferta de cursos e workshops no app (equivalente ao sistema de aprendizado).

9. **Páginas de empresas**  
   Perfil institucional, publicar vagas e conteúdo, cultura, funcionários, estatísticas de seguidores.

10. **Comunidades e grupos**  
    Grupos profissionais, discussões, compartilhamento.

11. **Estatísticas (analytics)**  
    Quem viu o perfil, alcance das postagens, crescimento de seguidores, aparições em busca, engajamento.

12. **Recomendações de colegas**  
    Pedidos e exibição de recomendações no perfil.

### 6.3 Backlog / fase posterior

- Eventos online e lives  
- Newsletter  
- Recursos premium (ex.: quem viu perfil, insights)  
- Recursos de IA (sugestão de vagas, melhorar perfil, etc.)

---

## 7. Checklist Consolidado (Backlog do App)

| # | Funcionalidade | Origem | Prioridade |
|---|----------------|--------|------------|
| 1 | Perfil profissional unificado (foto, banner, headline, sobre, experiência, educação, skills, links) | PC + LinkedIn | Alta |
| 2 | Upload de documentos e testes (lógica, interpretação, personalidade) | PC | Alta |
| 3 | Vagas: buscar, candidatar, salvar, alertas (candidato) | PC + LinkedIn | Alta |
| 4 | Vagas: publicar, ver candidatos, filtros (empresa) | AC + LinkedIn | Alta |
| 5 | Cursos de capacitação e workshops | PC + README | Média |
| 6 | Chat (mensagens privadas e em grupo) | LinkedIn / IdeiaPrincipal | Alta |
| 7 | Feed: postar, curtir, comentar, compartilhar, repost | LinkedIn / IdeiaPrincipal | Alta |
| 8 | Networking: conexões, seguir pessoas/empresas, sugestões | LinkedIn / README | Alta |
| 9 | Páginas de empresas (perfil, vagas, cultura) | LinkedIn / README | Média |
| 10 | Comunidades e grupos | README / IdeiaPrincipal | Média |
| 11 | Estatísticas (quem viu perfil, alcance, engajamento) | LinkedIn / README | Média |
| 12 | Recomendações de colegas | LinkedIn | Média |

---

## 8. Arquitetura e Stack

- **App:** React Native (Android; preparado para iOS).  
- **Fonte dos dados:** O **banco de dados** (perfil, vagas, documentos, testes, cursos) **vem das APIs do Plano de Chamadas (PC) e do Ache um Veterano (AC)**. O aplicativo consome essas APIs; não há banco de dados próprio para esses domínios.  
- **Backend complementar:** Node.js pode ser usado apenas para funcionalidades que o PC e o AC não oferecem (ex.: feed, chat, networking), com banco próprio somente para esses recursos.  
- **Referência de arquitetura:** Android (AOSP); considerações de bateria, memória e responsividade.  
- **Segurança:** Consumo seguro das APIs (HTTPS, tokens); criptografia e LGPD conforme políticas do PC e do AC.

---

## 9. Entregas e Documentação

- Desenvolvimento em repositório **GitHub** (público até apresentação).  
- Documentação conforme **ABNT**.  
- Para demonstrações após entrega: uso de banco fictício ou próprio, conforme necessidade.

---

## 10. Conclusão

O projeto visa construir um **hub profissional mobile** que una o ecossistema do **Plano de Chamadas** (preparação e perfil do candidato) e do **Ache um Veterano** (visibilidade para empresas e vagas), com as experiências de **networking, feed e chat** inspiradas no LinkedIn. O relatório e o checklist acima definem **o que será feito**: reutilizar e unificar o que já existe no PC e no AC e **criar** networking, feed, chat, páginas de empresas, comunidades, estatísticas e recomendações no aplicativo.

---

*Documento gerado com base em: README.md, docs/IdeiaPrincipalDotrabalho.md, docs/analise/PC.md, docs/analise/AC.md, docs/funcionalidades/Funcionalidades_PC.md, docs/funcionalidades/Funcionalidades_AC.md e docs/Correlacao_PC_AC_LinkedIn.md.*
