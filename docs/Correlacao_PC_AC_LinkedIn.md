# Correlação: Plano de Chamadas (PC) × Ache um Veterano (AC) × LinkedIn

**Objetivo:** Gerar uma base do que precisa ser criado no aplicativo, correlacionando o que já existe no PC e no AC com as funcionalidades do LinkedIn descritas em `IdeiaPrincipalDotrabalho.md`, alinhado ao ideal do projeto em `README.md`.

---

## 1. O que PC e AC já oferecem (equivalente ao LinkedIn)

### 1.1 Perfil profissional (currículo online)

| LinkedIn | Plano de Chamadas (PC) | Ache um Veterano (AC) |
|----------|------------------------|------------------------|
| Foto e banner profissional | ✅ Postar fotos minhas | — |
| Headline / título profissional | ✅ Área/Cargo Pretendido | — |
| Sobre / resumo profissional | ✅ Criar um "sobre mim" | — |
| Experiências de trabalho | ✅ Experiência Profissional | — |
| Formação acadêmica | ✅ Educação | — |
| Certificações | ✅ Documentos (diplomas, certificados, etc.) | — |
| Habilidades (skills) | ✅ Soft Skills, Hard Skills | — |
| Links / destaques | ✅ Colocar links | — |
| Informações complementares | ✅ Informações Complementares | — |
| Editar perfil | ✅ Editar meu perfil | — |

**Conclusão:** O PC já cobre a maior parte da estrutura de perfil profissional; o app deve **replicar e unificar** esse modelo (perfil único que serve para PC e AC).

---

### 1.2 Vagas e recrutamento

| LinkedIn | Plano de Chamadas (PC) | Ache um Veterano (AC) |
|----------|------------------------|------------------------|
| Buscar vagas | ✅ Vê oportunidades | ✅ Filtros de busca (Área, Cargo, Cidade, Estado) |
| Ver minhas candidaturas | ✅ Vê minhas candidaturas | — |
| Publicar vagas (empresa) | — | ✅ Vê e criar Minhas Vagas |
| Filtrar candidatos | — | ✅ Veteranos em Destaque + filtros (Área, Cargo, Cidade, Estado) |

**Conclusão:** PC foca no **candidato** (ver vagas e candidaturas); AC foca no **empresa/recrutador** (ver veteranos e publicar vagas). O app deve integrar os dois fluxos no estilo LinkedIn Jobs.

---

### 1.3 Documentos e comprovação

| LinkedIn | Plano de Chamadas (PC) | Ache um Veterano (AC) |
|----------|------------------------|------------------------|
| Certificações no perfil | ✅ Envio de documentos (diplomas, certificados, CT, reservista, etc.) | — |
| Testes/avaliações | ✅ Teste de Lógica, Interpretação, Personalidade | — |

**Conclusão:** O PC já tem **documentos e testes** além do que o LinkedIn mostra no perfil; o app pode manter esse diferencial (perfil + documentos verificáveis) como valor para empresas.

---

### 1.4 Aprendizado (cursos)

| LinkedIn (Learning) | Plano de Chamadas (PC) | Ache um Veterano (AC) |
|--------------------|------------------------|------------------------|
| Cursos profissionais / certificados | ✅ Vê cursos de Capacitação | — |
| Participação em eventos | ✅ Participar de Workshop | — |

**Conclusão:** O PC já oferece **cursos e workshops**; no app isso equivale ao “Sistema de Aprendizado” (cursos, certificações) previsto no README.

---

## 2. Resumo: o que é comum ou idêntico ao LinkedIn

- **Perfil profissional:** PC já cobre experiência, educação, skills, sobre mim, fotos, links e edição de perfil → **base para “currículo online” no app.**
- **Vagas:** PC = candidato (ver vagas, candidaturas); AC = empresa (ver veteranos, filtros, criar vagas) → **equivalente ao sistema de vagas e recrutamento do LinkedIn.**
- **Documentos e testes:** PC tem upload de documentos e testes (lógica, interpretação, personalidade) → **complementa o perfil no estilo LinkedIn com foco em verificação.**
- **Cursos e workshops:** PC tem capacitação e workshops → **equivalente ao LinkedIn Learning / sistema de aprendizado do app.**

---

## 3. O que precisa ser CRIADO (existe no LinkedIn / README, não detalhado no PC ou AC)

Com base em `IdeiaPrincipalDotrabalho.md` e `README.md`:

### 3.1 Networking (Rede de contatos)

- Adicionar conexões  
- Seguir profissionais  
- Seguir empresas  
- Mensagens privadas (chat)  
- Mensagens em grupo  
- Pedidos de recomendação  
- Ver conexões em comum  
- Sugestões de pessoas para conectar  

**Status no PC/AC:** Não descrito → **a implementar no app.**

---

### 3.2 Criação de conteúdo (feed)

- Post de texto, imagens, vídeos, documentos  
- Enquetes, artigos  
- Curtir, comentar, compartilhar, repost  

**Status no PC/AC:** Não descrito → **a implementar no app.**

---

### 3.3 Páginas de empresas

- Página institucional  
- Publicar vagas e conteúdo  
- Cultura, funcionários, produtos/serviços  
- Estatísticas de seguidores  

**Status no PC/AC:** AC tem “Minhas Vagas”; não há descrição de página de empresa completa → **a implementar no app.**

---

### 3.4 Estatísticas (analytics)

- Quem viu seu perfil  
- Alcance das postagens  
- Crescimento de seguidores  
- Aparições em busca  
- Engajamento de conteúdo  

**Status no PC/AC:** Não descrito → **a implementar no app.**

---

### 3.5 Comunidades e grupos

- Grupos profissionais  
- Discussões e compartilhamento dentro do grupo  

**Status no PC/AC:** Não descrito → **a implementar no app (conforme README).**

---

### 3.6 Recursos adicionais (podem ser fase posterior)

- Eventos online / lives  
- Newsletter  
- Recursos premium (quem viu perfil, insights, etc.)  
- Recursos de IA (sugestão de vagas, melhorar perfil, etc.)  

**Status no PC/AC:** Não descrito → **a definir em backlog.**

---

## 4. Base do que precisa ser criado (checklist do app)

Com base na correlação acima e no ideal do projeto:

| # | Funcionalidade | Origem | Prioridade sugerida |
|---|----------------|--------|----------------------|
| 1 | Perfil profissional unificado (foto, banner, headline, sobre, experiência, educação, skills, links) | PC + LinkedIn | Alta |
| 2 | Upload de documentos e testes (lógica, interpretação, personalidade) | PC | Alta |
| 3 | Sistema de vagas: buscar, candidatar, salvar, alertas (lado candidato) | PC + LinkedIn | Alta |
| 4 | Sistema de vagas: publicar vagas, ver candidatos, filtros (área, cargo, cidade, estado) (lado empresa) | AC + LinkedIn | Alta |
| 5 | Cursos de capacitação e workshops | PC + README | Média |
| 6 | Chat (mensagens privadas e em grupo) | LinkedIn / IdeiaPrincipal | Alta |
| 7 | Feed: postar, curtir, comentar, compartilhar, repost | LinkedIn / IdeiaPrincipal | Alta |
| 8 | Networking: conexões, seguir pessoas/empresas, sugestões | LinkedIn / README | Alta |
| 9 | Páginas de empresas (perfil, vagas, cultura) | LinkedIn / README | Média |
| 10 | Comunidades e grupos | README / IdeiaPrincipal | Média |
| 11 | Estatísticas (quem viu perfil, alcance, engajamento) | LinkedIn / README | Média |
| 12 | Recomendações de colegas | LinkedIn | Média |

---

## 5. Observações finais

- **PC** é a principal fonte de **perfil do candidato** (sobre mim, experiência, educação, skills, documentos, testes, cursos, vagas e candidaturas).  
- **AC** é a principal fonte de **visão empresa/recrutador** (ver veteranos em destaque, filtros, criar e gerenciar vagas).  
- O **LinkedIn** (via IdeiaPrincipal e README) define o **escopo completo** do app: perfil + vagas + networking + conteúdo + empresas + aprendizado + analytics.  

Este documento serve como **base para o backlog**: o que já está “mapeado” pelo PC e AC pode ser reutilizado ou adaptado; o que só existe no LinkedIn ou no README precisa ser criado do zero no aplicativo.
