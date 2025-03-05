💡 Como Usar
Substitua os valores entre {CHAVES} com as informações específicas da funcionalidade.
Adicione ou remova cenários conforme necessário.
Garanta que os critérios de aceite e regras de negócio estejam bem definidos.


### 📌 **Título do Jira:** {TITULO_DA_HISTORIA}  

## 📝 **User Story**  
**Como** {PERSONA} ({TIPO_DE_USUARIO})  
**Quero** {OBJETIVO_DA_HISTORIA}  
**Para** {BENEFICIO_DA_HISTORIA}  

---  

### ✅ **Critérios de Aceite**  

- O usuário deve conseguir acessar a tela de {NOME_DA_TELA} a partir do {LOCAL_DE_ACESSO}.  
- A tela deve conter os seguintes campos obrigatórios:  
  - {CAMPOS_OBRIGATORIOS}  
- Caso um campo obrigatório não seja preenchido, deve exibir uma mensagem de erro informando o campo pendente.  
- Deve ser possível {ACAO_ADICIONAL}, caso aplicável.  
- O sistema deve validar {REGRAS_DE_VALIDACAO}, caso aplicável.  
- O usuário pode {PERMISSOES_DO_USUARIO}.  
- O botão "{NOME_DO_BOTAO}" só deve estar disponível após {CONDICAO_PARA_HABILITAR}.  

---  

### 🔍 **Cenários de Teste (BDD)**  

#### 📌 **Cenário 1: Acesso à tela de {NOME_DA_TELA}**  
**Dado** que o usuário está logado no sistema  
**Quando** acessar o {LOCAL_DE_ACESSO}  
**Então** deve ser redirecionado para a tela de {NOME_DA_TELA}  

#### 📌 **Cenário 2: {DESCRICAO_DO_CENARIO_2}**  
**Dado** que o usuário está na tela de {NOME_DA_TELA}  
**E** {CONDICAO_INICIAL}  
**Quando** {ACAO_DO_USUARIO}  
**Então** {RESULTADO_ESPERADO}  

#### 📌 **Cenário 3: {DESCRICAO_DO_CENARIO_3}**  
**Dado** que o usuário está na tela de {NOME_DA_TELA}  
**E** {CONDICAO_INICIAL}  
**Quando** {ACAO_DO_USUARIO}  
**Então** {RESULTADO_ESPERADO}  

📌 **(Adicionar mais cenários conforme necessário)**  

---

## 🎨 **Design e Fluxo**  
📌 **Link do Figma:** {LINK_DO_FIGMA}  
📌 **Fluxo do Usuário:**  
![{INSERIR_IMAGEM_FLUXO}]  

---

## 🔗 **Links Úteis**  
📌 {LINKS_RELEVANTES}  