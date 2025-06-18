---
description: Esta regra explica como o agente deve verificar se uma determinada tarefa precisa ser expandida em subtarefas.
---
# Expandindo Tarefas Grandes

Sempre que usar esta regra, inicie sua mensagem com o seguinte:

"Verificando se a tarefa precisa ser expandida..."

Esta regra fornece diretrizes para um agente de IA avaliar se uma tarefa definida no sistema Task Planner é muito complexa ou grande e deve ser recomendada para expansão em subtarefas menores e mais gerenciáveis.

## 1. Quando Avaliar a Complexidade da Tarefa para Expansão

A complexidade da tarefa deve ser avaliada:

*   **Durante a Criação da Tarefa:** Quando uma nova tarefa está sendo definida com base em um PRD ou solicitação do usuário.
*   **Antes de Iniciar uma Tarefa:** Quando um agente está prestes a pegar uma tarefa `pending` (pendente).
*   **Se uma Tarefa Estagna:** Se uma tarefa `inprogress` (em andamento) mostra pouco progresso durante um período significativo.

## 2. Critérios para Identificar Tarefas que Precisam de Expansão

Uma tarefa pode ser candidata à expansão se atender a vários dos seguintes critérios:

*   **Esforço Estimado:** A tarefa parece provável que leve mais do que um limite predefinido (por exemplo, 2-3 dias ideais de desenvolvedor) para ser concluída.
*   **Múltiplos Componentes Distintos:** A tarefa envolve mudanças em vários módulos, serviços ou áreas de UI não relacionados.
*   **Alta Incerteza/Ambiguidade:** Os requisitos não estão totalmente claros, ou há muitos desafios técnicos desconhecidos.
*   **Múltiplos Resultados Lógicos:** A tarefa tem vários resultados distintos e independentemente verificáveis.
*   **Numerosos Critérios de Aceitação:** As seções "Detalhes" ou "Estratégia de Teste" são excepcionalmente longas e abrangem muitos aspectos diferentes.
*   **Bloqueia Múltiplas Outras Tarefas:** É um grande pré-requisito para um número significativo de tarefas subsequentes.

## 3. Recomendação para Expansão

Se uma tarefa for considerada muito complexa para execução direta com base nos critérios acima, o agente deve:

1.  **Identificar Submetas:** Mentalmente dividir o objetivo original da tarefa em submetas menores, lógicas e sequenciais (ou paralelizáveis).
2.  **Recomendar Subtarefas:** Propor uma lista de subtarefas ao usuário ou ao processo de chamada. Para cada subtarefa proposta, sugerir:
    *   Um título descritivo.
    *   Uma breve descrição do seu objetivo.
    *   Possíveis dependências de outras subtarefas propostas ou da tarefa pai original.
    *   Uma prioridade sugerida.
3.  **Declarar a Recomendação Claramente:** A saída do agente deve ser uma recomendação clara de que a tarefa original seja expandida, seguida pela lista de subtarefas sugeridas. Por exemplo:
    "Com base na complexidade, recomendo expandir a Tarefa {original_task_id} '{Título da Tarefa Original}' nas seguintes subtarefas:
    1.  **Título:** Configurar Esquema de Banco de Dados para Perfis de Usuário
        *   **Descrição:** Criar e migrar as tabelas de banco de dados necessárias para armazenar informações de perfil de usuário.
        *   **Prioridade:** crítica
        *   **Dependências:** Nenhuma
    2.  **Título:** Implementar Endpoints da API de Perfil de Usuário
        *   **Descrição:** Desenvolver os endpoints da API CRUD para gerenciar perfis de usuário.
        *   **Prioridade:** alta
        *   **Dependências:** Subtarefa 1
    3.  **Título:** Construir a Visualização Frontend do Perfil do Usuário
        *   **Descrição:** Criar os componentes de UI para exibir e editar perfis de usuário.
        *   **Prioridade:** alta
        *   **Dependências:** Subtarefa 2"

**A criação efetiva de arquivos de subtarefas, numeração e atualizações no `TASKS.md` será tratada pelo processo que recebe esta recomendação, tipicamente orientado pela regra `task-planner/tasks.instructions.md`.**

Ao se concentrar na análise e recomendação, esta regra fornece um ponto de decisão claro antes de prosseguir com os mecanismos de divisão de tarefas.
