# Script de Pitch — Ozzy Task Manager

**Duração estimada:** 4 minutos
**Formato:** Apresentação com narração + demonstração da aplicação

---

## 1. Abertura — O problema | 0:00–0:35

**Narração:**

> “No dia a dia de uma equipe, acompanhar projetos, tarefas, responsáveis e prazos pode rapidamente se tornar um desafio.
>
> Quando essas informações ficam espalhadas ou são acompanhadas de forma pouco estruturada, aumenta o risco de perder prazos, esquecer responsabilidades e dificultar o acompanhamento das atividades.
>
> Foi pensando nesse cenário que desenvolvemos o **Ozzy Task Manager**, uma aplicação para centralizar o gerenciamento de projetos e tarefas em um único ambiente, com controle de usuários, notificações e histórico das atividades.”

**Visual:**

* Mostrar rapidamente o problema.
* Entrar na tela de login da aplicação.

---

## 2. Apresentação da solução | 0:35–1:40

**Narração:**

> “O Ozzy foi desenvolvido para oferecer uma experiência simples e centralizada para os colaboradores.
>
> A aplicação possui dois perfis principais: Administrator e Member, permitindo separar as funcionalidades administrativas das operações do dia a dia.
>
> No Dashboard, temos uma visão geral das informações mais importantes.
>
> Na área de Projects, podemos visualizar e gerenciar os projetos disponíveis.
>
> Ao acessar um projeto, encontramos suas tarefas, com informações como prioridade, responsável, status e prazo.
>
> Também é possível criar e editar tarefas, alterar seus status e responsáveis e acompanhar os comentários relacionados.
>
> A aplicação ainda possui notificações e um histórico de atividades, permitindo entender o que aconteceu e quando cada alteração realizada.”

**Demonstração:**

1. Dashboard.
2. Projects.
3. Abrir um projeto.
4. Criar ou abrir uma tarefa.
5. Alterar status.
6. Mostrar comentário.
7. Mostrar Notification.
8. Mostrar Activity Log.

---

## 3. Modelagem de dados | 1:40–2:15

**Narração:**

> “Por trás da interface, estruturamos a aplicação utilizando o banco de dados nativo do Bubble.
>
> As principais entidades são User, Project, Task, Comment, Notification e ActivityLog.
>
> Essas entidades possuem relacionamentos que permitem, por exemplo, associar uma tarefa a um projeto e a um responsável, relacionar comentários às tarefas e associar notificações aos usuários.
>
> Também utilizamos Option Sets para controlar informações padronizadas, como roles, status, prioridades e tipos de ações.
>
> Essa modelagem permite manter os dados organizados e facilita a aplicação das regras de negócio.”

**Visual:**

* Mostrar o diagrama entidade-relacionamento.
* Em seguida, mostrar rapidamente os Data Types no Bubble.

---

## 4. Workflows e automações | 2:15–2:55

**Narração:**

> “A lógica da aplicação é implementada principalmente através dos Workflows do Bubble.
>
> Um exemplo é a criação de uma tarefa.
>
> Quando uma nova tarefa é criada, além da persistência do registro, o sistema pode registrar automaticamente a atividade correspondente e gerar uma notificação para o responsável.
>
> O mesmo princípio é utilizado em alterações de status, alteração de responsável, comentários e arquivamentos.
>
> Dessa forma, uma única ação do usuário pode desencadear todo o fluxo necessário sem que seja preciso implementar manualmente cada etapa na interface.
>
> Também utilizamos Privacy Rules e condições nos Workflows para garantir que cada perfil tenha acesso apenas às operações permitidas.”

**Visual:**

* Mostrar um Workflow de criação de Task.
* Destacar visualmente:
  `Task → ActivityLog → Notification`
* Mostrar rapidamente uma Privacy Rule.

---

## 5. Publicação e manutenção | 2:55–3:25

**Narração:**

> “A publicação foi realizada diretamente no Bubble, utilizando o ambiente de teste para implementação e validação antes da disponibilização da aplicação.
>
> Antes da publicação, utilizamos um checklist para validar banco de dados, Option Sets, Privacy Rules, Workflows, interface e testes.
>
> Para manutenção, a estratégia é manter os artefatos do projeto documentados e controlar alterações estruturais antes de aplicá-las na aplicação.
>
> Alterações em Data Types, Option Sets, Privacy Rules ou Workflows devem ser testadas antes da publicação.
>
> Isso reduz o risco de alterações em uma funcionalidade que pode afetar outras partes do sistema.”

**Visual:**

* Mostrar ambiente do Bubble.
* Mostrar brevemente o checklist/documentação do projeto.
* Mostrar aplicação publicada.

---

## 6. Valor do No-Code/Low-Code | 3:25–3:50

**Narração:**

> “A escolha do Bubble trouxe um ganho importante para este projeto.
>
> Como uma plataforma No-Code/Low-Code, foi possível construir a interface, banco de dados, autenticação, regras de acesso e workflows dentro de um único ambiente.
>
> Isso reduziu significativamente a necessidade de desenvolver infraestrutura e código de baixo nível, permitindo concentrar o esforço na solução do problema e nas regras de negócio.
>
> Além disso, a possibilidade de visualizar e alterar rapidamente os componentes tornou o ciclo de desenvolvimento mais rápido e facilitou a evolução da aplicação.”

**Visual:**

* Mostrar rapidamente editor visual.
* Mostrar Data Types.
* Mostrar Workflow.
* Voltar para a aplicação funcionando.

---

## 7. Encerramento | 3:50–4:00

**Narração:**

> “O resultado é uma solução funcional para centralizar o gerenciamento de projetos e tarefas, com controle de acesso, automações, notificações e histórico.
>
> O Ozzy Task Manager demonstra como uma abordagem No-Code/Low-Code pode transformar um problema operacional em uma aplicação funcional de forma rápida, estruturada e evolutiva.”

**Visual:**

* Dashboard ou tela principal.
* Logo/nome do projeto.
* Encerramento.

---

# Ordem sugerida da gravação

```text
Problema
   ↓
Dashboard
   ↓
Projects
   ↓
Project
   ↓
Task
   ↓
Comentários / Notifications
   ↓
Activity Log
   ↓
Modelo de Dados
   ↓
Workflow
   ↓
Privacy Rules
   ↓
Publicação
   ↓
No-Code / Low-Code
   ↓
Conclusão
```

**Tempo-alvo:** aproximadamente **4 minutos**, mantendo a demonstração da aplicação como elemento central do vídeo e evitando aprofundar detalhes técnicos que não sejam necessários para compreender a solução.
