# Checklist de Publicação (Deployment Checklist)

# Ozzy - Task Manager

**Versão:** 1.0
**Plataforma:** Bubble.io (Plano Gratuito)

---

# 1. Objetivo

Este documento estabelece o checklist oficial de publicação do **Ozzy - Task Manager**.

Seu objetivo é garantir que todas as configurações, funcionalidades, regras de negócio, testes e documentações estejam concluídos antes da entrega do MVP.

Este checklist deverá ser executado antes da publicação da aplicação.

---

# 2. Preparação do Ambiente

## Projeto Bubble

* [ ] Projeto criado.
* [ ] Nome da aplicação configurado.
* [ ] Ícone (favicon) configurado.
* [ ] Idioma definido.
* [ ] Timezone configurado corretamente.

---

## Banco de Dados

Verificar:

* [ ] Todos os Data Types criados.
* [ ] Todos os campos configurados.
* [ ] Todos os relacionamentos criados.
* [ ] Tipos dos campos corretos.
* [ ] Campos obrigatórios revisados.

---

## Option Sets

Confirmar a existência de:

* [ ] UserRole
* [ ] ProjectStatus
* [ ] TaskStatus
* [ ] TaskPriority
* [ ] NotificationType
* [ ] ActivityAction

---

# 3. Segurança

## Privacy Rules

Verificar:

* [ ] Usuários autenticados acessam apenas páginas privadas.
* [ ] Usuários editam apenas seus próprios dados.
* [ ] Projetos respeitam as permissões definidas.
* [ ] Tarefas respeitam as permissões definidas.
* [ ] Comentários respeitam as permissões definidas.
* [ ] Notificações são visíveis apenas ao destinatário.
* [ ] ActivityLog segue as regras de acesso definidas.

---

## Autenticação

Confirmar:

* [ ] Cadastro funcionando.
* [ ] Login funcionando.
* [ ] Logout funcionando.
* [ ] Recuperação de senha funcionando.
* [ ] Sessões encerradas corretamente.

---

# 4. Interface

## Páginas

Confirmar existência de:

* [ ] login
* [ ] signup
* [ ] dashboard
* [ ] projects
* [ ] project_details
* [ ] my_tasks
* [ ] task_details
* [ ] notifications
* [ ] profile

---

## Componentes Reutilizáveis

Verificar:

* [ ] re_header
* [ ] re_sidebar
* [ ] re_project_card
* [ ] re_task_card
* [ ] re_comment_card
* [ ] re_notification_card
* [ ] re_activity_card
* [ ] re_dashboard_widget
* [ ] re_confirmation_modal
* [ ] re_empty_state

---

## Estilos

Verificar:

* [ ] Tipografia padronizada.
* [ ] Botões consistentes.
* [ ] Inputs padronizados.
* [ ] Cards reutilizando Styles.
* [ ] Cores consistentes.

---

# 5. Funcionalidades

## Projetos

Verificar:

* [ ] Criar projeto.
* [ ] Editar projeto.
* [ ] Arquivar projeto.

---

## Tarefas

Verificar:

* [ ] Criar tarefa.
* [ ] Editar tarefa.
* [ ] Excluir tarefa.
* [ ] Alterar status.
* [ ] Alterar responsável.
* [ ] Definir prioridade.
* [ ] Definir data limite.

---

## Comentários

Verificar:

* [ ] Criar comentário.
* [ ] Editar comentário.
* [ ] Excluir comentário.

---

## Notificações

Verificar:

* [ ] Criadas automaticamente.
* [ ] Marcação como lida.
* [ ] Exibição correta ao destinatário.

---

## Histórico

Verificar:

* [ ] ActivityLog criado automaticamente.
* [ ] Ações registradas corretamente.
* [ ] Histórico exibido na tarefa.

---

## Perfil

Verificar:

* [ ] Atualização do nome.
* [ ] Atualização do avatar.

---

## Dashboard

Confirmar:

* [ ] Indicadores corretos.
* [ ] Projetos carregados.
* [ ] Tarefas carregadas.
* [ ] Atividades recentes carregadas.

---

# 6. Workflows

Verificar:

## Authentication

* [ ] Login
* [ ] Logout
* [ ] Sign Up
* [ ] Forgot Password

---

## Projects

* [ ] Create Project
* [ ] Update Project
* [ ] Archive Project

---

## Tasks

* [ ] Create Task
* [ ] Update Task
* [ ] Delete Task
* [ ] Change Status
* [ ] Change Assignee

---

## Comments

* [ ] Add Comment
* [ ] Edit Comment
* [ ] Delete Comment

---

## Notifications

* [ ] Create Notification
* [ ] Mark Notification Read

---

## Activity Log

* [ ] Register Activity

---

## User

* [ ] Update Profile

---

# 7. Validação dos Dados

Executar verificações para confirmar que:

* [ ] Toda tarefa pertence a um projeto.
* [ ] Todo projeto possui proprietário.
* [ ] Toda tarefa possui responsável.
* [ ] Toda notificação possui destinatário.
* [ ] Todo comentário pertence a uma tarefa.
* [ ] Todo ActivityLog referencia uma tarefa e um usuário.

---

# 8. Responsividade

## Desktop

* [ ] Layout correto.
* [ ] Navegação funcional.

---

## Tablet

* [ ] Sidebar adaptada.
* [ ] Componentes reorganizados.

---

## Mobile

* [ ] Menu responsivo.
* [ ] Cards reorganizados.
* [ ] Formulários utilizáveis.
* [ ] Botões acessíveis.

---

# 9. Performance

Validar:

* [ ] Tempo de login adequado.
* [ ] Dashboard carregando corretamente.
* [ ] Listas de tarefas responsivas.
* [ ] Navegação fluida.
* [ ] Nenhum Workflow executando operações desnecessárias.

---

# 10. Qualidade da Interface

Verificar:

* [ ] Mensagens de sucesso.
* [ ] Mensagens de erro.
* [ ] Estados vazios.
* [ ] Consistência visual.
* [ ] Alinhamento dos componentes.
* [ ] Espaçamentos.
* [ ] Ícones.
* [ ] Cores.
* [ ] Tipografia.

---

# 11. Documentação

Confirmar atualização dos seguintes artefatos:

* [ ] Planning
* [ ] Data Model
* [ ] Solution Architecture
* [ ] Development Guide
* [ ] Workflow Specification
* [ ] Screen Functional Specification
* [ ] Test Plan
* [ ] README

---

# 12. Publicação

Antes da publicação:

* [ ] Todos os testes aprovados.
* [ ] Nenhum erro crítico identificado.
* [ ] Todas as páginas funcionando.
* [ ] Todos os Workflows funcionando.
* [ ] Todos os Data Types revisados.
* [ ] Privacy Rules revisadas.
* [ ] Navegação validada.
* [ ] Responsividade validada.
* [ ] Documentação atualizada.

---

# 13. Critérios para Aprovação do MVP

O MVP será considerado pronto para publicação quando:

* Todos os requisitos funcionais estiverem implementados.
* Todos os testes do Plano de Testes forem aprovados.
* Não existirem defeitos críticos ou bloqueadores.
* Todos os Workflows estiverem funcionando conforme especificado.
* A documentação estiver completa e atualizada.
* A aplicação estiver operacional no ambiente do Bubble.io.

---

# 14. Registro da Publicação

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

# 15. Lições Aprendidas

Após a publicação, registrar:

## Pontos Positivos

* ---

* ---

* ---

---

## Melhorias Identificadas

* ---

* ---

* ---

---

## Funcionalidades Planejadas para Próximas Versões

* ---

* ---

* ---

---

# 16. Considerações Finais

Este Checklist de Publicação representa a última etapa da fase de planejamento do **Ozzy - Task Manager**.

Sua utilização garante que a aplicação seja entregue de forma organizada, consistente e aderente aos padrões definidos ao longo do projeto, reduzindo riscos durante a publicação e facilitando futuras manutenções e evoluções da solução.
