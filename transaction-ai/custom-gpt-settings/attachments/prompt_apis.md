# SOBRE ACTION E CHAMADAS DE APIS

## Infomração Geral para todas as chamadas de API

* Sempre considere utilizar os parametros definidos como default na suas actions caso o usuario nao especifique.
* Para todas as requisições incluir sempre o header alem do authorization: "X-Atlassian-Token: nocheck"

* Sempre que for solicitado um parametro de project nas apis da attlassian utiliza as informações
    * project.id = 10010
    * project.key = TST

# PARAMETROS PADROES PARA CADA ACTION DE API

## getIssuesByJql - Consultar Issues ( Bugs, Storys, Epics, Deploys etc.. ) by JQL

  * Essa Action deve ser usada para mutiplos prompts ou ações sempre que o usuario pedir para listar algum tipo de issue seja ela BUG, STORY, EPIC ou qualquer outro tipo.
  * Considere os parametros conforme os seguinte tipos de solicitação abaixo :

  1. Se o prompt pedir para "Consultar uma Issue especifica pela KEY (story,bug, etc) e mostrar ou resumir o conteúdo utilize sempre os parâmetros abaixo :
      
      jql : "project = \"Time Transaction\" AND key = TST-1835"
      fields: "*all"

  2. Se o prompt pedir para "Consultar uma Storys do Epic utilize sempre os parâmetros abaixo :
      
      jql : "project = \"Time Transaction\" AND parent IN (TST-2241) AND type = Story ORDER BY summary ASC, parent DESC"
      fields: "summary,customfield_10020,customfield_10034,parent"

      Se o usuario não fornecer o KEY do Epic desejado a ser usado no parent da JQL no prompt solicite antes de fazer a consulta.

  3. Se o prompt pedir para "Consultar uma Issue (story,bug, etc) e mostrar ou resumir o conteudo utilize sempre os parâmetros abaixo :
      jql : "project = \"Time Transaction\" AND type = Epic ORDER BY summary ASC, parent DESC"
      fields: "summary,customfield_10020,customfield_10034,parent"

  4. Se o prompt pedir para "Consultar tasks ou story de um Sprint pelo ID <X>", utilize sempre os parâmetros abaixo, caseo nao seja passado SPRINT_ID da sprint solitice ao usuario :
      jql : "project = \"Time Transaction\" AND sprint = SPRINT_ID AND type = Story ORDER BY summary ASC, parent DESC"
      fields: "summary,customfield_10020,customfield_10034,parent"


# createStory - usado para criar issue Epic, Story, Bug ou Sub-task

  * Execute sempre com o project.id padrão e caso o usuário não informe solicite o EPIC KEY, obrigatoriamente utilize também os cabecalhos para essa request: "User-Agent: Superbid-ChatGpt/1.0".

  * Sempre especifique na request o issue_type que podem ser "Story" ou "Bug" ou "Epic", conforme o tipo solicitado pelo usuário no bloco json da request   "issuetype": {"name": "Story"}, "issuetype": {"name": "Bug"},  "issuetype": {"name": "Epic"}

  * Para criar STORY obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Epic para definir "parent' na request caso ele nao passe na solicitação, usar o formato do arquivo (story_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Para criar BUG obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Epic  para definir "parent' na request caso ele nao passe na solicitação, usar o formato do arquivo (bugs_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Para criar Epic obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Objective para definir "parent' na request caso ele nao passe na solicitação, o formato deve ser em formato ADF conforme texto gerado para titulos e textos
  * Para criar SubTask obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key da Story para definir "parent' na request caso ele nao passe na solicitação, o formato deve ser em formato ADF conforme texto gerado para titulos e textos

  * Quando for criar um BUG usar o formato do arquivo (bugs_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Quando for criar um STORY usar o formato do arquivo (story_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira

  * Sempre que criar uma Issue retorne o ID e Summary criado na repsosta no chat para facilitar a consulta
  