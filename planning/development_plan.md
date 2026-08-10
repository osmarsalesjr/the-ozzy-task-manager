# Guia de Desenvolvimento

# Ozzy - Task Manager

**Versão:** 2.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento estabelece os padrões de desenvolvimento adotados no **Ozzy - Task Manager**, garantindo consistência na implementação, organização dos elementos e facilidade de manutenção da aplicação.

As definições deste documento devem ser utilizadas em conjunto com:

* Planejamento do Projeto;
* Modelagem de Dados;
* Especificação dos Workflows;
* Arquitetura da Solução;
* Especificação Funcional das Telas.

---

# 2. Princípios de Desenvolvimento

O projeto deverá seguir os seguintes princípios:

* Utilizar recursos compatíveis com o plano gratuito do Bubble.
* Priorizar simplicidade e manutenção.
* Evitar duplicação de lógica.
* Utilizar elementos reutilizáveis quando houver repetição.
* Centralizar regras de negócio nos Workflows.
* Utilizar Option Sets para valores controlados.
* Utilizar referências entre Data Types em vez de duplicação de dados.
* Aplicar Privacy Rules de acordo com as responsabilidades de cada entidade.
* Manter a interface desacoplada da lógica de negócio.
* Atualizar a documentação quando houver alterações estruturais relevantes.

---

# 3. Organização do Projeto

A aplicação deverá ser organizada nos seguintes recursos principais:

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

Cada recurso deverá possuir uma responsabilidade clara.

---

# 4. Convenção de Nomenclatura

Toda a estrutura técnica deverá utilizar nomenclatura em inglês.

Não utilizar:

* espaços;
* acentos;
* caracteres especiais;
* nomes ambíguos.

---

## 4.1 Páginas

Utilizar `snake_case`.

```text
login
signup
forgot_password
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

Utilizar `PascalCase`.

```text
User
Project
Task
Comment
Notification
ActivityLog
```

O `User` deverá utilizar exclusivamente o Data Type nativo do Bubble.

---

## 4.3 Campos

Utilizar `snake_case`.

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

Os nomes devem representar diretamente a finalidade do campo.

---

## 4.4 Option Sets

Utilizar `PascalCase`.

Option Sets atualmente utilizados:

```text
UserRole
ProjectStatus
TaskStatus
TaskPriority
ActivityAction
CommentStatus
```

O Option Set `NotificationType` não faz parte da estrutura atual do banco e não deverá ser criado apenas para seguir documentação anterior.

---

## 4.5 Reusable Elements

Utilizar o prefixo:

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
re_empty_state
re_confirmation_modal
```

---

## 4.6 Grupos

Utilizar o prefixo:

```text
grp_
```

Exemplos:

```text
grp_header
grp_sidebar
grp_filters
grp_task_details
grp_comments
```

Elementos removidos do projeto não deverão permanecer documentados ou ser recriados sem necessidade.

> O elemento `grp_dashboard_metrics` foi removido por não ser relevante para a primeira versão do produto.

---

## 4.7 Repeating Groups

Utilizar o prefixo:

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

Utilizar o prefixo:

```text
inp_
```

Exemplos:

```text
inp_name
inp_email
inp_title
inp_description
inp_due_date
inp_search
```

---

## 4.9 Dropdowns

Utilizar o prefixo:

```text
ddl_
```

Exemplos:

```text
ddl_status
ddl_priority
ddl_project
ddl_assignee
```

---

## 4.10 Date Pickers

Utilizar o prefixo:

```text
dtp_
```

Exemplo:

```text
dtp_due_date
```

---

## 4.11 Botões

Utilizar o prefixo:

```text
btn_
```

Exemplos:

```text
btn_login
btn_signup
btn_save
btn_cancel
btn_delete
btn_create_project
```

---

## 4.12 Ícones

Utilizar o prefixo:

```text
ico_
```

---

## 4.13 Textos

Utilizar o prefixo:

```text
txt_
```

---

## 4.14 Popups

Utilizar o prefixo:

```text
pop_
```

Exemplos:

```text
pop_new_task
pop_edit_task
pop_delete_task
pop_archive_project
```

---

## 4.15 Custom States

Utilizar o prefixo:

```text
cs_
```

Os Custom States devem representar somente estados temporários da interface.

Exemplos:

```text
cs_selected_project
cs_selected_task
cs_is_loading
cs_filter_status
```

---

## 4.16 Workflows

Utilizar o padrão:

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

Cada página deverá possuir uma responsabilidade específica.

| Página            | Responsabilidade                            |
| ----------------- | ------------------------------------------- |
| `login`           | Autenticação                                |
| `signup`          | Cadastro                                    |
| `forgot_password` | Recuperação de senha                        |
| `dashboard`       | Visão geral                                 |
| `projects`        | Gerenciamento de projetos                   |
| `project_details` | Detalhes e tarefas do projeto               |
| `my_tasks`        | Visualização de tarefas                     |
| `task_details`    | Detalhes, comentários e histórico da tarefa |
| `notifications`   | Central de notificações                     |
| `profile`         | Perfil do usuário                           |

A criação e edição de tarefas são realizadas através de **Popups**, não através de páginas independentes.

---

# 6. Organização dos Reusable Elements

Os seguintes elementos devem ser reutilizados quando aplicável:

* Header;
* Sidebar;
* Project Card;
* Task Card;
* Comment Card;
* Notification Card;
* Activity Card;
* Empty State;
* Confirmation Modal.

Componentes não utilizados pelo MVP não devem ser criados apenas por previsão de funcionalidades futuras.

---

# 7. Organização dos Workflows

Os Workflows deverão ser organizados por domínio funcional.

## Authentication

```text
Sign Up
Login
Logout
Forgot Password
```

---

## Projects

```text
Create Project
Update Project
Archive Project
```

---

## Tasks

```text
Create Task
Update Task
Delete Task
Change Status
Change Assignee
```

---

## Comments

```text
Add Comment
Edit Comment
Delete Comment
```

---

## Notifications

```text
Create Notification
Mark Notification Read
```

As notificações deverão respeitar a regra de acesso do `Notification`, permitindo visualização somente pelo destinatário.

---

## Activity Log

```text
Register Activity
```

O Workflow deverá ser reutilizado para registrar as ações relevantes da aplicação.

---

## User

```text
Update Profile
```

---

# 8. Estratégia de Custom States

Custom States devem ser utilizados exclusivamente para informações temporárias da interface.

Podem ser utilizados para:

* filtros;
* seleção de projeto;
* seleção de tarefa;
* controle de abas;
* estado de carregamento;
* abertura ou fechamento de componentes;
* controle temporário de interface.

Não devem ser utilizados para substituir informações persistidas no banco.

---

# 9. Estratégia de Privacy Rules

As Privacy Rules são parte fundamental da segurança da aplicação e deverão ser configuradas de acordo com a modelagem atual.

## User

* Informações públicas podem ser visualizadas conforme configuração.
* Dados próprios devem permanecer controlados pelo próprio usuário.

---

## Project

O proprietário possui controle completo sobre o projeto.

Usuários sem responsabilidade sobre o projeto possuem apenas acesso de leitura conforme as regras atuais.

---

## Task

A Task possui três níveis principais de acesso:

### Creator

O criador possui controle completo sobre a tarefa.

### Assignee

O responsável poderá alterar somente os campos permitidos, principalmente:

* `status`;
* `completed_date`.

### Outros usuários

Possuem somente acesso de leitura conforme as Privacy Rules.

---

## Comment

O autor possui controle completo sobre seus comentários.

Outros usuários possuem acesso de leitura conforme as regras configuradas.

O campo `archived` utiliza o Option Set `CommentStatus`.

---

## Notification

As notificações são privadas.

Somente o usuário definido em:

```text
recipient
```

poderá visualizar e marcar a notificação como lida.

A entidade não deverá ficar disponível para pesquisa geral de usuários.

---

## ActivityLog

Os registros de atividades são destinados à consulta do histórico da aplicação.

Não deverão ser utilizados como mecanismo de alteração das entidades originais.

---

# 10. Estratégia para Option Sets

Os valores controlados deverão utilizar Option Sets.

Estrutura atual:

### UserRole

```text
Administrator
Member
```

### ProjectStatus

```text
Active
Archived
```

### TaskStatus

```text
To Do
In Progress
Blocked
Done
```

### TaskPriority

```text
Low
Medium
High
Critical
```

### ActivityAction

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

### CommentStatus

```text
yes
no
```

O `CommentStatus` é utilizado como flag de arquivamento do comentário.

Não deverá ser substituído por texto livre.

---

# 11. Organização dos Estilos

Os estilos visuais deverão ser centralizados sempre que possível através do sistema de Styles do Bubble.

Categorias recomendadas:

```text
Heading
Body
Caption
Button Primary
Button Secondary
Input
Card
Badge
Modal
```

Deve-se evitar a criação de estilos isolados sem justificativa.

---

# 12. Boas Práticas

Durante o desenvolvimento:

* Evitar duplicação de Workflows.
* Reutilizar Workflows quando a mesma lógica for executada em diferentes pontos.
* Utilizar referências entre Data Types.
* Evitar lógica complexa diretamente nos elementos visuais.
* Validar permissões antes de alterações.
* Utilizar Option Sets para valores controlados.
* Registrar ações importantes no `ActivityLog`.
* Gerar notificações somente quando previstas pelas regras de negócio.
* Não expor entidades através de Privacy Rules desnecessárias.
* Manter os nomes dos elementos consistentes.
* Testar alterações de banco e Privacy Rules antes de avançar para novas funcionalidades.
* Manter a documentação sincronizada com a implementação.

---

# 13. Fluxo de Desenvolvimento

Cada funcionalidade deverá seguir o seguinte processo:

```text
Requisito
   ↓
Modelagem
   ↓
Privacy Rules
   ↓
Interface
   ↓
Workflow
   ↓
Testes
   ↓
Documentação
```

### Etapas

1. Validar o requisito.
2. Verificar se a modelagem existente atende à funcionalidade.
3. Atualizar Data Types ou Option Sets quando necessário.
4. Revisar as Privacy Rules.
5. Implementar ou atualizar a interface.
6. Implementar os Workflows.
7. Executar testes funcionais.
8. Validar comportamento das permissões.
9. Atualizar os documentos do projeto.

---

# 14. Checklist para Novas Funcionalidades

Antes de considerar uma funcionalidade concluída:

* [ ] Requisito validado.
* [ ] Banco de dados atualizado, quando necessário.
* [ ] Option Sets atualizados, quando necessário.
* [ ] Privacy Rules revisadas.
* [ ] Interface implementada.
* [ ] Reusable Elements utilizados quando aplicável.
* [ ] Workflow implementado.
* [ ] ActivityLog implementado quando aplicável.
* [ ] Notification implementada quando aplicável.
* [ ] Testes funcionais executados.
* [ ] Testes de permissão executados.
* [ ] Documentação atualizada.

---

# 15. Compatibilidade com o MVP

Toda implementação deverá respeitar o escopo atual do MVP.

Não deverão ser adicionadas funcionalidades fora do escopo sem atualização prévia do planejamento e dos demais artefatos.

Funcionalidades futuras, como:

* Teams;
* Tags;
* Subtasks;
* Dependências;
* Anexos;
* Dashboard analítico;
* Integrações externas;
* Aplicação mobile;
* Kanban avançado;

devem permanecer fora da implementação atual até que sejam formalmente incorporadas ao escopo.

---

# 16. Controle de Alterações Estruturais

Alterações que afetem a estrutura da aplicação deverão ser refletidas nos documentos correspondentes.

Exemplos:

* criação ou exclusão de Data Types;
* alteração de campos;
* criação ou remoção de Option Sets;
* alteração de Privacy Rules;
* criação ou remoção de páginas;
* alteração de componentes reutilizáveis;
* alteração de regras de negócio;
* alteração de Workflows.

Quando uma funcionalidade for removida, sua documentação também deverá ser atualizada para evitar divergência entre o projeto e os artefatos.

---

# 17. Considerações Finais

Este documento estabelece as convenções oficiais de desenvolvimento do **Ozzy - Task Manager**.

A implementação deverá priorizar simplicidade, segurança, reutilização e compatibilidade com o plano gratuito do Bubble.

As convenções aqui definidas devem permanecer alinhadas à implementação real da aplicação. Sempre que houver uma alteração estrutural relevante, os documentos de **Planejamento, Modelagem de Dados, Workflows, Arquitetura e Especificação das Telas** deverão ser revisados para manter a consistência do projeto.
