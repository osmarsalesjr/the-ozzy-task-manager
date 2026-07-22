# Guia de Desenvolvimento

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento estabelece os padrões de desenvolvimento adotados no **Ozzy - Task Manager**, garantindo consistência na implementação, organização dos artefatos e facilidade de manutenção da aplicação.

Todas as funcionalidades deverão seguir estas convenções durante o desenvolvimento.

---

# 2. Princípios de Desenvolvimento

O projeto será desenvolvido seguindo os seguintes princípios:

* Utilizar exclusivamente recursos compatíveis com o plano gratuito do Bubble.
* Priorizar simplicidade em vez de soluções complexas.
* Evitar duplicação de lógica.
* Reutilizar componentes sempre que possível.
* Centralizar regras de negócio nos Workflows.
* Utilizar Option Sets para valores fixos.
* Manter baixo acoplamento entre páginas.
* Documentar alterações estruturais relevantes.

---

# 3. Organização do Projeto

A aplicação será organizada conforme a seguinte estrutura lógica.

```text
Application

├── Pages
├── Reusable Elements
├── Data Types
├── Option Sets
├── Styles
├── Workflows
├── Privacy Rules
└── Custom States
```

Cada elemento deverá possuir uma responsabilidade única.

---

# 4. Convenção de Nomenclatura

Toda a aplicação utilizará nomenclatura em inglês.

Não deverão ser utilizados espaços, acentos ou caracteres especiais.

---

## 4.1 Páginas

Formato:

```text
snake_case
```

Exemplos:

```text
login
signup
dashboard
projects
project_details
my_tasks
task_details
notifications
profile
```

---

## 4.2 Data Types

Formato:

```text
PascalCase
```

Exemplos:

```text
Project
Task
Comment
Notification
ActivityLog
```

O tipo **User** será o tipo nativo do Bubble.

---

## 4.3 Campos

Formato:

```text
snake_case
```

Exemplos:

```text
assigned_to

created_by

completed_date

due_date

is_read

project

position
```

---

## 4.4 Option Sets

Formato:

```text
PascalCase
```

Exemplos:

```text
UserRole

ProjectStatus

TaskStatus

TaskPriority

NotificationType

ActivityAction
```

---

## 4.5 Reusable Elements

Prefixo:

```text
re_
```

Exemplos:

```text
re_header

re_sidebar

re_project_card

re_task_card

re_comment_card

re_notification_card

re_activity_card

re_dashboard_widget
```

---

## 4.6 Grupos

Prefixo:

```text
grp_
```

Exemplos:

```text
grp_filters

grp_header

grp_sidebar

grp_task_details

grp_comments
```

---

## 4.7 Repeating Groups

Prefixo:

```text
rg_
```

Exemplos:

```text
rg_projects

rg_tasks

rg_comments

rg_notifications

rg_activity_log
```

---

## 4.8 Inputs

Prefixo:

```text
inp_
```

Exemplos:

```text
inp_title

inp_description

inp_due_date

inp_search
```

---

## 4.9 Dropdowns

Prefixo:

```text
ddl_
```

Exemplos:

```text
ddl_status

ddl_priority

ddl_project
```

---

## 4.10 Date Pickers

Prefixo:

```text
dtp_
```

Exemplo:

```text
dtp_due_date
```

---

## 4.11 Botões

Prefixo:

```text
btn_
```

Exemplos:

```text
btn_save

btn_cancel

btn_delete

btn_login

btn_create_project
```

---

## 4.12 Ícones

Prefixo:

```text
ico_
```

---

## 4.13 Textos

Prefixo:

```text
txt_
```

---

## 4.14 Popups

Prefixo:

```text
pop_
```

Exemplos:

```text
pop_delete_task

pop_archive_project
```

---

## 4.15 Custom States

Formato:

```text
cs_
```

Exemplos:

```text
cs_selected_project

cs_selected_task

cs_is_loading

cs_filter_status
```

---

## 4.16 Workflows

Todos os Workflows deverão utilizar:

```text
Verbo + Objeto
```

Exemplos:

```text
Create Task

Update Task

Delete Task

Archive Project

Register Activity

Mark Notification Read
```

---

# 5. Organização das Páginas

Cada página deverá possuir responsabilidade única.

| Página          | Responsabilidade        |
| --------------- | ----------------------- |
| login           | Autenticação            |
| signup          | Cadastro                |
| dashboard       | Visão geral             |
| projects        | Lista de projetos       |
| project_details | Informações do projeto  |
| my_tasks        | Lista de tarefas        |
| task_details    | Detalhes da tarefa      |
| notifications   | Central de notificações |
| profile         | Perfil do usuário       |

---

# 6. Organização dos Reusable Elements

Todos os elementos reutilizados em mais de uma página deverão ser implementados como Reusable Elements.

Componentes obrigatórios:

* Header
* Sidebar
* Project Card
* Task Card
* Comment Card
* Notification Card
* Activity Card
* Dashboard Widget
* Empty State
* Confirmation Modal

---

# 7. Organização dos Workflows

Os Workflows deverão ser agrupados por domínio funcional.

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

# 8. Estratégia de Custom States

Os Custom States deverão ser utilizados apenas para armazenar estados temporários da interface.

Não deverão substituir informações persistidas no banco.

Casos recomendados:

* filtros;
* seleção de registros;
* controle de abas;
* estados de carregamento;
* exibição de modais.

---

# 9. Estratégia de Privacy Rules

Todas as regras de acesso deverão ser configuradas antes da implementação das funcionalidades.

Diretrizes:

* Usuários autenticados acessam apenas páginas privadas.
* Usuários alteram apenas seus próprios dados.
* Projetos e tarefas devem respeitar as permissões definidas pela aplicação.
* Campos sensíveis não devem ser expostos desnecessariamente.

---

# 10. Estratégia para Option Sets

Todos os valores fixos deverão utilizar Option Sets.

Nunca utilizar textos livres para representar:

* status;
* prioridades;
* perfis;
* ações;
* tipos de notificação.

Essa abordagem reduz erros de digitação e facilita futuras alterações.

---

# 11. Organização dos Estilos

Os estilos deverão ser centralizados no gerenciador de Styles do Bubble.

Categorias sugeridas:

* Heading
* Body
* Caption
* Button Primary
* Button Secondary
* Input
* Card
* Badge
* Modal

Nenhuma página deverá possuir estilos exclusivos sem justificativa.

---

# 12. Boas Práticas

Durante o desenvolvimento deverão ser observadas as seguintes diretrizes:

* Evitar duplicação de Workflows.
* Evitar lógica diretamente na interface.
* Reutilizar componentes sempre que possível.
* Utilizar relacionamentos entre Data Types.
* Manter nomes consistentes.
* Documentar alterações estruturais.
* Testar cada funcionalidade antes de iniciar a próxima.
* Registrar automaticamente ações importantes através do ActivityLog.

---

# 13. Fluxo de Desenvolvimento

Cada funcionalidade deverá seguir o seguinte processo:

1. Validar o requisito.
2. Atualizar a modelagem (quando necessário).
3. Criar ou atualizar a interface.
4. Implementar o Workflow.
5. Validar as Privacy Rules.
6. Executar testes.
7. Atualizar a documentação.

---

# 14. Checklist para Novas Funcionalidades

Antes de considerar uma funcionalidade concluída, verificar:

* [ ] Banco de dados atualizado.
* [ ] Option Sets atualizados.
* [ ] Privacy Rules revisadas.
* [ ] Interface implementada.
* [ ] Reusable Elements utilizados.
* [ ] Workflow implementado.
* [ ] ActivityLog registrado.
* [ ] Notificações implementadas (quando aplicável).
* [ ] Testes executados.
* [ ] Documentação atualizada.

---

# 15. Considerações Finais

Este guia estabelece o padrão oficial de desenvolvimento do **Ozzy - Task Manager**.

Todas as implementações futuras deverão seguir estas convenções para manter a consistência da solução, facilitar sua manutenção e permitir que novos desenvolvedores compreendam rapidamente a organização do projeto.
