# Arquitetura da Solução

# Ozzy - Task Manager

**Versão:** 1.0 (MVP)
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento descreve a arquitetura da solução do **Ozzy - Task Manager**, estabelecendo a organização estrutural da aplicação, os componentes reutilizáveis, a navegação entre páginas, a estratégia de autenticação e as convenções de desenvolvimento adotadas.

O objetivo é fornecer um guia para implementação e manutenção da aplicação, garantindo consistência e reduzindo retrabalho durante o desenvolvimento.

---

# 2. Visão Geral da Arquitetura

O Ozzy - Task Manager será desenvolvido utilizando exclusivamente recursos nativos do Bubble.io.

A arquitetura seguirá uma abordagem modular baseada em:

* Banco de dados nativo do Bubble;
* Páginas independentes;
* Componentes reutilizáveis (Reusable Elements);
* Workflows organizados por responsabilidade;
* Option Sets para valores fixos;
* Navegação controlada por autenticação.

A lógica de negócio será concentrada nos Workflows, enquanto as páginas serão responsáveis apenas pela apresentação e interação com o usuário.

---

# 3. Arquitetura Geral

```text
                   +---------------------------+
                   |        Bubble.io          |
                   +---------------------------+
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
+----------------+    +----------------+    +----------------+
| Authentication |    |   Database     |    |   Option Sets  |
| (User nativo)  |    |                |    |                |
+----------------+    +----------------+    +----------------+
                               │
                               ▼
                    +-----------------------+
                    |      Workflows        |
                    +-----------------------+
                               │
                               ▼
                    +-----------------------+
                    |      Pages (UI)       |
                    +-----------------------+
                               │
                               ▼
                    +-----------------------+
                    | Reusable Components   |
                    +-----------------------+
```

---

# 4. Organização da Aplicação

A aplicação será dividida em cinco camadas lógicas.

## Camada de Autenticação

Responsável pelo acesso dos usuários.

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

Entidades principais:

* User
* Task
* Comment
* Notification

---

## Camada de Negócio

Implementada através dos Workflows.

Responsável por:

* Criar tarefas
* Atualizar tarefas
* Gerenciar comentários
* Criar notificações
* Validar permissões

---

## Camada de Interface

Responsável pela experiência do usuário.

Cada página possui uma responsabilidade específica.

---

## Componentes Reutilizáveis

Responsáveis por padronizar elementos utilizados em diversas páginas.

---

# 5. Estrutura das Páginas

```text
Login
│
├── Sign Up
│
├── Forgot Password
│
└── Dashboard
      │
      ├── My Tasks
      │
      ├── Task Details
      │
      ├── New Task
      │
      ├── Edit Task
      │
      ├── Notifications
      │
      └── Profile
```

---

# 6. Descrição das Páginas

## Login

Responsável pela autenticação.

Funções:

* Login
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

Exibe:

* Resumo das tarefas
* Indicadores
* Atividades recentes
* Atalhos

---

## My Tasks

Lista todas as tarefas do usuário.

Permite:

* pesquisar;
* filtrar por status;
* filtrar por prioridade;
* ordenar resultados.

---

## Task Details

Apresenta todas as informações da tarefa.

Inclui:

* dados da tarefa;
* comentários;
* histórico de alterações;
* ações disponíveis.

---

## New Task

Formulário para criação de tarefas.

---

## Edit Task

Atualização das informações da tarefa.

---

## Notifications

Lista todas as notificações do usuário.

---

## Profile

Informações pessoais do usuário.

---

# 7. Componentes Reutilizáveis

Para manter consistência visual e facilitar manutenção, os seguintes componentes deverão ser implementados como **Reusable Elements**.

## Header

Responsável por:

* logotipo;
* menu principal;
* perfil do usuário;
* notificações.

---

## Sidebar

Menu de navegação.

Itens:

* Dashboard
* Minhas Tarefas
* Nova Tarefa
* Notificações
* Perfil

---

## Task Card

Representação resumida de uma tarefa.

Informações:

* título;
* prioridade;
* status;
* responsável;
* data limite.

---

## Comment Card

Componente utilizado para exibir comentários.

---

## Notification Card

Representação visual das notificações.

---

## Confirmation Modal

Utilizado para:

* exclusões;
* ações irreversíveis.

---

## Empty State

Exibido quando não houver informações para apresentar.

---

# 8. Fluxo de Navegação

```text
Login
   │
   ▼
Dashboard
   │
   ├────────────► My Tasks
   │                  │
   │                  ▼
   │            Task Details
   │                  │
   │                  ├────► Edit Task
   │                  │
   │                  └────► Comments
   │
   ├────────────► New Task
   │
   ├────────────► Notifications
   │
   └────────────► Profile
```

---

# 9. Estratégia de Autenticação

A autenticação será baseada exclusivamente no sistema nativo do Bubble.

Fluxo:

1. Usuário realiza login.
2. Bubble valida as credenciais.
3. Sessão é criada automaticamente.
4. Usuário é direcionado ao Dashboard.
5. Páginas privadas validam a existência de um usuário autenticado.
6. O logout encerra a sessão e redireciona para a página de Login.

---

# 10. Organização dos Workflows

Os Workflows deverão ser agrupados por domínio funcional.

## Authentication

* Login
* Logout
* Sign Up
* Forgot Password

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
* Mark as Read

---

## User

* Update Profile

---

# 11. Convenção de Nomenclatura

## Páginas

Utilizar nomes curtos e em inglês.

Exemplos:

* login
* signup
* dashboard
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
* re_task_card
* re_comment_card
* re_notification_card

---

## Grupos

Prefixo:

```text
grp_
```

Exemplos:

* grp_filters
* grp_task_details
* grp_comments

---

## Popups

Prefixo:

```text
pop_
```

Exemplos:

* pop_delete_task
* pop_edit_task

---

## Inputs

Prefixo:

```text
inp_
```

Exemplos:

* inp_title
* inp_description

---

## Botões

Prefixo:

```text
btn_
```

Exemplos:

* btn_save
* btn_cancel
* btn_delete

---

## Repeating Groups

Prefixo:

```text
rg_
```

Exemplos:

* rg_tasks
* rg_comments
* rg_notifications

---

## Workflows

Utilizar verbo + objeto.

Exemplos:

* Create Task
* Update Task
* Delete Task
* Create Comment
* Mark Notification Read

---

# 12. Boas Práticas

Durante o desenvolvimento deverão ser observadas as seguintes diretrizes:

* Utilizar apenas recursos nativos sempre que possível.
* Evitar duplicação de Workflows.
* Manter componentes reutilizáveis desacoplados.
* Centralizar regras de negócio nos Workflows.
* Utilizar Option Sets para valores fixos.
* Nomear elementos de forma consistente.
* Evitar lógica complexa diretamente na interface.
* Validar permissões antes de executar ações críticas.

---

# 13. Arquitetura de Evolução

A arquitetura foi planejada para permitir futuras expansões sem necessidade de reestruturação significativa.

Evoluções previstas incluem:

* Projetos (Projects);
* Etiquetas (Tags);
* Subtarefas (Subtasks);
* Equipes (Teams);
* Anexos (Attachments);
* Histórico de atividades (Activity Log);
* Dashboard analítico;
* Integração com APIs externas;
* Aplicação mobile.

---

# 14. Conclusão

A arquitetura proposta para o **Ozzy - Task Manager** prioriza simplicidade, reutilização de componentes e aderência às boas práticas do Bubble.io.

A separação entre dados, workflows, interface e componentes reutilizáveis reduz o acoplamento da aplicação, facilita sua manutenção e permite que novas funcionalidades sejam incorporadas de forma incremental, preservando a organização do projeto ao longo de sua evolução.
