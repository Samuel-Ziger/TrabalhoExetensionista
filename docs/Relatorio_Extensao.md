# Relatório de Extensão – Rede Profissional para Veteranos

**Projeto:** Aplicativo mobile de rede profissional para transição de militares e veteranos ao mercado civil  
**Tipo:** Atividade de extensão universitária  
**Documento:** Atende ao roteiro de extensão (diagnóstico, planejamento, encerramento).  
**Referências:** [Relatorio_Projeto.md](Relatorio_Projeto.md), [Plano_Desenvolvimento.md](Plano_Desenvolvimento.md), [Roteiro_Extensao_Mapa.md](Roteiro_Extensao_Mapa.md).

---

# 1 – DIAGNÓSTICO E TEORIZAÇÃO

## 1.1 – Identificação das partes envolvidas e parceiros

### Partes envolvidas e parceiros estratégicos

| Parceiro / Parte | Descrição | Contato / Observação |
|------------------|-----------|----------------------|
| **Plano de Chamadas (PC)** | Plataforma digital focada na transição de carreira de militares (veteranos e reservistas) para o mercado civil. Oferece criação de perfil e currículo, capacitação (cursos e workshops), testes de aptidão e banco de talentos. | Site: https://planodechamadas.com.br/ — [A PREENCHER: nome da instituição/entidade responsável, endereço ou e-mail formal se aplicável] |
| **Ache um Veterano (AC)** | Vitrine de talentos e motor de busca para recrutadores e empresas encontrarem veteranos. Oferece filtros por força, patente, especialidade e região; verificação de credenciais; criação e gestão de vagas pelas empresas. | Site: https://acheumveterano.com.br/ — [A PREENCHER: nome da instituição/entidade responsável, endereço ou e-mail formal se aplicável] |
| **Instituição de ensino** | Responsável pelo projeto extensionista (desenvolvimento do app e atividade de extensão). | [A PREENCHER: nome da instituição, curso, endereço] |
| **Comunidade / público impactado** | Militares da reserva e veteranos em transição para o mercado civil; empresas e recrutadores que buscam contratar veteranos; eventualmente instituições militares que apoiam programas de reinserção. | Ver perfil do público abaixo |

### Público da comunidade e pessoas impactadas

- **Veteranos e militares da reserva:** Indivíduos que encerraram o tempo de serviço ativo (carreira ou temporários) e buscam inserção no setor privado. São impactados na medida em que passam a ter um aplicativo único (mobile) para perfil, vagas, candidaturas, documentos e cursos (dados do PC) e maior visibilidade para empresas (ecossistema AC).
- **Empresas parceiras e recrutadores:** Organizações que buscam perfis com características valorizadas no meio militar (disciplina, liderança, resiliência, pontualidade). São impactadas ao acessarem, no mesmo app, a vitrine de veteranos e a gestão de vagas (dados do AC).
- **Quantidade estimada de participantes / pessoas impactadas:** [A PREENCHER: número estimado com base em dados do PC/AC ou em levantamento próprio]

### Perfil do público (a aprofundar no futuro)

| Dimensão | Observação |
|----------|------------|
| Perfil socioeconômico | [A PREENCHER no futuro: faixa de renda, situação ocupacional antes/depois da reserva] |
| Escolaridade | [A PREENCHER no futuro: nível de formação predominante entre veteranos do público] |
| Gênero e faixa etária | [A PREENCHER no futuro: se houver dados ou estimativas] |
| Dados sociais e território | [A PREENCHER no futuro: regiões, associações de veteranos, etc.] |

### Colaboradores e profissionais envolvidos no projeto

| Função / Papel | Nome / Observação |
|----------------|-------------------|
| Coordenação / orientação | [A PREENCHER] |
| Desenvolvimento (frontend / backend) | [A PREENCHER] |
| Contato com parceiros (PC / AC) | [A PREENCHER] |
| Outros colaboradores | [A PREENCHER] |

---

## 1.2 – Situação-problema identificada

Os problemas ou “dores” que motivam esta atividade de extensão são:

1. **Dificuldade de reinserção no mercado de trabalho civil**  
   Militares que deixam as Forças Armadas (reserva ou desligamento) enfrentam um **abismo entre a vida militar e a civil**: a linguagem, as competências e as experiências da carreira militar nem sempre são reconhecidas ou valorizadas pelos recrutadores e pelas empresas. Isso gera subutilização de habilidades (liderança, gestão de equipes, logística, resiliência, pontualidade) e dificuldade de inserção no setor privado.

2. **Estigma e desconhecimento sobre o perfil do veterano**  
   Persiste na sociedade e em parte do mercado a ideia de que o militar possui apenas competências ligadas ao combate. Empresas e recrutadores nem sempre conhecem o perfil técnico, logístico e de gestão que o veterano pode oferecer, o que reduz oportunidades e prejudica tanto o candidato quanto as empresas que poderiam se beneficiar desse perfil.

3. **Dispersão e acesso às oportunidades**  
   Hoje existem duas plataformas de referência — Plano de Chamadas (focada no candidato) e Ache um Veterano (focada na empresa e nas vagas). O candidato e a empresa precisam usar ambientes distintos; não há um único ponto de acesso mobile que una perfil, vagas, candidaturas e networking em uma experiência integrada, o que pode limitar o alcance e a adesão, sobretudo em dispositivos móveis.

Essas situações justificam a oferta de uma **solução em formato de aplicativo mobile** que integre as duas plataformas e ofereça, em um só lugar, perfil profissional, vagas, networking e comunicação, contribuindo para reduzir o problema da transição e da visibilidade do veterano no mercado de trabalho.

---

## 1.3 – Demanda sociocomunitária e motivação acadêmica

A **situação-problema** descrita na seção 1.2 impacta a vida dos envolvidos em várias dimensões:

- **Social:** A dificuldade de reinserção e o estigma podem afetar a autoestima e a inclusão social do veterano e de sua família; a comunidade de veteranos e as empresas ficam sem um canal unificado de encontro e confiança.
- **Educacional e cultural:** A “tradução” da experiência militar para a linguagem do mercado civil exige capacitação e divulgação de conhecimentos (soft skills, dinâmicas corporativas, preparação de currículo). O acesso a cursos e workshops (já ofertados pelo PC) e a um app que centralize perfil e vagas reforça a dimensão educacional e de valorização da cultura e do perfil do veterano.
- **Econômica:** A inserção no mercado de trabalho gera renda e estabilidade para o veterano; para as empresas, o acesso a um público qualificado (veteranos) melhora o recrutamento e a produtividade. Um app que integre PC e AC pode ampliar o número de candidaturas e de contratações, com impacto econômico direto.

A **aplicação do conhecimento acadêmico** (engenharia de software, desenvolvimento mobile, integração de sistemas, experiência do usuário e acessibilidade) permite:

- Desenvolver um **aplicativo mobile** (React Native) que consuma as APIs do Plano de Chamadas e do Ache um Veterano, unificando em um único ambiente as funcionalidades de perfil, vagas, documentos, testes e, quando for o caso, feed e chat.
- Oferecer **duas interfaces no mesmo app** (candidato e empresa), com login que direciona para a experiência adequada, aumentando a usabilidade e o alcance da extensão.
- Promover **competências** tanto na equipe (desenvolvimento, trabalho com APIs, extensão universitária) quanto na comunidade (uso de tecnologia para busca de emprego e para recrutamento), além do **engajamento** com os parceiros PC e AC e com o público de veteranos e empresas.

Assim, a demanda sociocomunitária (transição, visibilidade, acesso unificado) é atendida pela motivação acadêmica de aplicar conhecimentos de computação e tecnologia em uma solução concreta de extensão.

---

## 1.4 – Objetivos a serem alcançados em relação à situação-problema

Os objetivos da **atividade de extensão** em relação à situação-problema identificada são (verbos no infinitivo, a serem mensurados no prazo do projeto):

1. **Integrar** em um único aplicativo mobile o acesso às funcionalidades de perfil, vagas, documentos e candidaturas oferecidas pelo Plano de Chamadas e pelo Ache um Veterano, permitindo que candidatos (veteranos) e empresas utilizem uma mesma ferramenta com duas interfaces (candidato e empresa). *Prazo: [A DEFINIR – ex.: até DD/MM/AAAA]*

2. **Facilitar** a transição de militares e veteranos para o mercado civil, por meio do uso do app para construção e atualização de perfil profissional, realização de testes, envio de documentos e busca e candidatura a vagas, utilizando os dados das APIs do PC e do AC. *Prazo: [A DEFINIR]*

3. **Avaliar** a adesão e a utilidade do aplicativo para o público-alvo (veteranos e empresas), por meio de indicadores de uso e de instrumentos de satisfação e de impacto, conforme seção 2.3. *Prazo: [A DEFINIR – preferencialmente ao final do projeto]*

*(Os prazos [A DEFINIR] devem ser preenchidos conforme o cronograma oficial do projeto de extensão.)*

---

# 2 – PLANEJAMENTO PARA DESENVOLVIMENTO DO PROJETO

## 2.1 – Plano de trabalho com cronograma das atividades

O plano de trabalho técnico está detalhado no [Plano_Desenvolvimento.md](Plano_Desenvolvimento.md). Abaixo, a síntese em formato de cronograma para a extensão (o quê, quando, como, para quem, onde, recursos). As datas e o “onde” devem ser ajustados conforme o calendário da instituição e a disponibilidade dos parceiros.

| Fase | O quê | Quando | Como | Para quem | Onde | Recursos |
|------|------|--------|------|-----------|------|----------|
| 0 | Fundação: app + integração APIs PC/AC + login (candidato/empresa) | [A DEFINIR – ex.: Mês/Ano] | Desenvolvimento React Native; clientes HTTP; tela de login com duas opções | Equipe do projeto; depois candidatos e empresas (testes) | [A DEFINIR – ex.: laboratório da instituição; repositório GitHub] | Equipe; Android Studio; documentação das APIs PC e AC; acesso às APIs (homologação) |
| 1 | Perfil profissional unificado (perfil, documentos, testes via API do PC) | [A DEFINIR] | Consumir API do PC; telas de perfil, edição, documentos e testes no app | Candidatos (veteranos) | Idem | Idem; API do PC |
| 2 | Sistema de vagas (candidato: PC; empresa: AC) | [A DEFINIR] | Consumir APIs PC e AC; telas de vagas, candidaturas, Minhas Vagas, veteranos em destaque | Candidatos e empresas | Idem | APIs PC e AC |
| 3 | Networking (conexões, seguir, sugestões) | [A DEFINIR] | Backend complementar (se necessário); telas de conexões e sugestões | Usuários do app | Idem | Backend Node.js (opcional); banco próprio para conexões |
| 4 | Feed de conteúdo (postar, curtir, comentar, repost) | [A DEFINIR] | API de posts; telas de feed e interações | Usuários do app | Idem | Backend complementar; armazenamento |
| 5 | Chat (mensagens privadas e em grupo) | [A DEFINIR] | WebSocket ou serviço de mensagens; telas de conversas | Usuários do app | Idem | Backend; tempo real |
| 6 | Cursos e workshops (integração no app) | [A DEFINIR] | Consumir oferta do PC; telas de cursos e certificados | Candidatos | Idem | API do PC |
| 7 | Páginas de empresas; comunidades; estatísticas; recomendações | [A DEFINIR] | Funcionalidades conforme backlog do Plano_Desenvolvimento | Empresas e usuários | Idem | Backend; banco |
| 8 | Ajustes finais; testes; documentação; preparação iOS | [A DEFINIR] | Revisão de segurança, performance, testes manuais, documentação ABNT | Equipe e avaliadores | Idem | Equipe; ambiente de testes |

**Observações:**  
- “Quando”: preencher com o período (mês/ano ou sprint) de cada fase.  
- “Onde”: preencher com o local das atividades (desenvolvimento, testes, eventual oficina com comunidade).  
- “Recursos”: incluir equipamentos, acesso às APIs, equipe e qualquer outro recurso necessário.

---

## 2.2 – Metodologia

A metodologia da atividade de extensão combina **desenvolvimento de software** e **envolvimento com a comunidade** (veteranos e empresas), da seguinte forma:

### Desenvolvimento do aplicativo

- **Abordagem incremental:** O aplicativo é desenvolvido em fases (0 a 8), conforme [Plano_Desenvolvimento.md](Plano_Desenvolvimento.md), priorizando primeiro a fundação (login, integração com as APIs do PC e do AC) e depois as funcionalidades de vagas, perfil, networking, feed e chat.
- **Consumo de APIs existentes:** Os dados de perfil, vagas, documentos, testes e cursos vêm das APIs do Plano de Chamadas e do Ache um Veterano; o app não mantém banco próprio para esses domínios, garantindo alinhamento com as plataformas parceiras.
- **Duas interfaces no mesmo app:** A tela de login oferece a opção “Entrar como candidato” ou “Entrar como empresa”; após a autenticação, o usuário é direcionado para a interface correspondente (candidato ou empresa), adequada ao seu perfil e às APIs consumidas (PC ou AC).

### Envolvimento com a comunidade e coleta de dados

- **Parceria com PC e AC:** Manter contato com as plataformas Plano de Chamadas e Ache um Veterano para obtenção de documentação das APIs, credenciais de homologação e, quando possível, divulgação do app junto ao público delas (veteranos e empresas cadastrados).
- **Definição de necessidades e validação:**  
  - Antes ou no início do desenvolvimento: **entrevistas ou questionários** (online ou presenciais) com uma amostra de veteranos e de empresas/recrutadores para identificar necessidades, expectativas e dificuldades no uso das plataformas atuais (PC e AC), de modo a orientar prioridades e desenho das telas.  
  - Durante e após a entrega de versões funcionais: **testes de usabilidade** com usuários reais (veteranos e empresas), quando possível, para validar fluxos (login, perfil, vagas, candidaturas) e coletar sugestões de melhoria.
- **Oficinas ou encontros (se aplicável):** Se a instituição e os parceiros viabilizarem, realizar **oficinas** ou **rodas de conversa** com veteranos e/ou empresas para: (1) apresentar o aplicativo e suas funcionalidades; (2) demonstrar o uso (perfil, vagas, candidaturas); (3) coletar depoimentos e feedback para a avaliação (seção 2.3). A logística (data, local, público, material) deve ser planejada em conjunto com os parceiros.
- **Aplicação do conhecimento acadêmico:** O projeto aplica conhecimentos de engenharia de software, desenvolvimento mobile (React Native), integração de sistemas (APIs REST), experiência do usuário (UX) e acessibilidade, alinhados à formação acadêmica e à extensão universitária.

### Síntese

A metodologia utiliza, portanto: **desenvolvimento incremental** do app; **integração com as APIs** do PC e do AC; **entrevistas ou questionários** para necessidades e expectativas; **testes de usabilidade** para validação; e **oficinas ou encontros** com a comunidade quando viável, com o objetivo de garantir que o aplicativo responda à demanda sociocomunitária e que os resultados possam ser avaliados por indicadores e instrumentos definidos na seção 2.3.

---

## 2.3 – Avaliação dos resultados alcançados

A avaliação dos resultados da **atividade de extensão** utiliza indicadores e instrumentos que permitem verificar o alcance dos objetivos (seção 1.4) e a qualidade da solução oferecida à comunidade.

### Indicadores

| Indicador | Descrição | Como obter |
|-----------|------------|------------|
| **Entrega do aplicativo** | Conclusão das fases previstas (0 a 8) e disponibilização de versão utilizável (login, perfil, vagas, duas interfaces). | Plano_Desenvolvimento; critérios de conclusão por fase; documentação e repositório. |
| **Integração com as APIs** | App consumindo corretamente as APIs do PC e do AC para perfil, vagas, documentos e candidaturas. | Testes técnicos; validação com parceiros (se aplicável). |
| **Uso pelo público-alvo** | Número de usuários (candidatos e empresas) que utilizam o app para login, visualização de perfil/vagas e candidaturas ou publicação de vagas. | Métricas do app (quando disponíveis) ou relato dos parceiros PC/AC; número de acessos ou sessões em período definido. [A DEFINIR: ferramenta de analytics ou acordo com PC/AC.] |
| **Satisfação dos usuários** | Grau de satisfação com a usabilidade e com a utilidade do app (escala 1–5 ou satisfeito/insatisfeito). | Questionário pós-uso (online ou aplicado em oficina). Ver instrumentos abaixo. |
| **Impacto na empregabilidade (perspectiva)** | Relatos ou indicadores de que o app contribuiu para candidaturas, contatos ou contratações (quando possível obter esse dado). | Questionário ou entrevista com usuários; parceria com PC/AC para dados agregados. [A DEFINIR conforme disponibilidade.] |

### Instrumentos

| Instrumento | Objetivo | Aplicação |
|-------------|----------|-----------|
| **Checklist de conclusão por fase** | Verificar se cada fase do desenvolvimento foi concluída conforme critérios do Plano_Desenvolvimento. | Ao final de cada fase; preenchido pela equipe. |
| **Questionário de satisfação e utilidade** | Medir a satisfação e a percepção de utilidade do app entre veteranos e empresas que o utilizarem. Perguntas podem incluir: facilidade de uso, clareza das telas, utilidade para busca de vagas/publicação de vagas, sugestões de melhoria. | Após período de uso (ex.: 2–4 semanas); aplicado online (link) ou em oficina. [A PREENCHER: link ou modelo do questionário quando elaborado.] |
| **Relatos de experiência** | Registrar depoimentos (escritos ou em vídeo) de usuários sobre o uso do app e seu impacto na busca por emprego ou no recrutamento. | Coletados em oficinas, por formulário ou por contato direto. |
| **Métricas de uso (opcional)** | Número de logins, telas mais acessadas, candidaturas realizadas pelo app (se a API ou o backend permitir). | Implementação de analytics no app ou acordo com PC/AC para dados agregados. [A DEFINIR conforme viabilidade.] |

### Uso dos resultados

- Os **indicadores** e **instrumentos** acima permitem: (1) comprovar a entrega técnica do aplicativo; (2) avaliar a adesão e a satisfação do público; (3) documentar o impacto da extensão para relatórios finais, seminários e exposições.
- A avaliação deve ser planejada junto com o cronograma (seção 2.1), definindo em que momento(s) o questionário e os relatos serão aplicados e quem será responsável pela análise dos resultados.

---

# 3 – ENCERRAMENTO DO PROJETO

## 3.1 – Evidências das atividades realizadas

*(Esta seção deve ser preenchida **ao encerramento** do projeto, com as evidências documentais que comprovam a realização das atividades. Abaixo, um **modelo/checklist** do que reunir e como descrever.)*

Ao final do projeto, incluir evidências documentais conforme o roteiro de extensão. Cada evidência deve ser **descrita** (o que representa e como comprova a atividade), permitindo uso em exposições e seminários.

### Checklist de evidências sugeridas

| Tipo de evidência | Descrição sugerida | Exemplo de como comprova |
|-------------------|--------------------|---------------------------|
| **Capturas de tela do aplicativo** | Telas do app em funcionamento: login (opções candidato/empresa), perfil, listagem de vagas, candidaturas, interface empresa (Minhas Vagas, veteranos em destaque). | Comprova o desenvolvimento e a entrega do produto; mostra as duas interfaces. |
| **Fotos de oficinas ou encontros** | Registro de oficinas, palestras ou rodas de conversa com veteranos e/ou empresas (quando realizadas). | Comprova o envolvimento com a comunidade e a divulgação do app. |
| **Listas de presença** | Listas de participantes em eventos (oficinas, apresentações, testes de usabilidade). | Comprova o público alcançado e o número de participantes. |
| **Cartas de autorização / parceria** | Documentos que formalizem o apoio ou a parceria do Plano de Chamadas e/ou do Ache um Veterano (quando aplicável). | Comprova a articulação com os parceiros estratégicos. |
| **Materiais informativos** | Folders, cartazes ou artigos que divulguem o app e o projeto de extensão. | Comprova a divulgação e a comunicação com a comunidade. |
| **Vídeos** | Gravações de demonstração do app ou de depoimentos de usuários (respeitando autorização de imagem e voz). | Comprova o uso e o impacto; útil para seminários e redes sociais. |
| **Repositório e documentação** | Link do repositório GitHub (ou outro) e documentação técnica (README, Relatorio_Projeto, Plano_Desenvolvimento). | Comprova o desenvolvimento, a documentação e a conformidade com ABNT quando aplicável. |
| **Resultados da avaliação** | Síntese dos questionários de satisfação, relatos de experiência e, se houver, métricas de uso. | Comprova a avaliação dos resultados (seção 2.3) e o impacto da extensão. |

### Como registrar cada evidência

Para cada item incluído na pasta ou no relatório de encerramento:

1. **Título ou nome do arquivo** (ex.: “Captura – Tela de login – opções candidato e empresa”).
2. **Data** em que a evidência foi gerada (quando aplicável).
3. **Descrição em 1–3 linhas:** o que a evidência mostra e qual atividade ela comprova.
4. **Arquivo anexo** (foto, PDF, link) na pasta de evidências ou no relatório final.

*[Ao encerrar o projeto, preencher este espaço com a listagem real das evidências reunidas e anexá-las conforme as normas da instituição.]*

---

*Documento elaborado para atender ao roteiro de extensão. Itens marcados com [A PREENCHER] ou [A DEFINIR] devem ser completados pela equipe do projeto conforme dados disponíveis e cronograma institucional.*
