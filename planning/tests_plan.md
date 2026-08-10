# Plano de Testes

# Ozzy - Task Manager

**Versão:** 2.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento define a estratégia de testes do **Ozzy - Task Manager**, considerando a estrutura atualmente implementada no Bubble.io.

O objetivo é validar:

* funcionalidades;
* workflows;
* regras de negócio;
* permissões por perfil;
* Privacy Rules;
* persistência dos dados;
* navegação;
* notificações;
* histórico de atividades;
* comportamento da interface;
* responsividade.

A validação deverá considerar principalmente os dois perfis existentes:

* **Administrator**
* **Member**

---

# 2. Escopo dos Testes

Serão validados os seguintes módulos:

* Autenticação;
* Projetos;
* Tarefas;
* Comentários;
* Notificações;
* Histórico de atividades;
* Usuários;
* Perfil;
* Dashboard;
* Navegação;
* Permissões;
* Privacy Rules;
* Responsividade.

---

# 3. Perfis de Teste

## Administrator

Deve possuir acesso às funcionalidades administrativas, incluindo:

* gerenciamento de usuários;
* criação de projetos;
* edição de projetos;
* arquivamento de tarefas;
* gerenciamento ampliado do histórico;
* gerenciamento de comentários conforme as regras implementadas.

---

## Member

Deve possuir acesso às funcionalidades operacionais permitidas pelo sistema, incluindo:

* visualização de projetos;
* acesso às tarefas;
* edição das informações permitidas;
* alteração de status;
* criação e gerenciamento dos próprios comentários;
* visualização das próprias notificações;
* atualização do próprio perfil.

---

# 4. Estratégia de Testes

A validação será realizada em cinco níveis.

## 4.1 Testes Funcionais

Validam se cada funcionalidade produz o resultado esperado.

---

## 4.2 Testes de Regras de Negócio

Validam:

* obrigatoriedade de campos;
* status;
* prioridades;
* responsáveis;
* arquivamento;
* geração de ActivityLog;
* geração de Notification;
* comportamento por perfil.

---

## 4.3 Testes de Permissão

Validam as diferenças entre:

* Administrator;
* Member;
* usuário não autenticado.

---

## 4.4 Testes de Integração

Validam a interação entre:

* Interface;
* Workflows;
* Data Types;
* Option Sets;
* Privacy Rules;
* ActivityLog;
* Notification.

---

## 4.5 Testes de Interface

Validam:

* layout;
* navegação;
* estados vazios;
* popups;
* filtros;
* mensagens;
* responsividade;
* componentes reutilizáveis.

---

# 5. Ambiente de Testes

## Plataforma

Bubble.io.

## Navegadores

* Google Chrome;
* Microsoft Edge.

## Dispositivos

* Desktop;
* Tablet;
* Smartphone.

## Contas necessárias

Recomenda-se utilizar pelo menos:

* 1 usuário Administrator;
* 2 usuários Member;
* 1 usuário não autenticado.

---

# 6. Casos de Teste — Autenticação

## CT-001 — Cadastro de Usuário

### Objetivo

Validar a criação de uma nova conta.

### Passos

1. Acessar a página `auth`.
2. Informar os dados obrigatórios.
3. Confirmar a senha.
4. Criar a conta.

### Resultado Esperado

* Usuário criado;
* usuário autenticado conforme o fluxo implementado;
* acesso às páginas permitidas;
* role definida conforme a regra de criação.

---

## CT-002 — Login

### Resultado Esperado

* Credenciais válidas autenticam o usuário;
* usuário é direcionado para a aplicação.

---

## CT-003 — Login Inválido

### Resultado Esperado

* Usuário não autenticado;
* mensagem de erro apresentada;
* acesso às páginas privadas bloqueado.

---

## CT-004 — Logout

### Resultado Esperado

* Sessão encerrada;
* usuário direcionado para `auth`;
* páginas privadas não devem permanecer acessíveis.

---

## CT-005 — Recuperação de Senha

### Resultado Esperado

* E-mail de recuperação enviado;
* popup de confirmação exibido;
* usuário consegue iniciar o processo de redefinição.

---

# 7. Casos de Teste — Projetos

## CT-006 — Criar Projeto

### Pré-condição

Usuário Administrator.

### Passos

1. Acessar `projects`.
2. Selecionar **Novo Projeto**.
3. Informar nome.
4. Informar descrição.
5. Definir status.
6. Salvar.

### Resultado Esperado

Projeto criado com:

* `owner = CurrentUser`;
* `archived = false`;
* status informado.

O projeto deve aparecer na listagem.

---

## CT-007 — Criar Projeto sem Nome

### Resultado Esperado

* Projeto não criado;
* formulário permanece aberto;
* usuário deve corrigir o campo obrigatório.

---

## CT-008 — Editar Projeto

### Resultado Esperado

* Popup de edição aberto;
* dados atuais carregados;
* alterações persistidas;
* ActivityLog `project_updated` registrado quando aplicável.

---

## CT-009 — Arquivar Projeto

### Resultado Esperado

* Status alterado para `Archived`;
* projeto deixa de aparecer nas listagens onde apenas projetos ativos são exibidos.

---

## CT-010 — Member Acessando Criação de Projeto

### Resultado Esperado

* Botão **Novo Projeto** não deve estar disponível;
* tentativa de execução direta do workflow deve ser bloqueada pela condição de permissão.

---

# 8. Casos de Teste — Tarefas

## CT-011 — Criar Tarefa

### Passos

1. Acessar um projeto.
2. Abrir **Nova Tarefa**.
3. Informar título.
4. Informar descrição.
5. Selecionar prioridade.
6. Selecionar responsável.
7. Informar data limite.
8. Salvar.

### Resultado Esperado

Task criada com:

* projeto correto;
* responsável correto;
* status inicial `To Do`;
* `archived = false`.

Também devem ser criados:

* ActivityLog `task_created`;
* Notification para o responsável, quando o responsável for diferente do usuário que criou a tarefa.

---

## CT-012 — Criar Tarefa sem Título

### Resultado Esperado

* Task não criada;
* formulário permanece aberto.

---

## CT-013 — Editar Tarefa

### Resultado Esperado

Os campos permitidos são atualizados corretamente.

Deve ser criado:

* ActivityLog `task_updated`;
* Notification para o responsável quando aplicável.

---

## CT-014 — Alterar Status da Tarefa

### Resultado Esperado

* Status atualizado;
* ActivityLog registrado;
* Notification criada quando aplicável.

A alteração deve funcionar tanto:

* na página `tasks`, pelo popup de alteração rápida;
* na página `task`, pelo popup de alteração de status.

---

## CT-015 — Alterar Status para Done

### Resultado Esperado

* Status = `Done`;
* `completed_date` deve ser preenchida conforme a regra implementada.

---

## CT-016 — Alterar Responsável

### Resultado Esperado

* `assigned_to` atualizado;
* ActivityLog `assignee_changed` quando o fluxo correspondente for executado;
* Notification criada para o novo responsável quando aplicável.

---

## CT-017 — Arquivar Tarefa

### Pré-condição

Usuário Administrator.

### Resultado Esperado

* `archived = true`;
* tarefa deixa de aparecer nas listagens operacionais;
* dados permanecem persistidos;
* ActivityLog `task_archived` criado;
* usuário retorna à página do projeto.

---

## CT-018 — Member Tentando Arquivar Tarefa

### Resultado Esperado

* Botão de exclusão/arquivamento não deve estar disponível;
* workflow não deve executar para Member.

---

# 9. Casos de Teste — Listagem de Tarefas

## CT-019 — Filtrar por Status

### Resultado Esperado

O `rg_tasks` deve exibir somente tarefas correspondentes ao status selecionado.

---

## CT-020 — Filtrar por Prioridade

### Resultado Esperado

Somente tarefas da prioridade selecionada devem ser exibidas.

---

## CT-021 — Filtrar por Projeto

### Resultado Esperado

Somente tarefas pertencentes ao projeto selecionado devem ser exibidas.

---

## CT-022 — Pesquisar Tarefa

### Resultado Esperado

A lista deve ser filtrada pelo título da tarefa conforme o texto informado.

---

## CT-023 — Limpar Filtros

### Resultado Esperado

O botão **Limpar Filtros** deve resetar:

* status;
* prioridade;
* projeto;
* campo de pesquisa.

---

## CT-024 — Alteração Rápida de Status

### Resultado Esperado

* Popup `pop_quick_status` aberto;
* tarefa selecionada corretamente;
* novo status persistido;
* ActivityLog criado;
* Notification criada.

---

# 10. Casos de Teste — Comentários

## CT-025 — Adicionar Comentário

### Resultado Esperado

Comment criado contendo:

* `author = CurrentUser`;
* `task = tarefa atual`;
* mensagem informada;
* `archived = no`.

Também devem ser criados:

* ActivityLog `comment_added`;
* Notification para o responsável quando aplicável.

---

## CT-026 — Adicionar Comentário Vazio

### Resultado Esperado

Comentário não criado.

---

## CT-027 — Editar Comentário Próprio

### Resultado Esperado

* Autor consegue editar seu comentário;
* mensagem atualizada;
* ActivityLog criado.

---

## CT-028 — Editar Comentário de Outro Usuário

### Resultado Esperado

Member não consegue editar comentário pertencente a outro usuário.

---

## CT-029 — Arquivar Comentário Próprio

### Resultado Esperado

* comentário marcado como arquivado;
* comentário deixa de aparecer na listagem operacional;
* registro original permanece no banco.

---

## CT-030 — Administrator Arquivar Comentário

### Resultado Esperado

Administrator consegue arquivar comentários conforme a regra implementada.

---

# 11. Casos de Teste — Notificações

## CT-031 — Criar Notification

Validar a criação automática de notificações em eventos aplicáveis.

Devem ser validados especialmente:

* nova tarefa;
* alteração de tarefa;
* alteração de status;
* novo comentário;
* alteração de responsável.

---

## CT-032 — Visualizar Notificações

### Resultado Esperado

O usuário deve visualizar somente notificações cujo:

```text
recipient = CurrentUser
```

---

## CT-033 — Marcar Notification como Lida

### Resultado Esperado

Ao clicar em uma notificação:

* `is_read = true`;
* se houver tarefa vinculada, navegar para a página `task`;
* se não houver tarefa vinculada, permanecer na central de notificações.

---

## CT-034 — Marcar Todas como Lidas

### Resultado Esperado

Todas as notificações não lidas do usuário devem receber:

```text
is_read = true
```

---

## CT-035 — Acessar Notification de Outro Usuário

### Resultado Esperado

O usuário não deve conseguir visualizar ou manipular notificações pertencentes a outro usuário.

---

# 12. Casos de Teste — Histórico de Atividades

## CT-036 — Registrar Criação de Tarefa

### Resultado Esperado

ActivityLog criado com:

```text
action = task_created
```

---

## CT-037 — Registrar Atualização de Tarefa

### Resultado Esperado

ActivityLog:

```text
action = task_updated
```

---

## CT-038 — Registrar Alteração de Status

### Resultado Esperado

ActivityLog relacionado à alteração de status criado corretamente.

---

## CT-039 — Registrar Comentário

### Resultado Esperado

ActivityLog:

```text
action = comment_added
```

---

## CT-040 — Registrar Arquivamento

Validar os eventos:

```text
task_archived
```

e demais ações de arquivamento implementadas.

---

## CT-041 — Visualizar Atividades como Member

### Resultado Esperado

Member deve visualizar somente os registros permitidos pela implementação atual.

---

## CT-042 — Visualizar Atividades como Administrator

### Resultado Esperado

Administrator deve visualizar a visão administrativa disponível na página `activities`.

---

## CT-043 — Filtrar Atividades

Validar filtros por:

* ação;
* usuário;
* projeto;
* pesquisa textual.

O botão **Limpar Filtros** deve restaurar a listagem original.

---

## CT-044 — Visualizar Detalhes da Atividade

### Resultado Esperado

Ao selecionar uma atividade:

* popup `pop_activity_details` é exibido;
* descrição;
* ação;
* tarefa;
* usuário;
* data;
* identificador

são apresentados corretamente.

---

# 13. Casos de Teste — Usuários

## CT-045 — Visualizar Usuários

### Pré-condição

Administrator.

### Resultado Esperado

Administrator consegue visualizar a lista de usuários.

---

## CT-046 — Filtrar Usuários por Nome

### Resultado Esperado

Lista filtrada pelo nome pesquisado.

---

## CT-047 — Filtrar Usuários por Role

### Resultado Esperado

Lista filtrada por:

* Administrator;
* Member.

---

## CT-048 — Criar Usuário Administrativo

### Pré-condição

Administrator.

### Resultado Esperado

* novo User criado;
* dados persistidos;
* e-mail de definição de senha enviado;
* confirmação apresentada.

---

## CT-049 — Editar Usuário

### Resultado Esperado

Administrator consegue editar os campos permitidos do usuário.

O e-mail do usuário existente não deve ser alterado pelo fluxo atual.

---

## CT-050 — Member Acessando Gestão de Usuários

### Resultado Esperado

* funcionalidades administrativas não disponíveis;
* botões de criação/edição ocultos;
* workflow protegido por condição de role.

---

# 14. Casos de Teste — Perfil

## CT-051 — Atualizar Nome

### Resultado Esperado

Nome do usuário atualizado.

---

## CT-052 — Cancelar Alteração de Perfil

### Resultado Esperado

Campos retornam aos valores persistidos.

---

## CT-053 — Alterar Avatar

### Resultado Esperado

No estado atual, o controle de alteração de foto encontra-se desabilitado. O teste deve confirmar que a funcionalidade não pode ser executada.

---

## CT-054 — Redefinir Senha pelo Perfil

### Resultado Esperado

* e-mail de redefinição enviado;
* popup de confirmação exibido.

---

# 15. Casos de Teste — Dashboard

## CT-055 — Carregar Dashboard

Validar:

* carregamento da página;
* projetos apresentados;
* tarefas apresentadas;
* atividades recentes;
* navegação para os módulos.

O elemento `grp_dashboard_metrics` não faz parte da versão atual e não deve ser considerado requisito de teste.

---

# 16. Testes de Navegação

Validar os principais fluxos:

```text
auth
  ↓
dashboard
  ↓
projects
  ↓
project
  ↓
task
```

E também:

```text
dashboard
 ├── tasks
 ├── notifications
 ├── activities
 ├── users
 └── profile
```

Validar também:

* projeto → tarefa;
* tarefa → projeto;
* notificação → tarefa;
* atividade → detalhes;
* logout → auth.

---

# 17. Testes de Privacy Rules

Validar explicitamente os Data Types:

## User

* dados públicos disponíveis conforme configuração;
* dados privados protegidos.

## Project

* acesso de leitura conforme configuração;
* operações administrativas protegidas.

## Task

* criador com permissões previstas;
* responsável com permissões limitadas;
* demais usuários somente com acesso permitido.

## Comment

* autor pode manipular seu próprio comentário;
* demais usuários possuem somente o acesso previsto.

## Notification

* somente o destinatário deve acessar suas notificações.

## ActivityLog

* acesso deve respeitar as regras de visibilidade definidas para Member e Administrator.

---

# 18. Testes de Option Sets

Validar os valores utilizados pela aplicação.

## UserRole

* Administrator;
* Member.

## ProjectStatus

* Active;
* Archived.

## TaskStatus

* To Do;
* In Progress;
* Blocked;
* Done.

## TaskPriority

* Low;
* Medium;
* High;
* Critical.

## ActivityAction

Validar os eventos atualmente utilizados, incluindo:

* `task_created`;
* `task_updated`;
* `task_deleted`;
* `status_changed`;
* `comment_added`;
* `assignee_changed`;
* `notification_created`;
* `project_updated`;
* `task_archived`;
* `user_updated`;
* `role_user_updated`.

## CommentStatus

Validar:

* `yes`;
* `no`.

O Option Set representa o estado de arquivamento do comentário.

---

# 19. Testes de Interface

Verificar:

* alinhamento;
* espaçamento;
* tipografia;
* cores;
* bordas;
* estados vazios;
* filtros;
* popups;
* botões;
* campos obrigatórios;
* feedback de ações;
* navegação;
* comportamento dos cards.

Também devem ser validados os componentes reutilizáveis:

* `re_header`;
* `re_sidebar`;
* cards de projeto;
* cards de tarefa;
* cards de comentário;
* cards de notificação;
* cards de atividade.

---

# 20. Testes de Responsividade

## Desktop

Validar integralmente todas as funcionalidades.

---

## Tablet

Verificar:

* comportamento da sidebar;
* dimensionamento dos cards;
* filtros;
* tabelas/listagens;
* popups.

---

## Mobile

Verificar:

* navegação;
* menu;
* filtros;
* formulários;
* cards;
* botões;
* leitura de textos;
* popups.

---

# 21. Testes de Performance

Validar qualitativamente:

* tempo de carregamento das páginas;
* carregamento das listas;
* aplicação dos filtros;
* abertura dos popups;
* salvamento de registros;
* atualização das listas após workflows;
* carregamento das notificações.

Especial atenção deve ser dada às buscas realizadas pelos Repeating Groups.

---

# 22. Testes de Integridade dos Workflows

Após cada operação crítica, verificar o conjunto de efeitos esperados.

### Criar tarefa

```text
Task
  ↓
ActivityLog
  ↓
Notification
  ↓
Atualização da interface
```

### Alterar status

```text
Task
  ↓
ActivityLog
  ↓
Notification
  ↓
Atualização da interface
```

### Adicionar comentário

```text
Comment
  ↓
ActivityLog
  ↓
Notification
  ↓
Atualização da lista
```

### Arquivar tarefa

```text
Task.archived = true
  ↓
ActivityLog.task_archived
  ↓
Navegação para Project
```

---

# 23. Testes de Estados e Arquivamento

Validar que registros arquivados não apareçam indevidamente nas listagens operacionais.

Testar:

* projetos arquivados;
* tarefas arquivadas;
* comentários arquivados.

Também validar que o arquivamento não remove fisicamente o registro do banco.

---

# 24. Critérios de Aprovação

Uma funcionalidade será considerada aprovada quando:

* comportamento esperado estiver implementado;
* workflow executar corretamente;
* dados forem persistidos;
* permissões forem respeitadas;
* ActivityLog for criado quando aplicável;
* Notification for criada quando aplicável;
* interface refletir a alteração;
* nenhum defeito crítico permanecer aberto.

---

# 25. Registro de Defeitos

Cada defeito identificado deverá conter:

* Código;
* Descrição;
* Página;
* Elemento afetado;
* Perfil afetado;
* Passos para reprodução;
* Resultado obtido;
* Resultado esperado;
* Prioridade;
* Responsável;
* Status.

Sugestão de prioridades:

* **Crítica** — impede o uso do sistema;
* **Alta** — impede uma funcionalidade importante;
* **Média** — afeta parcialmente a experiência;
* **Baixa** — problema visual ou de baixo impacto.

---

# 26. Checklist de Validação Final

## Autenticação

* [ ] Cadastro
* [ ] Login
* [ ] Login inválido
* [ ] Logout
* [ ] Recuperação de senha

## Projetos

* [ ] Listagem
* [ ] Filtros
* [ ] Criar projeto
* [ ] Editar projeto
* [ ] Arquivar projeto
* [ ] Permissões de Administrator

## Tarefas

* [ ] Listagem
* [ ] Pesquisa
* [ ] Filtro por status
* [ ] Filtro por prioridade
* [ ] Filtro por projeto
* [ ] Criar tarefa
* [ ] Editar tarefa
* [ ] Alterar status
* [ ] Alterar responsável
* [ ] Arquivar tarefa
* [ ] Permissões

## Comentários

* [ ] Criar
* [ ] Editar próprio
* [ ] Impedir edição indevida
* [ ] Arquivar
* [ ] ActivityLog

## Notificações

* [ ] Criação automática
* [ ] Visualização
* [ ] Marcar como lida
* [ ] Marcar todas como lidas
* [ ] Navegação para tarefa
* [ ] Privacy Rules

## Histórico

* [ ] Registro de criação
* [ ] Registro de atualização
* [ ] Registro de status
* [ ] Registro de comentário
* [ ] Registro de arquivamento
* [ ] Filtros
* [ ] Detalhes
* [ ] Visão Member
* [ ] Visão Administrator

## Usuários

* [ ] Listagem
* [ ] Busca
* [ ] Filtro por role
* [ ] Criar usuário
* [ ] Editar usuário
* [ ] Restrição para Member

## Perfil

* [ ] Editar nome
* [ ] Cancelar edição
* [ ] E-mail somente leitura
* [ ] Avatar desabilitado
* [ ] Redefinição de senha

## Dashboard

* [ ] Carregamento
* [ ] Projetos
* [ ] Tarefas
* [ ] Atividades
* [ ] Navegação
* [ ] Ausência de `grp_dashboard_metrics`

## Interface

* [ ] Desktop
* [ ] Tablet
* [ ] Mobile
* [ ] Popups
* [ ] Empty states
* [ ] Filtros
* [ ] Navegação

---

# 27. Critérios para Conclusão do MVP

O MVP será considerado validado quando:

* todas as funcionalidades implementadas tiverem sido testadas;
* os fluxos principais estiverem funcionando;
* Administrator e Member possuírem os acessos corretos;
* as Privacy Rules estiverem validadas;
* os Workflows persistirem os dados corretamente;
* ActivityLogs forem gerados conforme os eventos implementados;
* Notifications forem geradas conforme as regras implementadas;
* registros arquivados não apareçam indevidamente nas listagens;
* não existirem defeitos críticos ou bloqueadores;
* a aplicação estiver pronta para publicação;
* a documentação estiver sincronizada com a implementação.

---

# 28. Considerações Finais

Este documento representa o plano oficial de testes do **Ozzy - Task Manager** na sua estrutura atual.

A execução dos testes deve acompanhar a implementação dos módulos e ser repetida após alterações relevantes nos Data Types, Option Sets, Privacy Rules, Workflows ou componentes reutilizáveis.

O objetivo não é apenas verificar se cada tela funciona isoladamente, mas garantir a consistência entre **interface, dados, permissões, workflows, notificações e histórico de atividades**.
