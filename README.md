# Seguranca-a-aws

Este projeto demonstra a utilização de vários serviços da AWS para implementar recursos de segurança.

## Serviços AWS utilizados

- Amazon Cognito
- Amazon DynamoDB
- Amazon API Gateway
- AWS Lambda

## Etapas do desenvolvimento

### Criando uma API REST no Amazon API Gateway

1. Acesse o painel de controle do API Gateway.
2. Clique em "Create API" e selecione "REST API".
3. Selecione o protocolo "REST" e clique em "Create new API".
4. Defina um nome para a API (exemplo: `dio_live_api`) e selecione o tipo de Endpoint como "Regional".
5. Clique em "Create API".

### Criando uma tabela no Amazon DynamoDB

1. Acesse o painel de controle do DynamoDB.
2. Clique em "Tables" e depois em "Create table".
3. Defina um nome para a tabela (exemplo: `Items`).
4. Escolha uma chave de partição (exemplo: `id`).
5. Clique em "Create table".

### Criando uma função AWS Lambda para inserir itens

1. Acesse o painel de controle do Lambda.
2. Clique em "Create function".
3. Defina um nome para a função (exemplo: `put_item_function`).
4. Cole o código da função `put_item_function.js` disponível na pasta `/src`.
5. Configure a função conforme suas necessidades.
6. Clique em "Create function".

### Integrando o API Gateway com o Lambda backend

1. No painel do API Gateway, selecione a API criada anteriormente.
2. Clique em "Resources" e selecione o resource criado.
3. Clique em "Actions" e depois em "Create method".
4. Escolha o método HTTP desejado (exemplo: POST).
5. Selecione "Lambda function" como tipo de integração.
6. Marque a opção "Use Lambda Proxy Integration".
7. Selecione a função Lambda criada anteriormente.
8. Clique em "Save" e depois em "Deploy API".
9. Crie um novo estágio (exemplo: `dev`) e clique em "Deploy".

### Utilizando o Postman para testar a API

1. Adicione uma nova requisição no Postman.
2. Selecione o método POST.
3. Copie o endpoint gerado pelo API Gateway.
4. Defina o corpo da requisição no formato JSON. Por exemplo:
   ```json
   {
     "id": "003",
     "price": 600
   }
   ```
5. Envie a requisição.

### Configurando o Amazon Cognito

1. Acesse o painel de controle do Cognito.
2. Clique em "Manage User Pools".
3. Crie um novo User Pool com um nome desejado (exemplo: `TestPool`).
4. Configure as opções de autenticação e personalização conforme necessário.
5. Clique em "Create Pool".
6. Crie um App Client para o User Pool.
7. Defina as configurações desejadas para o App Client (exemplo: `TestClient`).
8. Salve as alterações.

### Criando um autorizador do Amazon Cognito para a API REST

1.

 No painel do API Gateway, selecione a API criada anteriormente.
2. Clique em "Authorizers" e depois em "Create New Authorizer".
3. Defina um nome para o autorizador (exemplo: `CognitoAuth`).
4. Selecione o tipo "Cognito" e escolha o User Pool criado anteriormente.
5. Defina a fonte do token como "Authorization".
6. Selecione o resource e o método criados anteriormente.
7. Na seção "Method Request", configure a opção "Authorization" para utilizar o autorizador criado.

### Obtendo um token do Amazon Cognito no Postman

1. Adicione uma nova requisição no Postman para inserir um item.
2. Clique na aba "Authorization".
3. Selecione o tipo "OAuth 2.0".
4. Preencha os seguintes campos:
   - Callback URL: `https://example.com/logout`
   - Auth URL: `https://diolive.auth.sa-east-1.amazoncognito.com/login`
   - Client ID: Obtenha o Client ID do Cognito no App Client criado anteriormente.
   - Scope: `email openid`
   - Client Authentication: Selecione "Send client credentials in body".
5. Clique em "Get New Access Token".
6. Copie o token gerado.
7. Na requisição de inserção de item, vá para a aba "Authorization" e selecione o tipo "Bearer Token".
8. Cole o token copiado.
9. Envie a requisição.

### Executando a análise de código com o CodeQL

Este projeto também inclui um arquivo `codeql.yml` para configurar a análise de código com o CodeQL.

1. O workflow está configurado para rodar automaticamente quando ocorrer um push na branch "main" ou em pull requests para a branch "main".
2. A análise é realizada usando o CodeQL para a linguagem `javascript`.
3. A análise é agendada para ser executada semanalmente às 4h41 dos sábados.
4. O resultado da análise é gerado no painel de segurança do GitHub.
