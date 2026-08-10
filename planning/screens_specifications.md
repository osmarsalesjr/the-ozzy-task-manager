# Especificação Funcional das Telas

# Ozzy - Task Manager

**Versão:** 2.0 (MVP)
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento define a especificação funcional das telas atualmente implementadas no **Ozzy - Task Manager**.

A especificação considera a estrutura real da aplicação, incluindo:

* páginas;
* componentes reutilizáveis;
* Repeating Groups;
* popups;
* fontes de dados;
* ações disponíveis;
* regras de visibilidade;
* navegação;
* comportamentos específicos por perfil de usuário.

O documento deve servir como referência para manutenção, testes e evolução da interface.

---

# 2. Estrutura Atual da Aplicação

A aplicação atualmente utiliza as seguintes páginas principais:

```text
auth
│
├── Cadastro
└── Recuperação de senha

index
│
├── Meus Projetos
│   └── project
│
├── Minhas Tarefas Pendentes
│   └── tasks
│
├── Atividades Recentes
│   └── Popup de detalhes
│
└── Atalhos

project
│
├── Informações do projeto
├── Lista de tarefas
├── Nova tarefa
├── Editar projeto
└── Editar tarefa

tasks
│
├── Lista de tarefas
├── Filtros
├── Acesso à tarefa
├── Acesso ao projeto
└── Alteração rápida de status

task
│
├── Informações da tarefa
├── Comentários
├── Histórico
├── Edição
└── Exclusão

activities
│
├── Atividades do usuário
├── Atividades administrativas
├── Filtros
└── Detalhes da atividade

notifications
│
├── Lista de notificações
└── Marcação como lida

reset_pw
│
└── Redefinição de senha

404
│
└── Página de recurso não encontrado
```

## A aplicação utiliza `re_header` e `re_sidebar` como componentes compartilhados nas páginas autenticadas.

# 3. Elementos Reutilizáveis

## 3.1 `re_header`

Header compartilhado das páginas autenticadas.

Responsabilidades:

* identificação da aplicação;
* navegação;
* acesso ao perfil;
* acesso às notificações;
* ações globais do usuário.

---

## 3.2 `re_sidebar`

Menu lateral compartilhado.

Possui estado interno para controle de colapso da navegação.

Principais áreas:

* Dashboard;
* Tarefas;
* Notificações;
* Atividades;
* demais destinos disponíveis conforme a implementação atual.

A sidebar possui estado `is_collapsed`, permitindo alternar entre a versão expandida e compacta.

---

# 4. Página `auth`

## Objetivo

Centralizar a autenticação dos usuários.

## Funcionalidades

* Login;
* cadastro;
* recuperação de senha;
* redirecionamento para o Dashboard após autenticação.

## Regras

* Usuários não autenticados podem acessar a página.
* Usuários autenticados devem ser direcionados para `index`.

---

# 5. Página `index`

## Objetivo

Atuar como **Dashboard principal** da aplicação.

A página concentra as principais informações operacionais do usuário, eliminando a necessidade de uma página independente de projetos para o MVP.

## Estrutura

```text
grp_page_wrapper
│
├── grp_header
│   └── re_header
│
└── grp_body
    │
    ├── grp_sidebar
    │   └── re_sidebar
    │
    └── grp_content
        │
        └── grp_dashboard_content_wrapper
            │
            ├── grp_dashboard_title
            │
            └── SectionsWrapper
                ├── grp_projects_section
                ├── grp_tasks_section
                └── grp_activity_section
```

---

## 5.1 Seção Meus Projetos

### Elementos

* `grp_projects_section`
* `grp_projects_header`
* `NewProjectBtn`
* `rg_projects`
* `grp_projects_empty_state`

### Fonte de dados

`Project`

A lista apresenta projetos ativos associados ao usuário atual e é ordenada pela data de criação.

### Ações

* abrir projeto;
* criar novo projeto.

### Permissão

O botão de criação de projeto é apresentado conforme a regra de role atualmente configurada, com acesso para administradores.

---

# 6. Popup `pop_new_project`

## Objetivo

Permitir a criação de um novo projeto diretamente no Dashboard.

## Campos

* nome;
* descrição;
* status.

## Elementos principais

* `inp_project_name`;
* campo de descrição;
* dropdown de status;
* `btn_popup_cancel`;
* `btn_popup_create`.

## Comportamento

Ao confirmar:

1. Validar os campos necessários.
2. Criar `Project`.
3. Associar o projeto ao usuário responsável.
4. Fechar o popup.
5. Limpar os campos.

O popup possui aproximadamente 520px de largura.

---

# 7. Seção Minhas Tarefas Pendentes

## Objetivo

Apresentar rapidamente as tarefas que exigem atenção do usuário.

## Elementos

* `grp_tasks_section`;
* `grp_tasks_section_content`;
* `grp_tasks_header`;
* `rg_pending_tasks`;
* `grp_tasks_empty_state`;
* `btn_tasks_ver_todas`.

## Fonte

`Task`

### Filtros

A busca considera:

* `assigned_to = CurrentUser`;
* `archived = false`;
* `status != done`.

As tarefas são ordenadas pela `due_date`.

## Ações

* abrir tarefa;
* acessar a listagem completa de tarefas.

---

# 8. Seção Atividades Recentes

## Objetivo

Exibir as atividades mais recentes relacionadas ao usuário.

## Elementos

* `grp_activity_section`;
* `grp_activity_header`;
* `btn_activity_ver_historico`;
* `rg_recent_activity`;
* `grp_activity_empty_state`.

## Fonte

`ActivityLog`

A seção apresenta os últimos registros de atividade relacionados ao usuário atual.

## Ações

* abrir detalhes da atividade;
* acessar o histórico completo.

## Visibilidade

Existem ações distintas para membros e administradores:

* `btn_activity_ver_historico`;
* botão de histórico administrativo.

A disponibilidade é controlada pela role do usuário.

---

# 9. Popup `pop_activity_details`

## Objetivo

Exibir os detalhes de um registro de `ActivityLog`.

## Tipo de dado

`ActivityLog`

## Informações exibidas

* descrição;
* ação;
* tarefa relacionada;
* colaborador;
* data de criação;
* ID da atividade.

## Ações

* fechar popup.

## Funcionamento

O popup recebe o `ActivityLog` correspondente ao item selecionado no Repeating Group através de `DisplayGroupData`.

A implementação foi validada e o popup atualmente funciona conforme o padrão utilizado na página `activities`.

---

# 10. Página `project`

## Objetivo

Exibir os dados de um projeto específico e suas tarefas.

A página recebe um `Project` como contexto da página.

## Estrutura

```text
grp_sidebar
└── re_sidebar

grp_content
├── grp_project_header
└── grp_tasks_section
```

## Informações do projeto

* nome;
* descrição;
* status;
* proprietário;
* data de criação.

## Ações

* editar projeto;
* arquivar projeto;
* criar tarefa.

A estrutura atual utiliza `btn_edit_project` e `btn_new_task` para as principais operações.

---

# 11. Lista de Tarefas do Projeto

## Fonte

`Task`

### Restrições

```text
project = CurrentPageItem
archived = false
```

As tarefas são ordenadas pela data de criação.

## Informações exibidas

* título;
* prioridade;
* responsável;
* status;
* vencimento.

## Ações

* abrir tarefa;
* editar tarefa;
* criar nova tarefa.

---

# 12. Popup `pop_new_task`

## Objetivo

Criar uma nova tarefa vinculada ao projeto atual.

## Campos

* título;
* descrição;
* prioridade;
* status;
* responsável;
* data limite.

## Regras

A tarefa deve possuir:

* projeto;
* título;
* responsável;
* status.

Após a criação, devem ser executados os processos de histórico e notificação definidos nos workflows do sistema.

---

# 13. Popup `pop_edit_project`

## Objetivo

Editar as informações de um projeto existente.

## Tipo de dado

`Project`

## Campos

* nome;
* descrição;
* status;
* demais propriedades permitidas.

## Permissão

A edição deve respeitar as regras de privacidade e propriedade do `Project`.

---

# 14. Popup `pop_edit_task`

## Objetivo

Editar uma tarefa existente.

## Tipo de dado

`Task`

## Campos

* título;
* descrição;
* responsável;
* prioridade;
* status;
* data limite.

## Regras

O comportamento de edição deve respeitar as regras de privacidade da entidade `Task`.

O criador possui controle completo, enquanto o responsável possui edição limitada aos campos permitidos, principalmente status e data de conclusão.

---

# 15. Página `tasks`

## Objetivo

Apresentar a listagem completa de tarefas.

## Estrutura

A página possui:

* header;
* sidebar;
* filtros;
* campo de pesquisa;
* Repeating Group de tarefas;
* estado vazio;
* popup de alteração rápida de status.

## Fonte

`Task`

## Filtros

A listagem suporta filtros combinados de:

* status;
* prioridade;
* projeto;
* pesquisa textual.

Os filtros são aplicados diretamente na fonte de dados do Repeating Group, não sendo necessário um workflow específico para atualizar a lista.

---

# 16. Ações da Página `tasks`

## Abrir tarefa

O usuário pode acessar a página `task` através:

* do título da tarefa;
* do botão de abertura.

Ambos enviam a tarefa atual como contexto da página.

---

## Abrir projeto

O nome do projeto permite navegar para `project`, enviando o projeto relacionado à tarefa.

---

## Alteração rápida de status

O botão `btn_task_status` abre o popup `pop_quick_status`.

O workflow:

1. Define a tarefa selecionada.
2. Abre o popup.
3. Permite selecionar novo status.
4. Atualiza a tarefa.
5. Registra `ActivityLog`.
6. Cria `Notification`.
7. Fecha o popup.
8. Reseta os campos.

---

# 17. Popup `pop_quick_status`

## Objetivo

Permitir alteração rápida do status sem abrir a página da tarefa.

## Tipo de dado

`Task`

## Campos

* status atual;
* novo status.

## Ações

* Cancelar;
* Salvar.

---

# 18. Página `task`

## Objetivo

Exibir todas as informações de uma tarefa e permitir suas principais operações.

## Informações

* título;
* descrição;
* projeto;
* responsável;
* prioridade;
* status;
* data limite;
* data de conclusão.

## Comentários

A página possui:

* campo para novo comentário;
* botão `Adicionar Comentário`;
* Repeating Group de comentários;
* estado vazio;
* edição de comentário.

## Histórico

A página apresenta os registros de `ActivityLog` associados à tarefa.

## Ações

* editar tarefa;
* excluir tarefa;
* alterar status;
* adicionar comentário;
* editar comentário.

---

# 19. Comentários da Tarefa

## Fonte

`Comment`

Filtro:

```text
task = CurrentPageItem
```

Os comentários são apresentados em ordem cronológica.

## Adicionar comentário

Ao adicionar:

1. Criar `Comment`.
2. Associar `author = CurrentUser`.
3. Associar `task = CurrentPageItem`.
4. Atualizar a lista.
5. Registrar `ActivityLog`.
6. Criar notificação quando aplicável.

Esse fluxo está implementado diretamente na página `task`.

---

# 20. Página `activities`

## Objetivo

Exibir o histórico de atividades da aplicação.

A página é essencialmente de consulta: não cria nem edita registros de `ActivityLog`.

## Visualizações

### Member

`rg_activities_member`

Apresenta as atividades relacionadas ao usuário atual.

### Administrator

`rg_activities_admin`

Apresenta uma visão administrativa das atividades, permitindo consultar registros de diferentes usuários.

## Campos exibidos

* descrição;
* ação;
* tarefa;
* usuário;
* data.

## Filtros

A página possui estrutura para:

* pesquisa;
* filtros;
* limpeza dos filtros.

## Detalhes

Ao clicar em uma atividade, o sistema:

1. Define o `ActivityLog` selecionado como dado do popup.
2. Exibe `pop_activity_details`.

A mesma lógica existe para a visualização de membros e administradores.

---

# 21. Página `notifications`

## Objetivo

Apresentar as notificações recebidas pelo usuário autenticado.

## Fonte

`Notification`

Filtro:

```text
recipient = CurrentUser
```

As notificações são ordenadas pela data de criação em ordem decrescente.

## Elementos

* título;
* subtítulo;
* botão `Marcar todas como lidas`;
* `rg_notifications`;
* cards de notificação.

## Ações

* marcar notificação como lida;
* marcar todas como lidas.

O botão de marcar todas como lidas é exibido apenas quando existem notificações não lidas.

---

# 22. Página `reset_pw`

## Objetivo

Permitir que o usuário defina uma nova senha após utilizar o fluxo de recuperação de senha.

## Componentes

* campo de nova senha;
* confirmação de senha;
* botão de confirmação.

## Resultado

Após redefinir a senha, o usuário deve ser direcionado ao fluxo normal de autenticação.

---

# 23. Página `404`

## Objetivo

Informar que a página ou recurso solicitado não foi encontrado.

## Comportamento

A página deve oferecer uma ação para retornar ao Dashboard.

---

# 24. Regras de Visibilidade

## Usuário não autenticado

Pode acessar:

* `auth`;
* fluxo de recuperação de senha;
* `reset_pw`.

Ao tentar acessar páginas privadas, deve ser redirecionado para `auth`.

---

## Usuário autenticado

Pode acessar:

* `index`;
* `project`;
* `tasks`;
* `task`;
* `activities`;
* `notifications`.

---

## Administrador

Possui recursos adicionais relacionados ao gerenciamento e consulta administrativa, especialmente na página `activities`.

---

## Membro

Possui acesso à própria visão de atividades e às funcionalidades operacionais disponíveis para usuários comuns.

---

# 25. Responsividade

A aplicação utiliza layout responsivo baseado nos recursos nativos de responsive layout do Bubble.

Os principais elementos devem adaptar-se conforme a largura disponível:

### Desktop

* sidebar expandida;
* conteúdo principal em largura ampla;
* cards distribuídos horizontalmente quando aplicável.

### Tablet

* sidebar pode ser recolhida;
* conteúdo ocupa maior proporção da tela.

### Mobile

* sidebar recolhida;
* elementos organizados verticalmente;
* cards e formulários adaptados à largura disponível.

A `re_sidebar` possui estado `is_collapsed` para suportar essa adaptação.

---

# 26. Componentes e Padrões de Interface

Os principais padrões reutilizados na aplicação são:

* `re_header`;
* `re_sidebar`;
* cards de projetos;
* cards de tarefas;
* cards de comentários;
* cards de notificações;
* cards de atividades;
* estados vazios;
* popups de confirmação e edição.

A implementação deve priorizar os componentes já existentes em vez de duplicar estruturas entre páginas.

---

# 27. Critérios de Aceitação

Uma tela será considerada funcionalmente concluída quando:

* possuir os elementos previstos para sua responsabilidade;
* carregar corretamente os dados;
* respeitar as regras de privacidade;
* executar os workflows associados;
* respeitar as regras de visibilidade por autenticação e role;
* apresentar estados vazios quando não houver registros;
* atualizar a interface após operações persistidas;
* funcionar adequadamente nos layouts responsivos previstos.

---

# 28. Estado Atual do MVP

A estrutura atual do projeto representa uma simplificação em relação à especificação inicial.

### Removido da estrutura atual

Não existem mais como páginas independentes:

* `projects`;
* `my_tasks`;
* `profile`.

Os projetos são gerenciados diretamente pelo Dashboard e pela página `project`, enquanto as tarefas possuem uma listagem central em `tasks`. A área de perfil não faz parte da estrutura atual documentada.

### Removido do Dashboard

O elemento:

```text
grp_dashboard_metrics
```

foi **excluído do produto**, pois os indicadores avançados não são mais relevantes para a primeira versão do MVP.

Consequentemente, a documentação não deve considerar esse grupo como parte da interface atual.

---

# 29. Considerações Finais

A interface atual do **Ozzy - Task Manager** foi simplificada para concentrar as funcionalidades essenciais do MVP.

O `index` funciona como ponto central da aplicação, reunindo projetos, tarefas pendentes e atividades recentes. As páginas `project`, `tasks` e `task` concentram o fluxo operacional de gerenciamento, enquanto `activities` e `notifications` tratam respectivamente de histórico e comunicação interna.

A especificação deve ser mantida sincronizada com a implementação real do Bubble. Alterações estruturais em páginas, Repeating Groups, popups, componentes reutilizáveis ou regras de visibilidade devem ser refletidas neste documento antes da implementação de novas funcionalidades.
