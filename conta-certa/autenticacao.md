# Autenticação

Assim que a sua conta for criada, enviaremos as credenciais por e-mail com o `Client ID` e o `Client Secret`. Salve essas credenciais em um local seguro, preferencialmente um Cofre de senhas.

## Autenticação

Com o Client ID e Client Secret obtido, você precisa fazer uma requisição para o nosso endpoint de autorização no Login API, segue abaixo:

### Produção

`POST https://login-api.transfeera.com/authorization`

### Sandbox

`POST https://login-api-sandbox.transfeera.com/authorization`

Com o seguinte payload

```text
{
  "grant_type": "client_credentials",
  "client_id": "yourClientId",
  "client_secret": "yourClientSecret"
}
```

O retorno dessa request vai ser um access token junto com o tempo de expiração do token

```text
{
  "access_token": "theTokenForAuthorization",
  "expires_in": 1800 # the access token expiration time in seconds
}
```

O token de acesso obtido é o token que você precisa passar no Header de todas as requests subsequentes, como abaixo:

```text
Authorization: {accessToken}
```

Todas as nossas requests são criptografadas, não aceitamos requests usando o protocolo HTTP, só HTTPS.

## Conta Certa

Segue abaixo a URL base da nossa API:

### Produção

`https://contacerta-api.transfeera.com`

### Sandbox

`https://contacerta-api-sandbox.transfeera.com`

Todas as requests para a API da Transfeera deve conter o Header "User-Agent". Use este Header para nos dizer qual o nome da sua empresa e um e-mail para contato. Segue abaixo um padrão de exemplo:

```text
User-Agent: Company (contact@company.com)
```

