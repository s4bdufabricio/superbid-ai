# Instrução para Consulta de Story Points no Jira

# Regra Geral

Na Superbid, os Story Points são atribuídos apenas às Subtasks das histórias. Portanto, para calcular os pontos de uma Sprint ou de uma Story, é necessário buscar todas as Subtasks associadas.

## Pontos x Tempo

    Sempre que for solicitado um cálculo de estimativa de tempo com base em Story Points, utilize a seguinte conversão de acordo com a sequência de Fibonacci:

    1 ponto → 1 hora
    2 pontos → 4 horas
    3 pontos → 9 horas (média entre 6 e 12 horas)
    5 pontos → 15 horas
    8 pontos → 40 horas
    13 pontos → 80 horas
    Caso seja necessário calcular o tempo total de uma Sprint, siga os passos abaixo:

    Converta cada Sub-task associada a uma Story de acordo com a tabela acima.
    Some todas as horas estimadas das Sub-tasks para obter o total de horas da Sprint.
    Para calcular a carga de trabalho por desenvolvedor, divida o total de horas pelo número de desenvolvedores atribuídos à Sprint.
    Se houver arredondamentos na soma dos pontos, sempre arredonde para cima para evitar subestimação do tempo necessário.

# PROMPT - Consulta de Story Points de uma Sprint

Quando o usuário solicitar os Story Points de uma Sprint, execute a seguinte consulta no Jira:

## JQL:

    ```
    project = "Time Transaction" AND sprint = SPRINT_ID AND type = Sub-task ORDER BY summary ASC, parent DESC
    ```
    
## Campos a retornar:

    ```
    fields: "summary,parent,customfield_10034"
    ```

## Lógica de processamento:

    Somar os valores do campo customfield_10034 (Story Points) de todas as Subtasks.

    Apresentar o total de Story Points da Sprint.

    Caso o usuário solicite um detalhamento por Story, consolidar os pontos das Subtasks agrupadas por sua Story principal.

# PROMPT -  Consulta de Story Points de uma Story

    Quando o usuário solicitar os Story Points de uma Story específica, utilize a seguinte consulta no Jira:

## JQL:
    
    ```
    project = "Time Transaction" AND parent = STORY_ID AND type = Sub-task ORDER BY summary ASC, parent DESC
    ```

## Campos a retornar:

    ```
    fields: "summary,parent,customfield_10034"
    ```

## Lógica de processamento:

    Somar os valores do campo customfield_10034 de todas as Subtasks associadas à Story.
    Apresentar o total de Story Points da Story.
    
## Formato de Resposta

    A resposta deve seguir o seguinte formato:

    Story Points de uma Sprint

    ```
    Total de Story Points da Sprint [SPRINT_NAME]: XX pontos
    ```

# PROMPT - Caso o usuário peça um detalhamento de pontos por Story, ou um sumário de pontos da sprint:

Formato para retornar o Sumário de Pontos da Sprint

```
Total de Story Points da Sprint [SPRINT_NAME]: XX pontos


| Story Key  | Summary | Assignee | Status | Total de Story Points |
|------------|---------|----------|--------|------------------------|
| STORY-1    | Descrição da Story 1 | Nome do responsável | In Progress | XX |
| STORY-2    | Descrição da Story 2 | Nome do responsável | Done | XX |
```