# Banks

## Endpoints

{% api-method method="get" host="https://contacerta-api.transfeera.com" path="/bank" %}
{% api-method-summary %}
buscar bancos
{% endapi-method-summary %}

{% api-method-description %}
Por padrão será retornado apenas bancos onde é possível fazer liquidação via TEV e TED. Para obter uma lista de bancos e instituições de pagamentos onde é possível liquidar via Pix informe o query param `?pix=true`.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="pix" type="string" required=false %}
Buscar bancos que permitem liquidação via Pix
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "code": "033",
    "name": "Santander",
    "ispb": "90400888",
    "spi_participant_type": "DIRETO",
    "image": "https://cdn.transfeera.com/banks/santander.svg"
  },
  {
    "code": "041",
    "name": "Banrisul",
    "ispb": "92702067",
    "spi_participant_type": "DIRETO",
    "image": "https://cdn.transfeera.com/banks/banrisul.png"
  },
  {
    "code": "001",
    "name": "Banco do Brasil",
    "ispb": "00000000",
    "spi_participant_type": "DIRETO",
    "image": "https://cdn.transfeera.com/banks/bb.svg"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

