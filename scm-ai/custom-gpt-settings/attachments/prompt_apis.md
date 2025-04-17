# SOBRE ACTION E CHAMADAS DE APIS

## Informação Geral para todas as chamadas de API

* Sempre considere utilizar os parametros definidos como default na suas actions caso o usuario nao especifique.
* Para todas as requisições incluir sempre o header alem do authorization: "X-Atlassian-Token: nocheck"

# PARAMETROS PADROES PARA CADA ACTION DE API

## getIssuesByJql - Consultar Issues ( Bugs, Storys, Epics, Deploys etc.. ) by JQL

  * Essa Action deve ser usada para mutiplos prompts ou ações sempre que o usuario pedir para listar algum tipo de issue seja ela BUG, STORY, EPIC
  
  * O maximo de resultados por pagina da API do jira é de 100, sendo assim verifique sempre se retornou o campo nextPageToken no json da resposta caso exista é necessário fazer uma nova solicitação definindo o startAt para a proxima pagina sucetivamente até que a resposta não contenha o nextPageToken.

  * Considere os parametros conforme os seguinte tipos de solicitação abaixo :

  1. Se o prompt pedir para "Consultar Deploys" você deve utilizar os seguinte SQL:
      
      jql : project = "RDM - Controle de Deploys" AND type = Deploy
      fields: "summary,customfield_10448,customfield_10447"

      Interpretar o custome fields do reponse como : 

      customfield_10448 = Data Agendada ou Porgramada para o Deploy
      customfield_10447 = Lista de apps incluidas no pacote


  1. Se o prompt pedir para "Consultar uma Issue especifica pela KEY (story,bug, etc) e mostrar ou resumir o conteúdo utilize sempre os parâmetros abaixo :
     Nesse caso estou buscando as historias de outros projetos, sendo assim voce nao precisa usar o filtro "project" no JQL, apenas as keys mesmo. 
      
      jql : "key = TST-1835"
      fields: "*all"