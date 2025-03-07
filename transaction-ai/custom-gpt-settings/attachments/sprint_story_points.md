# Instrução para Consulta de Story Points no Jira

# Regra Geral

Na Superbid, os Story Points são atribuídos apenas às Subtasks das histórias. Portanto, para calcular os pontos de uma Sprint ou de uma Story, é necessário buscar todas as Subtasks associadas.

## Pontos x Tempo

1 ponto: aproximadamente 1 hora de trabalho.
2 pontos: tarefa que pode ser concluída em meio dia.
3 pontos: tarefa de 1 a 2 dias de esforço.
5 pontos: tarefa que requer cerca de 3 dias para ser finalizada.
8 pontos: tarefas mais complexas, que demandam cerca de 5 dias de trabalho.
13 pontos: atividades significativas que ocupam uma sprint inteira ( considerar quebrar estórias de 13 pontos em estórias menores )

Para fazer analises estimativas de esforço por dev, considere a carga horaria de 7 horas produtivas por dia.

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