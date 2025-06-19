# Exemplos de Prompts para Task Planner

Este documento contém exemplos detalhados de prompts para usar com o sistema Task Planner. Esses prompts são projetados para trabalhar com o GitHub Copilot ou assistentes de IA similares para gerenciar projetos através de uma estrutura baseada em arquivos Markdown.

## Prompts de Inicialização

### Configuração Inicial do Sistema

```
Preciso configurar um sistema de gerenciamento para meu projeto de [descrição do projeto]. 
Por favor, inicialize o Task Planner com uma estrutura básica adequada para o desenvolvimento de [tipo de software/aplicação].
```

### Ativação do Memory Bank

```
Este é um projeto complexo que envolve [descrição de complexidade, como "múltiplos componentes", "integrações com sistemas externos", etc.].
Por favor, configure o Task Planner com Memory Bank ativado para manter o contexto entre nossas sessões de trabalho.
```

## Prompts de Planejamento

### Criar um Plano de Projeto Principal

```
Crie um plano mestre para o projeto [nome do projeto]. 
O objetivo principal é [objetivo principal], e o projeto deve incluir os seguintes componentes:
- [Componente 1]
- [Componente 2]
- [Componente 3]

Considere também estas restrições e requisitos:
- [Requisito/restrição 1]
- [Requisito/restrição 2]
```

### Criar um Plano de Recurso Específico

```
Elabore um plano detalhado para o recurso de [nome do recurso] dentro do nosso projeto.
Este recurso deve permitir que os usuários [descrição da funcionalidade].
Os requisitos específicos incluem:
- [Requisito 1]
- [Requisito 2]
- [Requisito 3]

Considere também as integrações necessárias com [outros componentes/sistemas].
```

### Revisar e Atualizar um Plano Existente

```
Revise o plano atual para [nome do recurso/projeto] e atualize-o com base nestas novas informações:
- [Nova informação/requisito 1]
- [Nova informação/requisito 2]

O plano atualizado deve manter o escopo original, mas incorporar estas mudanças de forma coerente.
```

## Prompts de Gerenciamento de Tarefas

### Gerar Tarefas a partir de um Plano

```
Com base no plano para [nome do recurso], divida-o em tarefas gerenciáveis para implementação.
Para cada tarefa, defina:
- Um título claro
- Uma descrição detalhada
- Critérios de aceitação
- Dependências (se houver)
- Prioridade estimada
```

### Criar uma Nova Tarefa Manual

```
Crie uma nova tarefa com os seguintes detalhes:
- Título: [título da tarefa]
- Descrição: [descrição detalhada]
- Critérios de aceitação: [lista de critérios]
- Dependências: [IDs de tarefas das quais esta depende, se aplicável]
- Prioridade: [alta/média/baixa]
```

### Listar Tarefas Atuais

```
Mostre todas as tarefas ativas no momento, organizadas por status e prioridade.
Destaque quaisquer bloqueios ou dependências não atendidas.
```

### Encontrar a Próxima Tarefa para Trabalhar

```
Qual é a próxima tarefa mais importante em que devo trabalhar?
Considere as dependências, prioridades e o status atual do projeto.
```

### Atualizar Status de Tarefa

```
A tarefa [ID/título] está agora [em andamento/concluída/bloqueada].
[Se bloqueada] O bloqueio é devido a [razão do bloqueio].
Por favor, atualize o status e verifique se isso afeta outras tarefas.
```

### Expandir uma Tarefa Complexa

```
A tarefa [ID/título] parece muito complexa. Por favor, divida-a em subtarefas mais gerenciáveis,
mantendo o alinhamento com o objetivo original da tarefa.
```

## Prompts de Arquivamento e Memória

### Arquivar Tarefas Concluídas

```
Arquive todas as tarefas concluídas do projeto atual para manter nossa lista de tarefas ativa limpa.
Certifique-se de que elas sejam adequadamente registradas no log histórico.
```

### Revisar Histórico de Tarefas

```
Mostre-me um resumo das tarefas concluídas nas últimas [número] semanas,
organizadas por tipo ou componente do sistema.
```

### Analisar Padrões de Conclusão de Tarefas

```
Analise nosso histórico de tarefas concluídas e identifique quaisquer padrões em termos de:
- Tipos de tarefas que levam mais tempo que o esperado
- Áreas do sistema que tendem a ter mais problemas
- Progresso geral do desenvolvimento ao longo do tempo
```

## Prompts para Memory Bank (Projetos Complexos)

### Atualizar Contexto do Produto

```
Atualize nosso Memory Bank com estas novas informações sobre o contexto do produto:
- [Nova informação sobre o produto 1]
- [Nova informação sobre o produto 2]
- [Nova informação sobre o produto 3]

Estas informações são importantes porque [razão pela qual estas informações são relevantes].
```

### Consultar Decisões Técnicas Anteriores

```
No Memory Bank, quais foram nossas decisões técnicas anteriores relacionadas a [área técnica específica]?
Por que escolhemos essa abordagem e que alternativas consideramos?
```

### Atualizar Status de Progresso

```
Atualize o arquivo de progresso no Memory Bank para refletir estas mudanças recentes:
- Concluímos o desenvolvimento de [recurso/componente recentemente concluído]
- Estamos enfrentando desafios com [área problemática atual]
- O próximo foco será [próximo foco planejado]
```

## Prompts de Meta-sistema

### Avaliar Eficácia do Sistema

```
Com base no nosso uso do Task Planner até agora neste projeto, avalie sua eficácia.
Existem ajustes que podemos fazer para melhorar como gerenciamos tarefas ou mantemos o contexto?
```

### Personalizar o Sistema para Necessidades Específicas

```
Precisamos personalizar o Task Planner para melhor atender às necessidades da nossa equipe.
Especificamente, queremos [descrição da personalização desejada, como "rastrear estimativas de tempo" ou "adicionar categorias específicas de tarefas"].
Como podemos estender o sistema para incorporar isto?
```

---

Estes exemplos de prompts fornecem um ponto de partida para trabalhar com o sistema Task Planner. Você pode adaptá-los às necessidades específicas do seu projeto, combiná-los ou expandi-los conforme necessário para gerenciar efetivamente o desenvolvimento do seu projeto com assistentes de IA.
