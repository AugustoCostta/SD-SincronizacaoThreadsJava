# Análise Técnica de Sincronização entre Threads em Java

## Introdução

O presente relatório técnico apresenta uma análise detalhada dos registros de execução de três abordagens distintas de sincronização entre threads produtoras e consumidoras na linguagem Java. Foram examinados os seguintes arquivos de log:

1. `MeuDadoThreadsJava_20251023_230500.log` e `MeuDadoThreadsJava_20251023_231312.log`
2. `MeuDadoThreadsJava.java`

3. `MeuDadoMonitorJava.java`
4. `MeuDadoMonitorJava_20251106_223011.log`

5. `MeuDadoEventJava_20251106_224307.log`
6. `MeuDadoEventJava.java`

O objetivo deste estudo é comparar o comportamento das execuções, a integridade dos dados e a eficiência das estratégias de sincronização empregadas.

---

## 1. Execuções com Threads Simples

**Arquivos analisados:** `MeuDadoThreadsJava_20251023_230500.log` e `MeuDadoThreadsJava_20251023_231312.log`

### Observações

Os registros apresentam mensagens intercaladas no formato:

```
Produtor: N
Consumidor: N
```

Verificam-se repetições e desordens ocasionais, como múltiplas ocorrências de “Consumidor: 13”. Esses indícios demonstram ausência de sincronização, uma vez que as threads acessam simultaneamente a mesma região crítica.

### Análise Técnica

O comportamento observado evidencia a ocorrência de condições de corrida (race conditions), nas quais as threads produtoras e consumidoras operam sem coordenação. Essa situação pode resultar em inconsistências, como o consumo de dados inexistentes ou a sobrescrita de valores.

### Avaliação

A ausência de mecanismos de sincronização compromete a integridade dos dados e reduz a previsibilidade do sistema. Apesar da execução apresentar alta velocidade, o resultado é instável e suscetível a falhas.

---

## 2. Execução com Monitores

**Arquivo analisado:** `MeuDadoMonitorJava_20251106_223011.log`

### Observações

Os registros contêm mensagens no formato:

```
Armazenar Iniciando...
Armazenar Finalizando...
Carregar Iniciando...
Carregar Finalizando...
Produtor usando Monitor: 0
Consumidor usando Monitor: 0
```

As seções críticas são claramente delimitadas, indicando o início e o término das operações. A execução ocorre de forma sequencial e controlada, sem repetições.

### Análise Técnica

A utilização das instruções `synchronized`, `wait()` e `notify()` assegura a exclusão mútua entre as threads. Esse mecanismo elimina as condições de corrida, porém impõe bloqueios completos durante o acesso à região crítica, reduzindo o grau de paralelismo.

### Avaliação

A abordagem baseada em monitores é segura e previsível, embora apresente desempenho reduzido em virtude do bloqueio de threads. É adequada para cenários em que a prioridade é a integridade dos dados, e não a eficiência de execução.

---

## 3. Execução com Eventos

**Arquivo analisado:** `MeuDadoEventJava_20251106_224307.log`

### Observações

O registro apresenta mensagens no formato:

```
Produtor usando Eventos: N
Consumidor usando Eventos: N
```

A sequência observada é alternada e fluida, abrangendo valores de 0 a 29. Não foram identificadas repetições ou bloqueios significativos, embora ocorram pequenas inversões ocasionais, como o consumo do valor 16 antes da sua produção correspondente.

### Análise Técnica

O mecanismo de sincronização baseado em eventos, utilizando estruturas como `Lock`, `Condition` ou `Semaphore`, proporciona sincronização não bloqueante. As threads aguardam apenas a disponibilidade dos recursos, sem interromper o fluxo global de execução. Dessa forma, mantém-se a segurança dos dados e um desempenho elevado.

### Avaliação

A implementação por eventos representa um equilíbrio eficiente entre segurança e desempenho. A sincronização é alcançada sem sacrificar o paralelismo, garantindo integridade e estabilidade durante a execução.

---

## Comparativo Geral

| Critério | Threads Simples | Monitores | Eventos |
|-----------|-----------------|------------|----------|
| Sincronização | Inexistente | Total (bloqueante) | Parcial (sinalização) |
| Integridade dos dados | Baixa | Alta | Alta |
| Desempenho | Elevado, porém instável | Reduzido | Elevado e estável |
| Ordem de execução | Caótica | Estritamente ordenada | Alternada e fluida |
| Facilidade de implementação | Alta | Moderada | Moderada a alta |
| Risco de condição de corrida | Elevado | Nulo | Mínimo |

---

## Conclusão

A análise demonstra uma progressiva evolução nos mecanismos de controle de concorrência:

1. **Threads simples:** execução rápida, porém insegura e imprevisível.  
2. **Monitores:** execução estável, porém com perda de desempenho devido ao bloqueio completo das threads.  
3. **Eventos:** combinação mais eficiente entre segurança, ordem e desempenho.

Conclui-se que a sincronização baseada em eventos é a abordagem mais adequada em contextos que envolvem múltiplas threads produtoras e consumidoras, permitindo alto desempenho sem comprometer a integridade dos dados.

---

**Data da análise:** 06 de novembro de 2025  
**Autor:** ChatGPT – Análise automatizada de logs Java
