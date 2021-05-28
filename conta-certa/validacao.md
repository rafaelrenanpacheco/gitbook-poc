# Validação

## Tipos de conta suportados

* CONTA\_CORRENTE
* CONTA\_POUPANCA
* CONTA\_FACIL: "conta fácil" conta para a Caixa Econômica e Banco do Brasil
* ENTIDADES\_PUBLICAS: "entidades públicas" tipo de conta para a Caixa Econômica

## Código do banco

Use o código bancário fornecido pela Febraban. Acesso a lista completa em [https://www.codigobanco.com/](https://www.codigobanco.com/).

{% api-method method="post" host="https://contacerta-api.transfeera.com" path="/validate" %}
{% api-method-summary %}
validar dados
{% endapi-method-summary %}

{% api-method-description %}
Você pode validar os dados usando dois tipos de validações, **validação básica** e **validação com micro-depósito**.  
  
A validação básica vamos identificar padrões matemáticos na conta bancária para garantir que o documento, dígito da conta, tipo da conta, agência e banco estão corretos.  
  
A validação com micro depósito vamos enviar `R$ 0,01` \(ou o valor informado no campo `micro_deposit_value`\) na conta do recebedor para garantir que ela está ativa, pode receber dinheiro e pertence ao documento \(CPF/CNPJ\) informando.  
  
A validação com micro depósito é obrigatório o uso de webhooks, pois este é o único meio para você receber a resposta da validação.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="type" type="string" required=false %}
BASICA _\(default\)_ \| MICRO\_DEPOSITO
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
Nome do destinatário
{% endapi-method-parameter %}

{% api-method-parameter name="cpf\_cnpj" type="string" required=true %}
CPF ou CNPJ
{% endapi-method-parameter %}

{% api-method-parameter name="bank\_code" type="string" required=true %}
Código do banco
{% endapi-method-parameter %}

{% api-method-parameter name="agency" type="string" required=true %}
Número da agência
{% endapi-method-parameter %}

{% api-method-parameter name="agency\_digit" type="string" required=true %}
Dígito verificador da agência
{% endapi-method-parameter %}

{% api-method-parameter name="account" type="string" required=true %}
Número da conta
{% endapi-method-parameter %}

{% api-method-parameter name="account\_digit" type="string" required=true %}
Dígito da conta
{% endapi-method-parameter %}

{% api-method-parameter name="account\_type" type="string" required=true %}
CONTA\_CORRENTE \| CONTA\_POUPANCA
{% endapi-method-parameter %}

{% api-method-parameter name="integration\_id" type="string" required=true %}
ID de integração
{% endapi-method-parameter %}

{% api-method-parameter name="micro\_deposit\_value" type="number" required=true %}
Valor do micro-depósito
{% endapi-method-parameter %}

{% api-method-parameter name="pix\_description" type="string" required=true %}
Descrição para micro-depósito utilizando Pix
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**Validação básica**  
Você vai receber o mesmo dado que você enviou para validação como resposta, com o id da validação e um objeto adicional \_validation, que vai incluir o resultado da validação e possíveis sugestões se disponível.  
  
**Validação com micro-depósito**  
O resultado da validação será enviado para o webhook configurado. A resposta da requisição vai conter o ID da validação para identificar na notificação que irá ser enviado através do webhook.
{% endapi-method-response-example-description %}

{% tabs %}
{% tab title="Básica com sucesso" %}
```javascript
{
  "id": "d23a875e-ad1c-4571-a582-1940b87c76af",
  "name": "José da Silva",
  "cpf_cnpj": "55998432118",
  "bank_code": "033",
  "agency": "1234",
  "agency_digit": "",
  "account": "123456",
  "account_digit": "3",
  "account_type": "CONTA_CORRENTE",
  "integration_id": "",
  "_validation": {
    "valid": true,
    "errors": []
  }
}
```
{% endtab %}

{% tab title="Básica com erros" %}
```javascript
{
  "id": "d23a875e-ad1c-4571-a582-1940b87c76af",
  "name": "José da Silva",
  "cpf_cnpj": "55998432118",
  "bank_code": "033",
  "bank_ispb": null,
  "agency": "1234",
  "agency_digit": "",
  "account": "123456",
  "account_digit": "3",
  "account_type": "CONTA_CORRENTE",
  "integration_id": "",
  "_validation": {
    "valid": false,
    "errors": [
      {
        "message": "Dígito da Agência não é válido",
        "field": "agency_digit",
        "suggestion": {
          "agency_digit": "4"
        },
        "errorCode": "DBA_19"
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Micro-depósito" %}
```javascript
{
  "id": "d23a875e-ad1c-4571-a582-1940b87c76af"
}
```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Também é possível informar o banco usando o ISPB pelo campo `bank_ispb`, nesse caso não informe o `bank_code`. O campo `bank_ispb` deve ser to tipo `string` e conter `8` caracteres. _OBS.: é obrigatório informar ao menos um dos campos_.

Todos os campos, exceto `integration_id`, `name`, `agency_digit`, `pix_description` e `micro_deposit_value` são **obrigatórios**.

O campo `micro_deposit_value` é opcional e permite informar valores entre `0.01` e `1.00`, caso não seja informado será utilizado o valor padrão de `0.01`, somente deve ser informado para validações do tipo `MICRO_DEPOSITO`.

O campo `pix_description` é opcional e possibilita o envio de uma descrição com limite de até 140 caracteres em validações Pix, somente deve ser informado para validações do tipo `MICRO_DEPOSITO`.

{% api-method method="get" host="https://contacerta-api.transfeera.com" path="/validation" %}
{% api-method-summary %}
consultar validações
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="initialDate" type="string" required=true %}
Data inicial \(YYYY-MM-DD\)
{% endapi-method-parameter %}

{% api-method-parameter name="endDate" type="string" required=true %}
Data final \(YYYY-MM-DD\)
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="string" required=true %}
Paginação, começando em 0 \(zero\)
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
BASICA \| MICRO\_DEPOSITO
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": [
    {
      "id": "8f9d9bb5-119e-4da8-bd50-3418d227c1d6",
      "type": "BASICA",
      "integration_id": null,
      "created_at": "2021-01-29T10:11:06.000Z",
      "pre_validated_at": null,
      "validated_at": "2021-01-29T10:11:06.000Z",
      "bank_code": "33",
      "bank_ispb": null,
      "valid": true,
      "errors": [],
      "receipt_url": null,
      "bank_receipt_url": null,
      "micro_deposit_status": null,
      "micro_deposit_value": null,
      "pix_description": null
    },
    {
      "id": "8f9d9bb5-119e-4da8-bd50-3418d227c1d6",
      "type": "BASICA",
      "integration_id": null,
      "created_at": "2021-01-29T10:11:06.000Z",
      "pre_validated_at": null,
      "validated_at": "2021-01-29T10:11:06.000Z",
      "bank_code": null,
      "bank_ispb": "00000000",
      "valid": true,
      "errors": [],
      "receipt_url": null,
      "bank_receipt_url": null,
      "micro_deposit_status": null,
      "micro_deposit_value": null,
      "pix_description": null
    },
    {
      "id": "464818ed-a3fa-4327-a36d-514a9b6ab755",
      "type": "MICRO_DEPOSITO",
      "integration_id": null,
      "created_at": "2021-01-29T10:10:22.000Z",
      "pre_validated_at": "2021-01-29T10:12:22.000Z",
      "validated_at": "2021-01-29T15:02:22.000Z",
      "bank_code": "33",
      "bank_ispb": null,
      "valid": true,
      "errors": [],
      "receipt_url": "https://",
      "bank_receipt_url": "https://",
      "micro_deposit_status": "VALIDADO",
      "micro_deposit_value": null,
      "pix_description": null
    }
  ],
  "metadata": {
    "pagination": {
      "itemsPerPage": 45,
      "totalItems": 2
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://contacerta-api.transfeera.com" path="/validation/:id" %}
{% api-method-summary %}
consultar validação
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID da validação
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": "464818ed-a3fa-4327-a36d-514a9b6ab755",
  "type": "MICRO_DEPOSITO",
  "integration_id": null,
  "created_at": "2021-01-29T10:10:22.000Z",
  "pre_validated_at": "2021-01-29T10:12:22.000Z",
  "validated_at": "2021-01-29T15:02:22.000Z",
  "bank_code": "33",
  "bank_ispb": null,
  "valid": true,
  "errors": [],
  "receipt_url": "https://",
  "bank_receipt_url": "https://",
  "micro_deposit_status": "VALIDADO",
  "micro_deposit_value": null,
  "pix_description": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Detalhes da response

O objeto a seguir descreve os campos utilizados na response dos endpoints de [consulta de validações](validacao.md#consultar-validacoes) e [consulta de validação](validacao.md#consultar-validacao):

```javascript
{
  "id": "8f9d9bb5-119e-4da8-bd50-3418d227c1d6", // ID da validação
  "type": "BASICA",                             // Tipo de validação BASICA ou MICRO_DEPOSITO
  "integration_id": null,                       // Integration ID (Caso disponível)
  "created_at": "2021-01-29T10:11:06.000Z",     // Data de criação da validação
  "pre_validated_at": null,                     // Data em que foi realizada a pré validação (Caso disponível)
  "validated_at": "2021-01-29T10:11:06.000Z",   // Data em que a validação foi realizada (Caso disponível)
  "bank_code": "33"                             // ou null, código do banco informado no request da validação (Caso tenha sido informado no momento da validação, caso contrário será retornado como null)
  "bank_ispb": "00000000"                       // ou null, ISPB da instituição informado no request da validação (Caso tenha sido informado no momento da validação, caso contrário será retornado como null)
  "valid": true,                                // Indica se a conta é válida, caso seja null a validação ainda não foi finalizada
  "errors": [],                                 // Lista de erros caso exista algum (ver seção de erros)
  "receipt_url": null,                          // URL do recibo da Transfeera (Caso disponível)
  "bank_receipt_url": null,                     // URL do recibo do banco (Caso disponível)
  "micro_deposit_status": null,                 // Status da validação do tipo MICRO_DEPOSITO (Veja abaixo)
  "micro_deposit_value": null                   // Valor do micro depósito informado no request da validação (Somente para o tipo MICRO_DEPOSITO),
  "pix_description": null                       // Descrição informada no pagamento Pix da validação (Somente para o tipo MICRO_DEPOSITO)
}
```

## Status do micro-depósito

Segue abaixo os status possíveis para um micro depósito:

* **PRE\_VALIDADO\_NO\_BANCO**: O Micro Depósito foi pré validado no banco, isso significa que enviamos o pagamento para o banco. Ainda não é 100% de certeza que a conta está aberta e válida, o banco de destino as vezes retorna um erro tardio informando que a conta está bloqueada por exemplo.
* **VALIDADO**: O Micro Depósito foi enviado para o recebedor e em caso de sucesso validado que a conta está aberta, pode receber dinheiro e pertence ao documento informado. Você deve considerar o status VALIDADO para determinar se a conta está válida ou não. O Status `PRE_VALIDADO_NO_BANCO` tem um retorno mais rápido, mas em alguns casos pode ser um falso positivo.

{% hint style="warning" %}
Existem exceções onde mesmo depois de ser VALIDADO com sucesso o banco retornar o pagamento com falha. Neste caso um novo webhook vai ser enviado com o status atualizado.
{% endhint %}

