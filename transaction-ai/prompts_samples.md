## PROMPT BUG

```
Quero que você crie os bugs abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:

* Linhas duplicas de propostas apra aceite na tela de negociação para um usuario específico

* O botão de negociação não quando o usuário esta tentando comprar o mesmo lote pela segunda vez para shopping proposta

* Não deixar alterar quantidade no estoque para ofertas com quantity_unit_type TOTAL contendo quantidade reservado ou vendido a regra para os 3 tipos de quantidade é a seguinte : 
 - QUANTITY_UNIT_TYPE = TOTAL : Não deve deixar alterar quantidade caso existe quantidade reservada ou vendida
 - QUANTITY_UNIT_TYPE = FIXED : Permite alterar e aumentando em multiplos o UNIT ( nao deixar reduzir quantidade abaixo do  reserved + sold ) 
 - QUANTITY_UNIT_TYPE = UNIT  : Permite alterar ( nao deixar reduzir quantidade abaixo do  reserved + sold ) 
```

```
Quero que você crie os bugs abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:

 Analisar com o time do Terminal cenário que não está permitindo publicar nova oferta de shopping depois que o Evento já está publicado
```


## PROMPT PARA STORY baseade em uma unica Sentença 

```
Quero que você crie as storys abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:
 
* Ajuste da tela de detalhes do repasse para status aguardando e sem repasse previsto

```

```
Quero que você crie as storys abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:
 
* Voltar implementação de consulta para Cashouts alterada na task anterior. TST-3338

* Permitir solicitar Cashouts somente se todos os lotes previstos para o evento/vendedor do dia ja estiverem sido concluídos.

   Agrupar por : COD_RECEBEDOR, EVENTO, DATA_PROGRAMADA
   
   - FL_PEDIDO_PAG_ITEM (1 split) e FL_SPLIT_PAGAMENTO ( 2 split ) 
      estiverem COD_STATUS = 2 ( Transferencia Realizada ) 
	  
```

```
Quero que você crie as storys abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:

* Ao gerar venda para  uma oferta do tipo Shopping UNIT_TOTAL, finalizar os status.
   - Alterar os status conforme regra atual PRE_LANCAMENTO, BID, OFFER
	- TODO - fazer analise da finalizaçao atual dos status para remover do evento
	
```

```
Quero que você crie os Bugs abaixo no épico TST-3205, crie uma descrição clara mas não muito extensa:

* Ao finalizar leilão convencional não deve ser enviado para o myaccounts historico cobrança ( antigo minhas compras ).
   
   Com a implementação do carrinho, os items arreamatados do leilão não deveriam ir para histórico de cobrança no minha conta.
   Devem ficar apenas disponivel no carrinho para o usuário fechar o pedido. 
   o problema esta em uma lógica do transaction-event.
    
* Mapfre não mostra o link de pagamento no myaccount 

   Não estava socilitando integração com mapfre no caso de carrinho de compras
   Ao gerar a venda da mapfre após a implementação do carrinho ficava sem integração, 
   Precisa ser ajustado no caso da forma de pagamento ser boleto externo.
   
```

```
Quero que você crie as Stories abaixo no épico TST-3431, crie uma descrição clara mas não muito extensa:

* Implementação de Data Layer para GTM no Carrinho V2

   Contexto:
      O time identificou a necessidade de criar data layers para rastreamento via GTM (Google Tag Manager) no Carrinho V2. Isso permitirá um melhor monitoramento das interações do usuário nas etapas críticas do fluxo de pedido.

   Definição:
      Os seguintes cenários serão rastreados via data layer:

      PAGE_VIEW → Tela de revisão do pedido.
      PAGE_VIEW → Tela de liberação do pedido (fechado).
      PAGE_VIEW (virtual) → Clique no download da Guia Judicial.
      PAGE_VIEW (virtual) → Download do boleto externo.
    
   Próximos Passos:
      O mapeamento dessas tags será incluído no backlog para desenvolvimento e implementação.

``` 

CRIAÇÃO EM MASSA APARTIR DE UM EPICO MACRO

Prompt com busca pelo tema:

```
Existe um epico referente ao fluxo de carrinho de compras relacionado ao rural com uma unica historia filha ? 

Essa historia é uma descricao macro, eu preciso ler o conteudo delas, incluindo anexos de imagens com informações importantes destacadas em vermelho.
Para gerar um esboço aqui em formato texto de quais historias seria criadas a partir dessa inicial, para a descrição de cada nova historia nao dee esqueça de utilizar.

o template padrão de storyconforme prompt na base de conhecimento. Me apresenta todos os esboços de cada historica com titulos e descrições 
para minha revisão e após meu ok, quero que você crie as historias.
```

## ANALISE DE SIGNOFFs e GERAÇÃO DE HISTORIAS DE USUARIO

prompt 1 : 

```
Me mostre agora os Signoffs disponivels para a plataforma, depois vou querer saber mais detalhes sobre alguns deles
```

prompt 2 :

```
Existem subpaginas para Desligamento Finlei ? preciso entender mais sobre os signoffs desse tema
```

prompt 3 :

```
Perfeito eu quero que voce me mostre agora o conteudo dos 3 , preciso entender mais a fundo os detalhes dos 3, crie um resumo desses 3
```

prompt 4 :

```
Pode me sugerir Storys para o primeiro Sign-off: Faturamento Vendedor, considerando  template padrao de story etc.
```


## CRIANDO UM EPICO E STORYS BASEADO NO SIGNOFF

Prompt 1: Consultar e entender o signoff

```
Consulte a pagina 1269268487 referente um signoff e e retorne o conteudo completo aqui no chat.
Substitua os account_ids citados no conteudo pelo nome dos usuarios jira na sua base de conhecimento para facilitar a identificação.
```

Prompt 2: Elaborar conteudo do EPIC

```
Agora me crie um esboço de um EPIC com um paragrafo resumindo o signoff para a description e inclua o link da pagina confluence após a descrição,
depois disso vou validar o conteúdo e te passar o objetive KEY para criarmos ele no jira.
```

Prompt 3: Criar Epic

```
Pode criar o epic abaixo do objective TST-1975
```

Prompt 4: Explicando Cenário atual para gerar as Story do Epic

```
Baseado no conteudo do signoff voce pdoe me sugerir quais de historias devem ser criadas, após minha validação e ok podemos criar abaixo do epic criado anteriormente.
```


## CRIAR SUBSTASKS DA STORY

```

  **Criação de Subtasks para STORY**

    Para criar SubTask obrigatoriamente respeite o project.id default na action e solicite ao usuario o Key da Story para definir "parent' na request caso ele nao passe na solicitação.
 
    IMPORTANTE -SEMPRE que o usuário soliticar sugestão de Subtasks antes de tudo consulte a pagina ID 1295122435 do confluence, contendo a lista de APPS com os nomes e dependencias, e so então baseado nessa informação siga para a analisa da STORY.,
   
    **Formatação do titulo e descrição da Subtask :** 

     Exemplo de titulo para uma subtask : "[sb-fs] Adicionar botão da tela de oferta do site"
     Obedecer o template subtask_template.md para a descrição, contendo titulo, descricao e as dependencias.

    Importante considerar nas descrição da subtask todos os campos detalhados em negrito na STORY, bem caso nome de tabelas ou colunas no banco de dados caso exista alguma informação na descrição técnica da STORY, quanto mais direta a descrição melhor, lembre-se que o leitor da subtask é o desenvolvedor.

    Após ter o entendido das APPs e suas dependências e baseado na função de cada app consulte a STORY
    e me sugira as subtasks necessarias com titulo e descrição.

    Não quebre em exagero o numero de subtasks, não devem ser criadas tasks apenas para criação de testes , ou validações, isso dever ser parte da definição de pronta de cada subtask, criei o minimo de subtasks necessário.

    Importante considerar a coluna de dependencias ao analisar o impacto e quais apps precisam de subtasks, não inclua apps das quais não exita uma relação de dependência descrita na tabela

    Após a minha revisão dos textos eu te dou o ok para criar no JIRA as subtasks com o parent sendo a story definida acima.

    A STORY alvo é TST-3505
```


## ESTIMAR PONTOS DA SPRINT BASEADO NO HISTORICO

Preciso estimar os story points das subtasks da Sprint de Historica com base na Sprint alvo. A nova sprint contém diversas subtasks cujos nomes indicam as aplicações impactadas. Quero que a estimativa siga as regras de Story Points utilizadas na empresa, aplicando a tabela Fibonacci de estimativa de tempo conforme definido nas instruções (1 ponto = 1h, 2 pontos = 4h, 3 pontos = 9h, 5 pontos = 15h, 8 pontos = 40h, 13 pontos = 80h). Compare o escopo das novas subtasks com as subtasks da Sprint de Historica, analisando similaridades e complexidade técnica. Gere uma tabela contendo as subtasks, seus resumos e a estimativa de story points baseada nessa análise no modelo de sumario"

Para saber quais sao as sprint, consulte sempre a sprint atual e.x 31
Sprint Historica = a sprint concluida antes da atual, e.g 30

BAseado nisso estimar os pontos da Sprint 32