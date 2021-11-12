# conserta-meu-carro

Esse é o repositório com a API base, contendo rotas, para construção da aplicação do grupo 3 de acordo com os requisitos do projeto do Capstone.

## ENDEREÇO DE ACESSO:

https://conserta-meu-carro-api.herokuapp.com/

## Endpoints

- /register/
- /login/
- /orders/

### Cadastro de usuário (empresa)

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "empresa1@mail.com",
  "password": "123456",
  "name": "Empresa de retífica",
  "company_name": "Siga bem caminhoneiro LTDA",
  "cnpj": "01908120000181",
  "address": "Rua Ceará, 3312, Praça da Bandeira, Rio de Janeiro"
}
```

:exclamation:Informações obrigatórias para validação:

1. email
2. password

Os demais campos são necessários para construção do banco de dados utilizados na execução da aplicação.

Caso dê tudo certo, a resposta será assim:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtcHJlc2ExQG1haWwuY29tIiwiaWF0IjoxNjM2NTczMjcxLCJleHAiOjE2MzY1NzY4NzEsInN1YiI6IjMifQ.Er27RihgqDyQ05nAe2CCuWcQLhUFvszuz_T9rqj73Pg",
  "user": {
    "email": "empresa1@mail.com",
    "name": "Empresa de retífica",
    "company_name": "Siga bem caminhoneiro LTDA",
    "cnpj": "01908120000181",
    "address": "Rua Ceará, 3312, Praça da Bandeira, Rio de Janeiro",
    "id": 3
  }
}
```

### Cadastro de usuário (usuário)

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "fuladodaferrari@mail.com",
  "password": "123456",
  "name": "Fulano Roberto",
  "cpf": "96351322254"
}
```

:exclamation:Informações obrigatórias para validação:

1. email
2. password

Os demais campos são necessários para construção do banco de dados utilizados na execução da aplicação.

Caso dê tudo certo, as resposta será assim:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZ1bGFkb2RhZmVycmFyaUBtYWlsLmNvbSIsImlhdCI6MTYzNjU3NDA0OCwiZXhwIjoxNjM2NTc3NjQ4LCJzdWIiOiI0In0.Rg1jui678oI0tb02OWUoJutdNi6yxpcmO-7uTBxNfQU",
  "user": {
    "email": "fulanodaferrari@mail.com",
    "name": "Fulano Roberto",
    "cpf": "96351322254",
    "id": 4
  }
}
```

### Login de usuários (Empresas e usuários)

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "fuladodaferrari@mail.com",
  "password": "123456"
}
```

Caso tudo dê certo:

`POST /login - FORMATO DA RESPOSTA - STATUS 200 `

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZ1bGFkb2RhZmVycmFyaUBtYWlsLmNvbSIsImlhdCI6MTYzNjU3NDUwMSwiZXhwIjoxNjM2NTc4MTAxLCJzdWIiOiI0In0.Nlnw5Wmg5ZSMaYbGy91glk8G0Y_5Z4geWu4fVEvTHNw",
  "user": {
    "email": "fuladodaferrari@mail.com",
    "name": "Fulano Roberto",
    "cpf": "96351322254",
    "id": 4
  }
}
```

### Exclusão de usuários (login)

`DELETE /users/${userId} - FORMATO DA REQUISIÇÃO`

```json

Não é necessário um corpo de requisição

```

:exclamation: Auth: É necessário informar token para autenticação.

#### header

**authorization** `Bearer token`

`DELETE /users/${userId} - FORMATO DA RESPOSTA - 200`

```json

Para tanto, não há retorno explícito no corpo.

```

### Ordens

Para todas as próximas requisições, os usuários precisam estar logados e com o Auth Token devidamente configurado

#### header

**authorization** `Bearer token`

`GET /orders - FORMATO DA REQUISIÇÃO`

```json

Não é necessário corpo para requisição

```

`GET /orders - FORMATO DA RESPOSTA - 200`

```json
[
  {
    "title": "Pneu furado",
    "description": "Pneu rasgado por um buraco a caminho do trabalho",
    "address": "Avenida Principal, São Paulo, próximo SABESP",
    "rating": 1,
    "status": "pending",
    "veículo": {
      "modelo": "Volkswagen",
      "ano": "1980"
    },
    "id": 1
  }
]
```

### Criação de ordens

`POST /orders - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "Pneu furado",
  "description": "Pneu rasgado por um buraco a caminho do trabalho",
  "address": "Avenida Principal, São Paulo, próximo SABESP",
  "rating": 1,
  "status": "pending",
  "veículo": {
    "modelo": "Volkswagen",
    "ano": "1980"
  }
}
```

`POST /orders - FORMATO DA RESPOSTA - 201`

```json
{
  "title": "Pneu furado",
  "description": "Pneu rasgado por um buraco a caminho do trabalho",
  "address": "Avenida Principal, São Paulo, próximo SABESP",
  "rating": 1,
  "status": "pending",
  "veículo": {
    "modelo": "Volkswagen",
    "ano": "1980"
  },
  "id": 1
}
```

### Para atualizção das ordens

`PATCH /orders - FORMATO DA REQUISIÇÃO`

```json
{
  "rating": 3,
  "status": "completed"
}
```

Por padrão, esse endpoint é utilizado para fazer atualizações nas demais propriedades do banco de dados, entretanto, priorize atualização para as propriedades demonstradas acima.

`PATCH /orders - FORMATO DA RESPOSTA - 200`

```json
{
  "title": "Pneu furado",
  "description": "Pneu rasgado por um buraco a caminho do trabalho",
  "address": "Avenida Principal, São Paulo, próximo SABESP",
  "veículo": {
    "modelo": "Volkswagen",
    "ano": "1980"
  },
  "id": 1,
  "rating": 3,
  "status": "completed"
}
```

### Para exclusão das ordens

`DELETE /orders - FORMATO DA REQUISIÇÃO`

```json

Não é necessário corpo para requisição

```

`DELETE /orders - FORMATO DA RESPOSTA 200`

```json

Para tanto, não há retorno explícito no corpo.

```
