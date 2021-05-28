# Introduction

API de validação de dados bancários. Essa API fornece uma forma simples de você validar os dados bancários de um recebedor e também receber sugestões para correção de dados incorretos e também erros transparentes informando o exato problema da conta bancária.

O formato de comunicação dos dados é em JSON. Cada requisição que é feito com os métodos do HTTP `POST` ou `PUT` precisa ter o Header `Content-Type: application/json`.

Se você tiver qualquer problema com nossa API, acesse a nossa Status Page [https://status.transfeera.com/](https://status.transfeera.com/) para acompanhar os incidentes e manutenções agendadas. Caso não tenha nenhum incidente relatado, contate diretamente o nosso suporte pelo e-mail `suporte@transfeera.com`.

## Acesso a Sandbox

O ambiente de Sandbox é usado para testar a integração com a API da Transfeera antes de ir para produção. As APIs deste ambiente são as mesmas de produção. Existe uma particularidade em casos de validações com Micro Depósito onde precisamos acompanhar o processo manualmente para testar o fluxo por completo, para isso, é só entrar em contato com o nosso suporte pelo email `suporte@transfeera.com`.

URL's de Sandbox:

* Login API: [https://login-api-sandbox.transfeera.com/](https://login-api-sandbox.transfeera.com/)
* API: [https://contacerta-api-sandbox.transfeera.com/](https://contacerta-api-sandbox.transfeera.com/)

URL's de Produção:

* Login API: [https://login-api.transfeera.com/](https://login-api.transfeera.com/)
* API: [https://contacerta-api.transfeera.com/](https://contacerta-api.transfeera.com/)

