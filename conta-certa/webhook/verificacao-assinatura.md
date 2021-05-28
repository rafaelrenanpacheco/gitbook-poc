# Verificação da assinatura

Toda notificação que enviamos para o seu endpoint é assinada. Fazemos isso incluindo um header com o nome `Transfeera-Signature` em cada evento que enviamos. Isso permite verificar e garantir que o evento foi enviado pela Transfeera e não por um terceiro.

O header `Transfeera-Signature` contêm um timestamp e uma ou mais assinaturas. O timestamp é prefixado por `t=` e cada assinatura é prefixado por um schema. Schemas começam com `v` seguido de um integer. Atualmente existe apenas um schema de assinatura que é o `v1`.

Exemplo do header `Transfeera-Signature`:

```text
Transfeera-Signature: t=1580306324381,v1=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

Assinaturas são geradas usando uma mensagem baseada em hash com código de autenticação \(HMAC\) com SHA-256. Para prevenir ataques de reversão de versão \(downgrade attacks\), você deve ignorar todos os schemas que não são `v1`.

## Como validar a assinatura

### Passo 1: Extrair o timestamp e assinatura do Header

Faça um split no header usando o caractere `,` como separador para pegar a lista de elementos. Feito isso, faça outro split usando o caractere `=` como separador, para pegar o prefixo e o valor.

O valor obtido no prefixo `t` corresponde ao timestamp e o `v1` corresponde à assinatura. Você pode descartar outros valores.

### Passo 2: Preparar a string para comparar as assinaturas

Você deve concatenar essas informações:

* O timestamp \(como `string`\)
* O caractere `.`
* O payload JSON \(corpo da request, em formato de `string`\)

Computar o HMAC com a função hash SHA256. Use o **secret recebido na hora da criação do webhook** e use a string `signed_payload` como mensagem.

Exemplo em Node.js:

```javascript
const crypto = require('crypto');

const secretKey = 'my-secret'; // Essa secret não é a secret do token de autenticação, é a secret recebida na hora da criação do webhook através do POST /webhook
const ts = 1580306991086; // This is the "t" value received on Transfeera-Signature header
const requestPayload = {
  testing: true,
  someString: 'string-value'
};

const signed_payload = `${ts}.${JSON.stringify(requestPayload)}`;

const signature = crypto
  .createHmac('sha256', secretKey)
  .update(signed_payload)
  .digest('hex');

console.log(signature);
// Output: 348a92ec7864e30fc9cf3ea91b2e6e1392a14c8379103cb1d8e48e39334a4fd8
```

### Passo 3: Comparar as assinaturas

Compare a assinatura enviada pela Transfeera no header com a assinatura que você gerou no **Passo 2**.

Exemplo em Node.js:

```javascript
// Comparando assinaturas
// Exemplo do Header da requisição enviada pela Transfeera:
const requestHeaders = {
  'Transfeera-Signature': 't=1580306991086,v1=348a92ec7864e30fc9cf3ea91b2e6e1392a14c8379103cb1d8e48e39334a4fd8'
}

// Extraia o valor de 't' do Header 'Transfeera-Signature'
const reqTimestamp = requestHeaders['Transfeera-Signature'].split(',')[0].split('=')[1]; // '1580306991086'

// Extraia o valor de 'v1' do Header 'Transfeera-Signature'
const reqSignature = requestHeaders['Transfeera-Signature'].split(',')[1].split('=')[1]; // '348a92ec7864e30fc9cf3ea91b2e6e1392a14c8379103cb1d8e48e39334a4fd8'

// A Assinatura que você gerou no Passo 2 deve ser igual ao valor da variável "reqSignature".
console.log('yourSignature' === reqSignature); // Deve retornar verdadeiro
```

