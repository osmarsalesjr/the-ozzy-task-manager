# Arquitetura da Solução

# Ozzy - Task Manager

**Versão:** 3.0 — Arquitetura Atual do MVP
**Plataforma:** Bubble.io — Plano Gratuito

---

# 1. Objetivo

Este documento descreve a arquitetura atual do **Ozzy - Task Manager**, refletindo a estrutura efetivamente implementada no Bubble.io.

O documento estabelece:

* organização das páginas;
* arquitetura de dados;
* Option Sets;
* componentes reutilizáveis;
* estratégia de navegação;
* autenticação;
* organização dos workflows;
* controle de acesso por perfil;
* convenções de nomenclatura;
* diretrizes para manutenção e evolução.

Esta versão substitui a arquitetura originalmente planejada e deve ser utilizada como referência técnica para manutenção do MVP.

---

# 2. Visão Geral da Arquitetura

O **Ozzy - Task Manager** utiliza o Bubble.io como plataforma única de aplicação, banco de dados e autenticação.

A solução utiliza prioritariamente recursos nativos do Bubble, incluindo:

* Data Types;
* Privacy Rules;
* Option Sets;
* Workflows;
* Reusable Elements;
* Custom States;
* Repeating Groups;
* Popups;
* Conditional States;
* navegação entre páginas.

A aplicação está organizada em quatro principais responsabilidades:

```text
                    Bubble.io
                        │
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
   Autenticação      Dados          Option Sets
        │               │                │
        └───────────────┼────────────────┘
                        ▼
                    Workflows
                        │
                        ▼
                      Pages
                        │
                        ▼
              Reusable Elements
```

A lógica de negócio permanece concentrada nos Workflows, enquanto as páginas são responsáveis principalmente pela apresentação, interação e navegação.

---

# 3. Arquitetura de Dados

A aplicação utiliza o banco de dados nativo do Bubble.

As entidades principais são:

```text
User
 │
 ├──────────────► Project
 │                    │
 │                    ▼
 │                  Task
 │                ┌──┼──────────────┐
 │                │  │              │
 │                ▼  ▼              ▼
 │             Comment        Notification
 │                │
 │                └──────────────┐
 │                               ▼
 └────────────────────────► ActivityLog
```

## Data Types

* User
* Project
* Task
* Comment
* Notification
* ActivityLog

A **Task** permanece como a principal entidade operacional do sistema.

As entidades `Comment`, `Notification` e `ActivityLog` estão diretamente relacionadas ao fluxo das tarefas.

---

# 4. Option Sets

Os valores fixos da aplicação são controlados através de Option Sets.

## UserRole

* Administrator
* Member

## ProjectStatus

* Active
* Archived

## TaskStatus

* To Do
* In Progress
* Blocked
* Done

## TaskPriority

* Low
* Medium
* High
* Critical

## ActivityAction

As ações atualmente registradas incluem:

* task_created
* task_updated
* task_deleted
* status_changed
* comment_added
* assignee_changed
* notification_created
* project_updated
* task_archived
* user_updated
* role_user_updated

## CommentStatus

Utilizado como indicador de arquivamento dos comentários:

* yes
* no

---

# 5. Camada de Autenticação

A autenticação utiliza o mecanismo nativo do Bubble.

O tipo `User` é utilizado tanto para autenticação quanto para representar os usuários da aplicação.

A aplicação possui fluxo de:

* login;
* cadastro;
* logout;
* recuperação de senha;
* redefinição de senha;
* controle de sessão.

As páginas privadas possuem mecanismos de redirecionamento para a página `auth` quando o usuário não está autenticado, quando esse controle está implementado no workflow da página.

---

# 6. Controle de Acesso

O sistema utiliza o campo `role` do tipo `User` para diferenciar:

* `administrator`;
* `member`.

O controle de acesso é implementado através de uma combinação de:

* Privacy Rules;
* Conditionals;
* condições de execução dos Workflows;
* visibilidade de elementos.

O padrão utilizado é:

```text
CurrentUser
     │
     ▼
    role
     │
 ┌───┴───────────────┐
 ▼                   ▼
Member          Administrator
 │                   │
acesso comum    recursos administrativos
```

Exemplos atuais:

* criação de usuários é restrita a administradores;
* edição de projetos é restrita a administradores;
* exclusão/arquivamento de tarefas possui restrições administrativas;
* ações específicas da página `activities` variam conforme o role;
* elementos administrativos permanecem ocultos por padrão e são exibidos através de conditionals.

---

# 7. Estrutura Atual das Páginas

A aplicação atualmente possui páginas organizadas por responsabilidade funcional:

```text
auth
 │
 └── index
      │
      ├── projects
      │      │
      │      └── project
      │             │
      │             └── task
      │
      ├── tasks
      │
      ├── activities
      │
      ├── users
      │
      └── profile
```

A página `index` funciona como dashboard principal após a autenticação.

A página `project` recebe um `Project` como `CurrentPageItem`.

A página `task` recebe uma `Task` como `CurrentPageItem`.

---

# 8. Página `auth`

Responsável pela autenticação do usuário.

Principais responsabilidades:

* login;
* cadastro;
* recuperação de senha;
* redefinição de senha;
* direcionamento para a aplicação após autenticação.

A autenticação utiliza exclusivamente os recursos nativos do Bubble.

---

# 9. Página `index`

A página `index` é o dashboard principal da aplicação.

Sua estrutura atual é organizada em:

* `re_header`;
* `re_sidebar`;
* área principal do dashboard;
* projetos;
* tarefas pendentes;
* atividades recentes;
* popups relacionados ao dashboard.

## Projetos

O dashboard apresenta:

* projetos ativos do usuário;
* cards de projeto;
* acesso ao detalhe do projeto;
* criação de projeto para administradores.

O `RepeatingGroup rg_projects` consulta projetos ativos e apresenta os registros em formato de cards.

## Tarefas

A seção de tarefas apresenta as tarefas pendentes atribuídas ao usuário.

O `RepeatingGroup rg_pending_tasks`:

* filtra pelo usuário atual;
* ignora tarefas arquivadas;
* ignora tarefas concluídas;
* ordena por `due_date`;
* apresenta quantidade limitada de registros no dashboard.

## Atividades Recentes

A seção de atividades utiliza o `rg_recent_activity`.

São apresentados os registros recentes de `ActivityLog` relacionados ao usuário.

Cada item pode abrir o popup:

`pop_activity_details`

O popup recebe o `ActivityLog` correspondente no momento da interação.

## Remoção do Dashboard Metrics

O elemento:

`grp_dashboard_metrics`

foi **removido da aplicação**.

Esse componente não faz mais parte da arquitetura do MVP e não deve ser recriado ou considerado como dependência de nenhuma página ou workflow.

A primeira versão do produto prioriza:

* projetos;
* tarefas;
* atividades recentes;
* notificações;
* colaboração;
* perfil.

Indicadores analíticos mais avançados permanecem fora do MVP.

---

# 10. Página `projects`

Responsável pela gestão dos projetos.

Principais elementos:

* `re_header`;
* `re_sidebar`;
* `grp_projects_content`;
* filtros;
* `rg_projects`;
* estados vazios;
* popup de criação;
* popup de edição.

Funcionalidades:

* visualizar projetos;
* pesquisar projetos;
* filtrar por status;
* filtrar por proprietário;
* criar projeto;
* editar projeto;
* arquivar projeto;
* acessar detalhes do projeto.

A criação de projetos é controlada pelo role do usuário.

---

# 11. Página `project`

A página `project` representa o detalhe de um projeto específico.

O projeto é recebido como `CurrentPageItem`.

Estrutura principal:

```text
project
│
├── grp_sidebar
│    └── re_sidebar
│
└── grp_content
     │
     ├── grp_project_header
     │
     └── grp_tasks_section
          │
          └── rg_project_tasks
```

A página apresenta:

* nome do projeto;
* descrição;
* status;
* proprietário;
* data de criação;
* tarefas vinculadas.

Também permite:

* editar projeto;
* criar tarefa;
* editar tarefa;
* navegar para o detalhe da tarefa.

A listagem de tarefas considera tarefas não arquivadas pertencentes ao projeto atual.

---

# 12. Página `tasks`

A página `tasks` apresenta a visão geral das tarefas.

Possui filtros por:

* status;
* prioridade;
* projeto;
* texto.

O `RepeatingGroup rg_tasks` utiliza filtros combinados diretamente na fonte de dados.

A página também possui um estado:

`selected_task`

utilizado para ações de alteração rápida.

## Alteração rápida de status

O usuário pode abrir o popup:

`pop_quick_status`

para alterar o status da tarefa sem sair da listagem.

O fluxo:

```text
Selecionar tarefa
      ↓
Definir selected_task
      ↓
Abrir pop_quick_status
      ↓
Selecionar novo status
      ↓
Atualizar Task
      ↓
Criar ActivityLog
      ↓
Criar Notification
```

---

# 13. Página `task`

A página `task` apresenta o detalhe de uma tarefa específica.

A tarefa é recebida como `CurrentPageItem`.

Estrutura principal:

```text
task
│
├── grp_sidebar
│    └── re_sidebar
│
└── grp_content
     │
     ├── grp_task_header
     │
     └── grp_comments_section
          │
          └── rg_comments
```

A página apresenta:

* título;
* descrição;
* status;
* prioridade;
* responsável;
* projeto;
* data limite;
* comentários.

Funcionalidades:

* editar tarefa;
* alterar status;
* excluir/arquivar tarefa conforme permissão;
* adicionar comentário;
* editar comentário;
* arquivar comentário.

O estado `selected_comment` é utilizado para operações sobre comentários.

---

# 14. Página `activities`

A página `activities` funciona como área de consulta do histórico de atividades.

Ela utiliza dois Repeating Groups:

* `rg_activities_member`;
* `rg_activities_admin`.

A apresentação varia de acordo com o role do usuário.

A página permite:

* visualizar atividades;
* pesquisar;
* filtrar por ação;
* filtrar por usuário;
* filtrar por projeto;
* visualizar detalhes de uma atividade.

A página é essencialmente de **consulta**, não possuindo fluxo de criação ou edição manual de `ActivityLog`.

O popup:

`pop_activity_details`

recebe um `ActivityLog` no momento do clique e apresenta:

* descrição;
* ação;
* tarefa;
* colaborador;
* data;
* identificador da atividade.

---

# 15. Página `users`

A página `users` é destinada ao gerenciamento administrativo dos usuários.

Funcionalidades:

* visualizar usuários;
* pesquisar usuários;
* filtrar por role;
* criar usuários;
* editar usuários.

As ações de criação e edição são restritas a administradores.

A página utiliza estados para:

* armazenar o usuário selecionado;
* armazenar o e-mail do usuário recém-criado para o fluxo de confirmação.

---

# 16. Página `profile`

A página `profile` apresenta as informações do usuário autenticado.

Principais funcionalidades:

* visualizar nome;
* visualizar e-mail;
* editar nome;
* redefinir senha.

O e-mail é tratado como informação não editável pela interface atual.

O upload/alteração de avatar permanece como elemento preparado, mas desabilitado na implementação atual.

---

# 17. Componentes Reutilizáveis

A arquitetura atual utiliza principalmente os seguintes Reusable Elements:

## `re_header`

Responsável pela área superior da aplicação.

Inclui:

* identificação do sistema;
* informações do usuário;
* acesso a notificações;
* logout;
* navegação principal quando aplicável.

O componente utiliza `CurrentUser` diretamente e não depende de Data Source externo.

---

## `re_sidebar`

Responsável pela navegação lateral.

É utilizado pelas páginas internas da aplicação.

A sidebar possui comportamento de colapso através de estado próprio.

Itens de navegação são apresentados de acordo com a estrutura atual da aplicação e podem possuir restrições por role.

---

# 18. Componentes Internos

Além dos Reusable Elements, a aplicação utiliza componentes estruturais dentro das páginas:

* cards de projeto;
* cards de tarefa;
* cards de comentário;
* cards de notificação;
* cards de atividade;
* estados vazios;
* filtros;
* popups;
* grupos de formulário;
* Repeating Groups.

Esses elementos são mantidos dentro das respectivas páginas quando não existe necessidade de reutilização global.

---

# 19. Popups

Os popups são utilizados para ações contextuais sem necessidade de navegação.

Principais popups identificados:

* `pop_new_project`;
* `pop_edit_project`;
* `pop_new_task`;
* `pop_edit_task`;
* `pop_quick_status`;
* `pop_activity_details`;
* popups relacionados a comentários;
* popup de notificações;
* popup de redefinição de senha;
* popups de gerenciamento de usuários.

Os popups tipados utilizam o Data Type correspondente sempre que necessário.

Exemplos:

```text
pop_edit_project → Project
pop_edit_task → Task
pop_quick_status → Task
pop_activity_details → ActivityLog
```

---

# 20. Organização dos Workflows

Os Workflows são organizados por domínio funcional.

## Authentication

* Login
* Logout
* Sign Up
* Password Reset
* Redirect unauthenticated users

## Projects

* Create Project
* Update Project
* Archive Project
* Navigate to Project

## Tasks

* Create Task
* Update Task
* Delete/Archive Task
* Change Status
* Assign Task
* Navigate to Task

## Comments

* Add Comment
* Edit Comment
* Archive Comment

## Notifications

* Create Notification
* Mark Notification Read
* Mark All Notifications Read

## Activity Log

* Create ActivityLog
* Display Activity Details

## Users

* Create User
* Update User
* Manage User Role

## Profile

* Update Profile
* Reset Password

---

# 21. Comunicação entre Workflows

As operações importantes seguem um padrão de encadeamento.

Exemplo de criação de tarefa:

```text
Create Task
     │
     ├──► Create ActivityLog
     │
     └──► Create Notification
```

Alteração de status:

```text
Change Task Status
       │
       ├──► Update Task
       │
       ├──► Create ActivityLog
       │
       └──► Create Notification
```

Comentário:

```text
Create Comment
      │
      ├──► Create ActivityLog
      │
      └──► Create Notification
```

O objetivo é manter o registro das principais ações e fornecer feedback aos usuários afetados.

---

# 22. ActivityLog como Auditoria

O `ActivityLog` funciona como mecanismo de histórico da aplicação.

As principais ações registradas incluem:

* criação de tarefa;
* atualização de tarefa;
* exclusão/arquivamento de tarefa;
* alteração de status;
* alteração de responsável;
* criação de comentário;
* criação de notificação;
* atualização de projeto;
* arquivamento de tarefa;
* atualização de usuário;
* alteração de role.

A página `activities` utiliza esses registros para fornecer uma visão de auditoria.

---

# 23. Notifications

As notificações são armazenadas no Data Type `Notification`.

Cada notificação possui:

* título;
* mensagem;
* destinatário;
* indicador de leitura;
* tarefa relacionada, quando aplicável.

A privacidade garante que notificações sejam acessíveis apenas pelo destinatário.

As notificações podem:

* ser marcadas individualmente como lidas;
* ser marcadas em lote como lidas;
* direcionar o usuário para uma tarefa quando existir tarefa associada.

---

# 24. Navegação

A navegação atual segue principalmente o modelo de passagem de dados entre páginas.

Exemplo:

```text
Dashboard
   │
   ├── Project Card
   │       │
   │       ▼
   │    project
   │       │
   │       ▼
   │      task
   │
   ├── Task Card
   │       │
   │       ▼
   │      tasks
   │
   ├── Notification
   │       │
   │       ▼
   │      task
   │
   ├── Activities
   │
   ├── Users
   │
   └── Profile
```

Quando uma página representa uma entidade específica, o registro é enviado como `CurrentPageItem`.

Exemplos:

```text
Project → project
Task → task
```

Para operações temporárias dentro da mesma página, são utilizados Custom States.

Exemplos:

```text
selected_task
selected_comment
selected_project
selected_user
```

---

# 25. Convenção de Nomenclatura

A aplicação utiliza nomes curtos e consistentes em inglês para os elementos técnicos.

## Pages

Exemplos atuais:

```text
auth
index
projects
project
tasks
task
activities
users
profile
```

---

## Reusable Elements

Prefixo:

```text
re_
```

Exemplos:

```text
re_header
re_sidebar
```

---

## Groups

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

## Buttons

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

Preferencialmente:

```text
Verbo + Objeto
```

Exemplos:

```text
Create Task
Update Project
Create Notification
Mark Notification Read
Create Activity Log
```

---

# 26. Padrões de Interface

A maioria das páginas internas utiliza uma estrutura comum:

```text
Page
│
└── grp_page_wrapper
     │
     ├── grp_header
     │    └── re_header
     │
     └── grp_body
          │
          ├── grp_sidebar
          │    └── re_sidebar
          │
          └── grp_content
```

Esse padrão reduz duplicação visual e mantém consistência entre as páginas.

---

# 27. Padrões de Listagem

As listagens utilizam Repeating Groups com filtros aplicados diretamente na Data Source sempre que possível.

Exemplo:

```text
RepeatingGroup
      │
      ├── filtro por status
      ├── filtro por prioridade
      ├── filtro por projeto
      └── filtro textual
```

Essa abordagem reduz a quantidade de workflows necessários para operações de filtragem.

Estados vazios utilizam grupos ocultos por padrão com `collapse_when_hidden` quando necessário para evitar ocupação de espaço.

---

# 28. Privacidade e Segurança

O controle de acesso é dividido entre:

1. Privacy Rules;
2. Conditionals;
3. condições dos Workflows;
4. visibilidade dos elementos.

As regras mais importantes incluem:

* usuários possuem acesso aos próprios dados conforme as regras definidas;
* proprietários possuem controle sobre seus projetos;
* criadores possuem controle sobre suas tarefas;
* responsáveis possuem permissões específicas sobre tarefas;
* autores possuem controle sobre seus comentários;
* notificações são privadas para seus destinatários;
* atividades são disponibilizadas conforme o nível de acesso definido pela aplicação;
* ações administrativas são restritas ao role `Administrator`.

A interface não deve ser considerada o único mecanismo de segurança. Operações críticas devem possuir validação também no Workflow e/ou nas Privacy Rules.

---

# 29. Boas Práticas de Desenvolvimento

A manutenção da aplicação deve seguir as seguintes diretrizes:

* utilizar recursos nativos do Bubble sempre que possível;
* evitar duplicação de Workflows;
* centralizar regras de negócio nos Workflows;
* utilizar Option Sets para valores fixos;
* utilizar referências entre Data Types;
* utilizar Custom States apenas para dados temporários de interface;
* utilizar Repeating Groups para listagens;
* utilizar Popups para operações contextuais;
* manter Reusable Elements desacoplados;
* validar permissões antes de operações críticas;
* registrar ações relevantes no `ActivityLog`;
* manter as Privacy Rules alinhadas às regras de negócio;
* evitar lógica de negócio complexa diretamente na interface;
* atualizar a documentação quando houver alteração estrutural.

---

# 30. Elementos Removidos do MVP

O elemento:

```text
grp_dashboard_metrics
```

foi removido por não ser relevante para a primeira versão do produto.

Consequentemente:

* não deve ser referenciado em workflows;
* não deve ser considerado parte do dashboard atual;
* não deve ser incluído na documentação futura como componente ativo;
* métricas analíticas avançadas permanecem fora do MVP.

Essa decisão reduz a complexidade da primeira versão e mantém o dashboard focado nas funcionalidades essenciais.

---

# 31. Arquitetura de Evolução

A arquitetura atual permite futuras expansões sem alteração imediata da estrutura principal.

Possíveis evoluções:

* equipes;
* etiquetas;
* subtarefas;
* dependências entre tarefas;
* anexos;
* checklist;
* dashboard analítico;
* integrações externas;
* notificações externas;
* automações;
* aplicação mobile;
* quadro Kanban;
* funcionalidades avançadas de colaboração.

Essas funcionalidades não fazem parte da arquitetura funcional atual do MVP e devem ser tratadas como extensões futuras.

---

# 32. Estado Atual da Arquitetura

A arquitetura atual pode ser resumida da seguinte forma:

```text
                    OZYY - TASK MANAGER
                            │
                            ▼
                       Bubble.io
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
   Authentication        Database          Option Sets
        │                   │                   │
        │             ┌─────┼─────┐             │
        │             ▼     ▼     ▼             │
        │          Project Task  User           │
        │                  │                    │
        │             ┌────┴────┐               │
        │             ▼         ▼               │
        │          Comment  Notification        │
        │                  │                    │
        │                  └──────┐             │
        │                         ▼             │
        │                    ActivityLog        │
        │                         │             │
        └─────────────────────────┼─────────────┘
                                  ▼
                              Workflows
                                  │
                                  ▼
                                Pages
                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                    re_header         re_sidebar
```

O dashboard atual concentra projetos, tarefas pendentes e atividades recentes, sem o antigo componente de métricas analíticas.

---

# 33. Conclusão

A arquitetura atual do **Ozzy - Task Manager** está estruturada em torno dos recursos nativos do Bubble.io, utilizando Data Types, Option Sets, Privacy Rules, Workflows, Reusable Elements, Custom States, Repeating Groups e Popups.

A aplicação possui uma separação clara entre:

* autenticação;
* persistência de dados;
* regras de negócio;
* interface;
* componentes reutilizáveis.

A entidade `Task` permanece como núcleo operacional, enquanto `Project`, `Comment`, `Notification` e `ActivityLog` complementam o fluxo de gerenciamento.

A utilização de `re_header` e `re_sidebar` estabelece um padrão visual comum entre as páginas internas. As páginas específicas utilizam `CurrentPageItem` para entidades de detalhe e Custom States para operações temporárias de interface.

A arquitetura também incorpora controle de acesso por `UserRole`, combinando Privacy Rules, Workflows e Conditionals.

Esta versão deve ser considerada a **referência oficial da arquitetura do MVP atualmente implementado**, substituindo descrições de páginas, componentes ou funcionalidades que pertenciam apenas à fase de planejamento.
