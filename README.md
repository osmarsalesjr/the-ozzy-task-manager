# Ozzy - Task Manager

Repositório de artefatos do **Ozzy - Task Manager**, uma aplicação web para gerenciamento colaborativo de projetos e tarefas, desenvolvida utilizando **Bubble.io**.

Este repositório reúne a documentação técnica e os principais artefatos utilizados durante o desenvolvimento do MVP.

---

## 1. Explicação Do Projeto

O **Ozzy - Task Manager** permite que usuários gerenciem projetos e tarefas de forma colaborativa.

Entre as principais funcionalidades estão:

* Gerenciamento De Usuários
* Gerenciamento De Projetos
* Criação E Gerenciamento De Tarefas
* Atribuição De Responsáveis
* Controle De Status E Prioridade
* Comentários Em Tarefas
* Notificações
* Histórico De Atividades
* Gerenciamento De Perfil
* Controle De Acesso Por Perfil

A aplicação foi desenvolvida utilizando recursos nativos do **Bubble.io**, priorizando baixo acoplamento, reutilização de componentes e facilidade de manutenção.

---

## 2. Como Acessar E Testar

### Versão De Teste

A versão funcional do projeto está disponível no link abaixo:

**[Acessar Versão De Teste](https://ozzy-task-manager.bubbleapps.io/version-test/)**

### Perfis De Acesso

O sistema possui diferentes níveis de acesso:

| Perfil        | Descrição                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------- |
| Administrator | Responsável pelo gerenciamento administrativo da aplicação, incluindo a criação de novos usuários. |
| Member        | Usuário da aplicação com acesso às funcionalidades operacionais permitidas pelo sistema.           |

Novos usuários **não realizam cadastro diretamente pela aplicação**. A criação de usuários é realizada exclusivamente por um **Administrator**.

> Os dados de acesso para teste deverão ser disponibilizados junto ao link da aplicação, quando necessário.

---

## 3. Tecnologias Utilizadas

* **Bubble.io** — Desenvolvimento Da Aplicação Web
* **Bubble Database** — Armazenamento Dos Dados
* **Bubble Authentication** — Autenticação Dos Usuários
* **Option Sets** — Controle De Estados E Valores Fixos
* **Workflows** — Implementação Das Regras De Negócio
* **Reusable Elements** — Componentização Da Interface

---

## 4. Prints De Tela

Esta seção apresenta as principais telas da aplicação.

Os links das imagens abaixo devem ser substituídos pelos respectivos arquivos ou URLs dos screenshots.

### 4.1 Login

![Tela De Login](/images/login.png)

---

### 4.2 Dashboard — Administrator

![Dashboard Administrator](/images/index_dashboard_01.png)

![Dashboard Administrator](/images/index_dashboard_02.png)

### 4.3 Dashboard — Member

![Dashboard Member](/images/index_dashboard_member_vision.png)

---

### 4.4 Projetos — Administrator

![Projetos Administrator](/images/projects_admin_vision.png)

### 4.5 Projetos — Member

![Projetos Member](/images/projects_member_vision.png)

---

### 4.6 Detalhes Do Projeto — Administrator

![Detalhes Do Projeto Administrator](/images/project_admin_vision.png)

### 4.7 Detalhes Do Projeto — Member

![Detalhes Do Projeto Member](/images/project_member_vision.png)

---

### 4.8 Tarefas — Administrator / Member

![Tarefas Administrator](/images/tasks_both_vision.png)


---

### 4.10 Detalhes Da Tarefa — Administrator

![Detalhes Da Tarefa Administrator](/images/task_admin_vision.png)

### 4.11 Detalhes Da Tarefa — Member

![Detalhes Da Tarefa Member](/images/task_member_vision.png)

---

### 4.12 Notificações — Administrator / Member

![Notificações Administrator](/images/notifications_both_vision.png)

---

## 5. Artefatos Do Projeto

Os principais documentos utilizados para especificação, desenvolvimento e validação do projeto estão disponíveis neste repositório.

Entre eles:

* **Documentação Oficial**
* **Modelagem De Dados**
* **Arquitetura Da Solução**
* **Especificação De Workflows**
* **Especificação Funcional Das Telas**
* **Guia De Desenvolvimento**
* **Plano De Testes**
* **Checklist De Deploy**

---

## 6. Links Funcionais

| Recurso                     | Link                                       |
| --------------------------- | ------------------------------------------ |
| Aplicação — Versão De Teste | [Acessar](https://ozzy-task-manager.bubbleapps.io/version-test/) |
| Repositório De Artefatos    | [Acessar](https://github.com/osmarsalesjr/the-ozzy-task-manager)     |
| Documentação Oficial        | [Acessar](/pdfs/documentation.pdf)    |

---

## 7. Observações

A aplicação corresponde à versão **MVP** do projeto.

Os acessos, links funcionais e imagens apresentados neste README poderão ser atualizados conforme a evolução e publicação da solução.
