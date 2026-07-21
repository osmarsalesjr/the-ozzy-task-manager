# Planejamento do Projeto

## Ozzy - Task Manager

### Sistema Colaborativo de Gerenciamento de Projetos e Tarefas

---

# 1. Visão Geral

## Objetivo

Desenvolver uma aplicação web utilizando **Bubble.io (Plano Gratuito)** para gerenciamento colaborativo de projetos, tarefas e comunicação entre membros de uma equipe.

A aplicação permitirá que usuários autenticados organizem projetos, criem e acompanhem tarefas, registrem comentários, recebam notificações e mantenham um histórico das atividades realizadas.

O projeto será desenvolvido priorizando simplicidade, organização, reutilização de componentes e boas práticas de modelagem de dados, utilizando exclusivamente recursos compatíveis com o plano gratuito do Bubble.

---

# 2. Objetivos do Projeto

* Construir uma aplicação funcional utilizando Bubble.io.
* Aplicar conceitos de desenvolvimento No-Code.
* Modelar uma estrutura de dados escalável.
* Implementar workflows para automação das regras de negócio.
* Desenvolver uma interface moderna e responsiva.
* Publicar a aplicação.
* Produzir documentação técnica completa para manutenção e evolução do sistema.

---

# 3. Escopo do MVP

O MVP contemplará apenas as funcionalidades essenciais para validar a proposta do sistema.

## Funcionalidades Incluídas

### Autenticação

* Cadastro de usuários
* Login
* Logout
* Recuperação de senha

---

### Gerenciamento de Projetos

* Visualizar projetos
* Criar projetos
* Editar projetos
* Arquivar projetos
* Definir proprietário do projeto

> **Observação:** Caso seja necessário simplificar a implementação inicial, poderá ser utilizado um único projeto padrão ("Default"), mantendo a estrutura preparada para suportar múltiplos projetos futuramente.

---

### Dashboard

* Resumo das tarefas
* Indicadores por status
* Atividades recentes
* Acesso rápido às principais funcionalidades

---

### Gerenciamento de Tarefas

* Criar tarefa
* Editar tarefa
* Excluir tarefa
* Alterar status
* Definir responsável
* Definir prioridade
* Definir data limite
* Associar tarefa a um projeto

---

### Comentários

* Adicionar comentários
* Histórico de comentários por tarefa

---

### Notificações

* Notificações internas
* Marcação como lida
* Classificação por tipo de notificação

---

### Histórico de Atividades

* Registrar automaticamente ações importantes da aplicação
* Exibir timeline da tarefa

---

### Perfil

* Visualizar informações do usuário
* Editar nome
* Editar avatar

---

# 4. Funcionalidades Fora do Escopo

As funcionalidades abaixo não fazem parte do MVP por aumentarem significativamente a complexidade da solução ou exigirem recursos além do plano gratuito do Bubble.

* Chat em tempo real
* Upload de arquivos
* Integrações com serviços externos
* Notificações Push
* Aplicativo mobile
* Controle avançado de permissões
* Dashboard analítico avançado
* API pública
* Automações externas
* Integração com calendário
* Subtarefas
* Etiquetas (Tags)
* Dependência entre tarefas

---

# 5. Requisitos Funcionais

## RF01

O sistema deverá permitir o cadastro de novos usuários.

## RF02

O sistema deverá permitir autenticação através de login e senha.

## RF03

O usuário autenticado poderá encerrar sua sessão (logout).

## RF04

O sistema deverá permitir visualizar e gerenciar projetos.

## RF05

O sistema deverá permitir criar tarefas vinculadas a um projeto.

## RF06

O sistema deverá permitir editar tarefas.

## RF07

O sistema deverá permitir excluir tarefas.

## RF08

Cada tarefa deverá possuir um responsável.

## RF09

Cada tarefa deverá possuir um status.

## RF10

Cada tarefa poderá receber comentários.

## RF11

O sistema deverá registrar notificações relacionadas às tarefas.

## RF12

O usuário poderá visualizar apenas suas notificações.

## RF13

O dashboard deverá apresentar as tarefas do usuário.

## RF14

O sistema deverá registrar automaticamente o histórico das principais ações realizadas nas tarefas.

---

# 6. Requisitos Não Funcionais

* Desenvolvido utilizando Bubble.io.
* Compatível com o plano gratuito da plataforma.
* Interface responsiva.
* Navegação simples e intuitiva.
* Dados persistidos no banco nativo do Bubble.
* Utilização exclusiva de recursos nativos sempre que possível.
* Utilização de Option Sets para estados fixos da aplicação.
* Organização dos workflows por domínio funcional.
* Estrutura preparada para evolução futura.

---

# 7. Regras de Negócio

**RN01**

Somente usuários autenticados poderão acessar o sistema.

**RN02**

Toda tarefa deverá estar vinculada a um projeto.

**RN03**

Toda tarefa deverá possuir um responsável.

**RN04**

Toda tarefa deverá possuir um status.

**RN05**

Ao criar uma tarefa, deverá ser gerada uma notificação para o responsável.

**RN06**

Ao adicionar um comentário, deverá ser criada uma nova notificação.

**RN07**

Toda alteração relevante deverá gerar um registro no histórico de atividades.

**RN08**

O usuário poderá marcar notificações como lidas.

**RN09**

Somente o criador da tarefa poderá excluí-la.

---

# 8. Backlog do Produto

| ID   | História de Usuário                                                       | Prioridade |
| ---- | ------------------------------------------------------------------------- | ---------- |
| US01 | Como visitante, desejo criar uma conta para utilizar o sistema.           | Alta       |
| US02 | Como usuário, desejo realizar login para acessar meus projetos e tarefas. | Alta       |
| US03 | Como usuário, desejo encerrar minha sessão.                               | Alta       |
| US04 | Como usuário, desejo visualizar meus projetos.                            | Média      |
| US05 | Como usuário, desejo criar um projeto para organizar minhas tarefas.      | Média      |
| US06 | Como usuário, desejo visualizar minhas tarefas.                           | Alta       |
| US07 | Como usuário, desejo criar uma tarefa.                                    | Alta       |
| US08 | Como usuário, desejo editar uma tarefa.                                   | Alta       |
| US09 | Como usuário, desejo excluir uma tarefa.                                  | Média      |
| US10 | Como usuário, desejo alterar o status de uma tarefa.                      | Alta       |
| US11 | Como usuário, desejo definir um responsável para uma tarefa.              | Alta       |
| US12 | Como usuário, desejo comentar em uma tarefa.                              | Alta       |
| US13 | Como usuário, desejo visualizar minhas notificações.                      | Média      |
| US14 | Como usuário, desejo marcar notificações como lidas.                      | Média      |
| US15 | Como usuário, desejo visualizar o histórico de atividades de uma tarefa.  | Média      |
| US16 | Como usuário, desejo editar meu perfil.                                   | Baixa      |

---

# 9. Priorização do MVP

## Sprint 1 — Fundação

* Estrutura do banco de dados
* Cadastro
* Login
* Logout
* Dashboard inicial

---

## Sprint 2 — Projetos e Tarefas

* Gerenciamento de projetos
* Criação de tarefas
* Edição de tarefas
* Exclusão de tarefas
* Alteração de status
* Definição de responsável

---

## Sprint 3 — Colaboração

* Comentários
* Notificações
* Histórico de atividades
* Perfil do usuário

---

## Sprint 4 — Finalização

* Ajustes visuais
* Testes funcionais
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
* O usuário conseguir visualizar seus projetos.
* O usuário conseguir criar tarefas vinculadas a um projeto.
* O usuário conseguir editar tarefas.
* O usuário conseguir alterar o status das tarefas.
* O usuário conseguir comentar em tarefas.
* O sistema registrar notificações automaticamente.
* O sistema registrar o histórico das principais ações das tarefas.
* O dashboard apresentar corretamente as tarefas do usuário.
* A aplicação estiver publicada no Bubble.

---

# 11. Riscos do Projeto

| Risco                          | Impacto | Mitigação                                              |
| ------------------------------ | ------- | ------------------------------------------------------ |
| Limitações do plano gratuito   | Médio   | Utilizar apenas recursos nativos do Bubble             |
| Retrabalho na modelagem        | Alto    | Validar a estrutura do banco antes da implementação    |
| Workflows complexos            | Médio   | Desenvolver e testar incrementalmente                  |
| Crescimento do escopo          | Alto    | Priorizar exclusivamente o MVP                         |
| Inconsistência entre artefatos | Médio   | Manter a documentação sincronizada com a implementação |

---

# 12. Próximos Artefatos

Após a aprovação deste planejamento, serão produzidos os seguintes documentos:

1. Modelagem do Banco de Dados.
2. Arquitetura da Aplicação.
3. Especificação dos Workflows.
4. Wireframes das Telas.
5. Plano de Testes.
6. README do Projeto.
7. Roteiro do Vídeo Pitch.
