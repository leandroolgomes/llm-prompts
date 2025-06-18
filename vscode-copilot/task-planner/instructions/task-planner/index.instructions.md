---
applyTo: '**'
---
# Visão Geral do Sistema Task Planner

Sempre que você usar esta regra, inicie sua mensagem com o seguinte:

"Acessando visão geral do sistema Task Planner..."

O sistema Task Planner é um framework operacional de gerenciamento de projetos baseado em arquivos e agente de IA, projetado para planejar recursos, gerenciar tarefas de desenvolvimento e manter uma memória de trabalhos anteriores. Ele se integra perfeitamente com o sistema Memory Bank para fornecer contexto persistente entre sessões do agente de IA.

O sistema consiste em três componentes principais, cada um governado por seu próprio arquivo de regras detalhado, além da integração com o Memory Bank:

1.  **Planos (`@plans.instructions.md`)**:
    *   **Objetivo**: Define como os Documentos de Requisitos do Produto (PRDs) são criados e estruturados para o projeto geral e recursos específicos.
    *   **Localização**: PRDs são armazenados em `.github/ai/plans/`, com planos específicos de recursos em `.github/ai/plans/features/`.
    *   **Arquivo-chave**: Um `PLAN.md` global é obrigatório em `.github/ai/plans/`.
    *   **Detalhes**: Para criação de planos, revise completamente [task-planner/plans.instructions.md](mdc:.github/instructions/task-planner/plans.instructions.md)

2.  **Tarefas (`@tasks.instructions.md`)**:
    *   **Objetivo**: Governa a criação, gerenciamento e ciclo de vida de tarefas individuais de desenvolvimento.
    *   **Tarefas Ativas**: Todas as tarefas ativas residem em `.github/ai/tasks/` como arquivos `task{id}_name.md`.
    *   **Visão Principal**: Uma lista de verificação principal, `.github/ai/TASKS.md`, espelha o status das tarefas no diretório `.github/ai/tasks/` e deve ser mantida sincronizada.
    *   **Detalhes**: Para criação de tarefas, revise completamente [task-planner/tasks.instructions.md](mdc:.github/instructions/task-planner/tasks.instructions.md)

3.  **Memória (`@memory.instructions.md`)**:
    *   **Objetivo**: Arquiva tarefas concluídas e falhas para fornecer contexto histórico.
    *   **Localização**: Arquivos de tarefas arquivados são armazenados em `.github/ai/memory/tasks/`.
    *   **Arquivo de Registro**: Um registro cronológico de tarefas arquivadas é mantido em `.github/ai/memory/TASKS_LOG.md`.
    *   **Detalhes**: Para armazenamento na memória, revise completamente [task-planner/memory.instructions.md](mdc:.github/instructions/task-planner/memory.instructions.md)

4.  **Integração com Memory Bank (`@memory-bank/index.instructions.md`)**:
    *   **Objetivo**: Fornece contexto persistente entre sessões de agente de IA e integra-se com o Task Planner.
    *   **Localização**: Arquivos do Memory Bank armazenados no diretório `memory-bank/`.
    *   **Integração**: Sincronização perfeita entre contexto persistente e histórico operacional.
    *   **Detalhes**: Para operações do Memory Bank, revise [memory-bank/index.instructions.md](mdc:.github/instructions/memory-bank/index.instructions.md) e seus componentes modulares

Este sistema interconectado permite o desenvolvimento estruturado de projetos com memória persistente, desde o planejamento de alto nível até a execução de tarefas, revisão histórica e aprendizado contínuo entre sessões de agente de IA.
