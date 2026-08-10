# Planejamento do Projeto

## Ozzy - Task Manager

### Sistema Colaborativo de Gerenciamento de Projetos e Tarefas

---

# 1. Visão Geral

## Objetivo

Desenvolver uma aplicação web utilizando **Bubble.io (Plano Gratuito)** para gerenciamento colaborativo de projetos, tarefas e comunicação entre membros de uma equipe.

A aplicação permite que usuários autenticados visualizem projetos, acompanhem tarefas, registrem comentários, recebam notificações e consultem o histórico das atividades realizadas no sistema.

O projeto prioriza simplicidade, organização, reutilização de componentes e utilização de recursos nativos compatíveis com o plano gratuito do Bubble.

---

# 2. Objetivos do Projeto

* Construir uma aplicação funcional utilizando Bubble.io.
* Aplicar conceitos de desenvolvimento No-Code.
* Modelar uma estrutura de dados organizada e preparada para evolução.
* Implementar workflows para as principais regras de negócio.
* Desenvolver uma interface moderna e responsiva.
* Implementar controle de acesso baseado em perfil de usuário.
* Publicar a aplicação.
* Produzir documentação técnica para manutenção e evolução do sistema.

---

# 3. Escopo do MVP

O MVP contempla as funcionalidades essenciais para validar a proposta do sistema.

## Autenticação

* Cadastro de usuários.
* Login.
* Logout.
* Recuperação de senha.
* Restrição de acesso às páginas para usuários não autenticados.

---

## Dashboard

A página `index` funciona como dashboard principal do sistema.

Funcionalidades atuais:

* Saudação personalizada ao usuário.
* Visualização dos projetos ativos do usuário.
* Visualização das tarefas pendentes do usuário.
* Visualização das atividades recentes.
* Acesso rápido à listagem de tarefas.
* Acesso ao histórico completo de atividades.
* Acesso à criação de projetos para administradores.
* Visualização detalhada de uma atividade recente através de popup.

> **Nota:** O grupo `grp_dashboard_metrics` foi removido por não ser relevante para a primeira versão do produto. O MVP não possui atualmente indicadores adicionais de métricas no dashboard.

---

## Gerenciamento de Projetos

A aplicação possui uma página específica para gerenciamento de projetos.

Funcionalidades:

* Visualizar projetos.
* Buscar projetos.
* Filtrar projetos por status.
* Filtrar projetos por proprietário.
* Criar projetos.
* Editar projetos.
* Arquivar projetos.
* Definir proprietário do projeto.
* Acessar o detalhe de um projeto.
* Visualizar as tarefas vinculadas ao projeto.

A criação de projetos é restrita a administradores.

---

## Gerenciamento de Tarefas

Funcionalidades:

* Visualizar tarefas.
* Buscar tarefas.
* Filtrar por status.
* Filtrar por prioridade.
* Filtrar por projeto.
* Criar tarefa.
* Editar tarefa.
* Excluir/arquivar tarefa.
* Alterar status.
* Definir responsável.
* Definir prioridade.
* Definir data limite.
* Associar tarefa a um projeto.
* Visualizar detalhes de uma tarefa.
* Acessar os comentários da tarefa.

A aplicação também possui alteração rápida de status diretamente na listagem de tarefas.

---

## Comentários

Cada tarefa possui uma área própria para colaboração.

Funcionalidades:

* Adicionar comentários.
* Visualizar comentários.
* Editar comentários.
* Arquivar/excluir comentários conforme as regras de permissão.
* Registrar alterações relevantes no histórico de atividades.

---

## Notificações

O sistema possui uma página de notificações para o usuário autenticado.

Funcionalidades:

* Visualizar notificações recebidas.
* Marcar uma notificação como lida.
* Marcar todas as notificações como lidas.
* Navegar para a tarefa relacionada quando existir.
* Exibir notificações em ordem cronológica.

---

## Histórico de Atividades

O sistema registra automaticamente ações relevantes realizadas na aplicação.

A página `activities` é exclusivamente de consulta.

Funcionalidades:

* Visualizar atividades recentes.
* Visualizar histórico completo.
* Filtrar por ação.
* Filtrar por colaborador.
* Filtrar por projeto.
* Buscar atividades.
* Limpar filtros.
* Visualizar detalhes completos de uma atividade em popup.

A página possui visualizações diferentes para `member` e `administrator`, mantendo os respectivos Repeating Groups e regras de acesso.

Não existe CRUD de atividades.

---

## Perfil

Funcionalidades:

* Visualizar informações do usuário.
* Editar nome.
* Editar avatar.
* Acessar funcionalidades relacionadas à segurança da conta.
* Solicitar redefinição de senha.

---

## Gerenciamento de Usuários

A aplicação possui uma área administrativa para gerenciamento dos colaboradores.

Funcionalidades:

* Visualizar usuários.
* Buscar por nome ou e-mail.
* Filtrar por role.
* Criar usuários.
* Editar usuários.
* Visualizar informações dos colaboradores.

As operações administrativas são protegidas por regras baseadas no perfil `administrator`.

---

# 4. Funcionalidades Fora do Escopo

As funcionalidades abaixo permanecem fora do MVP:

* Chat em tempo real.
* Upload de arquivos.
* Integrações com serviços externos.
* Notificações Push.
* Aplicativo mobile.
* Controle avançado de permissões.
* Dashboard analítico avançado.
* API pública.
* Automações externas.
* Integração com calendário.
* Subtarefas.
* Etiquetas (Tags).
* Dependência entre tarefas.

---

# 5. Requisitos Funcionais

## RF01

O sistema deverá permitir o cadastro de novos usuários.

## RF02

O sistema deverá permitir autenticação através de login e senha.

## RF03

O usuário autenticado poderá encerrar sua sessão.

## RF04

Somente usuários autenticados poderão acessar as áreas internas da aplicação.

## RF05

O sistema deverá permitir visualizar e gerenciar projetos conforme as permissões do usuário.

## RF06

Administradores poderão criar e editar projetos.

## RF07

O sistema deverá permitir criar tarefas vinculadas a um projeto.

## RF08

O sistema deverá permitir editar tarefas.

## RF09

O sistema deverá permitir excluir ou arquivar tarefas conforme as regras implementadas.

## RF10

O sistema deverá permitir alterar o status de uma tarefa.

## RF11

Cada tarefa deverá possuir um responsável.

## RF12

Cada tarefa deverá possuir um status e uma prioridade.

## RF13

Cada tarefa poderá receber comentários.

## RF14

O sistema deverá permitir editar e arquivar comentários conforme as permissões aplicáveis.

## RF15

O sistema deverá registrar notificações relacionadas às tarefas e comentários.

## RF16

O usuário poderá visualizar suas notificações.

## RF17

O usuário poderá marcar notificações como lidas.

## RF18

O sistema deverá registrar automaticamente o histórico das principais ações realizadas.

## RF19

O usuário poderá consultar o histórico de atividades ao qual possui acesso.

## RF20

O usuário poderá visualizar os detalhes de uma atividade através de um popup somente leitura.

## RF21

Administradores poderão gerenciar usuários do sistema.

## RF22

O usuário poderá editar suas informações básicas de perfil.

---

# 6. Requisitos Não Funcionais

* Desenvolvido utilizando Bubble.io.
* Compatível com o plano gratuito da plataforma.
* Interface responsiva.
* Navegação simples e intuitiva.
* Dados persistidos no banco nativo do Bubble.
* Utilização de recursos nativos sempre que possível.
* Utilização de Option Sets para estados fixos da aplicação.
* Organização dos workflows por domínio funcional.
* Uso de elementos reutilizáveis para componentes compartilhados.
* Estrutura preparada para evolução futura.

---

# 7. Regras de Negócio

**RN01**

Somente usuários autenticados poderão acessar o sistema.

**RN02**

Toda tarefa deverá estar vinculada a um projeto.

**RN03**

Toda tarefa deverá possuir um responsável.

**RN04**

Toda tarefa deverá possuir um status.

**RN05**

Ao criar uma tarefa, deverá ser gerada uma notificação para o responsável quando aplicável.

**RN06**

Ao adicionar um comentário, deverá ser criada uma notificação quando aplicável.

**RN07**

Alterações relevantes em tarefas e comentários deverão gerar registros no histórico de atividades.

**RN08**

O usuário poderá marcar notificações como lidas.

**RN09**

Operações administrativas deverão ser restritas ao perfil `administrator`.

**RN10**

A página de atividades será somente leitura e não permitirá criação, edição ou exclusão manual de registros de atividade.

**RN11**

O histórico exibido no dashboard deverá apresentar as atividades recentes do usuário autenticado.

**RN12**

O acesso ao histórico completo deverá respeitar o perfil do usuário, diferenciando a visualização de membros e administradores.

**RN13**

Somente o criador da tarefa poderá excluí-la, salvo regras administrativas específicas implementadas no sistema.

---

# 8. Backlog do Produto

| ID   | História de Usuário                                                  | Prioridade |
| ---- | -------------------------------------------------------------------- | ---------- |
| US01 | Como visitante, desejo criar uma conta para utilizar o sistema.      | Alta       |
| US02 | Como usuário, desejo realizar login para acessar o sistema.          | Alta       |
| US03 | Como usuário, desejo encerrar minha sessão.                          | Alta       |
| US04 | Como usuário, desejo visualizar meus projetos.                       | Alta       |
| US05 | Como administrador, desejo criar projetos para organizar o trabalho. | Média      |
| US06 | Como usuário, desejo editar projetos.                                | Média      |
| US07 | Como usuário, desejo visualizar minhas tarefas.                      | Alta       |
| US08 | Como usuário, desejo criar uma tarefa.                               | Alta       |
| US09 | Como usuário, desejo editar uma tarefa.                              | Alta       |
| US10 | Como usuário, desejo excluir ou arquivar uma tarefa.                 | Média      |
| US11 | Como usuário, desejo alterar o status de uma tarefa.                 | Alta       |
| US12 | Como usuário, desejo definir um responsável para uma tarefa.         | Alta       |
| US13 | Como usuário, desejo comentar em tarefas.                            | Alta       |
| US14 | Como usuário, desejo visualizar minhas notificações.                 | Média      |
| US15 | Como usuário, desejo marcar notificações como lidas.                 | Média      |
| US16 | Como usuário, desejo visualizar o histórico de atividades.           | Média      |
| US17 | Como usuário, desejo consultar os detalhes de uma atividade.         | Média      |
| US18 | Como usuário, desejo editar meu perfil.                              | Baixa      |
| US19 | Como administrador, desejo gerenciar os usuários do sistema.         | Média      |

---

# 9. Priorização do MVP

## Sprint 1 — Fundação

* Estrutura do banco de dados.
* Cadastro.
* Login.
* Logout.
* Recuperação de senha.
* Estrutura base da aplicação.
* Header e Sidebar reutilizáveis.
* Dashboard inicial.

---

## Sprint 2 — Projetos e Tarefas

* Gerenciamento de projetos.
* Criação de tarefas.
* Edição de tarefas.
* Exclusão/arquivamento de tarefas.
* Alteração de status.
* Definição de responsável.
* Definição de prioridade.
* Página de detalhe do projeto.
* Página de detalhe da tarefa.

---

## Sprint 3 — Colaboração

* Comentários.
* Notificações.
* Histórico de atividades.
* Popup de detalhes de atividade.
* Perfil do usuário.
* Gerenciamento administrativo de usuários.

---

## Sprint 4 — Finalização

* Ajustes visuais.
* Responsividade.
* Testes funcionais.
* Correções.
* Validação das regras de acesso.
* Publicação.
* Documentação.
* Vídeo Pitch.

---

# 10. Critérios de Aceitação do MVP

O MVP será considerado concluído quando:

* O usuário conseguir criar uma conta.
* O usuário conseguir realizar login.
* O usuário conseguir realizar logout.
* O usuário conseguir recuperar sua senha.
* O usuário conseguir visualizar seus projetos.
* O administrador conseguir criar e gerenciar projetos.
* O usuário conseguir visualizar suas tarefas.
* O usuário conseguir criar tarefas vinculadas a projetos.
* O usuário conseguir editar tarefas.
* O usuário conseguir alterar o status das tarefas.
* O usuário conseguir definir responsável e prioridade.
* O usuário conseguir comentar em tarefas.
* O sistema registrar notificações automaticamente.
* O usuário conseguir visualizar e marcar notificações como lidas.
* O sistema registrar o histórico das principais ações.
* O usuário conseguir visualizar o histórico de atividades.
* O usuário conseguir visualizar os detalhes de uma atividade em modo somente leitura.
* O administrador conseguir gerenciar usuários.
* O usuário conseguir editar seu perfil.
* O dashboard apresentar projetos, tarefas pendentes e atividades recentes.
* A aplicação estiver publicada no Bubble.

> O dashboard não dependerá de um bloco separado de métricas. O antigo `grp_dashboard_metrics` foi removido por não fazer parte da primeira versão do produto.

---

# 11. Riscos do Projeto

| Risco                          | Impacto | Mitigação                                                  |
| ------------------------------ | ------- | ---------------------------------------------------------- |
| Limitações do plano gratuito   | Médio   | Utilizar prioritariamente recursos nativos do Bubble       |
| Retrabalho na modelagem        | Alto    | Validar a estrutura do banco antes da implementação        |
| Workflows complexos            | Médio   | Desenvolver e testar incrementalmente                      |
| Crescimento do escopo          | Alto    | Priorizar exclusivamente o MVP                             |
| Inconsistência entre artefatos | Médio   | Manter a documentação sincronizada com a implementação     |
| Regras de permissão incorretas | Alto    | Validar workflows, conditionals e Privacy Rules por perfil |
| Problemas de responsividade    | Médio   | Validar os layouts após cada alteração estrutural          |

---

# 12. Estrutura Atual da Aplicação

A aplicação está organizada atualmente nas seguintes áreas principais:

| Página          | Finalidade                                      |
| --------------- | ----------------------------------------------- |
| `auth`          | Autenticação e acesso ao sistema                |
| `index`         | Dashboard principal                             |
| `projects`      | Listagem e gerenciamento de projetos            |
| `project`       | Detalhes de um projeto e suas tarefas           |
| `tasks`         | Listagem, filtros e gerenciamento de tarefas    |
| `task`          | Detalhes da tarefa e comentários                |
| `activities`    | Histórico de atividades em modo somente leitura |
| `notifications` | Notificações do usuário                         |
| `users`         | Gerenciamento administrativo de usuários        |
| `profile`       | Perfil e segurança do usuário                   |

A aplicação utiliza componentes reutilizáveis, principalmente **Header** e **Sidebar**, compartilhados entre as páginas internas.

---

# 13. Estado Atual da Implementação

As principais inconsistências identificadas durante a auditoria foram corrigidas.

Entre os pontos já validados estão:

* Página `activities` sem CRUD de atividades.
* Dois Repeating Groups de atividades separados por role.
* Popup de detalhes de atividade funcional.
* Atividades recentes do dashboard com abertura do mesmo popup.
* Filtros da página `activities` preservados.
* Data sources dos Repeating Groups preservados.
* Empty states preservados.
* Workflows existentes preservados durante as correções.
* Controle de visibilidade baseado em role mantido.
* `grp_dashboard_metrics` removido por não ser necessário para o MVP inicial.

---

# 14. Próximos Artefatos

Após a aprovação deste planejamento, serão mantidos/produzidos os seguintes documentos:

1. Modelagem do Banco de Dados.
2. Arquitetura da Aplicação.
3. Especificação dos Workflows.
4. Wireframes das Telas.
5. Plano de Testes.
6. README do Projeto.
7. Roteiro do Vídeo Pitch.
