# Modelagem de Dados

# Ozzy - Task Manager

## Visão Geral

Este documento apresenta a modelagem de dados do **Ozzy - Task Manager**, uma aplicação web desenvolvida em **Bubble.io** para gerenciamento colaborativo de projetos e tarefas.

Como a plataforma Bubble possui um banco de dados No-Code próprio, a modelagem foi elaborada considerando suas características nativas, priorizando simplicidade, baixo acoplamento, reutilização de relacionamentos e facilidade de manutenção.

A estrutura foi projetada para atender integralmente ao MVP definido durante o planejamento, mantendo a solução preparada para futuras evoluções.

---

# Princípios da Modelagem

A estrutura do banco foi definida seguindo os seguintes princípios:

* Utilizar o tipo **User** nativo do Bubble para autenticação.
* Evitar duplicação de informações.
* Utilizar relacionamentos por referência.
* Centralizar as regras de negócio nos Workflows.
* Utilizar Option Sets para estados fixos da aplicação.
* Manter baixo acoplamento entre entidades.
* Facilitar futuras expansões sem necessidade de remodelagem.

---

# Diagrama Entidade-Relacionamento

```text
                              +----------------------+
                              |        User          |
                              +----------------------+
                              | email (nativo)       |
                              | name                |
                              | role               |
                              | avatar             |
                              +----------+----------+
                                         │
                          owner          │
                                         ▼
                              +----------------------+
                              |      Project         |
                              +----------------------+
                              | name                |
                              | description         |
                              | status              |
                              | color              |
                              | archived           |
                              +----------+----------+
                                         │
                                         │
                                         ▼
                              +----------------------+
                              |        Task          |
                              +----------------------+
                              | title               |
                              | description         |
                              | status              |
                              | priority            |
                              | position            |
                              | due_date            |
                              | completed_date      |
                              | archived            |
                              +-----+------+--------+
                                    │      │
                task                │      │ task
                                    │      │
                +-------------------+      +------------------+
                │                                         │
                ▼                                         ▼
       +------------------+                     +----------------------+
       |     Comment      |                     |    Notification      |
       +------------------+                     +----------------------+
       | message          |                     | title                |
       | author           |                     | message              |
       | task             |                     | recipient            |
       +------------------+                     | type                 |
                                                | is_read              |
                                                | task                 |
                                                +-----------+----------+
                                                            │
                                                            │
                                                            ▼
                                                +----------------------+
                                                |    ActivityLog       |
                                                +----------------------+
                                                | action               |
                                                | description          |
                                                | metadata             |
                                                | task                 |
                                                | user                 |
                                                +----------------------+
```

---

# Estrutura das Entidades

## User

O Bubble utiliza uma entidade nativa denominada **User**, responsável pela autenticação e gerenciamento de sessões.

### Campos personalizados

| Campo  | Tipo     |
| ------ | -------- |
| name   | text     |
| role   | UserRole |
| avatar | image    |

### Campos nativos

* email
* Created Date
* Modified Date

### Responsabilidades

* Autenticação
* Proprietário de projetos
* Responsável por tarefas
* Autor de comentários
* Destinatário de notificações
* Autor de registros de atividades

---

## Project

Representa um projeto dentro da aplicação.

Todas as tarefas deverão estar vinculadas a um projeto.

### Campos

| Campo       | Tipo          |
| ----------- | ------------- |
| name        | text          |
| description | text          |
| status      | ProjectStatus |
| owner       | User          |
| color       | text          |
| archived    | yes/no        |

### Responsabilidades

* Organizar tarefas
* Centralizar informações do projeto
* Servir como agrupador lógico das tarefas

---

## Task

Representa a principal entidade operacional do sistema.

Cada registro corresponde a uma tarefa pertencente a um projeto.

### Campos

| Campo          | Tipo         |
| -------------- | ------------ |
| title          | text         |
| description    | text         |
| project        | Project      |
| status         | TaskStatus   |
| priority       | TaskPriority |
| position       | number       |
| due_date       | date         |
| completed_date | date         |
| assigned_to    | User         |
| created_by     | User         |
| archived       | yes/no       |

### Responsabilidades

* Representar atividades do projeto
* Controlar responsáveis
* Controlar status
* Receber comentários
* Originar notificações
* Registrar histórico

---

## Comment

Representa as interações entre usuários dentro de uma tarefa.

### Campos

| Campo   | Tipo |
| ------- | ---- |
| message | text |
| author  | User |
| task    | Task |

---

## Notification

Responsável pelas notificações internas.

### Campos

| Campo     | Tipo             |
| --------- | ---------------- |
| title     | text             |
| message   | text             |
| recipient | User             |
| task      | Task             |
| type      | NotificationType |
| is_read   | yes/no           |

---

## ActivityLog

Responsável por registrar automaticamente as principais ações executadas nas tarefas.

### Campos

| Campo       | Tipo           |
| ----------- | -------------- |
| task        | Task           |
| user        | User           |
| action      | ActivityAction |
| description | text           |
| metadata    | text           |

### Responsabilidades

* Registrar alterações importantes
* Manter histórico das tarefas
* Apoiar auditoria da aplicação

---

# Relacionamentos

## User → Project

Um usuário pode ser proprietário de vários projetos.

```text
User (1) -------- (N) Project
```

---

## Project → Task

Um projeto pode possuir diversas tarefas.

```text
Project (1) -------- (N) Task
```

---

## User → Task

Um usuário pode:

* Criar tarefas.
* Ser responsável por tarefas.

```text
User (1) -------- (N) Task
```

---

## Task → Comment

Uma tarefa pode possuir diversos comentários.

```text
Task (1) -------- (N) Comment
```

---

## User → Comment

Um usuário pode registrar diversos comentários.

```text
User (1) -------- (N) Comment
```

---

## Task → Notification

Uma tarefa pode originar diversas notificações.

```text
Task (1) -------- (N) Notification
```

---

## User → Notification

Cada usuário possui sua própria lista de notificações.

```text
User (1) -------- (N) Notification
```

---

## Task → ActivityLog

Cada tarefa pode possuir diversos registros de atividades.

```text
Task (1) -------- (N) ActivityLog
```

---

## User → ActivityLog

Um usuário pode gerar diversos registros de atividades.

```text
User (1) -------- (N) ActivityLog
```

---

# Option Sets

Para garantir consistência dos dados, todos os estados fixos da aplicação serão implementados utilizando **Option Sets**.

## UserRole

* Administrator
* Member

---

## ProjectStatus

* Active
* Archived

---

## TaskStatus

* To Do
* In Progress
* Blocked
* Done

---

## TaskPriority

* Low
* Medium
* High
* Critical

---

## NotificationType

* Task Assigned
* Task Updated
* New Comment
* Status Changed
* Reminder

---

## ActivityAction

* Task Created
* Task Updated
* Task Deleted
* Status Changed
* Comment Added
* Assignee Changed
* Notification Created

---

# Regras de Modelagem

## Regra 1 — Utilizar o User nativo

Não será criada uma tabela própria de usuários.

Toda autenticação será realizada pelo mecanismo nativo do Bubble.

---

## Regra 2 — Projetos organizam as tarefas

Toda tarefa deverá pertencer obrigatoriamente a um projeto.

---

## Regra 3 — Task é a entidade central

A Task concentra o fluxo operacional da aplicação.

Comentários, notificações e histórico existem exclusivamente em função das tarefas.

---

## Regra 4 — Sem duplicação de dados

Todas as relações serão implementadas por referência entre Data Types.

---

## Regra 5 — Estados controlados

Perfis, status, prioridades, tipos de notificação e ações utilizarão Option Sets.

---

## Regra 6 — Workflows controlam a lógica

O banco de dados será responsável apenas pelo armazenamento das informações.

Toda lógica de negócio será implementada através dos Workflows do Bubble.

---

# Escalabilidade

Embora a modelagem tenha sido definida para o MVP, ela suporta futuras expansões sem necessidade de remodelagem significativa.

Possíveis evoluções incluem:

* Equipes (Teams)
* Etiquetas (Tags)
* Subtarefas
* Dependências entre tarefas
* Checklist
* Anexos
* Dashboard analítico
* Integrações externas
* Quadro Kanban com drag-and-drop (utilizando o campo `position`)

---

# Conclusão

A modelagem proposta atende integralmente aos requisitos do **Ozzy - Task Manager**, utilizando exclusivamente recursos compatíveis com o plano gratuito do Bubble.

A estrutura foi projetada para ser simples, consistente, normalizada e escalável, reduzindo a complexidade dos Workflows, facilitando a manutenção da aplicação e preparando a solução para futuras evoluções sem necessidade de alterações estruturais significativas.
