---
description: Esta regra explica como o agente deve usar o sistema de memória para encontrar o contexto do projeto
---
# Sistema de Memória da IA

Sempre que você usar esta regra, comece sua mensagem com o seguinte:

"Verificando a memória do Task Planner..."

Este projeto utiliza um sistema de memória localizado no diretório `.github/ai/memory/` para armazenar um histórico de trabalhos concluídos, falhos ou substituídos, fornecendo um valioso contexto para o desenvolvimento em andamento. Ele arquiva tanto tarefas quanto planos.

## Estrutura

O sistema de memória consiste em:

### Arquivo de Tarefas

*   **`.github/ai/memory/tasks/`**: Este diretório contém os arquivos Markdown completos (`task{id}_nome.md`) das tarefas que foram arquivadas (status: `completed` ou `failed`). Esses arquivos mantêm os detalhes originais, descrições e estratégias de teste definidas quando a tarefa estava ativa.
*   **`.github/ai/memory/TASKS_LOG.md`**: Este é um arquivo Markdown de apenas anexação que serve como um registro cronológico de quando as tarefas foram arquivadas. Cada entrada resume a tarefa arquivada, incluindo seu ID, Título, Status final, Dependências e a Descrição extraída do arquivo da tarefa no momento do arquivamento.

### Arquivo de Planos

*   **`.github/ai/memory/plans/`**: Este diretório contém os arquivos Markdown completos dos PRDs (tanto versões globais do `PLAN.md` quanto planos de recursos como `{recurso}-plan.md`) que foram arquivados. Os planos podem ser arquivados quando são concluídos (todos os recursos associados são implementados e estáveis), descontinuados (a direção do recurso ou projeto é abandonada) ou substituídos por uma versão mais nova do plano.
*   **`.github/ai/memory/PLANS_LOG.md`**: Este é um arquivo Markdown de apenas anexação que serve como um registro cronológico de quando os planos foram arquivados. Cada entrada deve resumir o plano arquivado, incluindo seu **caminho completo dentro do diretório `.github/ai/memory/plans/`** (ex., `.github/ai/memory/plans/plano-recurso-antigo.md`), uma versão ou carimbo de data, o motivo do arquivamento (ex., Concluído, Descontinuado, Substituído) e uma breve descrição ou título do plano.
    *   **Exemplo de Formato de Entrada de Log para PLANS_LOG.md:**
        ```markdown
        - **Plano Arquivado:** `.github/ai/memory/plans/plano-recurso-antigo.md`
          - **Arquivado Em:** AAAA-MM-DD HH:MM:SS
          - **Motivo:** Descontinuado
          - **Título:** PRD: Recurso Antigo
          - **Arquivo Original (Opcional):** {.github/ai/plans/features/plano-recurso-antigo.md}
        ```

## Gerenciamento de Diretórios e Arquivos

Ao trabalhar com o sistema de memória, o agente deve sempre verificar se os diretórios e arquivos necessários existem antes de tentar operações:

1. **Verificar Diretórios Antes da Criação:** Antes de realizar operações, verifique se diretórios como `.github/ai/memory/tasks/` ou `.github/ai/memory/plans/` existem usando a ferramenta `list_dir` no seu pai (`.github/ai/memory/`) ou usando `file_search` para o caminho específico do diretório. Se um diretório não aparecer nos resultados, ele pode ser implicitamente criado ao usar `edit_file` para escrever um arquivo dentro desse caminho, pois `edit_file` cria os diretórios pai necessários.

2. **Verificar Arquivos Antes das Operações:** Antes de operar em arquivos como `.github/ai/memory/TASKS_LOG.md` ou `.github/ai/memory/PLANS_LOG.md`, o agente deve usar a ferramenta `file_search` com o caminho completo do arquivo para verificar sua existência.

3. **Criação/Modificação Segura de Arquivos:** Se um arquivo como `.github/ai/memory/TASKS_LOG.md` ou `.github/ai/memory/PLANS_LOG.md` não existir (conforme determinado por `file_search`), e precisar ser criado com conteúdo inicial (ex., `"\# Log de Arquivo de Tarefas\\n\\n"` ou `"\# Log de Arquivo de Planos\\n\\n"`), use a ferramenta `edit_file`. Para anexar a um arquivo existente, primeiro use `read_file` para obter seu conteúdo atual, depois anexe os novos dados a este conteúdo e, finalmente, use `edit_file` para escrever o conteúdo combinado de volta.

4. **Arquivamento de Arquivos de Plano:** Ao mover um arquivo de plano (ex., de `.github/ai/plans/features/` para `.github/ai/memory/plans/`), sempre use a ferramenta `run_terminal_cmd` com o comando `mv`. Não use `edit_file` para criar um novo arquivo no destino e `delete_file` para remover o original. Isso garante que o arquivo seja movido atomicamente e preserva seu histórico se o controle de versão for usado. Exemplo: `mv .github/ai/plans/features/meu-recurso-plan.md .github/ai/memory/plans/meu-recurso-plan.md`.

## Propósito e Uso

O sistema de memória serve como o registro histórico do projeto de atividade de desenvolvimento e planejamento gerenciado pelo sistema de tarefas de IA.

**Quando Consultar a Memória:**

*   **Entendendo Implementações e Planos Passados:** Antes de iniciar uma nova tarefa ou planejar um novo recurso, consulte a memória (`TASKS_LOG.md`, `PLANS_LOG.md` e arquivos arquivados relevantes) para entender como recursos similares ou dependentes foram construídos e planejados.
*   **Evitando Redundância:** Verifique se uma tarefa, requisito ou plano similar já foi abordado anteriormente.
*   **Planejamento de Recursos Relacionados:** Revise tarefas e planos anteriores para um recurso para informar o planejamento e a divisão de tarefas de novos recursos relacionados.
*   **Investigando Tarefas com Falha:** Se uma tarefa falhou anteriormente, revisar seu arquivo arquivado (incluindo o `error_log` no YAML) pode fornecer contexto.
*   **Contexto Histórico de Decisões:** Os planos arquivados fornecem um instantâneo dos objetivos, requisitos e direção pretendida do projeto em um determinado momento.

**Como Consultar a Memória:**

1.  **Comece pelos Logs:** Leia `.github/ai/memory/TASKS_LOG.md` e `.github/ai/memory/PLANS_LOG.md` para obter uma visão geral cronológica dos itens arquivados. Identifique tarefas ou planos potencialmente relevantes com base em seus títulos, descrições e motivos de arquivamento.
2.  **Mergulhe nos Arquivos Arquivados:** Se uma entrada de log sugerir que um item é altamente relevante, leia o arquivo arquivado completo de seu respectivo diretório (`.github/ai/memory/tasks/` ou `.github/ai/memory/plans/`) para obter os detalhes completos.

Ao aproveitar este contexto histórico, a IA pode tomar decisões mais informadas, manter a consistência e trabalhar com mais eficiência no projeto.
