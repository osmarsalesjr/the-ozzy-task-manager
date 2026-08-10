# UI Design System

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento define o padrão visual do **Ozzy - Task Manager**, estabelecendo diretrizes para identidade visual, componentes, layout e experiência do usuário.

Como o projeto será desenvolvido sem um UI Designer dedicado, este documento servirá como referência para manter consistência visual durante toda a implementação.

---

# 2. Conceito Visual

O **Ozzy - Task Manager** é uma aplicação para gerenciamento de projetos e tarefas. Sua interface deve transmitir:

* Organização
* Clareza
* Simplicidade
* Produtividade
* Confiabilidade

A experiência deve priorizar a leitura das informações e reduzir distrações, utilizando uma identidade visual discreta, moderna e profissional.

---

# 3. Configurações Gerais

## Idioma

Português (Brasil)

---

## Timezone

America/Sao_Paulo (Brasília)

---

## Plataforma

Bubble.io (Plano Gratuito)

---

## Responsividade

A aplicação deverá ser compatível com:

* Desktop (prioridade)
* Tablet
* Smartphone

---

# 4. Identidade Visual

## Estilo

Minimalista

Profissional

Organizado

Moderno

---

## Cores

A aplicação deverá utilizar uma paleta predominantemente neutra, reservando cores de destaque apenas para indicar ações importantes ou estados do sistema.

### Cor Primária

Azul moderado

Utilizada para:

* Botões principais
* Links
* Elementos ativos
* Indicadores

---

### Cor Secundária

Cinza claro

Utilizada para:

* Fundos
* Containers
* Cards
* Menus

---

### Fundo

Branco ou cinza muito claro.

---

### Texto

Cinza escuro.

Evitar texto totalmente preto para melhorar a leitura.

---

### Cores de Estado

Sucesso

* Verde

Aviso

* Amarelo

Erro

* Vermelho

Informação

* Azul

Essas cores deverão aparecer apenas em mensagens, badges e indicadores.

---

# 5. Tipografia

Utilizar fonte sem serifa.

Sugestão:

* Inter
* Open Sans
* Roboto

Hierarquia recomendada:

Título Principal

28 px

---

Título de Página

22 px

---

Subtítulo

18 px

---

Texto

14–16 px

---

Legenda

12 px

---

# 6. Espaçamentos

Utilizar múltiplos de 8 px.

Exemplos:

* 8 px
* 16 px
* 24 px
* 32 px

Evitar espaçamentos arbitrários.

---

# 7. Bordas

Utilizar cantos arredondados.

Sugestão:

8 px

---

# 8. Sombras

Sombras discretas.

Utilizar apenas para destacar:

* Cards
* Modais
* Menus suspensos

Evitar efeitos exagerados.

---

# 9. Animações

Utilizar apenas transições suaves.

Exemplos:

* Hover em botões
* Hover em cards
* Abertura de modais
* Menu lateral

Tempo sugerido:

150–250 ms

Evitar animações longas.

---

# 10. Componentes

## Botões

Primário

* Fundo azul
* Texto branco

Secundário

* Fundo branco
* Borda cinza

Perigo

* Fundo vermelho

---

## Inputs

Todos os campos deverão possuir:

* Label
* Placeholder
* Mensagem de erro
* Estado desabilitado

---

## Cards

Todos os cards deverão possuir:

* Fundo branco
* Cantos arredondados
* Sombra discreta
* Padding interno consistente

---

## Badges

Utilizados para:

* Status
* Prioridade
* Perfil

Exemplo:

To Do

Cinza

In Progress

Azul

Blocked

Vermelho

Done

Verde

---

## Modais

Utilizados para:

* Exclusão
* Arquivamento
* Confirmações

---

# 11. Template do Dashboard

O Dashboard será a página inicial da aplicação após o login do usuário.

Seu objetivo é fornecer uma visão consolidada dos projetos, tarefas e atividades recentes.

## Estrutura Geral

```text
+---------------------------------------------------------------+
| Header                                                        |
| Logo | Pesquisa (futuro) | Notificações | Perfil              |
+----------------------+----------------------------------------+
| Sidebar              | Dashboard                             |
|                      |                                        |
| • Dashboard          | Indicadores                           |
| • Projetos           |----------------------------------------|
| • Notificações       | Meus Projetos                         |
| • Perfil             |----------------------------------------|
|                      | Minhas Tarefas Pendentes              |
|                      |----------------------------------------|
|                      | Atividades Recentes                   |
+----------------------+----------------------------------------+
```

---

# 12. Dashboard

## Indicadores

Na parte superior deverão ser exibidos quatro cards com informações resumidas:

* Projetos ativos
* Tarefas pendentes
* Tarefas concluídas
* Notificações não lidas

Esses indicadores devem ser atualizados automaticamente a partir dos dados do usuário autenticado.

---

## Seção "Meus Projetos"

Esta será a principal área do Dashboard.

Deverá exibir apenas os projetos cujo **owner** seja o usuário autenticado.

Cada projeto será apresentado em um card contendo:

* Nome do projeto
* Descrição resumida
* Status
* Quantidade total de tarefas
* Quantidade de tarefas concluídas
* Barra de progresso baseada na conclusão das tarefas

Ao clicar no card, o usuário será direcionado para a página de detalhes do projeto.

Caso o usuário não possua projetos cadastrados, deverá ser exibido um estado vazio com uma mensagem convidando-o a criar seu primeiro projeto.

---

## Seção "Minhas Tarefas Pendentes"

Exibir uma lista das tarefas atribuídas ao usuário autenticado que ainda não foram concluídas.

Cada item deverá apresentar:

* Título
* Projeto
* Prioridade
* Status
* Data limite

As tarefas deverão ser ordenadas pela data de vencimento mais próxima.

---

## Seção "Atividades Recentes"

Apresentar as últimas ações registradas no **ActivityLog** relacionadas aos projetos e tarefas do usuário.

Cada registro deverá exibir:

* Usuário responsável
* Ação realizada
* Tarefa relacionada
* Data e hora

Esta seção facilita o acompanhamento das alterações recentes na aplicação.

---

# 13. Navegação

A navegação principal será realizada por meio de uma barra lateral fixa.

Itens do menu:

* Dashboard
* Projetos
* Notificações
* Perfil

O item correspondente à página atual deverá permanecer destacado.

---

# 14. Estados Vazios

Sempre que uma lista não possuir registros, deverá ser exibida uma mensagem amigável acompanhada de uma ilustração simples ou ícone.

Exemplos:

**Projetos**

"Você ainda não possui projetos. Crie seu primeiro projeto para começar."

**Tarefas**

"Nenhuma tarefa pendente no momento."

**Notificações**

"Você não possui notificações."

---

# 15. Princípios de Experiência do Usuário

Durante o desenvolvimento deverão ser observadas as seguintes diretrizes:

* Priorizar a simplicidade da interface.
* Evitar excesso de informações na mesma tela.
* Destacar apenas ações importantes.
* Utilizar componentes reutilizáveis em toda a aplicação.
* Manter consistência visual entre páginas.
* Reduzir a quantidade de cliques necessários para executar tarefas frequentes.
* Exibir feedback visual após operações de criação, edição ou exclusão.
* Garantir boa legibilidade em diferentes tamanhos de tela.

---

# 16. Considerações Finais

O UI Design System do **Ozzy - Task Manager** estabelece uma base visual consistente para toda a aplicação.

A adoção dessas diretrizes permitirá desenvolver uma interface organizada, moderna e intuitiva, alinhada ao propósito da ferramenta: facilitar o gerenciamento de projetos e tarefas sem adicionar complexidade desnecessária ao fluxo de trabalho do usuário.
    