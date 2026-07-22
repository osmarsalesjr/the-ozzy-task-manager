# Plano de Testes

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento define a estratégia de testes do **Ozzy - Task Manager**, estabelecendo os critérios para validação das funcionalidades implementadas durante o desenvolvimento.

O objetivo é garantir que a aplicação atenda aos requisitos funcionais, não funcionais e regras de negócio definidos para o MVP.

---

# 2. Escopo dos Testes

Serão validados:

* Autenticação
* Gerenciamento de Projetos
* Gerenciamento de Tarefas
* Comentários
* Notificações
* Histórico de Atividades
* Perfil do Usuário
* Dashboard
* Navegação
* Responsividade

---

# 3. Estratégia de Testes

A validação será realizada em quatro níveis.

## Testes Funcionais

Verificam se cada funcionalidade atende ao comportamento esperado.

---

## Testes de Interface

Validam:

* Layout
* Componentes
* Responsividade
* Navegação

---

## Testes de Regras de Negócio

Verificam:

* Permissões
* Validações
* Estados
* Fluxos

---

## Testes de Integração

Validam o funcionamento conjunto entre:

* Interface
* Workflows
* Banco de Dados
* Option Sets

---

# 4. Ambiente de Testes

## Plataforma

Bubble.io

---

## Navegadores

* Google Chrome
* Microsoft Edge

---

## Dispositivos

* Desktop
* Tablet
* Smartphone

---

# 5. Casos de Teste

## CT-001 — Cadastro de Usuário

### Objetivo

Validar o cadastro de um novo usuário.

### Pré-condição

Usuário não autenticado.

### Passos

1. Acessar Sign Up.
2. Informar nome.
3. Informar e-mail válido.
4. Informar senha.
5. Confirmar senha.
6. Clicar em Criar Conta.

### Resultado Esperado

* Usuário criado.
* Login automático.
* Redirecionamento para Dashboard.

---

## CT-002 — Login

### Objetivo

Validar autenticação.

### Passos

1. Informar e-mail.
2. Informar senha.
3. Clicar em Entrar.

### Resultado Esperado

Usuário autenticado.

---

## CT-003 — Logout

### Resultado Esperado

Sessão encerrada.

Usuário redirecionado para Login.

---

## CT-004 — Criar Projeto

### Passos

1. Novo Projeto.
2. Informar nome.
3. Salvar.

### Resultado Esperado

Projeto criado.

Status inicial:

Active

Owner:

Current User

---

## CT-005 — Editar Projeto

### Resultado Esperado

Informações atualizadas corretamente.

---

## CT-006 — Arquivar Projeto

### Resultado Esperado

Projeto arquivado.

Não aparece na listagem principal.

---

## CT-007 — Criar Tarefa

### Passos

1. Selecionar projeto.
2. Informar título.
3. Informar responsável.
4. Salvar.

### Resultado Esperado

* Task criada.
* ActivityLog criado.
* Notification criada.

---

## CT-008 — Editar Tarefa

### Resultado Esperado

Dados atualizados corretamente.

---

## CT-009 — Excluir Tarefa

### Resultado Esperado

Task removida.

ActivityLog registrado.

---

## CT-010 — Alterar Status

### Resultado Esperado

Status atualizado.

Se Done:

completed_date preenchida.

ActivityLog criado.

---

## CT-011 — Alterar Responsável

### Resultado Esperado

assigned_to atualizado.

Nova Notification criada.

---

## CT-012 — Adicionar Comentário

### Resultado Esperado

Comment criado.

ActivityLog criado.

Notification criada.

---

## CT-013 — Editar Comentário

### Resultado Esperado

Comentário atualizado.

---

## CT-014 — Excluir Comentário

### Resultado Esperado

Comentário removido.

---

## CT-015 — Marcar Notificação como Lida

### Resultado Esperado

is_read = yes

---

## CT-016 — Atualizar Perfil

### Resultado Esperado

Nome e avatar atualizados.

---

# 6. Testes das Regras de Negócio

| Código | Regra                                                 | Resultado Esperado               |
| ------ | ----------------------------------------------------- | -------------------------------- |
| RN-01  | Apenas usuários autenticados acessam páginas privadas | Acesso negado para visitantes    |
| RN-02  | Todo projeto possui proprietário                      | Owner preenchido automaticamente |
| RN-03  | Toda tarefa pertence a um projeto                     | Não permitir salvar sem projeto  |
| RN-04  | Toda tarefa possui responsável                        | Campo obrigatório                |
| RN-05  | Alterações importantes geram ActivityLog              | Registro criado automaticamente  |
| RN-06  | Comentários geram Notification                        | Notificação criada               |
| RN-07  | Apenas usuários autorizados alteram dados             | Operação bloqueada               |

---

# 7. Testes das Privacy Rules

Validar:

* Usuário acessa apenas seus próprios dados.
* Usuário visualiza apenas suas notificações.
* Usuário não altera registros sem permissão.
* Dados sensíveis não ficam expostos.

---

# 8. Testes de Interface

Verificar:

* Alinhamento dos componentes.
* Espaçamentos.
* Consistência visual.
* Estados vazios.
* Mensagens de erro.
* Mensagens de sucesso.
* Modais.
* Navegação.

---

# 9. Testes de Responsividade

## Desktop

Validar todas as funcionalidades.

---

## Tablet

Verificar:

* Sidebar recolhida.
* Componentes reorganizados.

---

## Mobile

Validar:

* Menu responsivo.
* Cards empilhados.
* Botões acessíveis.
* Formulários utilizáveis.

---

# 10. Testes de Performance

Verificar:

* Tempo de login.
* Tempo de carregamento do Dashboard.
* Tempo de carregamento das listas.
* Tempo para salvar registros.

---

# 11. Critérios de Aprovação

Uma funcionalidade será considerada aprovada quando:

* Todos os casos de teste forem executados.
* Nenhum erro crítico permanecer aberto.
* As regras de negócio forem atendidas.
* As Privacy Rules funcionarem corretamente.
* Os dados forem persistidos corretamente.
* A interface apresentar comportamento consistente.

---

# 12. Registro de Defeitos

Cada defeito identificado deverá conter:

* Código
* Descrição
* Tela afetada
* Passos para reprodução
* Resultado obtido
* Resultado esperado
* Prioridade
* Responsável
* Status

---

# 13. Checklist de Validação Final

## Autenticação

* [ ] Cadastro
* [ ] Login
* [ ] Logout
* [ ] Recuperação de senha

---

## Projetos

* [ ] Criar
* [ ] Editar
* [ ] Arquivar

---

## Tarefas

* [ ] Criar
* [ ] Editar
* [ ] Excluir
* [ ] Alterar status
* [ ] Alterar responsável

---

## Comentários

* [ ] Criar
* [ ] Editar
* [ ] Excluir

---

## Notificações

* [ ] Criar
* [ ] Marcar como lida

---

## Histórico

* [ ] ActivityLog criado corretamente

---

## Perfil

* [ ] Atualizar nome
* [ ] Atualizar avatar

---

## Dashboard

* [ ] Indicadores corretos
* [ ] Projetos carregados
* [ ] Tarefas carregadas
* [ ] Atividades recentes carregadas

---

## Interface

* [ ] Responsividade
* [ ] Navegação
* [ ] Mensagens
* [ ] Componentes reutilizáveis

---

# 14. Critérios para Conclusão do MVP

O MVP será considerado concluído quando:

* Todos os requisitos funcionais estiverem implementados.
* Todos os casos de teste estiverem aprovados.
* Não existirem defeitos críticos ou bloqueadores.
* A aplicação estiver publicada no Bubble.io.
* A documentação estiver atualizada.

---

# 15. Considerações Finais

Este Plano de Testes estabelece o processo oficial de validação do **Ozzy - Task Manager**.

Todos os testes deverão ser executados antes da publicação do MVP, garantindo que a aplicação atenda aos requisitos definidos no planejamento, arquitetura e modelagem de dados, assegurando qualidade, estabilidade e consistência da solução.
