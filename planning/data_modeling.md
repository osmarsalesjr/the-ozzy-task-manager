# Modelagem de Dados

# Ozzy - Task Manager

## Visão Geral

Este documento apresenta a modelagem inicial do banco de dados do **Ozzy - Task Manager**, uma aplicação web desenvolvida em **Bubble.io** para gerenciamento colaborativo de tarefas.

Como a plataforma Bubble possui um banco de dados No-Code próprio, a modelagem foi elaborada considerando suas características nativas, priorizando simplicidade, baixo acoplamento e facilidade de manutenção.

A solução foi projetada para atender completamente ao MVP definido durante o planejamento, mantendo uma arquitetura preparada para futuras evoluções.

---

# Princípios da Modelagem

A estrutura do banco foi definida seguindo os seguintes princípios:

* Utilizar o tipo **User** nativo do Bubble para autenticação.
* Evitar duplicação de informações.
* Manter baixo acoplamento entre entidades.
* Utilizar relacionamentos por referência em vez de listas sempre que possível.
* Centralizar regras de negócio nos Workflows.
* Utilizar **Option Sets** para estados fixos da aplicação.
* Facilitar futuras expansões da solução.

---

# Diagrama Entidade-Relacionamento

```text
                                     +---------------------------+
                                     |          User             |
                                     +---------------------------+
                                     | name                      |
                                     | email (nativo)            |
                                     | role                      |
                                     | avatar                    |
                                     | created date (nativo)     |
                                     +-------------+-------------+
                                                   ▲
                                created_by         │        assigned_to
                                                   │
                                                   │
                             +---------------------+---------------------+
                             |                                           |
                             |                                           |
                    +--------+---------+                                 |
                    |      Task        |---------------------------------+
                    +------------------+
                    | title            |
                    | description      |
                    | status           |
                    | priority         |
                    | due_date         |
                    | assigned_to      |
                    | created_by       |
                    | created date     |
                    | modified date    |
                    +--------+---------+
                             ▲
                 task        │        task
                             │
          +------------------+------------------+
          |                                     |
          |                                     |
+---------+---------+                 +---------+-----------+
|     Comment       |                 |    Notification     |
+-------------------+                 +---------------------+
| message           |                 | title               |
| author (User)     |                 | message             |
| task (Task)       |                 | recipient (User)    |
| created date      |                 | task (Task)         |
+-------------------+                 | is_read             |
                                      | created date        |
                                      +---------------------+
```

---

# Estrutura das Entidades

## User

O Bubble possui uma entidade nativa denominada **User**, responsável pela autenticação e gerenciamento de sessões.

### Campos personalizados

| Campo  | Tipo     | Descrição        |
| ------ | -------- | ---------------- |
| name   | text     | Nome do usuário  |
| role   | UserRole | Perfil de acesso |
| avatar | image    | Foto do usuário  |

### Campos nativos

* email
* created date
* modified date

### Responsabilidades

* Autenticação
* Proprietário das tarefas
* Responsável pelas tarefas
* Autor dos comentários
* Destinatário das notificações

---

## Task

Representa a principal entidade do sistema.

Cada registro corresponde a uma tarefa que será acompanhada durante seu ciclo de vida.

### Campos

| Campo       | Tipo         |
| ----------- | ------------ |
| title       | text         |
| description | text         |
| status      | TaskStatus   |
| priority    | TaskPriority |
| due_date    | date         |
| assigned_to | User         |
| created_by  | User         |

### Responsabilidades

* Centralizar todas as atividades.
* Relacionar usuários.
* Receber comentários.
* Gerar notificações.

---

## Comment

Representa as interações entre os usuários dentro de uma tarefa.

Cada comentário pertence exclusivamente a uma tarefa.

### Campos

| Campo   | Tipo |
| ------- | ---- |
| message | text |
| author  | User |
| task    | Task |

---

## Notification

Responsável pelo sistema de notificações internas.

Cada notificação pertence a apenas um usuário.

### Campos

| Campo     | Tipo   |
| --------- | ------ |
| title     | text   |
| message   | text   |
| recipient | User   |
| task      | Task   |
| is_read   | yes/no |

---

# Relacionamentos

## User → Task

Um usuário pode:

* Criar várias tarefas.
* Ser responsável por várias tarefas.

Relacionamento:

```
User (1) -------- (N) Task
```

---

## Task → Comment

Uma tarefa pode possuir diversos comentários.

```
Task (1) -------- (N) Comment
```

---

## User → Comment

Um usuário pode registrar vários comentários.

```
User (1) -------- (N) Comment
```

---

## Task → Notification

Uma tarefa pode originar diversas notificações ao longo do seu ciclo de vida.

```
Task (1) -------- (N) Notification
```

---

## User → Notification

Cada usuário possui sua própria lista de notificações.

```
User (1) -------- (N) Notification
```

---

# Option Sets

Como os valores abaixo são fixos, optou-se pela utilização de **Option Sets**, recurso nativo do Bubble que melhora a organização da aplicação e reduz a ocorrência de erros de digitação.

## UserRole

* Administrator
* Member

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

# Regras de Modelagem

Durante a definição da estrutura do banco foram adotadas as seguintes regras:

## Regra 1 — Utilizar o User nativo

Não será criada uma tabela própria de usuários.

A autenticação, recuperação de senha e gerenciamento de sessões serão fornecidos pelo Bubble.

---

## Regra 2 — Uma única entidade central

Toda a aplicação gira em torno da entidade **Task**.

Comentários e notificações existem apenas como informações complementares da tarefa.

---

## Regra 3 — Sem duplicação de dados

Nenhuma informação será armazenada em mais de uma entidade.

Os relacionamentos ocorrerão sempre por referência.

---

## Regra 4 — Estados controlados

Status, prioridade e perfil do usuário utilizarão Option Sets, garantindo consistência em toda a aplicação.

---

## Regra 5 — Workflows controlam as regras

O banco armazenará apenas informações.

Toda lógica de negócio será implementada através dos Workflows do Bubble.

---

# Escalabilidade

Embora esta modelagem tenha sido projetada para o MVP, ela permite expansão sem necessidade de reestruturação significativa.

Possíveis evoluções incluem:

* Projetos (Projects)
* Etiquetas (Tags)
* Equipes (Teams)
* Histórico de alterações
* Anexos
* Checklist de tarefas
* Subtarefas
* Dashboard analítico
* Integrações externas

---

# Conclusão

A modelagem proposta atende integralmente aos requisitos do **Ozzy - Task Manager**, utilizando exclusivamente recursos compatíveis com o plano gratuito do Bubble.

A estrutura foi projetada para ser simples, consistente e escalável, reduzindo a complexidade dos Workflows e facilitando a manutenção da aplicação ao longo de sua evolução.
