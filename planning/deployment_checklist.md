# Checklist de Publicação (Deployment Checklist)

# Ozzy - Task Manager

**Versão:** 2.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento estabelece o checklist oficial de publicação do **Ozzy - Task Manager**.

Seu objetivo é garantir que a aplicação, banco de dados, workflows, permissões, interface, testes e documentação estejam devidamente validados antes da publicação do MVP.

O checklist deverá ser executado antes da disponibilização da aplicação no ambiente de produção.

---

# 2. Preparação do Ambiente

## Projeto Bubble

* [ ] Projeto criado e configurado.
* [ ] Nome da aplicação configurado.
* [ ] Favicon configurado.
* [ ] Idioma revisado.
* [ ] Timezone revisado.
* [ ] Configurações gerais revisadas.
* [ ] Ambiente de Development validado.
* [ ] Ambiente Live preparado.

---

# 3. Banco de Dados

## Data Types

Confirmar a existência e configuração dos seguintes tipos:

* [ ] User — tipo nativo do Bubble.
* [ ] Project.
* [ ] Task.
* [ ] Comment.
* [ ] Notification.
* [ ] ActivityLog.

---

## Campos e Relacionamentos

Verificar:

* [ ] Todos os campos possuem o tipo correto.
* [ ] Relacionamentos entre entidades estão configurados.
* [ ] `Project.owner` referencia User.
* [ ] `Task.project` referencia Project.
* [ ] `Task.created_by` referencia User.
* [ ] `Task.assigned_to` referencia User.
* [ ] `Comment.task` referencia Task.
* [ ] `Comment.author` referencia User.
* [ ] `Notification.recipient` referencia User.
* [ ] `Notification.task` referencia Task.
* [ ] `ActivityLog.user` referencia User.
* [ ] `ActivityLog.task` referencia Task.
* [ ] Campos obrigatórios estão revisados.
* [ ] Não existem campos obsoletos utilizados pela aplicação.

---

# 4. Option Sets

Confirmar a existência e utilização correta de:

* [ ] `UserRole`
* [ ] `ProjectStatus`
* [ ] `TaskStatus`
* [ ] `TaskPriority`
* [ ] `ActivityAction`
* [ ] `CommentStatus`

---

## UserRole

* [ ] Administrator
* [ ] Member

---

## ProjectStatus

* [ ] Active
* [ ] Archived

---

## TaskStatus

* [ ] To Do
* [ ] In Progress
* [ ] Blocked
* [ ] Done

---

## TaskPriority

* [ ] Low
* [ ] Medium
* [ ] High
* [ ] Critical

---

## ActivityAction

Validar os eventos atualmente utilizados:

* [ ] `task_created`
* [ ] `task_updated`
* [ ] `task_deleted`
* [ ] `status_changed`
* [ ] `comment_added`
* [ ] `assignee_changed`
* [ ] `notification_created`
* [ ] `project_updated`
* [ ] `task_archived`
* [ ] `user_updated`
* [ ] `role_user_updated`

---

## CommentStatus

* [ ] `yes`
* [ ] `no`

Confirmar que este Option Set é utilizado como controle de arquivamento dos comentários.

---

# 5. Segurança

## Privacy Rules

Validar as regras atualmente configuradas para:

### User

* [ ] Dados públicos disponíveis conforme configuração.
* [ ] Dados privados protegidos.
* [ ] Dados do próprio usuário protegidos.

### Project

* [ ] Owner possui permissões administrativas previstas.
* [ ] Demais usuários possuem somente acesso de leitura previsto.

### Task

* [ ] Creator possui permissões completas previstas.
* [ ] Assignee possui somente as permissões permitidas.
* [ ] Demais usuários possuem somente acesso de leitura previsto.

### Comment

* [ ] Author possui permissões de edição previstas.
* [ ] Demais usuários possuem somente acesso permitido.

### Notification

* [ ] Somente o recipient consegue visualizar suas notificações.
* [ ] Somente o recipient consegue marcar notificações como lidas.

### ActivityLog

* [ ] Acesso respeita as regras definidas para usuários autenticados.
* [ ] Dados de auditoria não podem ser alterados indevidamente.

---

# 6. Perfis de Acesso

Validar a aplicação utilizando pelo menos:

* [ ] Usuário Administrator.
* [ ] Usuário Member.
* [ ] Usuário não autenticado.

---

## Administrator

Validar acesso a:

* [ ] Dashboard.
* [ ] Projects.
* [ ] Tasks.
* [ ] Notifications.
* [ ] Activities.
* [ ] Users.
* [ ] Profile.
* [ ] Funcionalidades administrativas.

---

## Member

Validar acesso permitido a:

* [ ] Dashboard.
* [ ] Projects.
* [ ] Tasks.
* [ ] Notifications.
* [ ] Profile.

Confirmar que funcionalidades administrativas não estejam disponíveis.

---

## Usuário Não Autenticado

* [ ] Não consegue acessar páginas privadas.
* [ ] É direcionado para autenticação.
* [ ] Não consegue executar workflows protegidos.

---

# 7. Autenticação

Confirmar:

* [ ] Cadastro funcionando.
* [ ] Login funcionando.
* [ ] Login inválido tratado corretamente.
* [ ] Logout funcionando.
* [ ] Recuperação de senha funcionando.
* [ ] Sessão persistida corretamente.
* [ ] Usuário autenticado não acessa novamente a tela de autenticação indevidamente.
* [ ] Usuário não autenticado não acessa páginas privadas.

---

# 8. Interface

## Páginas

Confirmar a existência e funcionamento das páginas atuais:

* [ ] `auth`
* [ ] `dashboard`
* [ ] `projects`
* [ ] `project`
* [ ] `tasks`
* [ ] `task`
* [ ] `notifications`
* [ ] `activities`
* [ ] `users`
* [ ] `profile`

---

## Popups

Validar os popups utilizados pela aplicação, incluindo:

* [ ] Criação de projeto.
* [ ] Edição de projeto.
* [ ] Criação de tarefa.
* [ ] Edição de tarefa.
* [ ] Alteração rápida de status.
* [ ] Adição de comentário.
* [ ] Edição de comentário.
* [ ] Detalhes da atividade.
* [ ] Confirmação de arquivamento/exclusão lógica.
* [ ] Feedback de sucesso.
* [ ] Feedback de erro.

---

# 9. Componentes Reutilizáveis

Verificar:

* [ ] Header.
* [ ] Sidebar.
* [ ] Project Card.
* [ ] Task Card.
* [ ] Comment Card.
* [ ] Notification Card.
* [ ] Activity Card.
* [ ] Empty State.
* [ ] Confirmation Modal.

Confirmar que os componentes reutilizáveis estejam sendo utilizados onde aplicável e não existam cópias desnecessárias de componentes compartilhados.

---

# 10. Funcionalidades

## Projetos

Verificar:

* [ ] Listagem de projetos.
* [ ] Pesquisa.
* [ ] Filtro por status.
* [ ] Criar projeto.
* [ ] Editar projeto.
* [ ] Arquivar projeto.
* [ ] Definição automática do owner.
* [ ] Status inicial correto.
* [ ] Restrição para usuários sem permissão.

---

## Tarefas

Verificar:

* [ ] Listagem.
* [ ] Pesquisa.
* [ ] Filtro por status.
* [ ] Filtro por prioridade.
* [ ] Filtro por projeto.
* [ ] Criar tarefa.
* [ ] Editar tarefa.
* [ ] Alterar status.
* [ ] Alterar responsável.
* [ ] Definir prioridade.
* [ ] Definir data limite.
* [ ] Registrar conclusão quando status = Done.
* [ ] Arquivar tarefa.
* [ ] Tarefa arquivada não aparece nas listagens operacionais.
* [ ] Permissões por creator/assignee respeitadas.

> A tarefa não deverá ser tratada como exclusão física no fluxo atual. O processo implementado utiliza arquivamento lógico.

---

## Comentários

Verificar:

* [ ] Criar comentário.
* [ ] Editar comentário próprio.
* [ ] Restringir edição indevida.
* [ ] Arquivar comentário.
* [ ] Comentários arquivados não aparecem nas listagens operacionais.
* [ ] ActivityLog criado quando aplicável.
* [ ] Notification criada quando aplicável.

---

## Notificações

Verificar:

* [ ] Criação automática.
* [ ] Destinatário correto.
* [ ] Visualização somente pelo destinatário.
* [ ] Marcar como lida.
* [ ] Marcar todas como lidas.
* [ ] Navegação para tarefa vinculada.
* [ ] Tratamento de notificação sem tarefa vinculada.

---

## Histórico de Atividades

Verificar:

* [ ] ActivityLog criado automaticamente.
* [ ] Criação de tarefa registrada.
* [ ] Atualização de tarefa registrada.
* [ ] Alteração de status registrada.
* [ ] Alteração de responsável registrada.
* [ ] Comentário registrado.
* [ ] Arquivamento de tarefa registrado.
* [ ] Atualização de projeto registrada.
* [ ] Atualização de usuário registrada quando aplicável.
* [ ] Alteração de role registrada quando aplicável.
* [ ] Notificação registrada quando aplicável.
* [ ] Filtros funcionando.
* [ ] Detalhes da atividade funcionando.

---

## Usuários

Verificar:

* [ ] Listagem de usuários.
* [ ] Pesquisa por nome.
* [ ] Filtro por role.
* [ ] Criação de usuário administrativo.
* [ ] E-mail de definição de senha.
* [ ] Edição de usuário.
* [ ] Alteração de role.
* [ ] Restrição de acesso para Member.

---

## Perfil

Verificar:

* [ ] Nome carregado corretamente.
* [ ] E-mail exibido como somente leitura.
* [ ] Atualização do nome.
* [ ] Cancelamento de alterações.
* [ ] Avatar apresentado corretamente.
* [ ] Controle de alteração de avatar conforme estado atual da implementação.
* [ ] Redefinição de senha.

---

## Dashboard

Confirmar:

* [ ] Página carregando corretamente.
* [ ] Projetos carregados.
* [ ] Tarefas carregadas.
* [ ] Atividades recentes carregadas.
* [ ] Navegação para os módulos funcionando.
* [ ] Estados vazios funcionando.

O elemento `grp_dashboard_metrics` **não faz parte da versão atual** e não deve ser considerado requisito para publicação.

---

# 11. Workflows

Validar todos os workflows implementados e seus efeitos no banco.

## Authentication

* [ ] Sign Up.
* [ ] Login.
* [ ] Logout.
* [ ] Forgot Password.

---

## Projects

* [ ] Create Project.
* [ ] Update Project.
* [ ] Archive Project.

---

## Tasks

* [ ] Create Task.
* [ ] Update Task.
* [ ] Change Status.
* [ ] Change Assignee.
* [ ] Archive Task.

---

## Comments

* [ ] Add Comment.
* [ ] Edit Comment.
* [ ] Archive Comment.

---

## Notifications

* [ ] Create Notification.
* [ ] Mark Notification Read.
* [ ] Mark All Notifications Read.

---

## Activity Log

* [ ] Register Activity.

---

## Users

* [ ] Create User.
* [ ] Update User.
* [ ] Update User Role.

---

## Profile

* [ ] Update Profile.
* [ ] Reset Password.

---

# 12. Validação de Dados

Confirmar:

* [ ] Todo projeto possui owner.
* [ ] Toda tarefa possui project.
* [ ] Toda tarefa possui created_by.
* [ ] Toda tarefa possui assigned_to.
* [ ] Todo comentário possui author.
* [ ] Todo comentário possui task.
* [ ] Toda notification possui recipient.
* [ ] ActivityLog possui user quando aplicável.
* [ ] ActivityLog possui task quando a ação estiver relacionada a uma tarefa.
* [ ] Status utilizam Option Sets.
* [ ] Prioridades utilizam Option Sets.
* [ ] Roles utilizam Option Sets.
* [ ] Comentários utilizam CommentStatus.
* [ ] Não existem registros inconsistentes criados durante os testes.

---

# 13. Integridade dos Workflows

Validar os efeitos encadeados das principais operações.

## Criar Tarefa

```text
Create Task
     ↓
ActivityLog
     ↓
Notification
     ↓
Interface
```

* [ ] Task criada.
* [ ] ActivityLog criado.
* [ ] Notification criada quando aplicável.
* [ ] Lista atualizada.

---

## Alterar Status

```text
Change Status
     ↓
Task
     ↓
ActivityLog
     ↓
Notification
     ↓
Interface
```

* [ ] Status atualizado.
* [ ] `completed_date` atualizado quando aplicável.
* [ ] ActivityLog criado.
* [ ] Notification criada quando aplicável.
* [ ] Interface atualizada.

---

## Adicionar Comentário

```text
Add Comment
     ↓
Comment
     ↓
ActivityLog
     ↓
Notification
     ↓
Interface
```

* [ ] Comment criado.
* [ ] ActivityLog criado.
* [ ] Notification criada quando aplicável.
* [ ] Lista de comentários atualizada.

---

## Arquivar Tarefa

```text
Archive Task
     ↓
Task.archived = true
     ↓
ActivityLog
     ↓
Interface
```

* [ ] Tarefa arquivada.
* [ ] Registro permanece no banco.
* [ ] ActivityLog criado.
* [ ] Tarefa desaparece das listagens operacionais.

---

# 14. Responsividade

## Desktop

* [ ] Layout correto.
* [ ] Sidebar funcionando.
* [ ] Listagens funcionando.
* [ ] Popups funcionando.
* [ ] Formulários funcionando.

---

## Tablet

* [ ] Sidebar adaptada.
* [ ] Cards reorganizados.
* [ ] Filtros utilizáveis.
* [ ] Popups adequados à resolução.

---

## Mobile

* [ ] Menu responsivo.
* [ ] Cards reorganizados.
* [ ] Formulários utilizáveis.
* [ ] Botões acessíveis.
* [ ] Textos legíveis.
* [ ] Listagens utilizáveis.
* [ ] Popups adequados à resolução.

---

# 15. Performance

Validar:

* [ ] Login com tempo de resposta aceitável.
* [ ] Dashboard carregando corretamente.
* [ ] Projects carregando corretamente.
* [ ] Tasks carregando corretamente.
* [ ] Notifications carregando corretamente.
* [ ] Activities carregando corretamente.
* [ ] Users carregando corretamente.
* [ ] Filtros executando sem atrasos significativos.
* [ ] Popups abrindo corretamente.
* [ ] Workflows não executando operações desnecessárias.
* [ ] Repeating Groups utilizando buscas adequadas.

---

# 16. Qualidade da Interface

Verificar:

* [ ] Mensagens de sucesso.
* [ ] Mensagens de erro.
* [ ] Estados vazios.
* [ ] Estados de carregamento.
* [ ] Botões habilitados/desabilitados corretamente.
* [ ] Elementos administrativos ocultos para Member.
* [ ] Consistência visual.
* [ ] Alinhamento.
* [ ] Espaçamentos.
* [ ] Ícones.
* [ ] Cores.
* [ ] Tipografia.
* [ ] Popups.
* [ ] Filtros.
* [ ] Cards.

---

# 17. Documentação

Confirmar que os seguintes artefatos estão atualizados:

* [ ] Planning.
* [ ] Data Model.
* [ ] Solution Architecture.
* [ ] Development Guide.
* [ ] Workflow Specification.
* [ ] Screen Functional Specification.
* [ ] Test Plan.
* [ ] Deployment Checklist.
* [ ] README.

Também verificar:

* [ ] Nenhum documento referencia funcionalidades removidas.
* [ ] Nenhum documento utiliza nomenclatura desatualizada.
* [ ] Páginas documentadas correspondem às páginas existentes.
* [ ] Workflows documentados correspondem aos workflows implementados.
* [ ] Data Types documentados correspondem ao banco atual.

---

# 18. Validação Final

Antes da publicação:

* [ ] Todos os testes do Plano de Testes executados.
* [ ] Todos os casos críticos aprovados.
* [ ] Nenhum defeito crítico ou bloqueador aberto.
* [ ] Todas as páginas funcionando.
* [ ] Todos os workflows principais funcionando.
* [ ] Data Types revisados.
* [ ] Option Sets revisados.
* [ ] Privacy Rules revisadas.
* [ ] Perfis Administrator e Member validados.
* [ ] Navegação validada.
* [ ] Responsividade validada.
* [ ] Performance validada.
* [ ] Documentação atualizada.

---

# 19. Publicação

Antes de colocar a aplicação em produção:

* [ ] Última versão validada no ambiente Development.
* [ ] Alterações estruturais revisadas.
* [ ] Banco revisado.
* [ ] Privacy Rules revisadas.
* [ ] Workflows revisados.
* [ ] Interface revisada.
* [ ] Testes de regressão executados.
* [ ] Publicação executada no ambiente Live.
* [ ] Aplicação acessível pela URL oficial.
* [ ] Login validado no ambiente Live.
* [ ] Funcionalidades críticas validadas no ambiente Live.

---

# 20. Pós-Publicação

Após a publicação:

* [ ] Realizar smoke test da aplicação.
* [ ] Validar login.
* [ ] Validar Dashboard.
* [ ] Validar Projects.
* [ ] Validar Tasks.
* [ ] Validar Notifications.
* [ ] Validar Profile.
* [ ] Validar funcionalidades administrativas.
* [ ] Verificar erros inesperados.
* [ ] Registrar problemas encontrados.
* [ ] Registrar versão publicada.

---

# 21. Registro da Publicação

| Item               | Informação             |
| ------------------ | ---------------------- |
| Versão             |                        |
| Data da Publicação |                        |
| Responsável        |                        |
| Ambiente           | Development / Live     |
| URL da Aplicação   |                        |
| Última Revisão     |                        |
| Status             | ☐ Aprovado ☐ Reprovado |

---

# 22. Lições Aprendidas

Após a publicação, registrar:

## Pontos Positivos

*
*
*

---

## Melhorias Identificadas

*
*
*

---

## Funcionalidades Planejadas para Próximas Versões

*
*
*

---

# 23. Critérios para Aprovação do MVP

O MVP será considerado pronto para publicação quando:

* Todos os requisitos implementados estiverem validados.
* Todos os testes críticos estiverem aprovados.
* Administrator e Member possuírem os acessos corretos.
* As Privacy Rules estiverem funcionando.
* Os Workflows principais estiverem funcionando.
* Os dados estiverem sendo persistidos corretamente.
* ActivityLogs estiverem sendo registrados conforme os eventos implementados.
* Notifications estiverem sendo geradas conforme as regras aplicáveis.
* Arquivamentos estiverem funcionando corretamente.
* Não existirem defeitos críticos ou bloqueadores.
* A aplicação estiver operacional no ambiente Live.
* Toda a documentação estiver sincronizada com a implementação.

---

# 24. Considerações Finais

Este **Deployment Checklist** representa a etapa final de validação e publicação do **Ozzy - Task Manager**.

Sua execução deve garantir que a versão publicada corresponda efetivamente à solução documentada e testada, considerando especialmente:

* estrutura atual do banco;
* perfis Administrator e Member;
* Privacy Rules;
* workflows;
* arquivamento lógico;
* notificações;
* histórico de atividades;
* páginas administrativas;
* responsividade;
* documentação.

Após cada alteração estrutural relevante, o checklist deverá ser revisado antes de uma nova publicação.
