# Modelagem de Dados

# Ozzy - Task Manager

## Visão Geral

Este documento apresenta a modelagem de dados atual do **Ozzy - Task Manager**, aplicação web desenvolvida em **Bubble.io** para gerenciamento colaborativo de projetos e tarefas.

A modelagem utiliza os recursos nativos do Bubble, priorizando:

* Simplicidade.
* Relacionamentos por referência.
* Option Sets para valores controlados.
* Regras de privacidade nativas.
* Baixo acoplamento.
* Facilidade de manutenção e evolução.

A estrutura atual atende ao MVP e está preparada para futuras expansões.

---

# 1. Data Types

## User

Representa os usuários da plataforma.

| Campo  | Tipo     |
| ------ | -------- |
| name   | text     |
| avatar | image    |
| role   | UserRole |
| email  | text     |

O `User` é utilizado como entidade central de autenticação e relacionamento com as demais entidades.

### Responsabilidades

* Autenticação.
* Proprietário de projetos.
* Criador de tarefas.
* Responsável por tarefas.
* Autor de comentários.
* Destinatário de notificações.
* Autor de registros de atividades.

### Privacidade

* `everyone`: pode visualizar e pesquisar campos públicos.
* `User's own data`: somente o próprio usuário pode visualizar seus anexos/dados privados.

---

## Project

Representa um projeto e funciona como agrupador das tarefas.

| Campo       | Tipo          |
| ----------- | ------------- |
| name        | text          |
| owner       | User          |
| archived    | yes/no        |
| description | text          |
| status      | ProjectStatus |

### Relacionamentos

Um projeto possui um proprietário e pode estar relacionado a diversas tarefas.

### Privacidade

* `owner`: acesso completo de CRUD e auto-binding nos campos principais.
* `everyone`: somente leitura e pesquisa.

---

## Task

É a entidade central do sistema e representa uma tarefa operacional.

| Campo          | Tipo         |
| -------------- | ------------ |
| title          | text         |
| description    | text         |
| due_date       | date         |
| completed_date | date         |
| archived       | yes/no       |
| created_by     | User         |
| assigned_to    | User         |
| project        | Project      |
| status         | TaskStatus   |
| priority       | TaskPriority |

### Responsabilidades

* Representar atividades do projeto.
* Controlar responsável.
* Controlar status.
* Controlar prioridade.
* Definir prazo.
* Receber comentários.
* Originar notificações.
* Gerar registros no histórico de atividades.

### Privacidade

* `creator`: CRUD completo sobre todos os campos.
* `assignee`: pode editar apenas `status` e `completed_date`.
* `everyone`: somente leitura e pesquisa.

---

## Comment

Representa comentários realizados pelos usuários dentro das tarefas.

| Campo    | Tipo          |
| -------- | ------------- |
| author   | User          |
| message  | text          |
| task     | Task          |
| archived | CommentStatus |

O campo `archived` utiliza o Option Set `CommentStatus` como uma flag de arquivamento.

### Privacidade

* `author`: CRUD completo.
* `everyone`: somente leitura e pesquisa.

---

## Notification

Representa notificações internas direcionadas a usuários específicos.

| Campo     | Tipo   |
| --------- | ------ |
| title     | text   |
| message   | text   |
| recipient | User   |
| is_read   | yes/no |
| task      | Task   |

### Responsabilidades

* Informar o usuário sobre eventos relevantes.
* Associar a notificação à tarefa relacionada.
* Controlar o estado de leitura.

### Privacidade

* `everyone`: sem acesso (`view_all: false`).
* `recipient`: somente o destinatário pode visualizar a notificação e alterar `is_read`.

---

## ActivityLog

Registra ações realizadas no sistema para fins de histórico e auditoria.

| Campo       | Tipo           |
| ----------- | -------------- |
| user        | User           |
| description | text           |
| task        | Task           |
| action      | ActivityAction |

### Responsabilidades

* Registrar ações relevantes realizadas no sistema.
* Manter o histórico das tarefas.
* Apoiar auditoria e rastreabilidade.

### Privacidade

* Usuários autenticados: acesso somente para leitura e pesquisa.
* `everyone`: somente leitura e pesquisa, conforme configuração atual.

> O registro de atividades é criado pelos workflows da aplicação e não deve ser utilizado como mecanismo de alteração manual dos dados.

---

# 2. Relacionamentos

## User → Project

Um usuário pode possuir diversos projetos.

```text
User (1) -------- (N) Project
```

A relação é representada pelo campo:

```text
Project.owner → User
```

---

## Project → Task

Um projeto pode possuir diversas tarefas.

```text
Project (1) -------- (N) Task
```

A relação é representada pelo campo:

```text
Task.project → Project
```

---

## User → Task

Um usuário pode criar diversas tarefas e também ser responsável por diversas tarefas.

```text
User (1) -------- (N) Task
```

Representado pelos campos:

```text
Task.created_by → User
Task.assigned_to → User
```

---

## Task → Comment

Uma tarefa pode possuir diversos comentários.

```text
Task (1) -------- (N) Comment
```

Representado por:

```text
Comment.task → Task
```

---

## User → Comment

Um usuário pode criar diversos comentários.

```text
User (1) -------- (N) Comment
```

Representado por:

```text
Comment.author → User
```

---

## User → Notification

Um usuário pode receber diversas notificações.

```text
User (1) -------- (N) Notification
```

Representado por:

```text
Notification.recipient → User
```

---

## Task → Notification

Uma tarefa pode estar relacionada a diversas notificações.

```text
Task (1) -------- (N) Notification
```

Representado por:

```text
Notification.task → Task
```

---

## User → ActivityLog

Um usuário pode gerar diversos registros de atividade.

```text
User (1) -------- (N) ActivityLog
```

Representado por:

```text
ActivityLog.user → User
```

---

## Task → ActivityLog

Uma tarefa pode possuir diversos registros de atividade.

```text
Task (1) -------- (N) ActivityLog
```

Representado por:

```text
ActivityLog.task → Task
```

---

# 3. Option Sets

Os valores controlados da aplicação são implementados utilizando Option Sets.

## UserRole

| Valor         | db_value      |
| ------------- | ------------- |
| Administrator | administrator |
| Member        | member        |

---

## ProjectStatus

| Valor    | db_value |
| -------- | -------- |
| Active   | active   |
| Archived | archived |

---

## TaskStatus

| Valor       | db_value    |
| ----------- | ----------- |
| To Do       | to_do       |
| In Progress | in_progress |
| Blocked     | blocked     |
| Done        | done        |

---

## TaskPriority

| Valor    | db_value |
| -------- | -------- |
| Low      | low      |
| Medium   | medium   |
| High     | high     |
| Critical | critical |

---

## ActivityAction

Utilizado para identificar o tipo de ação registrada no histórico.

| db_value             |
| -------------------- |
| task_created         |
| task_updated         |
| task_deleted         |
| status_changed       |
| comment_added        |
| assignee_changed     |
| notification_created |
| project_updated      |
| task_archived        |
| user_updated         |
| role_user_updated    |

---

## CommentStatus

Utilizado como flag de arquivamento dos comentários.

| Valor | db_value |
| ----- | -------- |
| yes   | yes      |
| no    | no       |

> Apesar de representar uma condição de arquivamento, `CommentStatus` é utilizado atualmente como Option Set em vez de um campo booleano direto.

---

# 4. Regras de Modelagem

## Regra 1 — Utilizar o User nativo

Não deve ser criada uma entidade própria para substituir o mecanismo de usuários do Bubble.

O `User` é a entidade central de autenticação e relacionamento.

---

## Regra 2 — Projetos agrupam tarefas

Toda tarefa deve estar vinculada a um `Project`.

```text
Task.project → Project
```

---

## Regra 3 — Task é a entidade operacional central

A `Task` concentra o fluxo principal da aplicação.

As entidades `Comment`, `Notification` e `ActivityLog` possuem relacionamento direto com tarefas.

---

## Regra 4 — Relacionamentos devem utilizar referências

As entidades devem armazenar referências aos demais Data Types, evitando duplicação de informações.

Exemplo:

```text
Task.assigned_to → User
```

em vez de armazenar o nome do responsável diretamente na tarefa.

---

## Regra 5 — Estados controlados devem utilizar Option Sets

Estados, prioridades, perfis e classificações fixas devem utilizar Option Sets.

Atualmente:

* UserRole
* ProjectStatus
* TaskStatus
* TaskPriority
* ActivityAction
* CommentStatus

---

## Regra 6 — Privacidade deve ser aplicada no Data Type

As restrições de acesso aos dados devem ser configuradas através das Privacy Rules do Bubble.

A interface não deve ser considerada o único mecanismo de proteção dos dados.

---

## Regra 7 — Workflows controlam a lógica de negócio

Os Data Types armazenam os dados.

Os workflows são responsáveis por executar regras como:

* Criação de notificações.
* Registro de atividades.
* Alteração de status.
* Atualização de tarefas.
* Criação de comentários.
* Atualização de responsáveis.

---

## Regra 8 — ActivityLog é somente leitura

Os registros de atividades devem ser gerados automaticamente pelos workflows.

Usuários não devem editar manualmente registros de auditoria.

---

## Regra 9 — Notificações pertencem ao destinatário

Uma notificação deve possuir um `recipient` definido.

O acesso às notificações deve ser restrito ao usuário destinatário.

---

## Regra 10 — Comentários podem ser arquivados

Comentários não são necessariamente excluídos fisicamente quando deixam de ser relevantes.

O campo `archived` utiliza o `CommentStatus` para representar essa condição.

---

# 5. Visão Simplificada da Estrutura

```text
User
 │
 ├── Project
 │     │
 │     └── Task
 │          ├── Comment
 │          ├── Notification
 │          └── ActivityLog
 │
 ├── Task (created_by / assigned_to)
 ├── Comment (author)
 ├── Notification (recipient)
 └── ActivityLog (user)
```

A `Task` permanece como o principal ponto de integração entre os módulos operacionais do sistema.

---

# 6. Privacidade — Resumo

| Data Type    | Principal regra de acesso                             |
| ------------ | ----------------------------------------------------- |
| User         | Dados públicos disponíveis; dados próprios protegidos |
| Project      | Owner possui CRUD; demais usuários possuem leitura    |
| Task         | Creator possui CRUD; assignee possui edição limitada  |
| Comment      | Author possui CRUD; demais possuem leitura            |
| Notification | Somente recipient possui acesso                       |
| ActivityLog  | Usuários autenticados possuem leitura/pesquisa        |

---

# 7. Considerações para o MVP

A estrutura atual não deve ser expandida com novas entidades sem necessidade funcional.

Devem ser priorizados os Data Types já existentes:

```text
User
Project
Task
Comment
Notification
ActivityLog
```

Novos Data Types somente devem ser adicionados quando houver uma necessidade funcional validada no produto.

---

# 8. Evoluções Futuras

A estrutura atual permite futuras extensões, caso sejam incorporadas ao produto:

* Teams.
* Tags.
* Subtarefas.
* Dependências entre tarefas.
* Checklists.
* Anexos.
* Dashboard analítico.
* Integrações externas.
* Calendário.
* Recursos avançados de colaboração.

Essas funcionalidades permanecem fora do escopo atual do MVP.

---

# Conclusão

A modelagem atual do **Ozzy - Task Manager** utiliza uma estrutura simples e adequada ao MVP, baseada nos recursos nativos do Bubble.

A arquitetura de dados possui como entidades principais:

```text
User
Project
Task
```

e como módulos complementares:

```text
Comment
Notification
ActivityLog
```

A `Task` atua como entidade central do fluxo operacional, enquanto `Comment`, `Notification` e `ActivityLog` fornecem os recursos de colaboração, comunicação e rastreabilidade.

O modelo utiliza referências entre Data Types, Option Sets para valores controlados, Privacy Rules para segurança e Workflows para implementação das regras de negócio.

A estrutura atual deve ser considerada a **fonte de referência da modelagem de dados do MVP** e mantida sincronizada com a implementação do Bubble.
