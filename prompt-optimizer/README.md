# Optimize-Prompt - Documentação do Prompt

Este documento descreve o prompt de otimização baseado no algoritmo ProTeGi (Otimização de Prompt com Gradientes Textuais).

## Descrição

O `optimize-prompt.prompt.md` é um prompt projetado para ser utilizado com modelos de linguagem avançados, como o Claude Sonnet 3.7 e Gemini 2.5 Flash, permitindo implementar o algoritmo ProTeGi para otimização iterativa de outros prompts.

## Funcionalidade

O prompt transforma o modelo de linguagem em um otimizador de prompts que:

1. Recebe um prompt inicial como entrada
2. Aplica o algoritmo ProTeGi para otimizá-lo iterativamente
3. Retorna um prompt otimizado junto com métricas de desempenho

## Parâmetros

O prompt aceita os seguintes parâmetros:

- **INITIAL_PROMPT**: O prompt que você deseja otimizar
- **MAX_ITERATIONS**: O número máximo de iterações (padrão: 10)
- **CONVERGENCE_THRESHOLD**: O limiar de convergência para parar o processo (padrão: 0.01)

## Como usar

1. Forneça um prompt inicial dentro das tags `<prompt_inicial>` e `</prompt_inicial>`. Se isso não for feito, o agente vai perguntar por um.
2. Opcionalmente, especifique os valores para `MAX_ITERATIONS` e `CONVERGENCE_THRESHOLD`
3. O algoritmo executará o processo de otimização automaticamente
4. Os resultados serão apresentados em um formato estruturado

## Exemplo de Uso

```
<prompt_inicial>
Classifique o sentimento do texto fornecido como positivo, negativo ou neutro.
</prompt_inicial>

Máximo de iterações: 5
Limiar de convergência: 0.02
```

## Resultados

O algoritmo apresentará os resultados no seguinte formato:

```
<resultados>

<prompt_otimizado>
[O prompt final otimizado]
</prompt_otimizado>

<metricas_de_desempenho>
[Métricas-chave de desempenho]
</metricas_de_desempenho>

<processo_de_otimizacao>
[Resumo do processo de otimização]
</processo_de_otimizacao>

</resultados>
```

## Considerações

- O algoritmo ProTeGi busca melhorar o prompt sem alterar sua essência original
- O processo de otimização é iterativo e pode variar em eficácia dependendo do prompt inicial
- As métricas de desempenho ajudam a entender as melhorias alcançadas

## Limitações

- A otimização depende da qualidade e clareza do prompt inicial
- O algoritmo pode não encontrar melhorias significativas para prompts já bem otimizados
- O número de iterações afeta diretamente o tempo de processamento e o resultado final
