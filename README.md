# 📱 Projeto Extensionista – Rede Profissional para Veteranos

## 📖 Sobre o Projeto

Este projeto consiste no desenvolvimento de um **aplicativo mobile para Android** voltado à criação de uma **rede social profissional semelhante ao LinkedIn**, com foco na conexão entre **militares, veteranos e empresas**.

A proposta é integrar e unificar funcionalidades das plataformas:

- [Plano de Chamadas](https://planodechamadas.com.br/) – preparação do candidato (perfil, documentos, testes, cursos, vagas)
- [Ache um Veterano](https://acheumveterano.com.br/) – vitrine de talentos e vagas para empresas/recrutadores

O objetivo é facilitar a **transição de militares para o mercado civil**, criando uma plataforma onde profissionais divulguem suas habilidades e empresas encontrem candidatos qualificados. O aplicativo funcionará como um **hub profissional**, reunindo networking, vagas de emprego, criação de conteúdo e comunicação entre usuários.

---

## 📄 Documentação do Projeto

A documentação está organizada na pasta [**docs/**](docs/). Índice completo: [docs/README.md](docs/README.md).

| Documento | Descrição |
|-----------|-----------|
| [**Plano_Desenvolvimento.md**](docs/Plano_Desenvolvimento.md) | Plano completo de desenvolvimento: arquitetura, fases e ordem de implementação |
| [**Relatorio_Projeto.md**](docs/Relatorio_Projeto.md) | Relatório completo: escopo, backlog, prioridades e o que será feito |
| [Correlacao_PC_AC_LinkedIn.md](docs/Correlacao_PC_AC_LinkedIn.md) | Correlação entre PC, AC e LinkedIn (base do backlog) |
| [IdeiaPrincipalDotrabalho.md](docs/IdeiaPrincipalDotrabalho.md) | Ideia principal, arquitetura e funcionalidades de referência |
| [PC.md](docs/analise/PC.md) | Análise da plataforma Plano de Chamadas |
| [AC.md](docs/analise/AC.md) | Análise da plataforma Ache um Veterano |
| [Funcionalidades_PC.md](docs/funcionalidades/Funcionalidades_PC.md) | Funcionalidades mapeadas do Plano de Chamadas |
| [Funcionalidades_AC.md](docs/funcionalidades/Funcionalidades_AC.md) | Funcionalidades mapeadas do Ache um Veterano |

---

## 🎯 Objetivo

Criar uma **plataforma digital de networking profissional** que permita:

- conexão entre profissionais
- divulgação de oportunidades de trabalho
- construção de perfil profissional (currículo online unificado)
- interação entre empresas e candidatos
- fortalecimento da comunidade profissional

---

## 📱 Plataforma

- **Android** (prioridade)
- Baseado na arquitetura do [Android Open Source Project (AOSP)](https://android.googlesource.com/)
- Código preparado para **futura expansão para iOS** (React Native)

---

## 🏗 Arquitetura do Sistema

A estrutura segue a arquitetura padrão do Android.

| Camada | Descrição |
|--------|-----------|
| **Aplicações** | Apps Android (terceiros, privilegiados, fabricantes) |
| **APIs** | Android API (dev), APIs internas do sistema |
| **Runtime** | Android Runtime (ART), HAL, bibliotecas nativas |
| **Núcleo** | Kernel Linux (memória, processos, hardware, segurança) |

---

## ⚙ Requisitos Técnicos

| Aspecto | Requisito |
|--------|-----------|
| **Bateria** | Uso mínimo possível; evitar processos desnecessários em segundo plano |
| **Memória** | Menor consumo possível; bom desempenho em dispositivos mais simples |
| **Responsividade** | Interface adaptável a diferentes resoluções |
| **Conectividade** | App sempre conectado; avisar usuário quando internet for necessária; bloquear funções offline |
| **Usabilidade** | Interface intuitiva, navegação simples, UX eficiente |

---

## 🚀 Funcionalidades

O aplicativo terá funcionalidades inspiradas no **LinkedIn**, integrando o que já existe no Plano de Chamadas e no Ache um Veterano. Detalhamento e prioridades estão em [Relatorio_Projeto.md](docs/Relatorio_Projeto.md).

### 👤 Perfil Profissional

Perfil unificado (currículo online): foto, banner, headline, resumo, experiências, formação, certificações, projetos, habilidades, recomendações, destaques. Inclui **upload de documentos** e **testes** (lógica, interpretação, personalidade) como diferencial para empresas.

### 🤝 Networking

Conexões, seguir profissionais e empresas, mensagens privadas e em grupo, conexões em comum, sugestões de conexão.

### 💼 Sistema de Vagas

**Candidato:** buscar vagas, candidatura rápida, salvar vagas, alertas, ver empresa contratante.  
**Empresa:** publicar vagas, ver candidatos, filtros (área, cargo, cidade, estado).

### 📢 Criação de Conteúdo (Feed)

Postar texto, imagens, vídeos, documentos, enquetes, artigos. Curtir, comentar, compartilhar, repost.

### 🏢 Páginas de Empresas

Perfil institucional, publicação de vagas e conteúdo, cultura, funcionários, produtos/serviços, estatísticas de seguidores.

### 💬 Comunidades e Grupos

Grupos profissionais (ex.: cibersegurança, programação, empreendedorismo).

### 📊 Estatísticas

Visualizações de perfil, alcance de postagens, crescimento de seguidores, aparições em busca, engajamento.

### 🎓 Sistema de Aprendizado

Cursos de capacitação, workshops, certificações, trilhas de aprendizado.

---

## 🔐 Segurança

- Comunicação segura via API
- Proteção e criptografia de dados sensíveis
- Validação de requisições e controle de acesso
- Alinhamento à LGPD (conforme políticas das plataformas de referência)

---

## 🛠 Tecnologias

| Camada | Tecnologia |
|--------|------------|
| **Frontend** | React Native (obrigatório) |
| **Backend** | Node.js |
| **IDE** | Android Studio |
| **SDK** | Java SDK |

---

## 📂 Repositório

- Hospedado no **GitHub**
- **Público** durante o desenvolvimento até a apresentação
- Após apresentação: pode ser privatizado ou transferido para empresa
- Para demonstrações: banco de dados fictício ou próprio

---

## 📚 Documentação

Toda a documentação do projeto segue as normas da **ABNT** (Associação Brasileira de Normas Técnicas).

---

## 📌 Status e Nome

- **Status:** 🚧 Em desenvolvimento
- **Nome do aplicativo:** Ainda não definido

---

## 👨‍💻 Autor

Projeto desenvolvido como **trabalho extensionista acadêmico**.
