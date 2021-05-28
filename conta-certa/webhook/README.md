---
description: >-
  Com webhooks você pode inscrever uma URL da sua aplicação que esteja
  disponível para a internet, para receber notificações referentes a mudanças de
  status de pagamento na Transfeera.
---

# Webhook

## Eventos

Todos os eventos são enviados através de uma requisição HTTP/HTTPS `POST` com o formato JSON no payload.

Seu endpoint precisa retornar um status code de sucesso na resposta, sendo \(`2xx`\) um formato válido, assim consideraremos como entregue. Caso contrário, vamos retentar entregar a notificação mais 2 vezes, depois disso, não vamos mais tentar entregar a notificação deste evento.

O exemplo abaixo é um exemplo de um payload de evento que enviamos.

### Transfer

```javascript
{
  "id": "7d3aae40-6655-4d9a-801b-d0ab7ae906d7", // Event ID
  "version": "v1",                              // Event payload schema version
  "object": "Transfer",                         // Event object type
  "date": "2019-10-01T17:54:39.000Z",           // Event date and time
  "data": {                                     // Event Payload
    "id": "367997",                             // Payment ID
    "status": "TRANSFERIDO",                    // Payment status
    "status_description": null,                 // Payment status description
    "integration_id": null                      // Payment Integration ID
  }
}
```

### CashIn

```javascript
{
  "id": "7d3aae40-6655-4d9a-801b-d0ab7ae906d7",   // Event ID
  "version": "v1",                                // Event payload schema version
  "object": "CashIn",                             // Event object type
  "date": "2019-10-01T17:54:39.000Z",             // Event date and time
  "data": {                                       // Event Payload
    "id": "7d3aae40-6655-4d9a-801b-d0ab7ae906d7", // CashIn ID
    "value": 50.54,                               // CashIn value
    "end2end_id": "E12345asdf123",                // Cashin end2end ID
    "txid": "abc123",                             // CashIn QRCode txid
    "integration_id": "abc123",                   // CashIn QRCode integration id
    "pix_key": "pix@transfeera.com",              // CashIn receiver pix key
    "payer": {
      "name": "João da Silva",                    // CashIn payer name
      "document": "12312312355",                  // CashIn payer document (CPF / CNPJ)
      "account_type": "CONTA_CORRENTE",           // CashIn payer account type ("CONTA_CORRENTE" or "CONTA_POUPANCA")
      "account": "12345",                         // CashIn payer account number
      "account_digit": "9",                       // CashIn payer account number verification digit
      "agency": "4321",                           // CashIn payer account agency
      "bank": {
        "name": "Banco do Brasil",                // CashIn payer bank name
        "code": "001",                            // CashIn payer bank code
        "ispb": "00000000"                        // CashIn payer bank ISPB code
      }
    }
  }
}
```

### CashInRefund

```javascript
{
  "id": "7d3aae40-6655-4d9a-801b-d0ab7ae906d7",   // Event ID
  "version": "v1",                                // Event payload schema version
  "object": "CashInRefund",                       // Event object type
  "date": "2019-10-01T17:54:39.000Z",             // Event date and time
  "data": {                                       // Event Payload
    "id": "7d3aae40-6655-4d9a-801b-d0ab7ae906d7", // CashInRefund ID
    "status": "DEVOLVIDO",                        // CashInRefund status ("DEVOLVIDO" or "NAO_REALIZADO")
    "value": 50.54,                               // CashInRefund value
    "original_end2end_id": "E12345asdf123",       // CashIn original end2end ID
    "return_id": "R12345asdf123",                 // CashInRefund end2end ID
    "integration_id": "abc123",                   // CashInRefund integration id
    "receiver": {
      "name": "João da Silva",                    // CashInRefund receiver name
      "document": "12312312355",                  // CashInRefund receiver document (CPF / CNPJ)
      "account_type": "CONTA_CORRENTE",           // CashInRefund receiver account type ("CONTA_CORRENTE" or "CONTA_POUPANCA")
      "account": "12345",                         // CashInRefund receiver account number
      "account_digit": "9"                        // CashInRefund receiver account number verification digit
      "agency": "4321",                           // CashInRefund receiver account agency
      "bank": {
        "name": "Banco do Brasil",                // CashInRefund receiver bank name
        "code": "001",                            // CashInRefund receiver bank code
        "ispb": "00000000"                        // CashInRefund receiver bank ISPB code
      }
    }
  }
}
```

## Endpoints

{% api-method method="get" host="https://contacerta-api.transfeera.com" path="/webhook" %}
{% api-method-summary %}
consultar URLs
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "id": "05fedf85-6425-4ed1-a397-1817b7fa3760",
    "company_id": "4c0c8cf2-25d1-4deb-bb05-3f64789c3761",
    "url": "https://your-webhook-url",
    "object_types": ["Transfer"], // "Transfer", "CashIn", "CashInRefund"
    "schema_version": "v1",
    "signature_secret": "5d55729305b197168018fcff2a18e99f78ab8dd4efd03b6e895cf08bf104bca204944e45", // Chave usada para validação da assinatura enviada no header da notificação
    "created_at": "2019-09-30T20:38:11.000Z",
    "updated_at": "2019-09-30T20:38:11.069Z",
    "deleted_at": null
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://contacerta-api.transfeera.com" path="/webhook" %}
{% api-method-summary %}
cadastrar URL
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="url" type="string" required=true %}
Sua URL que iremos chamar
{% endapi-method-parameter %}

{% api-method-parameter name="object\_types" type="array" required=true %}
\["Transfer", "CashIn", "CashInRefund"\]
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": "5211e1a1-77a6-4662-80e0-8b9b98068ace",
  "signature_secret": "5d55729305b197168018fcff2a18e99f78ab8dd4efd03b6e895cf08bf104bca204944e45" // chave usada para validação da assinatura enviada no header da notificação
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Nós vamos testar este endpoint com uma requisição `POST` e com o payload `{ "test": true }` para verificar se existe comunicação.

{% hint style="info" %}
Você pode criar URLs com query params, e com isso adicionar um token para verificação interna, garantindo a segurança da comunicação.
{% endhint %}

{% api-method method="put" host="https://contacerta-api.transfeera.com" path="/webhook/:id" %}
{% api-method-summary %}
atualizar URL
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID do webhook
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="url" type="string" required=true %}
Sua nova URL que iremos chamar
{% endapi-method-parameter %}

{% api-method-parameter name="object\_types" type="string" required=true %}
\["Transfer", "CashIn", "CashInRefund"\]
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Nós vamos testar este endpoint com uma requisição `POST` e com o payload `{ "test": true }` para verificar se existe comunicação.

{% api-method method="delete" host="https://contacerta-api.transfeera.com" path="/webhook/:id" %}
{% api-method-summary %}
remover URL
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID do webhook
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



