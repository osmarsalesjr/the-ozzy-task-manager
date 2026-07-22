# Especificação Funcional das Telas

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento define a especificação funcional das telas do **Ozzy - Task Manager**.

Cada tela descreve:

* Objetivo;
* Componentes visuais;
* Fonte dos dados;
* Ações disponíveis;
* Workflows associados;
* Regras de visibilidade;
* Critérios de navegação.

O objetivo é padronizar a implementação da interface e garantir consistência durante o desenvolvimento da aplicação.

---

# 2. Estrutura de Navegação

```text
Login
│
├── Sign Up
├── Forgot Password
│
└── Dashboard
      │
      ├── Projects
      │      │
      │      └── Project Details
      │               │
      │               ├── My Tasks
      │               │      │
      │               │      └── Task Details
      │               │
      │               ├── New Task (Popup)
      │               └── Edit Task (Popup)
      │
      ├── Notifications
      │
      └── Profile
```

---

# 3. Tela: Login

## Objetivo

Permitir que usuários autenticados acessem a aplicação.

## Componentes

* Logo
* Campo de e-mail
* Campo de senha
* Botão Entrar
* Link Criar Conta
* Link Esqueci minha senha

## Fonte de Dados

Não aplicável.

## Workflows

* WF-001 — Login
* Navegação para Sign Up
* Navegação para Forgot Password

## Regras

* Não permitir acesso ao Dashboard sem autenticação.
* Caso o usuário já esteja autenticado, redirecionar automaticamente para o Dashboard.

---

# 4. Tela: Sign Up

## Objetivo

Cadastrar novos usuários.

## Componentes

* Nome
* E-mail
* Senha
* Confirmar senha
* Botão Criar Conta

## Fonte de Dados

User (nativo do Bubble)

## Workflows

* WF-001 — Cadastro de Usuário

## Regras

Todo novo usuário deverá possuir:

* role = Member

---

# 5. Tela: Forgot Password

## Objetivo

Permitir recuperação de senha.

## Componentes

* Campo de e-mail
* Botão Enviar

## Workflows

* WF-004 — Recuperação de Senha

---

# 6. Tela: Dashboard

## Objetivo

Apresentar uma visão geral da aplicação.

## Componentes

* Header
* Sidebar
* Cards de indicadores
* Projetos recentes
* Tarefas pendentes
* Atividades recentes

## Indicadores

* Projetos ativos
* Tarefas pendentes
* Tarefas concluídas
* Notificações não lidas

## Fonte dos Dados

* Project
* Task
* Notification
* ActivityLog

## Workflows

Atualização automática após alterações.

---

# 7. Tela: Projects

## Objetivo

Gerenciar os projetos do usuário.

## Componentes

* Lista de projetos
* Campo de pesquisa
* Botão Novo Projeto
* Filtro por status

## Repeating Group

Project

## Campos exibidos

* Nome
* Cor
* Status
* Quantidade de tarefas

## Workflows

* Criar Projeto
* Editar Projeto
* Arquivar Projeto

## Navegação

Selecionar projeto abre:

Project Details

---

# 8. Tela: Project Details

## Objetivo

Exibir informações completas de um projeto.

## Componentes

* Nome
* Descrição
* Cor
* Status
* Indicadores
* Lista de tarefas

## Fonte

Project selecionado.

## Indicadores

* Total de tarefas
* Pendentes
* Em andamento
* Concluídas

## Workflows

* Atualizar Projeto
* Arquivar Projeto

---

# 9. Tela: My Tasks

## Objetivo

Exibir as tarefas pertencentes ao projeto.

## Componentes

* Pesquisa
* Filtro por status
* Filtro por prioridade
* Ordenação
* Lista de tarefas

## Fonte

Task

Filtradas pelo projeto atual.

## Campos exibidos

* Título
* Prioridade
* Status
* Responsável
* Data limite

## Workflows

* Criar
* Editar
* Excluir
* Alterar status

---

# 10. Tela: Task Details

## Objetivo

Exibir todas as informações da tarefa.

## Componentes

### Informações gerais

* Título
* Descrição
* Projeto
* Prioridade
* Status
* Responsável
* Data limite

### Comentários

Repeating Group

Comment

### Histórico

Repeating Group

ActivityLog

### Ações

* Editar
* Alterar status
* Excluir

## Workflows

* Atualizar Task
* Alterar Status
* Adicionar Comentário

---

# 11. Popup: Nova Tarefa

## Objetivo

Cadastrar uma nova tarefa.

## Campos

* Projeto
* Título
* Descrição
* Responsável
* Prioridade
* Data limite

## Workflows

WF-201

---

# 12. Popup: Editar Tarefa

## Objetivo

Atualizar uma tarefa existente.

## Campos

Mesmos da criação.

## Workflows

WF-202

---

# 13. Tela: Notifications

## Objetivo

Apresentar todas as notificações do usuário.

## Componentes

Repeating Group

Notification

## Campos

* Ícone
* Título
* Mensagem
* Data
* Status de leitura

## Workflows

* Marcar como lida

---

# 14. Tela: Profile

## Objetivo

Permitir atualização dos dados pessoais.

## Campos

* Nome
* Avatar

## Workflows

* Atualizar Perfil

---

# 15. Componentes Reutilizáveis

## Header

Presente em todas as páginas privadas.

Contém:

* Logo
* Menu
* Pesquisa (evolução futura)
* Notificações
* Perfil

---

## Sidebar

Itens:

* Dashboard
* Projects
* Notifications
* Profile

---

## Project Card

Exibe:

* Nome
* Cor
* Status
* Quantidade de tarefas

---

## Task Card

Exibe:

* Título
* Prioridade
* Status
* Responsável
* Data limite

---

## Comment Card

Exibe:

* Autor
* Data
* Comentário

---

## Notification Card

Exibe:

* Tipo
* Mensagem
* Data

---

## Activity Card

Exibe:

* Usuário
* Ação
* Data

---

## Dashboard Widget

Utilizado para indicadores.

---

## Empty State

Exibido quando não houver registros.

---

## Confirmation Modal

Utilizado para:

* Exclusão
* Arquivamento

---

# 16. Regras de Visibilidade

## Login

Visível apenas para usuários não autenticados.

---

## Dashboard

Visível apenas para usuários autenticados.

---

## Projects

Exibir apenas projetos do usuário autenticado.

---

## My Tasks

Exibir apenas tarefas do projeto selecionado.

---

## Notifications

Exibir apenas notificações do usuário autenticado.

---

## Profile

Permitir edição apenas do próprio usuário.

---

# 17. Responsividade

A aplicação deverá ser compatível com:

## Desktop

Layout principal.

---

## Tablet

Sidebar recolhida.

---

## Mobile

Menu lateral substituído por menu expansível.

Cards reorganizados verticalmente.

---

# 18. Critérios de Aceitação

Cada tela será considerada concluída quando:

* Todos os componentes estiverem implementados.
* Os dados forem carregados corretamente.
* Os Workflows associados funcionarem conforme especificação.
* As regras de visibilidade forem respeitadas.
* Os componentes reutilizáveis forem utilizados.
* O layout estiver responsivo.

---

# 19. Considerações Finais

Esta especificação representa a definição oficial da interface do **Ozzy - Task Manager**.

Todas as telas deverão seguir este documento durante a implementação, garantindo consistência visual, reutilização de componentes e aderência à arquitetura definida para o projeto.
