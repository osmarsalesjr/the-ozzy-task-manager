# Arquitetura da Solução

# Ozzy - Task Manager

**Versão:** 2.0 (MVP)
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento descreve a arquitetura da solução do **Ozzy - Task Manager**, estabelecendo a organização estrutural da aplicação, a arquitetura de dados, os componentes reutilizáveis, a navegação entre páginas, a estratégia de autenticação, a organização dos workflows e as convenções de desenvolvimento adotadas.

O objetivo é fornecer um guia técnico para implementação, manutenção e evolução da aplicação, garantindo consistência entre todos os artefatos do projeto.

---

# 2. Visão Geral da Arquitetura

O **Ozzy - Task Manager** será desenvolvido utilizando exclusivamente recursos nativos do Bubble.io, mantendo compatibilidade com o plano gratuito da plataforma.

A arquitetura foi projetada seguindo princípios de modularidade, baixo acoplamento e escalabilidade.

A solução é composta pelas seguintes camadas:

* Autenticação
* Banco de Dados
* Option Sets
* Workflows
* Interface (Pages)
* Componentes Reutilizáveis

Toda a lógica de negócio será implementada através dos Workflows do Bubble, mantendo as páginas responsáveis apenas pela interação com o usuário.

---

# 3. Arquitetura Geral

```text
                    Bubble.io
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
 Authentication      Database       Option Sets
        │                │                │
        │                ▼                │
        │         Project ────────────────┐
        │              │                  │
        │              ▼                  │
        │            Task                 │
        │        ┌────┼────┐              │
        │        ▼    ▼    ▼              │
        │   Comment Notification ActivityLog
        │                │
        └────────────────▼
               Workflows
                    │
                    ▼
              Pages (UI)
                    │
                    ▼
         Reusable Components
```

---

# 4. Organização da Aplicação

A aplicação será dividida em seis camadas lógicas.

---

## Camada de Autenticação

Responsável pelo controle de acesso dos usuários.

Utiliza exclusivamente o sistema nativo do Bubble.

Responsabilidades:

* Cadastro
* Login
* Logout
* Recuperação de senha
* Controle de sessão

---

## Camada de Dados

Responsável pelo armazenamento das informações.

Entidades:

* User
* Project
* Task
* Comment
* Notification
* ActivityLog

---

## Camada de Option Sets

Responsável pelos valores fixos da aplicação.

Option Sets:

* UserRole
* ProjectStatus
* TaskStatus
* TaskPriority
* NotificationType
* ActivityAction

---

## Camada de Negócio

Implementada através dos Workflows.

Responsável por:

* Gerenciar projetos
* Gerenciar tarefas
* Gerenciar comentários
* Gerenciar notificações
* Registrar histórico de atividades
* Validar permissões
* Automatizar regras de negócio

---

## Camada de Interface

Responsável pela experiência do usuário.

Cada página possui uma responsabilidade única.

---

## Componentes Reutilizáveis

Responsáveis por padronizar elementos compartilhados entre as páginas.

---

# 5. Arquitetura dos Dados

```text
User
 │
 ├──────────────► Project
 │                    │
 │                    ▼
 │                  Task
 │                ┌──┼──┐
 │                ▼  ▼  ▼
 │         Comment Notification ActivityLog
```

Relacionamentos principais:

* Um User pode ser proprietário de vários Projects.
* Um Project possui várias Tasks.
* Cada Task pertence a um único Project.
* Uma Task pode possuir vários Comments.
* Uma Task pode gerar várias Notifications.
* Toda alteração importante gera um ActivityLog.

---

# 6. Estrutura das Páginas

```text
Login
│
├── Sign Up
│
├── Forgot Password
│
└── Dashboard
      │
      ├── Projects
      │      │
      │      └── Project Details
      │              │
      │              ├── My Tasks
      │              │      │
      │              │      └── Task Details
      │              │
      │              ├── New Task
      │              └── Edit Task
      │
      ├── Notifications
      │
      └── Profile
```

---

# 7. Descrição das Páginas

## Login

* Autenticação
* Navegação para cadastro
* Recuperação de senha

---

## Sign Up

Cadastro de novos usuários.

---

## Forgot Password

Solicitação de redefinição de senha.

---

## Dashboard

Página inicial da aplicação.

Apresenta:

* resumo geral;
* indicadores;
* atividades recentes;
* acesso rápido aos projetos.

---

## Projects

Lista todos os projetos do usuário.

Permite:

* visualizar;
* criar;
* editar;
* arquivar projetos.

---

## Project Details

Exibe informações do projeto.

Permite acessar:

* tarefas;
* membros (evolução futura);
* indicadores.

---

## My Tasks

Lista todas as tarefas do projeto.

Permite:

* pesquisar;
* filtrar;
* ordenar;
* acessar detalhes.

---

## Task Details

Apresenta todas as informações da tarefa.

Inclui:

* descrição;
* comentários;
* notificações;
* histórico de atividades.

---

## New Task

Criação de tarefas.

---

## Edit Task

Atualização das informações da tarefa.

---

## Notifications

Central de notificações do usuário.

---

## Profile

Informações do usuário.

---

# 8. Componentes Reutilizáveis

Todos os componentes compartilhados deverão ser implementados como **Reusable Elements**.

## Header

* logotipo
* menu principal
* perfil
* notificações

---

## Sidebar

Itens:

* Dashboard
* Projects
* My Tasks
* Notifications
* Profile

---

## Project Card

Representação resumida de um projeto.

Exibe:

* nome;
* status;
* quantidade de tarefas;
* cor do projeto.

---

## Task Card

Representação resumida da tarefa.

Exibe:

* título;
* prioridade;
* status;
* responsável;
* data limite.

---

## Comment Card

Exibição de comentários.

---

## Notification Card

Exibição de notificações.

---

## Activity Card

Exibição do histórico de atividades.

---

## Dashboard Widget

Componente reutilizável para indicadores.

---

## Confirmation Modal

Utilizado para ações irreversíveis.

---

## Empty State

Componente exibido quando não houver registros.

---

# 9. Fluxo de Navegação

```text
Login
   │
   ▼
Dashboard
   │
   ├────────► Projects
   │             │
   │             ▼
   │      Project Details
   │             │
   │             ▼
   │         My Tasks
   │             │
   │             ▼
   │       Task Details
   │             │
   │     ┌───────┴────────┐
   │     ▼                ▼
   │ Edit Task      Comments
   │
   ├────────► Notifications
   │
   └────────► Profile
```

---

# 10. Estratégia de Autenticação

A autenticação será baseada exclusivamente no sistema nativo do Bubble.

Fluxo:

1. Usuário realiza login.
2. Bubble valida as credenciais.
3. A sessão é criada automaticamente.
4. O usuário é direcionado ao Dashboard.
5. Todas as páginas privadas verificam a existência de um usuário autenticado.
6. O logout encerra a sessão e redireciona para Login.

---

# 11. Organização dos Workflows

Os workflows deverão ser agrupados por domínio funcional.

## Authentication

* Login
* Logout
* Sign Up
* Forgot Password

---

## Projects

* Create Project
* Update Project
* Archive Project

---

## Tasks

* Create Task
* Update Task
* Delete Task
* Change Status

---

## Comments

* Add Comment
* Edit Comment
* Delete Comment

---

## Notifications

* Create Notification
* Mark Notification Read

---

## Activity Log

* Register Activity

---

## User

* Update Profile

---

# 12. Convenção de Nomenclatura

## Páginas

Utilizar nomes curtos em inglês.

Exemplos:

* login
* signup
* dashboard
* projects
* project_details
* my_tasks
* task_details
* notifications
* profile

---

## Reusable Elements

Prefixo:

```text
re_
```

Exemplos:

* re_header
* re_sidebar
* re_project_card
* re_task_card
* re_comment_card
* re_notification_card
* re_activity_card

---

## Grupos

Prefixo:

```text
grp_
```

---

## Popups

Prefixo:

```text
pop_
```

---

## Inputs

Prefixo:

```text
inp_
```

---

## Botões

Prefixo:

```text
btn_
```

---

## Repeating Groups

Prefixo:

```text
rg_
```

---

## Workflows

Utilizar sempre:

**Verbo + Objeto**

Exemplos:

* Create Task
* Update Task
* Archive Project
* Register Activity
* Mark Notification Read

---

# 13. Boas Práticas

Durante o desenvolvimento deverão ser observadas as seguintes diretrizes:

* Utilizar apenas recursos nativos do Bubble sempre que possível.
* Evitar duplicação de Workflows.
* Centralizar regras de negócio nos Workflows.
* Utilizar Option Sets para valores fixos.
* Manter componentes reutilizáveis desacoplados.
* Evitar lógica complexa diretamente na interface.
* Utilizar relacionamentos entre Data Types em vez de duplicação de dados.
* Nomear todos os elementos seguindo as convenções definidas.
* Registrar automaticamente ações importantes através da entidade ActivityLog.
* Validar permissões antes da execução de qualquer operação crítica.

---

# 14. Arquitetura de Evolução

A arquitetura foi projetada para suportar futuras expansões sem necessidade de remodelagem significativa.

Evoluções previstas:

* Equipes (Teams)
* Etiquetas (Tags)
* Subtarefas (Subtasks)
* Dependências entre tarefas
* Anexos (Attachments)
* Dashboard analítico
* Integração com APIs externas
* Aplicação mobile
* Quadro Kanban com drag-and-drop
* Automações e notificações externas

---

# 15. Conclusão

A arquitetura proposta para o **Ozzy - Task Manager** foi projetada para equilibrar simplicidade, organização e escalabilidade, aproveitando ao máximo os recursos nativos do Bubble.io.

A separação entre autenticação, dados, Option Sets, workflows, interface e componentes reutilizáveis reduz o acoplamento da aplicação, facilita sua manutenção e prepara o sistema para futuras evoluções sem comprometer o MVP.

Toda a documentação da solução foi estruturada para servir como referência durante a implementação e para garantir consistência entre o planejamento, a modelagem de dados, os workflows e a interface do sistema.
