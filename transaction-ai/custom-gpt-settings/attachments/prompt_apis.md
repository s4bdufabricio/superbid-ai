# SOBRE ACTION E CHAMADAS DE APIS

## Informação Geral para todas as chamadas de API

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

  * Sempre especifique na request o issue_type que podem ser "Story" ou "Bug" ou "Epic" ou "Sub-task", conforme o tipo solicitado pelo usuário no bloco json da request   "issuetype": {"name": "Story"}, "issuetype": {"name": "Bug"},  "issuetype": {"name": "Epic"},  "issuetype": {"name": "Sub-task"}

  * Para criar STORY obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Epic para definir "parent' na request caso ele nao passe na solicitação, usar o formato do arquivo (story_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Para criar BUG obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Epic  para definir "parent' na request caso ele nao passe na solicitação, usar o formato do arquivo (bugs_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Para criar Epic obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key do Objective para definir "parent' na request caso ele nao passe na solicitação, o formato deve ser em formato ADF conforme texto gerado para titulos e textos

  * Quando for criar um BUG usar o formato do arquivo (bugs_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira
  * Quando for criar um STORY usar o formato do arquivo (story_template.md), converta a sintaxe de formatacao dos mds para ADF para formatar no jira

  * Sempre que criar uma Issue retorne o ID e Summary criado na repsosta no chat para facilitar a consulta

  **Criação de Subtasks para STORY**

    Para criar SubTask obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key da Story para definir "parent' na request caso ele nao passe na solicitação.
 
    IMPORTANTE -SEMPRE que o usuário soliticar sugestão de Subtasks antes de tudo consulte a pagina ID 1295122435 do confluence, contendo a lista de APPS com os nomes e dependencias, e so então baseado nessa informação siga para a analisa da STORY.,
   
    **Formatação do titulo e descrição da Subtask :** 

     Exemplo de titulo para uma subtask : "[sb-fs] Adicionar botão da tela de oferta do site"
     Obedecer o template subtask_template.md para a descrição, contendo titulo, descricao e as dependencias.

    Importante considerar nas descrição da subtask todos os campos detalhados em negrito na STORY, bem caso nome de tabelas ou colunas no banco de dados caso exista alguma informação na descrição técnica da STORY, quanto mais direta a descrição melhor, lembre-se que o leitor da subtask é o desenvolvedor.

    Após ter o entendido das APPs e suas dependências e baseado na função de cada app consulte a STORY <<KEY>> 
    e me sugira as subtasks necessarias com titulo e descrição.

    Não quebre em exagero o numero de subtasks, não devem ser criadas tasks apenas para criação de testes , ou validações, isso dever ser parte da definição de pronta de cada subtask, criei o minimo de subtasks necessário.

    Importante considerar a coluna de dependencias ao analisar o impacto e quais apps precisam de subtasks, não inclua apps das quais não exita uma relação de dependência descrita na tabela

    Após a minha revisão dos textos eu te dou o ok para criar no JIRA as subtasks com o parent sendo a story definida acima.

# FORMATAÇÃO ADF DOS TEXTOS PARA CRIAR TODAS AS ISSUES :

   Sempre mostre o esboço da issue a ser criada no chat em formato texto, Porém ao enviar a requisição para a API sempre formatar em  ADF, mantenha os icones e identações descritos no chat comm o usuário sempre, e 

   Como exemplo de ADF voce poder usar o arquivo adf.example.md
   Observe no exemplo acima principal a estrutura de listas aninhadas.

#  SPRINT - ESTIMATIVAS e STORY POINTS 

  
  Caso o usuário pesão qualquer informação sobre STORY POINTS, Velocidade ou Estimativa sempre considere as instruções no arquivo sprint_story_points.md.md


#  setStoryPointsSubTask  

  obrigatoriamente utilize também os cabecalhos para essa request: "User-Agent: Superbid-ChatGpt/1.0", alem do Authorization Basic configurado para a action


'
# Listar Problemas de produção reportados em sustentação no Jira ITSM 

Quando for solicitado a lista de problemas atualmente em produção do tive transaction utilize a seguinte JQL abaixo 
e nesse caso em especifico o project é diferente

```
project = N2SUS AND resolution in (Unresolved) AND type = "[System] Problem" AND component in ("Terminal Gestor - Cobrança", "Terminal Gestor - Contratos", "Transaction , Oracle , Totvs", "Terminal Gestor - Relatórios") ORDER BY priority
```
  









  