# Prompt Padrão para Payloads ADF no Jira

Ao criar payloads no formato ADF para issues no Jira, siga as seguintes orientações:

## Estrutura Básica do Documento:

O objeto principal deve ter "type": "doc", "version": 1 e uma propriedade "content" contendo uma lista de nós.
Parágrafos:

Cada parágrafo deve ser um nó do tipo "paragraph" com seu conteúdo definido em "content" como uma lista de nós do tipo "text".
Listas (bulletList/orderedList):

Cada lista deve ser definida como um nó do tipo "bulletList" (ou "orderedList", se aplicável).
Importante: Cada item da lista deve estar dentro de um nó do tipo "listItem".
Se você tiver listas aninhadas (por exemplo, parâmetros dentro de um item), a lista interna deve estar contida dentro de um "listItem" do item pai.

## Exemplo de item de lista simples:

```
{
  "type": "listItem",
  "content": [
    {
      "type": "paragraph",
      "content": [
        { "type": "text", "text": "Texto do item" }
      ]
    }
  ]
}
```

## Exemplo de lista aninhada:

```
{
  "type": "listItem",
  "content": [
    {
      "type": "paragraph",
      "content": [
        { "type": "text", "text": "Título dos parâmetros:" }
      ]
    },
    {
      "type": "bulletList",
      "content": [
        {
          "type": "listItem",
          "content": [
            {
              "type": "paragraph",
              "content": [
                { "type": "text", "text": "Parâmetro 1" }
              ]
            }
          ]
        },
        {
          "type": "listItem",
          "content": [
            {
              "type": "paragraph",
              "content": [
                { "type": "text", "text": "Parâmetro 2" }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

# Code Blocks:

Para blocos de código, use o nó "codeBlock" com o atributo "attrs" definindo a linguagem.
Outros Elementos:

Siga o padrão definido pela especificação ADF para quaisquer outros elementos.
Headers e Outros Campos:

Mantenha os demais campos do payload (como issuetype, parent, project e summary) conforme o padrão requerido pela sua instância do Jira.


# Exemplo de Payload Completo:

```
{
  "fields": {
    "description": {
      "type": "doc",
      "version": 1,
      "content": [
        {
          "type": "paragraph",
          "content": [
            { "type": "text", "text": "Texto do seu parágrafo principal." }
          ]
        },
        {
          "type": "paragraph",
          "content": [
            { "type": "text", "text": "📌 Requisitos Técnicos:" }
          ]
        },
        {
          "type": "bulletList",
          "content": [
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [
                    { "type": "text", "text": "Item 1 da lista." }
                  ]
                }
              ]
            },
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [
                    { "type": "text", "text": "Item 2 com subitens:" }
                  ]
                },
                {
                  "type": "bulletList",
                  "content": [
                    {
                      "type": "listItem",
                      "content": [
                        {
                          "type": "paragraph",
                          "content": [
                            { "type": "text", "text": "Subitem 2.1" }
                          ]
                        }
                      ]
                    },
                    {
                      "type": "listItem",
                      "content": [
                        {
                          "type": "paragraph",
                          "content": [
                            { "type": "text", "text": "Subitem 2.2" }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "type": "codeBlock",
          "attrs": { "language": "json" },
          "content": [
            {
              "type": "text",
              "text": "{ \"exemplo\": \"payload\" }"
            }
          ]
        }
      ]
    },
    "issuetype": { "name": "Sub-task" },
    "parent": { "key": "TST-XXXX" },
    "project": { "id": "10010" },
    "summary": "Título da tarefa"
  }
}
```

# Resumo:

O erro de formatação que estava ocorrendo era por causa da estrutura incorreta de listas aninhadas.
Sempre que criar listas aninhadas, garanta que elas estejam dentro de um listItem do item pai.
Utilize esse prompt como referência para todas as próximas chamadas, para evitar erros do tipo "INVALID_INPUT" devido a problemas de formatação ADF.