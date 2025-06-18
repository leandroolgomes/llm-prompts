---
description: This rule specifies the technical details for creating Product Requirements Documents (PRDs), also known as plans, in the project's file-based planning system.
---
# Regra de Geração de PRD

Sempre que você usar esta regra, inicie sua mensagem com o seguinte:

"Verificando planejador do Task Planner..."

Esta regra especifica os detalhes técnicos para criar Documentos de Requisitos do Produto (PRDs) no sistema de planejamento baseado em arquivos do projeto.

Sua tarefa é criar um documento abrangente de requisitos do produto (PRD) para o projeto ou recurso solicitado pelo usuário.

## Conceitos Principais

1.  **Pasta de Planejamento:** O diretório `ai/plans/` contém todos os arquivos PRD.
2.  **Plano Global (`PLAN.MD`):** Um único arquivo obrigatório `PLAN.MD` deve existir diretamente dentro de `ai/plans/`. Seu papel principal é servir como uma **visão geral concisa de alto nível do projeto global e um índice para PRDs específicos de recursos detalhados**. Ele deve definir a visão e os objetivos principais do projeto, mas **não deve se tornar um PRD extenso por si só**. Ele fornece contexto essencial vinculando-se a planos de recursos abrangentes.
3.  **Planos de Recursos:** Os recursos específicos **devem** ter seus PRDs detalhados localizados dentro do subdiretório `ai/plans/features/` (por exemplo, `features/{recurso}-plan.md`). Esses documentos contêm o planejamento abrangente, requisitos, histórias de usuários e considerações técnicas para recursos individuais.
4.  **Propósito:** Os PRDs servem como especificação detalhada para recursos específicos (`features/{recurso}-plan.md`). O `PLAN.MD` global apoia isso fornecendo o resumo geral do projeto e atuando como um hub central que **vincula-se a esses PRDs detalhados de recursos**. A divisão de tarefas (usando o sistema `ai-tasks`) é baseada no conteúdo detalhado dentro dos planos de recursos.
5.  **Ciclo de Vida do Plano:** Planos ativos residem em `ai/plans/`. Planos concluídos, obsoletos ou substituídos podem ser arquivados em `ai/memory/plans/` para referência histórica, conforme detalhado na regra `task-planner/memory`.

## Estrutura de Diretório

```
ai/
  plans/          # Diretório pai para todos os PRDs
    PLAN.md       # Obrigatório: PRD global do projeto
    features/     # Diretório para PRDs específicos de recursos
      {feature}-plan.md # Exemplo de PRD de recurso
  tasks/          # (Para referência - Tarefas são geradas com base nos PRDs)
  memory/         # (Para referência - Arquivo de tarefas)
  TASKS.md        # (Para referência - Checklist principal de tarefas)
```

**Nota:** Antes de criar diretórios como `ai/plans/` ou `ai/plans/features/`, o agente deve primeiro verificar se eles existem usando `list_dir` no diretório pai ou `file_search` para o caminho específico do diretório. Se um diretório não existir, ele pode ser criado implicitamente ao usar `edit_file` para colocar um arquivo dentro desse caminho, já que `edit_file` criará os diretórios pai necessários. O agente também deve garantir que `PLAN.md` exista (verificando com `file_search` e criando com `edit_file`, se necessário, com uma estrutura básica) antes de gerar planos de recursos.

## Formato de Arquivo PRD

PRDs são arquivos Markdown (`.md`) seguindo um modelo estruturado.

**Convenção de Nome de Arquivo:**

-   **Global:** `PLAN.md` (Obrigatório).
-   **Recurso:** `{recurso}-plan.md`, onde `{recurso}` é um nome curto e descritivo em formato kebab-case para o recurso (por exemplo, `autenticacao-usuario-plan.md`).

**Modelo de PRD (Markdown):**

Os agentes devem gerar PRDs seguindo esta estrutura, preenchendo os detalhes com base nas solicitações do usuário e no contexto. Use maiúsculas apenas na primeira letra dos títulos, a menos que especificado de outra forma.

```markdown
# PRD: {Título do Projeto/Recurso}

## 1. Visão geral do produto

### 1.1 Título do documento e versão

-   PRD: {Título do Projeto/Recurso}
-   Versão: 1.0

### 1.2 Resumo do produto

(2-3 parágrafos curtos fornecendo uma visão geral do projeto ou recurso.)

## 2. Objetivos

### 2.1 Objetivos de negócio

-   (Lista com marcadores dos objetivos de negócio)

### 2.2 Objetivos do usuário

-   (Lista com marcadores do que os usuários pretendem alcançar)

### 2.3 Não-objetivos

-   (Lista com marcadores de itens explicitamente fora do escopo)

## 3. Personas de usuário

### 3.1 Tipos principais de usuários

-   (Lista com marcadores das categorias principais de usuários)

### 3.2 Detalhes básicos da persona

-   **{Nome da Persona 1}**: {Breve descrição}
-   **{Nome da Persona 2}**: {Breve descrição}

### 3.3 Acesso baseado em papéis

-   **{Nome do Papel 1}**: {Descrição de permissões/acesso}
-   **{Nome do Papel 2}**: {Descrição de permissões/acesso}

## 4. Requisitos funcionais

-   **{Nome do Recurso 1}** (Prioridade: {Alta/Média/Baixa})
    -   {Requisito 1.1}
    -   {Requisito 1.2}
-   **{Nome do Recurso 2}** (Prioridade: {Alta/Média/Baixa})
    -   {Requisito 2.1}

## 5. Experiência do usuário

### 5.1 Pontos de entrada e fluxo de primeiro uso

-   (Como os usuários acessam este recurso/produto inicialmente)

### 5.2 Experiência principal

-   **{Etapa 1}**: {Explicação da etapa}
    -   {Detalhes para torná-la uma boa experiência}
-   **{Etapa 2}**: {Explicação da etapa}
    -   {Detalhes para torná-la uma boa experiência}

### 5.3 Recursos avançados e casos extremos

-   (Lista com marcadores de cenários menos comuns ou capacidades avançadas)

### 5.4 Destaques de UI/UX

-   (Princípios de design principais ou elementos de interface do usuário)

## 6. Narrativa

(Um único parágrafo descrevendo a jornada do usuário e o benefício que ele recebe.)

## 7. Métricas de sucesso

### 7.1 Métricas centradas no usuário

-   (por exemplo, Taxa de conclusão de tarefas, satisfação do usuário)

### 7.2 Métricas de negócios

-   (por exemplo, Taxa de conversão, impacto na receita)

### 7.3 Métricas técnicas

-   (por exemplo, Tempo de carregamento da página, taxa de erro)

## 8. Considerações técnicas

### 8.1 Pontos de integração

-   (Interação com outros sistemas/serviços)

### 8.2 Armazenamento de dados e privacidade

-   (Como os dados são tratados, conformidade com LGPD/GDPR/CCPA, etc.)

### 8.3 Escalabilidade e desempenho

-   (Carga prevista, metas de desempenho)

### 8.4 Desafios potenciais

-   (Riscos ou obstáculos técnicos)

## 9. Marcos e sequenciamento

### 9.1 Estimativa do projeto

-   {Pequeno/Médio/Grande}: {Estimativa aproximada de tempo, ex: 2-4 semanas}

### 9.2 Tamanho e composição da equipe

-   {ex: Equipe Pequena: 1-2 pessoas (1 PM, 1 Eng)}

### 9.3 Fases sugeridas

-   **{Fase 1}**: {Descrição} ({Estimativa de tempo})
    -   Entregas principais: {Lista}
-   **{Fase 2}**: {Descrição} ({Estimativa de tempo})
    -   Entregas principais: {Lista}

## 10. Histórias de usuário

(Gerar uma subseção para cada história de usuário)

### 10.1 {Título da História de Usuário 1}

-   **ID**: US-001
-   **Descrição**: Como {persona}, eu quero {ação} para que {benefício}.
-   **Critérios de Aceitação**:
    -   {Critério 1.1}
    -   {Critério 1.2}

### 10.2 {Título da História de Usuário 2}

-   **ID**: US-002
-   **Descrição**: Como {persona}, eu quero {ação} para que {benefício}.
-   **Critérios de Aceitação**:
    -   {Critério 2.1}
    -   {Critério 2.2}

```

## Responsabilidades do Agente

1.  **Garantir que o Plano Global Existe:** Antes de criar planos de recursos, verificar se `ai/plans/PLAN.MD` existe. Se não existir, informar ao usuário e oferecer a criação de uma estrutura básica para ele, enfatizando seu papel como um **resumo conciso do projeto e um índice para planos detalhados de recursos**, não um PRD abrangente por si só.
2.  **Determinar o Escopo:** Esclarecer se a solicitação é para atualizar o `PLAN.MD` global (o que geralmente envolve refinar a visão geral do projeto, atualizar objetivos principais ou adicionar/modificar links para PRDs de recursos) ou para criar/atualizar um **plano detalhado específico de recurso** em `ai/plans/features/{recurso}-plan.md`. Evitar adicionar detalhes extensos de recursos diretamente em `PLAN.MD`.
3.  **Nome de Arquivo:** Usar a convenção correta de nome de arquivo. Criar diretórios se não existirem.
4.  **Usar o Modelo:** Gerar o conteúdo do PRD seguindo rigorosamente a estrutura do modelo Markdown fornecido acima.
5.  **Preencher Conteúdo:** Preencher as seções com base na solicitação do usuário, contexto do projeto (especialmente `PLAN.md`), e melhores práticas para a escrita de PRD.
6.  **Completude:** Garantir que todas as histórias de usuário necessárias (principal, alternativa, casos extremos, segurança) sejam incluídas com critérios de aceitação claros.
7.  **Foco:** O papel do agente é *apenas* gerar ou atualizar arquivos Markdown de PRD no diretório de planejamento ativo (`ai/plans/`). Isso significa criar/editar os arquivos de alto nível `PLAN.MD` ou `features/{recurso}-plan.md` detalhados. A criação de tarefas é um processo separado tratado pela interpretação dos PRDs detalhados de recursos usando a regra `ai-tasks`. O arquivamento de planos é tratado pela regra `task-planner/memory`.
