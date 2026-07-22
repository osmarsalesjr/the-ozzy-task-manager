# Especificação Funcional dos Workflows

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento descreve o comportamento funcional de todos os Workflows do **Ozzy - Task Manager**.

Cada Workflow define:

* Evento disparador
* Validações
* Operações executadas
* Atualizações no banco de dados
* Atualizações na interface
* Registros de histórico
* Notificações geradas

O objetivo é servir como guia para implementação da lógica de negócio da aplicação.

---

# 2. Fluxo Geral dos Workflows

Todos os Workflows deverão seguir a seguinte estrutura lógica:

```text
Evento

↓

Validação

↓

Regra de Negócio

↓

Persistência

↓

ActivityLog

↓

Notification

↓

Atualização da Interface
```

---

# 3. Workflows de Autenticação

## WF-001 — Cadastro de Usuário

### Evento

Clique no botão **Criar Conta**.

### Validações

* Nome obrigatório.
* E-mail obrigatório.
* Senha obrigatória.
* Senha confirmada corretamente.

### Ações

1. Criar User.
2. Definir UserRole = Member.
3. Realizar login automaticamente.
4. Redirecionar para Dashboard.

### ActivityLog

Não aplicável.

### Notification

Não aplicável.

---

## WF-002 — Login

### Evento

Clique em **Entrar**.

### Validações

* Usuário existente.
* Senha válida.

### Ações

1. Autenticar usuário.
2. Criar sessão.
3. Redirecionar para Dashboard.

---

## WF-003 — Logout

### Evento

Clique em **Sair**.

### Ações

1. Encerrar sessão.
2. Redirecionar para Login.

---

## WF-004 — Recuperação de Senha

### Evento

Solicitação de redefinição.

### Ações

1. Enviar e-mail de recuperação utilizando recurso nativo do Bubble.

---

# 4. Workflows de Projetos

## WF-101 — Criar Projeto

### Evento

Clique em **Novo Projeto**.

### Validações

* Nome obrigatório.

### Banco

Criar:

Project

* name
* description
* status = Active
* owner = Current User
* archived = no

### Interface

Atualizar lista de projetos.

---

## WF-102 — Editar Projeto

### Evento

Salvar alterações.

### Banco

Atualizar:

* name
* description
* color

---

## WF-103 — Arquivar Projeto

### Evento

Clique em **Arquivar Projeto**.

### Banco

Atualizar:

* archived = yes
* status = Archived

### Interface

Ocultar projeto da listagem principal.

---

# 5. Workflows de Tarefas

## WF-201 — Criar Tarefa

### Evento

Clique em **Salvar**.

### Validações

* Projeto obrigatório.
* Título obrigatório.
* Responsável obrigatório.

### Banco

Criar Task.

### ActivityLog

Registrar:

Task Created

### Notification

Criar notificação para o responsável.

### Interface

Atualizar lista de tarefas.

---

## WF-202 — Editar Tarefa

### Evento

Salvar alterações.

### Banco

Atualizar Task.

### ActivityLog

Registrar:

Task Updated

### Notification

Criar notificação caso o responsável tenha sido alterado.

---

## WF-203 — Excluir Tarefa

### Evento

Confirmação da exclusão.

### Validações

Somente o criador da tarefa poderá excluir.

### Banco

Excluir Task.

### ActivityLog

Registrar:

Task Deleted

---

## WF-204 — Alterar Status

### Evento

Mudança do Status.

### Banco

Atualizar:

status

Se status = Done:

completed_date = Current Date

### ActivityLog

Status Changed

### Notification

Criar notificação para o responsável.

---

## WF-205 — Alterar Responsável

### Evento

Novo responsável selecionado.

### Banco

Atualizar assigned_to.

### ActivityLog

Assignee Changed.

### Notification

Criar notificação.

---

# 6. Workflows de Comentários

## WF-301 — Adicionar Comentário

### Evento

Clique em **Enviar**.

### Banco

Criar Comment.

### ActivityLog

Comment Added.

### Notification

Criar notificação para o responsável da tarefa.

### Interface

Atualizar lista de comentários.

---

## WF-302 — Editar Comentário

### Evento

Salvar.

### Banco

Atualizar Comment.

---

## WF-303 — Excluir Comentário

### Evento

Confirmação.

### Banco

Excluir Comment.

---

# 7. Workflows de Notificações

## WF-401 — Criar Notificação

Este Workflow será reutilizado por toda a aplicação.

Campos:

* title
* message
* recipient
* task
* type

---

## WF-402 — Marcar como Lida

### Evento

Clique sobre a notificação.

### Banco

is_read = yes

---

# 8. Workflows de Histórico

## WF-501 — Registrar ActivityLog

Este Workflow será reutilizado por todos os processos da aplicação.

Campos registrados:

* task
* user
* action
* description
* metadata

Sempre que ocorrer:

* criação;
* atualização;
* exclusão;
* mudança de status;
* mudança de responsável;
* comentário.

---

# 9. Workflows do Perfil

## WF-601 — Atualizar Perfil

### Banco

Atualizar:

* name
* avatar

---

# 10. Fluxos Integrados

## Criar Projeto

```text
Usuário

↓

Preenche formulário

↓

Validar campos

↓

Criar Project

↓

Atualizar Dashboard

↓

Mensagem de sucesso
```

---

## Criar Tarefa

```text
Usuário

↓

Preenche formulário

↓

Validar dados

↓

Criar Task

↓

Registrar ActivityLog

↓

Criar Notification

↓

Atualizar Dashboard

↓

Mensagem de sucesso
```

---

## Alterar Status

```text
Usuário

↓

Seleciona novo status

↓

Atualizar Task

↓

Registrar ActivityLog

↓

Criar Notification

↓

Atualizar Interface
```

---

## Adicionar Comentário

```text
Usuário

↓

Digita comentário

↓

Criar Comment

↓

Registrar ActivityLog

↓

Criar Notification

↓

Atualizar comentários
```

---

# 11. Regras Gerais

Todos os Workflows deverão observar as seguintes diretrizes:

* Validar permissões antes de qualquer alteração.
* Evitar duplicação de lógica.
* Utilizar Workflows reutilizáveis sempre que possível.
* Registrar alterações importantes no ActivityLog.
* Gerar notificações apenas quando agregarem valor ao usuário.
* Atualizar a interface imediatamente após alterações persistidas.

---

# 12. Tratamento de Erros

Sempre que uma operação falhar:

* Exibir mensagem amigável ao usuário.
* Não atualizar a interface.
* Não registrar ActivityLog.
* Não criar Notification.

---

# 13. Critérios de Conclusão

Um Workflow será considerado concluído quando:

* Todas as validações estiverem implementadas.
* As regras de negócio forem executadas corretamente.
* Os dados forem persistidos.
* O ActivityLog for registrado quando aplicável.
* As notificações forem geradas quando necessário.
* A interface refletir imediatamente as alterações.
* O fluxo tiver sido validado em testes funcionais.

---

# 14. Considerações Finais

Esta especificação funcional representa a definição oficial dos Workflows do **Ozzy - Task Manager**.

Durante a implementação no Bubble.io, toda lógica de negócio deverá seguir os fluxos descritos neste documento, garantindo consistência, reutilização e facilidade de manutenção da aplicação.
