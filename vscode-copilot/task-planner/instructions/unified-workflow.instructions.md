# Fluxo de Trabalho do Sistema Unificado: Memory Bank + Task Planner

Este documento descreve o fluxo de trabalho operacional completo para o sistema unificado Memory Bank + Task Planner, abrangendo o gerenciamento de sessões do agente de IA, operações de tarefas e padrões de aprendizado contínuo.

## Visão Geral do Sistema

```mermaid
graph TD
    subgraph "Ciclo de Vida da Sessão do Agente de IA"
        Start[Nova Sessão de IA] --> MB_Init[Inicialização do Memory Bank]
        MB_Init --> TM_Init[Integração do Task Planner]
        TM_Init --> Ready[Pronto para Operações]
        Ready --> Operations[Executar Operações]
        Operations --> Learn[Aprender e Atualizar]
        Learn --> End[Fim da Sessão]
    end
    
    subgraph "Núcleo do Memory Bank"
        MB_Files[Arquivos do Memory Bank]
        MB_Context[Contexto Ativo]
        MB_Intelligence[Inteligência do Projeto]
    end
    
    subgraph "Núcleo do Task Planner"
        TM_Active[Tarefas Ativas]
        TM_Plans[Planos Atuais]
        TM_Archive[Arquivo Histórico]
    end
    
    MB_Init --> MB_Files
    TM_Init --> TM_Active
    Learn --> MB_Intelligence
```

## Fase 1: Inicialização de Sessão

### 1.1 Protocolo de Auto-Detecção (PRIMEIRO PASSO OBRIGATÓRIO)

```mermaid
flowchart TD
    Session[Nova Sessão de IA] --> ConfigExists{ai/.system-config existe?}
    
    ConfigExists -->|Sim| ReadConfig[Ler Configuração]
    ConfigExists -->|Não| FirstTime[Configuração de Primeira Vez]
    
    ReadConfig --> ValidConfig{Configuração Válida?}
    ValidConfig -->|Sim| ApplyMode[Aplicar Modo Salvo]
    ValidConfig -->|Não| ReDetect[Executar Detecção Novamente]
    
    FirstTime --> AutoDetect[Auto-detectar do Plano]
    ReDetect --> AutoDetect
    
    AutoDetect --> ReadPlan[Ler .github/ai/plans/PLAN.md]
    ReadPlan --> Analyze[Analisar Conteúdo do Plano]
    Analyze --> Decision{Memory Bank Necessário?}
    
    Decision -->|Sim| EnableMB[Ativar Modo Memory Bank]
    Decision -->|Não| TaskOnly[Modo Apenas Task Planner]
    
    EnableMB --> SaveConfig[Salvar em .github/ai/.system-config]
    TaskOnly --> SaveConfig
    SaveConfig --> ApplyMode
    
    ApplyMode --> InitializeSystem[Inicializar Sistema Selecionado]
```

### 1.2 Inicialização do Memory Bank (Quando Ativado)

```mermaid
flowchart TD
    Session[Nova Sessão de IA] --> Check[Verificar Arquivos do Memory Bank]
    Check --> Exists{Todos os Arquivos Existem?}
    
    Exists -->|Sim| ReadAll[Ler TODOS os Arquivos do Memory Bank]
    Exists -->|Não| Create[Criar Arquivos Faltantes]
    
    Create --> Template[Usar Estrutura de Template]
    Template --> Populate[Preencher com Contexto Atual]
    Populate --> ReadAll
    
    ReadAll --> Hierarchy[Aplicar Hierarquia de Arquivos]
    Hierarchy --> Context[Estabelecer Contexto Completo]
    Context --> Ready[Memory Bank Pronto]
```

**Ações Obrigatórias:**
1. **Ler `memory-bank/projectbrief.md`** - Entendimento básico
2. **Ler `memory-bank/productContext.md`** - Objetivos e problemas do produto
3. **Ler `memory-bank/systemPatterns.md`** - Arquitetura e padrões
4. **Ler `memory-bank/techContext.md`** - Ambiente técnico
5. **Ler `memory-bank/activeContext.md`** - Foco atual de trabalho
6. **Ler `memory-bank/progress.md`** - Status atual e progresso

### 1.3 Integração do Task Planner (Sempre Ativo)

```mermaid
flowchart TD
    MB_Ready[Memory Bank Pronto] --> TM_Check[Verificar Estado do Task Planner]
    TM_Check --> ActiveTasks[Revisar .github/ai/TASKS.md]
    ActiveTasks --> History[Verificar arquivos .github/ai/memory/]
    History --> Plans[Revisar .github/ai/plans/]
    Plans --> Sync[Sincronizar Entendimento]
    Sync --> Unified[Contexto Unificado Estabelecido]
```

## Fase 2: Modos de Operação

### 2.1 Fluxo do Modo de Planejamento

```mermaid
flowchart TD
    PlanMode[Modo Planejamento Acionado] --> ReadContext[Ler Contexto do Memory Bank]
    ReadContext --> CheckFiles{Arquivos Completos?}
    
    CheckFiles -->|Não| CreatePlan[Criar Contexto Ausente]
    CreatePlan --> DocumentPlan[Documentar Plano no Chat]
    
    CheckFiles -->|Sim| VerifyContext[Verificar Contexto Atual]
    VerifyContext --> Strategy[Desenvolver Estratégia]
    Strategy --> Present[Apresentar Abordagem ao Usuário]
    
    Present --> Approval{Aprovação do Usuário?}
    Approval -->|Não| Revise[Revisar Plano]
    Revise --> Strategy
    Approval -->|Sim| ActMode[Mudar para Modo de Ação]
```

### 2.2 Fluxo do Modo de Ação

```mermaid
flowchart TD
    ActMode[Modo de Ação Acionado] --> CheckContext[Verificar Memory Bank]
    CheckContext --> Execute[Executar Tarefa]
    
    Execute --> TaskType{Tipo de Tarefa?}
    
    TaskType -->|Atualização de Memória| MB_Update[Atualizar Memory Bank]
    TaskType -->|Criação de Tarefa| TM_Create[Criar Tarefa no Task Planner]
    TaskType -->|Execução de Tarefa| TM_Execute[Executar Tarefa do Task Planner]
    TaskType -->|Integração| Both[Atualizar Ambos Sistemas]
    
    MB_Update --> Sync1[Sincronizar com Task Planner]
    TM_Create --> Sync2[Sincronizar com Memory Bank]
    TM_Execute --> Sync3[Atualizar Progresso no Memory Bank]
    Both --> Sync4[Sincronização Completa do Sistema]
    
    Sync1 --> Document[Documentar Alterações]
    Sync2 --> Document
    Sync3 --> Document
    Sync4 --> Document
    
    Document --> Learn[Aprender com a Experiência]
```

## Fase 3: Operações do Task Planner

### 3.1 Criação e Gerenciamento de Tarefas

```mermaid
flowchart TD
    TaskReq[Requisição de Tarefa] --> PlanTasks[Planejar Todas as Tarefas]
    PlanTasks --> Expansion{Tarefas Complexas?}
    
    Expansion -->|Sim| SubTasks[Definir Sub-tarefas]
    Expansion -->|Não| UpdateMaster[Atualizar .github/ai/TASKS.md]
    
    SubTasks --> ParentTasks[Atualizar Tarefas Pai]
    ParentTasks --> UpdateMaster
    
    UpdateMaster --> CreateFiles[Criar Arquivos de Tarefas Individuais]
    CreateFiles --> PopulateYAML[Preencher YAML e Markdown]
    PopulateYAML --> SyncMB[Atualizar Memory Bank activeContext.md]
    SyncMB --> Ready[Tarefas Prontas]
```

### 3.2 Fluxo de Execução de Tarefas

```mermaid
flowchart TD
    Execute[Executar Requisição de Tarefa] --> ReadTasks[Ler .github/ai/TASKS.md]
    ReadTasks --> FindTask[Encontrar Primeira Tarefa Pendente]
    FindTask --> CheckDeps{Dependências Atendidas?}
    
    CheckDeps -->|Não| NotifyUser[Notificar Usuário: Dependências Faltantes]
    CheckDeps -->|Sim| UpdateStatus[Atualizar Status da Tarefa: inprogress]
    
    UpdateStatus --> UpdateMaster[Atualizar marcador no TASKS.md]
    UpdateMaster --> ExecuteTask[Executar Tarefa]
    
    ExecuteTask --> Result{Resultado da Tarefa?}
    
    Result -->|Sucesso| Success[Atualizar status: completed]
    Result -->|Falha| Failure[Atualizar status: failed, adicionar error_log]
    
    Success --> UpdateMasterSuccess[Atualizar TASKS.md: completed]
    Failure --> UpdateMasterFailed[Atualizar TASKS.md: failed]
    
    UpdateMasterSuccess --> UpdateProgress[Atualizar Memory Bank progress.md]
    UpdateMasterFailed --> UpdateProgress
    
    UpdateProgress --> Complete[Tarefa Completa]
```

### 3.3 Fluxo de Arquivamento de Tarefas

```mermaid
flowchart TD
    Archive[Requisição de Arquivamento] --> FindCompleted[Encontrar Tarefas Concluídas/Falhas]
    FindCompleted --> MoveFiles[Mover arquivos de tarefas para .github/ai/memory/tasks/]
    MoveFiles --> UpdateLog[Adicionar resumo ao .github/ai/memory/TASKS_LOG.md]
    UpdateLog --> RemoveEntries[Remover entradas de .github/ai/TASKS.md]
    RemoveEntries --> UpdateMB[Atualizar Memory Bank progress.md]
    UpdateMB --> UpdateActive[Atualizar activeContext.md]
    UpdateActive --> ArchiveComplete[Arquivamento Completo]
```

## Fase 4: Fluxos de Atualização do Memory Bank

### 4.1 Gatilhos de Atualização Automática

```mermaid
flowchart TD
    Trigger{Gatilho de Atualização} --> Type{Tipo de Gatilho?}
    
    Type -->|Tarefa Concluída| TaskComplete[Atualizar progress.md]
    Type -->|Novo Padrão| PatternUpdate[Atualizar systemPatterns.md]
    Type -->|Mudança no Foco de Trabalho| FocusUpdate[Atualizar activeContext.md]
    Type -->|Decisão Técnica| TechUpdate[Atualizar techContext.md]
    Type -->|Solicitação Manual| ManualUpdate[Revisar TODOS os arquivos]
    
    TaskComplete --> SyncTM1[Sincronizar com Task Planner]
    PatternUpdate --> SyncTM2[Sincronizar com Task Planner]
    FocusUpdate --> SyncTM3[Sincronizar com Task Planner]
    TechUpdate --> SyncTM4[Sincronizar com Task Planner]
    ManualUpdate --> ReviewAll[Revisar TODOS os Arquivos do Memory Bank]
    
    ReviewAll --> UpdateNeeded{Atualizações Necessárias?}
    UpdateNeeded -->|Sim| UpdateFiles[Atualizar Arquivos Relevantes]
    UpdateNeeded -->|Não| DocumentState[Documentar Estado Atual]
    
    UpdateFiles --> DocumentState
    DocumentState --> SyncTM5[Sincronizar com Task Planner]
    
    SyncTM1 --> Complete[Atualização Concluída]
    SyncTM2 --> Complete
    SyncTM3 --> Complete
    SyncTM4 --> Complete
    SyncTM5 --> Complete
```

### 4.2 Processo de Atualização Manual do Memory Bank

```mermaid
flowchart TD
    Manual["Manual 'atualizar memory bank' Request"] --> ReadAll[OBRIGATÓRIO: Ler TODOS os Arquivos]
    
    ReadAll --> ReviewFiles[Revisar Cada Arquivo]
    ReviewFiles --> ProjectBrief[Revisar projectbrief.md]
    ProjectBrief --> ProductContext[Revisar productContext.md]
    ProductContext --> SystemPatterns[Revisar systemPatterns.md]
    SystemPatterns --> TechContext[Revisar techContext.md]
    TechContext --> ActiveContext[Revisar activeContext.md]
    ActiveContext --> Progress[Revisar progress.md]
    
    Progress --> Identify[Identificar Atualizações Necessárias]
    Identify --> Update[Atualizar Arquivos Relevantes]
    Update --> Consistency[Verificar Consistência]
    Consistency --> Sync[Sincronizar com Task Planner]
    Sync --> Complete[Atualização Completa]
```

## Fase 5: Inteligência e Aprendizado do Projeto

### 5.1 Descoberta e Aprendizado de Padrões

```mermaid
flowchart TD
    Experience[Novo Padrão/Experiência] --> Identify[Identificar Tipo de Padrão]
    Identify --> Validate[Validar com Usuário]
    Validate --> Document[Documentar em .github/instructions]
    Document --> Apply[Aplicar em Trabalhos Futuros]
    
    Identify --> Categories{Categoria do Padrão?}
    Categories -->|Implementação| ImplPattern[Caminho de Implementação]
    Categories -->|Preferência do Usuário| UserPattern[Fluxo de Trabalho do Usuário]
    Categories -->|Técnico| TechPattern[Decisão Técnica]
    Categories -->|Processo| ProcessPattern[Melhoria de Processo]
    
    ImplPattern --> Document
    UserPattern --> Document
    TechPattern --> Document
    ProcessPattern --> Document
```

### 5.2 Ciclo de Melhoria Contínua

```mermaid
flowchart TD
    Start[Início da Sessão] --> ReadRules[Ler .github/instructions]
    ReadRules --> ApplyLearning[Aplicar Padrões Aprendidos]
    ApplyLearning --> Work[Executar Trabalho]
    Work --> Observe[Observar Resultados]
    Observe --> NewInsights{Novos Insights?}
    
    NewInsights -->|Sim| CaptureInsight[Capturar Novo Insight]
    NewInsights -->|Não| SessionEnd[Fim da Sessão]
    
    CaptureInsight --> UpdateRules[Atualizar .github/instructions]
    UpdateRules --> SessionEnd
```

## Fase 6: Tratamento de Erros e Recuperação

### 6.1 Recuperação do Estado do Sistema

```mermaid
flowchart TD
    Error[Erro de Sistema Detectado] --> Assess[Avaliar Danos]
    Assess --> ErrorType{Tipo de Erro?}
    
    ErrorType -->|Memory Bank| MBError[Problema no Memory Bank]
    ErrorType -->|Task Planner| TMError[Problema no Task Planner]
    ErrorType -->|Ambos Sistemas| BothError[Problema em Ambos Sistemas]
    
    MBError --> RecoverFromTM[Recuperar do Task Planner]
    TMError --> RecoverFromMB[Recuperar do Memory Bank]
    BothError --> ManualRecover[Recuperação Manual Necessária]
    
    RecoverFromTM --> Verify[Verificar Recuperação]
    RecoverFromMB --> Verify
    ManualRecover --> UserInput[Solicitar Input do Usuário]
    
    UserInput --> Verify
    Verify --> Complete[Recuperação Completa]
```

### 6.2 Verificações de Consistência de Dados

```mermaid
flowchart TD
    Check[Verificação de Consistência] --> MemoryBank[Verificar Arquivos do Memory Bank]
    MemoryBank --> TaskPlanner[Verificar Estado do Task Planner]
    TaskPlanner --> Compare[Comparar Sistemas]
    Compare --> Conflicts{Conflitos Encontrados?}
    
    Conflicts -->|Sim| Resolve[Resolver Conflitos]
    Conflicts -->|Não| Healthy[Sistema Saudável]
    
    Resolve --> Priority[Aplicar Regras de Prioridade]
    Priority --> Update[Atualizar Sistemas]
    Update --> Verify[Verificar Resolução]
    Verify --> Healthy
```

## Matriz de Responsabilidade do Sistema

### Separação Clara de Responsabilidades

```mermaid
graph TD
    subgraph "Sistema Memory Bank"
        MB_P[Estado e Contexto do Projeto]
        MB_T[Decisões Técnicas]
        MB_PR[Acompanhamento de Progresso]
        MB_A[Foco de Trabalho Ativo]
        
        MB_P --> MB_Files[arquivos memory-bank/]
        MB_T --> MB_Files
        MB_PR --> MB_Files
        MB_A --> MB_Files
    end
    
    subgraph "Sistema Task Planner"
        TM_L[Ciclo de Vida das Tarefas]
        TM_D[Dependências]
        TM_H[Arquivo Histórico]
        
        TM_L --> TM_Files[arquivos .github/ai/]
        TM_D --> TM_Files
        TM_H --> TM_Files
    end
    
    subgraph "Aprendizado do Agente de IA"
        AI_P[Preferências do Usuário]
        AI_B[Padrões de Comportamento]
        AI_W[Melhorias de Fluxo de Trabalho]
        
        AI_P --> Rules_Files[arquivos .github/instructions]
        AI_B --> Rules_Files
        AI_W --> Rules_Files
    end
```

### Regras de Responsabilidade de Atualização

| Sistema | Atualiza | Nunca Atualiza |
|---------|----------|----------------|
| **Memory Bank** | Contexto do projeto, progresso, decisões técnicas | .github/instructions, arquivos de tarefas |
| **Task Planner** | Status de tarefas, dependências, arquivos | Arquivos do Memory Bank, .github/instructions |
| **Agente de IA** | .github/instructions com base na experiência | Conteúdo do Memory Bank, detalhes de tarefas |

### Limites de Fluxo de Dados

```mermaid
flowchart TD
    Experience[Experiência do Agente de IA] --> Learn{Tipo de Aprendizado?}
    
    Learn -->|Contexto do Projeto| MB_Update[Atualizar Memory Bank]
    Learn -->|Progresso de Tarefas| TM_Update[Atualizar Task Planner]
    Learn -->|Padrão de Comportamento| Rules_Update[Atualizar .github/instructions]
    
    MB_Update --> MB_Sync[Sincronizar com Task Planner]
    TM_Update --> TM_Sync[Sincronizar com Memory Bank]
    Rules_Update --> Rules_Apply[Aplicar em Sessões Futuras]
    
    MB_Sync --> Consistent[Manter Consistência]
    TM_Sync --> Consistent
    Rules_Apply --> Improved[Comportamento de IA Aprimorado]
```

## Princípios Operacionais Chave

### 1. Abordagem Memory-First
- **Sempre ler arquivos do Memory Bank primeiro** no início da sessão
- **Memory Bank conduz todas as operações** com o Task Planner fornecendo suporte
- **Preservação de contexto** é crítica para operação eficaz da IA

### 2. Processamento de Comando Unificado
- **Ponto de entrada único** através do sistema Memory Bank
- **Sincronização automática** entre sistemas
- **Estado consistente** mantido em todas as operações

### 3. Aprendizado Contínuo
- **Reconhecimento de padrões** e documentação em .github/instructions
- **Inteligência do projeto** acumulada ao longo do tempo
- **Comportamento adaptativo** baseado em padrões aprendidos

### 4. Garantia de Qualidade
- **Revisões obrigatórias de arquivos** para operações críticas
- **Verificações de consistência** entre sistemas
- **Mecanismos de recuperação de erros** integrados

Este fluxo de trabalho unificado garante uma operação confiável, consistente e inteligente do agente de IA com memória persistente e capacidades de melhoria contínua. 