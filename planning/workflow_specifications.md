# Especificação Funcional dos Workflows

# Ozzy - Task Manager

**Versão:** 2.0
**Plataforma:** Bubble.io — Plano Gratuito
**Status:** Atualizado conforme implementação atual

---

# 1. Objetivo

Este documento descreve os principais Workflows atualmente implementados no **Ozzy - Task Manager**.

A especificação tem como objetivo servir como referência para:

* manutenção;
* correção de problemas;
* evolução da aplicação;
* entendimento das regras de negócio;
* validação dos fluxos implementados no Bubble.

A documentação prioriza o comportamento efetivamente implementado na aplicação.

---

# 2. Arquitetura Geral dos Workflows

Os workflows seguem, de forma geral, o seguinte fluxo:

```text
Evento do usuário
       ↓
Validação / Permissão
       ↓
Alteração ou criação de dados
       ↓
ActivityLog (quando aplicável)
       ↓
Notification (quando aplicável)
       ↓
Atualização da interface
```

Nem todos os workflows possuem todas as etapas.

Workflows exclusivamente visuais, como abrir ou fechar popups e navegar entre páginas, não geram registros de atividade.

---

# 3. Autenticação

## WF-001 — Redirecionar usuário não autenticado

### Evento

`Page is loaded`.

### Condição

```text
CurrentUser's not_logged_in = true
```

### Ação

Redirecionar para:

```text
auth
```

Esse padrão está presente nas principais páginas operacionais do sistema.

---

## WF-002 — Logout

### Evento

Clique em **Sair**.

### Ações

1. Executar `LogOut`.
2. Navegar para `auth`.

O logout também é disponibilizado pelo componente reutilizável `re_header` e pela navegação global.

---

# 4. Workflows do Dashboard

Página:

```text
index
```

## WF-101 — Redirecionar usuário não autenticado

Executa o redirecionamento para `auth` quando o usuário não está autenticado.

---

## WF-102 — Abrir popup de novo projeto

### Evento

Clique em:

```text
NewProjectBtn
```

### Ação

Exibir:

```text
pop_new_project
```

---

## WF-103 — Criar projeto pelo Dashboard

### Evento

Clique em:

```text
btn_popup_create
```

### Condição

Nome do projeto não vazio.

### Ações

1. Criar `Project`.
2. Fechar `pop_new_project`.
3. Resetar os campos do formulário.

### Dados principais

```text
name = inp_project_name
description = inp_project_description
owner = CurrentUser
archived = false
```

### Observação

A criação de projeto pelo Dashboard atualmente **não gera ActivityLog nem Notification**.

---

## WF-104 — Cancelar criação de projeto

### Evento

Clique em `btn_popup_cancel`.

### Ação

Ocultar:

```text
pop_new_project
```

---

## WF-105 — Abrir projeto

### Evento

Clique no card de projeto.

### Ação

Navegar para:

```text
project
```

enviando o projeto selecionado como dado da página.

---

## WF-106 — Abrir tarefas

### Evento

Clique em:

```text
btn_tasks_ver_todas
```

### Ação

Navegar para:

```text
tasks
```

---

## WF-107 — Abrir tarefa

### Evento

Clique no card de tarefa.

### Ação

Navegar para a página:

```text
tasks
```

enviando a tarefa selecionada.

---

## WF-108 — Abrir detalhes da atividade

### Evento

Clique em um item do:

```text
rg_recent_activity
```

### Ações

1. Definir os dados do `pop_activity_details`.
2. Exibir o popup.

O popup recebe diretamente o `ActivityLog` correspondente à célula selecionada. A funcionalidade foi validada durante a auditoria e o grupo `grp_dashboard_metrics` posteriormente foi removido do produto por não fazer mais parte do MVP.

---

## WF-109 — Fechar detalhes da atividade

### Evento

Clique em:

```text
btn_close_activity_details
```

### Ação

Ocultar:

```text
pop_activity_details
```

---

## WF-110 — Histórico de atividades — Member

### Evento

Clique em:

```text
btn_activity_ver_historico
```

### Ação

Navegar para a página de atividades.

---

## WF-111 — Histórico de atividades — Administrator

### Evento

Clique em:

```text
btn_activity_ver_historico_admin
```

### Ação

Navegar para a página de atividades.

---

## WF-112 — Logout

Executado pelo evento global de logout.

---

# 5. Workflows de Projetos

Página:

```text
projects
```

## WF-201 — Abrir popup de novo projeto

### Evento

Clique em:

```text
NewProjectBtn
```

### Ação

Exibir:

```text
pop_new_project
```

O botão é visível somente para usuários com:

```text
CurrentUser's role = administrator
```

---

## WF-202 — Criar projeto

### Evento

Clique em:

```text
btn_save_new_project
```

### Condição

```text
inp_project_name is not empty
```

### Ação

Criar `Project` com:

```text
name = inp_project_name
description = inp_project_description
status = dd_project_status
owner = CurrentUser
archived = false
```

Depois:

1. Ocultar popup.
2. Resetar nome.
3. Resetar descrição.
4. Resetar status.

### ActivityLog

Não é criado atualmente.

---

## WF-203 — Cancelar criação de projeto

### Ações

1. Resetar campos.
2. Ocultar popup.

---

## WF-204 — Abrir edição de projeto

### Evento

Clique em:

```text
btn_edit_project
```

### Ações

1. Salvar projeto selecionado no custom state `selected_project_`.
2. Exibir `pop_edit_project`.

O popup utiliza o projeto armazenado no custom state como `data source`.

---

## WF-205 — Editar projeto

### Evento

Clique em:

```text
btn_save_edit_project
```

### Condição

Nome não vazio.

### Ações

Atualizar:

```text
name
description
status
```

Depois:

1. Ocultar popup.
2. Resetar os inputs.

---

## WF-206 — Cancelar edição de projeto

### Ações

1. Resetar inputs.
2. Ocultar popup.

---

## WF-207 — Abrir projeto

### Evento

Clique no card do projeto.

### Ação

Navegar para:

```text
project
```

enviando o projeto selecionado.

---

## WF-208 — Limpar filtros de projetos

### Evento

Clique em:

```text
btn_clear_project_filters
```

### Ação

Resetar o grupo:

```text
grp_projects_filters
```

Os filtros são aplicados diretamente na fonte do RepeatingGroup, sem workflow de pesquisa separado.

---

# 6. Workflows de Tarefas — Projeto

Página:

```text
project
```

## WF-301 — Abrir criação de tarefa

### Evento

Clique em:

```text
btn_new_task
```

ou

```text
btn_tasks_new_task
```

### Ação

Exibir:

```text
pop_new_task
```

---

## WF-302 — Cancelar criação de tarefa

### Evento

Clique em:

```text
btn_task_cancel
```

### Ação

Ocultar:

```text
pop_new_task
```

---

## WF-303 — Criar tarefa

### Evento

Clique em:

```text
btn_task_create
```

### Condição

Título não vazio.

### Ações

1. Criar `Task`.
2. Definir projeto como `CurrentPageItem`.
3. Definir status inicial como `to_do`.
4. Criar `ActivityLog` com `task_created`.
5. Criar `Notification` para o responsável quando o responsável for diferente do usuário atual.
6. Ocultar popup.
7. Resetar inputs.
8. Atualizar `rg_project_tasks`.

---

## WF-304 — Abrir tarefa

### Evento

Clique no card:

```text
grp_task_card_placeholder
```

### Ação

Navegar para:

```text
task
```

enviando a tarefa atual da célula.

---

## WF-305 — Abrir edição de tarefa

### Evento

Clique em:

```text
btn_edit_task_card
```

### Ações

1. Definir custom state `selected task`.
2. Exibir `pop_edit_task`.

---

## WF-306 — Salvar edição de tarefa

### Evento

Clique em:

```text
btn_edit_task_save
```

### Condição

Título não vazio.

### Dados atualizados

```text
title
description
priority
assigned_to
due_date
status
```

### Ações

1. Atualizar a tarefa selecionada.
2. Criar `ActivityLog` com `task_updated`.
3. Criar `Notification` para o responsável quando aplicável.
4. Ocultar popup.
5. Resetar inputs.
6. Atualizar `rg_project_tasks`.

---

## WF-307 — Cancelar edição de tarefa

Oculta o popup de edição.

---

# 7. Workflows da Página de Tarefa

Página:

```text
task
```

A página possui atualmente 19 workflows.

## WF-401 — Redirecionar usuário não autenticado

Redireciona para `auth` quando necessário.

---

## WF-402 — Navegar para projeto

### Evento

Clique no projeto exibido nos metadados da tarefa.

### Ação

Navegar para:

```text
project
```

enviando:

```text
CurrentPageItem's project
```

---

## WF-403 — Abrir alteração de status

### Evento

Clique em:

```text
btn_change_status
```

### Ação

Exibir:

```text
pop_change_status
```

---

## WF-404 — Abrir arquivamento da tarefa

### Evento

Clique em:

```text
btn_delete_task
```

### Ação

Exibir:

```text
pop_delete_task
```

---

## WF-405 — Cancelar edição da tarefa

Oculta:

```text
pop_edit_task
```

---

## WF-406 — Salvar edição da tarefa

### Evento

Clique em:

```text
btn_edit_save
```

### Condição

Título não vazio.

### Atualizações

```text
title
description
priority
status
assigned_to
due_date
```

### Ações complementares

* Criar `ActivityLog` com `task_updated`.
* Ocultar popup.
* Resetar inputs.

---

## WF-407 — Cancelar alteração de status

Oculta:

```text
pop_change_status
```

---

## WF-408 — Salvar alteração de status

### Evento

Clique em:

```text
btn_status_save
```

### Ações

1. Atualizar somente `status`.
2. Criar `ActivityLog` com `status_changed`.
3. Criar `Notification` para o responsável quando aplicável.
4. Ocultar popup.
5. Resetar inputs.

---

## WF-409 — Cancelar arquivamento da tarefa

Oculta:

```text
pop_delete_task
```

---

## WF-410 — Arquivar tarefa

O sistema utiliza **soft delete**, portanto a tarefa não é fisicamente excluída.

### Evento

Clique em:

```text
btn_delete_confirm
```

### Condição

```text
CurrentUser's role = administrator
```

### Ações

1. Alterar `Task.archived = true`.
2. Criar `ActivityLog` com `task_archived`.
3. Fechar popup.
4. Navegar para o projeto da tarefa.

> Portanto, a especificação atual não deve tratar a exclusão de tarefa como `DeleteThing`.

---

# 8. Workflows de Comentários

## WF-501 — Adicionar comentário

### Evento

Clique em:

```text
btn_add_comment
```

### Condição

Mensagem não vazia.

### Ações

1. Criar `Comment`.
2. Definir:

   * `message`
   * `author = CurrentUser`
   * `task = CurrentPageItem`
3. Resetar campo de comentário.
4. Atualizar lista de comentários.
5. Criar `ActivityLog` com `comment_added`.
6. Criar `Notification` para o responsável quando este for diferente do usuário atual.

---

## WF-502 — Abrir edição de comentário

### Evento

Clique em:

```text
btn_edit_comment
```

### Ações

1. Armazenar o comentário atual no custom state `selected_comment`.
2. Exibir `pop_edit_comment`.

---

## WF-503 — Abrir arquivamento de comentário

### Evento

Clique em:

```text
btn_delete_comment
```

### Ações

1. Armazenar comentário em `selected_comment`.
2. Exibir `pop_delete_comment`.

---

## WF-504 — Cancelar edição de comentário

Oculta:

```text
pop_edit_comment
```

---

## WF-505 — Editar comentário

### Evento

Clique em:

```text
btn_edit_comment_save
```

### Condições

* Mensagem não vazia.
* Usuário atual é o autor.

### Ações

1. Atualizar `message`.
2. Criar `ActivityLog`.
3. Ocultar popup.
4. Resetar inputs.
5. Atualizar lista de comentários.

O tipo de `ActivityAction` utilizado especificamente para a edição do comentário não foi identificado na auditoria disponível e não deve ser presumido nesta documentação.

---

## WF-506 — Cancelar arquivamento de comentário

Oculta:

```text
pop_delete_comment
```

---

## WF-507 — Arquivar comentário

### Evento

Clique em:

```text
btn_delete_comment_confirm
```

### Condição

Usuário é:

```text
administrator
```

ou

```text
author do comentário
```

### Ações

1. Alterar `Comment.archived = yes`.
2. Criar `ActivityLog`.
3. Fechar popup.
4. Atualizar lista de comentários.

> Assim como as tarefas, comentários utilizam arquivamento em vez de exclusão física.

---

# 9. Workflows da Página de Tarefas

Página:

```text
tasks
```

## WF-601 — Redirecionar usuário não autenticado

Redireciona para `auth`.

---

## WF-602 — Limpar filtros

### Evento

Clique em:

```text
btn_clear_filters
```

### Ação

Resetar:

```text
grp_tasks_filters
```

---

## WF-603 — Abrir tarefa pelo título

### Evento

Clique em:

```text
txt_placeholder_task
```

### Ação

Navegar para:

```text
task
```

enviando a tarefa da célula.

---

## WF-604 — Abrir projeto pela tabela

### Evento

Clique em:

```text
txt_placeholder_project
```

### Ação

Navegar para:

```text
project
```

enviando o projeto relacionado à tarefa.

---

## WF-605 — Abrir tarefa pelo botão

### Evento

Clique em:

```text
btn_task_open
```

### Ação

Navegar para:

```text
task
```

---

## WF-606 — Abrir alteração rápida de status

### Evento

Clique em:

```text
btn_task_status
```

### Ações

1. Definir `selected task` no `grp_tasks_list_container`.
2. Exibir `pop_quick_status`.

---

## WF-607 — Cancelar alteração rápida

Oculta:

```text
pop_quick_status
```

---

## WF-608 — Salvar alteração rápida de status

### Ações

1. Atualizar o status da tarefa selecionada.
2. Criar `ActivityLog` com `status_changed`.
3. Criar `Notification` para o responsável.
4. Ocultar popup.
5. Resetar dropdown.

---

# 10. Workflows de Notificações

Página:

```text
notifications
```

## WF-701 — Redirecionar usuário não autenticado

Redireciona para `auth`.

---

## WF-702 — Marcar notificação como lida

### Evento

Clique no:

```text
grp_notification_card
```

### Ações

1. Alterar `is_read = true`.
2. Se a notificação possuir tarefa vinculada, navegar para a página `task`.
3. Caso não possua tarefa, permanecer na página de notificações.

---

## WF-703 — Marcar todas como lidas

### Evento

Clique em:

```text
btn_mark_all_read
```

### Ações

1. Buscar notificações não lidas do `CurrentUser`.
2. Alterar todas para `is_read = true`.

## O botão somente é exibido quando existem notificações não lidas.

# 11. Workflows de Usuários

Página:

```text
users
```

As operações de gestão de usuários são restritas a administradores.

## WF-801 — Abrir edição de usuário

### Evento

Clique em:

```text
btn_edit_user
```

### Ações

1. Armazenar usuário selecionado em `selected user`.
2. Exibir `pop_edit_user`.

---

## WF-802 — Abrir criação de usuário

### Evento

Clique em:

```text
btn_new_user
```

### Ação

Exibir:

```text
pop_new_user
```

O botão é visível somente para administradores.

---

## WF-803 — Limpar filtros de usuários

### Evento

Clique em:

```text
btn_clear_user_filters
```

### Ação

Resetar:

```text
grp_users_filters
```

---

## WF-804 — Cancelar edição de usuário

### Ações

1. Resetar inputs.
2. Ocultar popup.

---

## WF-805 — Editar usuário

### Evento

Clique em:

```text
btn_save_edit_user
```

### Atualizações

```text
name
role
```

O e-mail não é alterado pelo workflow.

---

## WF-806 — Cancelar criação de usuário

### Ações

1. Resetar inputs.
2. Ocultar popup.

---

## WF-807 — Criar usuário

### Evento

Clique em:

```text
btn_save_new_user
```

### Condições

Nome e e-mail preenchidos.

### Ações

1. Criar conta através de `CreateUserAccount`.
2. Utilizar role selecionada.
3. Armazenar e-mail no custom state `new user email`.
4. Enviar e-mail de redefinição de senha.
5. Ocultar popup.
6. Resetar inputs.
7. Exibir popup de confirmação.

O fluxo utiliza atualmente uma senha temporária fixa (`12345678`), seguida imediatamente pelo envio do e-mail para definição da senha definitiva.

---

## WF-808 — Fechar confirmação de criação

### Evento

Clique em:

```text
btn_close_new_user_confirmation
```

### Ação

Ocultar:

```text
pop_new_user_confirmation
```

---

# 12. Workflows de Atividades

Página:

```text
activities
```

A página é essencialmente de consulta e auditoria. Ela não cria nem edita `ActivityLog`.

## WF-901 — Redirecionar usuário não autenticado

Redireciona para `auth`.

---

## WF-902 — Abrir detalhes de atividade — Member

### Evento

Clique em:

```text
grp_activities_row_placeholder
```

### Ações

1. Definir o `ActivityLog` selecionado no popup.
2. Exibir `pop_activity_details`.

---

## WF-903 — Abrir detalhes de atividade — Administrator

### Evento

Clique na linha correspondente do RG administrativo.

### Ações

1. Definir o `ActivityLog` selecionado.
2. Exibir `pop_activity_details`.

---

## WF-904 — Fechar detalhes da atividade

### Evento

Clique em:

```text
btn_close_activity_details
```

### Ação

Ocultar:

```text
pop_activity_details
```

---

## WF-905 — Limpar filtros

A página possui um quinto workflow identificado pelo contador, relacionado aos filtros da página, embora sua implementação detalhada não tenha sido completamente capturada na auditoria.

---

# 13. Workflows de Perfil

Página:

```text
profile
```

## WF-1001 — Salvar alterações do perfil

### Evento

Clique em:

```text
BtnSave
```

### Ação

Atualizar somente:

```text
CurrentUser.name
```

O e-mail não pode ser alterado pelo usuário.

---

## WF-1002 — Cancelar edição do perfil

### Evento

Clique em:

```text
BtnCancel
```

### Ação

Resetar os inputs do perfil.

---

## WF-1003 — Solicitar redefinição de senha

### Evento

Clique em:

```text
btn_change_password
```

### Ações

1. Enviar e-mail de redefinição para o e-mail do usuário atual.
2. Exibir popup de confirmação.

---

## WF-1004 — Fechar confirmação de redefinição

### Evento

Clique em:

```text
btn_close_password_reset_confirmation
```

### Ação

Ocultar o popup.

---

# 14. Workflows do Header Reutilizável

Reusable:

```text
re_header
```

## WF-1101 — Navegar para Dashboard

### Evento

Clique em:

```text
grp_brand
```

### Ação

Navegar para:

```text
index
```

---

## WF-1102 — Abrir popup de notificações

### Evento

Clique em:

```text
btn_notifications
```

### Ação

Exibir:

```text
pop_notifications
```

---

## WF-1103 — Abrir notificação

### Evento

Clique em:

```text
btn_notification_open
```

### Ações

1. Marcar notificação como lida.
2. Fechar popup.
3. Navegar para `task`.
4. Enviar a tarefa relacionada.

O workflow também utiliza o `task_id` como parâmetro de URL.

---

## WF-1104 — Marcar todas as notificações como lidas

### Evento

Clique em:

```text
btn_mark_all_read
```

### Ações

1. Buscar notificações não lidas do usuário.
2. Alterar `is_read = true`.
3. Atualizar o RepeatingGroup de notificações.

O refresh manual do RG é realizado após o `ChangeListOfThings`.

---

## WF-1105 — Logout

### Evento

Clique em:

```text
btn_logout
```

### Ações

1. Executar `LogOut`.
2. Navegar para `auth`.

---

# 15. Workflows da Sidebar Reutilizável

Reusable:

```text
re_sidebar
```

## WF-1201 — Alternar sidebar

### Evento

Clique em:

```text
btn_sidebar_toggle
```

### Ação

Inverter o custom state:

```text
is_collapsed
```

A expressão utilizada é equivalente a:

```text
re_sidebar's is_collapsed is false
```

Isso implementa o toggle entre expandido e colapsado.

---

## WF-1202 — Navegar para Dashboard

Destino:

```text
index
```

---

## WF-1203 — Navegar para Projetos

Destino:

```text
projects
```

---

## WF-1204 — Navegar para Notificações

Destino:

```text
notifications
```

---

## WF-1205 — Navegar para Tarefas

Destino:

```text
tasks
```

---

## WF-1206 — Navegar para Atividades

Destino:

```text
activities
```

---

## WF-1207 — Navegar para Colaboradores

Destino:

```text
users
```

---

## WF-1208 — Navegar para Perfil

Destino:

```text
profile
```

---

# 16. Regras de Negócio Implementadas nos Workflows

## RN-WF01 — Somente administradores gerenciam usuários

Os botões de criação e edição de usuários são exibidos somente para:

```text
CurrentUser's role = administrator
```

---

## RN-WF02 — Somente administradores arquivam tarefas

O workflow de arquivamento verifica explicitamente a role do usuário.

---

## RN-WF03 — O criador controla a edição de comentários

O workflow de edição verifica se:

```text
CurrentUser = Comment.author
```

---

## RN-WF04 — Administrador ou autor pode arquivar comentários

O arquivamento de comentário permite:

```text
administrator
OU
author
```

---

## RN-WF05 — Exclusões utilizam arquivamento

As tarefas e comentários não são removidos fisicamente pelo fluxo atual.

```text
Task.archived = true
Comment.archived = yes
```

---

## RN-WF06 — Alterações relevantes geram ActivityLog

São registrados, entre outros:

```text
task_created
task_updated
task_archived
status_changed
comment_added
project_updated
```

A lista atual de `ActivityAction` também contempla ações relacionadas a usuários e notificações.

---

## RN-WF07 — Notificações são direcionadas ao responsável

As notificações relacionadas a tarefas são criadas para o responsável quando aplicável.

Em diversos fluxos existe a condição de não notificar o próprio usuário quando ele é o responsável pela ação.

---

## RN-WF08 — Notificações pertencem ao usuário destinatário

As buscas de notificações utilizam:

```text
recipient = CurrentUser
```

e as regras de privacidade restringem o acesso ao destinatário.

---

## RN-WF09 — Filtros são aplicados diretamente na fonte dos RepeatingGroups

As páginas `projects`, `tasks`, `notifications` e `activities` utilizam buscas com constraints diretamente na fonte dos RepeatingGroups.

Não é necessário um workflow separado para executar a pesquisa.

---

# 17. ActivityLog

O `ActivityLog` é criado pelos workflows responsáveis pelas alterações relevantes.

### Ações atualmente utilizadas

```text
task_created
task_updated
task_deleted
status_changed
comment_added
assignee_changed
notification_created
project_updated
task_archived
user_updated
role_user_updated
```

### Observação

Embora a especificação anterior previsse um campo `metadata`, o Data Type atual de `ActivityLog` não possui esse campo. Os workflows devem utilizar somente os campos existentes:

```text
user
description
task
action
```

---

# 18. Notification

O Data Type atual de `Notification` possui:

```text
title
message
recipient
is_read
task
```

Portanto, a especificação anterior que previa um campo `type` deve ser considerada obsoleta.

Os workflows devem utilizar os campos atualmente existentes.

---

# 19. Soft Delete

O sistema utiliza arquivamento para preservar registros.

### Task

```text
archived = true
```

### Comment

```text
archived = yes
```

Os RepeatingGroups principais utilizam esse estado para impedir que registros arquivados apareçam nas listagens operacionais.

---

# 20. Fluxos Integrados

## Criar Tarefa

```text
Usuário
   ↓
Preenche formulário
   ↓
Validar título
   ↓
Criar Task
   ↓
Criar ActivityLog: task_created
   ↓
Criar Notification para responsável
   ↓
Fechar popup
   ↓
Atualizar lista
```

---

## Editar Tarefa

```text
Usuário
   ↓
Seleciona tarefa
   ↓
Abre edição
   ↓
Atualiza Task
   ↓
Criar ActivityLog: task_updated
   ↓
Criar Notification quando aplicável
   ↓
Atualizar interface
```

---

## Alterar Status

```text
Usuário
   ↓
Seleciona novo status
   ↓
Atualizar Task.status
   ↓
Criar ActivityLog: status_changed
   ↓
Criar Notification
   ↓
Atualizar interface
```

---

## Arquivar Tarefa

```text
Administrador
   ↓
Confirma arquivamento
   ↓
Task.archived = true
   ↓
Criar ActivityLog: task_archived
   ↓
Retornar para projeto
```

---

## Adicionar Comentário

```text
Usuário
   ↓
Escreve comentário
   ↓
Criar Comment
   ↓
Criar ActivityLog: comment_added
   ↓
Criar Notification
   ↓
Atualizar comentários
```

---

## Arquivar Comentário

```text
Administrador ou autor
   ↓
Confirma arquivamento
   ↓
Comment.archived = yes
   ↓
Criar ActivityLog
   ↓
Atualizar comentários
```

---

# 21. Workflows que Não Devem Ser Tratados Como Funcionalidades Independentes

Algumas operações são implementadas diretamente na fonte de dados ou em componentes reutilizáveis e, portanto, não exigem workflows específicos.

Exemplos:

* filtros dos RepeatingGroups;
* ordenação das listas;
* exibição condicional por role;
* exibição do badge de notificações;
* estados vazios;
* alteração visual da sidebar;
* navegação global.

Isso evita criar workflows desnecessários para comportamentos que o Bubble já consegue executar de forma declarativa.

---

# 22. Pontos de Atenção para Manutenção

## 22.1 ActivityLog

Sempre que uma nova ação relevante for criada, avaliar se ela deve gerar um novo `ActivityLog`.

---

## 22.2 Notification

Antes de criar uma notificação, verificar se:

* existe um destinatário;
* existe uma tarefa relacionada quando necessário;
* o usuário atual não deve receber sua própria notificação.

---

## 22.3 Permissões

Alterações críticas devem possuir validação tanto na interface quanto no próprio workflow.

Exemplos atuais:

* gestão de usuários;
* arquivamento de tarefas;
* edição de comentários;
* arquivamento de comentários.

---

## 22.4 Soft Delete

Não substituir:

```text
archived = true
```

ou:

```text
archived = yes
```

por `DeleteThing` sem validar previamente o impacto sobre histórico e relacionamentos.

---

## 22.5 Custom States

Os principais estados temporários atualmente utilizados incluem:

```text
selected_project_
selected task
selected_comment
selected user
new user email
is_collapsed
```

Esses estados devem ser mantidos apenas quando necessários para controlar contexto de popups ou componentes.

---

# 23. Critérios para Novos Workflows

Antes de criar um novo workflow, verificar:

1. O comportamento já pode ser resolvido pela fonte de dados?
2. O comportamento já existe em um componente reutilizável?
3. Existe um workflow semelhante que pode ser reutilizado?
4. A ação altera dados?
5. A ação exige ActivityLog?
6. A ação exige Notification?
7. Existe uma regra de permissão?
8. A interface precisa ser atualizada após a alteração?

A criação de workflows duplicados deve ser evitada.

---

# 24. Considerações Finais

Esta especificação representa o **estado funcional atual dos workflows do Ozzy - Task Manager**.

A implementação atual utiliza uma arquitetura baseada em:

```text
Pages
   ↓
Reusable Components
   ↓
Workflows
   ↓
Bubble Data Types
   ↓
ActivityLog / Notifications
```

As principais entidades operacionais são:

```text
User
Project
Task
Comment
Notification
ActivityLog
```

A `Task` permanece como o centro do fluxo operacional, enquanto `Comment`, `Notification` e `ActivityLog` complementam os recursos de colaboração, comunicação e rastreabilidade.

A documentação deve ser atualizada sempre que novos workflows ou regras de negócio forem adicionados ao Bubble.

**Regra principal de manutenção:**

> A implementação do Bubble deve ser considerada a fonte de verdade. Este documento deve refletir o comportamento efetivamente implementado, e não workflows planejados que ainda não existem.
