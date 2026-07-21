# Planejamento do Projeto

## Ozzy - Task Manager (Sistema de Gerenciamento de Tarefas Colaborativo)

---

# 1. Visão Geral

## Objetivo

Desenvolver uma aplicação web utilizando **Bubble.io (Plano Gratuito)** para gerenciamento de tarefas e comunicação entre membros de uma equipe.

A aplicação deverá permitir que usuários autenticados criem, acompanhem e atualizem tarefas, além de registrar comentários e notificações relacionadas às atividades.

O projeto será desenvolvido priorizando simplicidade, organização e boas práticas de modelagem de dados, atendendo aos requisitos propostos no desafio acadêmico.

---

# 2. Objetivos do Projeto

* Construir uma aplicação funcional utilizando Bubble.io.
* Aplicar conceitos de desenvolvimento No-Code.
* Utilizar banco de dados relacional.
* Implementar workflows para automação das regras de negócio.
* Desenvolver interface responsiva.
* Publicar a aplicação.
* Produzir documentação técnica e artefatos para portfólio.

---

# 3. Escopo do MVP

O MVP contemplará apenas as funcionalidades necessárias para validar a proposta do sistema.

## Funcionalidades Incluídas

### Autenticação

* Cadastro de usuários
* Login
* Logout
* Recuperação de senha

### Dashboard

* Visualização das tarefas do usuário
* Resumo por status
* Lista das atividades recentes

### Gerenciamento de Tarefas

* Criar tarefa
* Editar tarefa
* Excluir tarefa
* Alterar status
* Definir responsável
* Definir prioridade
* Definir data limite

### Comentários

* Adicionar comentários em tarefas
* Histórico de comentários

### Notificações

* Notificações internas
* Marcação como lida

### Perfil

* Visualizar informações do usuário
* Editar nome e foto de perfil

---

# 4. Funcionalidades Fora do Escopo

As funcionalidades abaixo não fazem parte do MVP por aumentarem significativamente a complexidade da solução ou exigirem recursos além do plano gratuito do Bubble.

* Chat em tempo real
* Upload de arquivos
* Integração com serviços externos
* Notificações Push
* Aplicativo mobile
* Controle avançado de permissões
* Relatórios analíticos
* Integração com calendário
* API pública

---

# 5. Requisitos Funcionais

## RF01

O sistema deverá permitir o cadastro de novos usuários.

## RF02

O sistema deverá permitir autenticação através de login e senha.

## RF03

O usuário autenticado poderá encerrar sua sessão (logout).

## RF04

O sistema deverá permitir criar tarefas.

## RF05

O sistema deverá permitir editar tarefas.

## RF06

O sistema deverá permitir excluir tarefas.

## RF07

Cada tarefa deverá possuir um responsável.

## RF08

Cada tarefa deverá possuir um status.

## RF09

Cada tarefa poderá receber comentários.

## RF10

O sistema deverá registrar notificações relacionadas às tarefas.

## RF11

O usuário poderá visualizar apenas suas notificações.

## RF12

O dashboard deverá apresentar as tarefas do usuário.

---

# 6. Requisitos Não Funcionais

* Desenvolvido utilizando Bubble.io.
* Compatível com o plano gratuito da plataforma.
* Interface responsiva.
* Navegação simples e intuitiva.
* Dados persistidos no banco nativo do Bubble.
* Utilização exclusiva de recursos nativos sempre que possível.
* Código organizado por boas práticas de Workflows.

---

# 7. Regras de Negócio

**RN01**

Somente usuários autenticados poderão acessar o sistema.

**RN02**

Toda tarefa deverá possuir um responsável.

**RN03**

Toda tarefa deverá possuir um status.

**RN04**

Ao criar uma tarefa, deverá ser gerada uma notificação para o responsável.

**RN05**

Ao adicionar um comentário, deverá ser criada uma nova notificação.

**RN06**

O usuário poderá marcar notificações como lidas.

**RN07**

Somente o criador da tarefa poderá excluí-la.

---

# 8. Backlog do Produto

| ID   | História de Usuário                                              | Prioridade |
| ---- | ---------------------------------------------------------------- | ---------- |
| US01 | Como visitante, desejo criar uma conta para utilizar o sistema.  | Alta       |
| US02 | Como usuário, desejo realizar login para acessar minhas tarefas. | Alta       |
| US03 | Como usuário, desejo encerrar minha sessão.                      | Alta       |
| US04 | Como usuário, desejo visualizar minhas tarefas.                  | Alta       |
| US05 | Como usuário, desejo criar uma tarefa.                           | Alta       |
| US06 | Como usuário, desejo editar uma tarefa.                          | Alta       |
| US07 | Como usuário, desejo excluir uma tarefa.                         | Média      |
| US08 | Como usuário, desejo alterar o status de uma tarefa.             | Alta       |
| US09 | Como usuário, desejo definir um responsável para uma tarefa.     | Alta       |
| US10 | Como usuário, desejo comentar em uma tarefa.                     | Alta       |
| US11 | Como usuário, desejo visualizar minhas notificações.             | Média      |
| US12 | Como usuário, desejo marcar notificações como lidas.             | Média      |
| US13 | Como usuário, desejo editar meu perfil.                          | Baixa      |

---

# 9. Priorização do MVP

## Sprint 1 — Fundação

* Cadastro
* Login
* Logout
* Estrutura do banco
* Dashboard inicial

---

## Sprint 2 — Gerenciamento de Tarefas

* Criar tarefas
* Editar tarefas
* Excluir tarefas
* Alterar status
* Responsável

---

## Sprint 3 — Colaboração

* Comentários
* Notificações
* Perfil

---

## Sprint 4 — Finalização

* Ajustes visuais
* Testes
* Correções
* Publicação
* Documentação
* Vídeo Pitch

---

# 10. Critérios de Aceitação do MVP

O MVP será considerado concluído quando:

* O usuário conseguir criar uma conta.
* O usuário conseguir realizar login.
* O usuário conseguir realizar logout.
* O usuário conseguir criar tarefas.
* O usuário conseguir editar tarefas.
* O usuário conseguir alterar o status das tarefas.
* O usuário conseguir comentar em tarefas.
* O sistema registrar notificações.
* O dashboard apresentar corretamente as tarefas do usuário.
* A aplicação estiver publicada no Bubble.

---

# 11. Riscos do Projeto

| Risco                        | Impacto | Mitigação                                     |
| ---------------------------- | ------- | --------------------------------------------- |
| Limitações do plano gratuito | Médio   | Utilizar apenas recursos nativos              |
| Retrabalho na modelagem      | Alto    | Definir banco de dados antes da implementação |
| Workflows complexos          | Médio   | Desenvolver e testar incrementalmente         |
| Falta de tempo               | Alto    | Priorizar apenas o MVP                        |

---

# 12. Próximos Artefatos

Após a aprovação deste planejamento, serão produzidos os seguintes documentos:

1. Modelagem do Banco de Dados.
2. Arquitetura da Aplicação.
3. Fluxograma dos Workflows.
4. Wireframes das Telas.
5. Plano de Testes.
6. README do Projeto.
7. Roteiro do Vídeo Pitch.
