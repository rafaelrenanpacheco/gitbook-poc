# Erros

Os erros listados abaixo são agrupados por contexto e pode ser apresentado em situações diversas. O erro contêm:

* **errorCode**: O código começa com as iniciais do contexto, por exemplo: DBA\_1 na qual pertence ao contexto de DBA.
* **message**: A mensagem de erro.
* **field**: Informações adicionais.
* **variable**: Informações adicionais.
* **data**: Informações adicionais.

## Exemplo de response

```text
{
  data: {
    maxLength: 8,
    minLength: 7
  },
  error: "Bad Request",
  errorCode: "DBA_6",
  field: "account",
  message: "Account is required and must have between 7 and 8 numbers (Agency: 0001 / Account: 111111 / Value: 10)",
  statusCode: 400
}
```

## Validações

| Código | Mensagem |
| :--- | :--- |
| CCE\_1 | Micro deposit is not allowed for your account ⚠  |
| CCE\_2 | Specify the micro deposit value is not allowed for your account ⚠  |
| CCE\_3 | Description is only allowed in Pix validations ⚠  |
| CCE\_4 | Pix description can not be greater than 140 characters |
| CCE\_5 | The Pix description cannot contain unsafe html tags |

{% hint style="warning" %}
Para habilitar este recurso é só entrar em contato com o nosso suporte pelo email [suporte@transfeera.com](mailto:suporte@transfeera.com)
{% endhint %}

## Destination Bank Account

<table>
  <thead>
    <tr>
      <th style="text-align:left">C&#xF3;digo</th>
      <th style="text-align:left">Mensagem</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">DBA_1</td>
      <td style="text-align:left">D&#xED;gito da ag&#xEA;ncia &#xE9; obrigat&#xF3;rio e deve ser num&#xE9;rico
        ou x</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_2</td>
      <td style="text-align:left">D&#xED;gito da conta &#xE9; obrigat&#xF3;rio e deve ser num&#xE9;rico
        ou x</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_3</td>
      <td style="text-align:left">Ag&#xEA;ncia deve ser 1&quot; or &quot;Ag&#xEA;ncia inv&#xE1;lida</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_4</td>
      <td style="text-align:left">Ag&#xEA;ncia &#xE9; obrigat&#xF3;ria e deve conter no m&#xE1;ximo n&#xFA;meros</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_5</td>
      <td style="text-align:left">D&#xED;gito da ag&#xEA;ncia deve ter apenas 1 d&#xED;gito</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_6</td>
      <td style="text-align:left">Conta &#xE9; obrigat&#xF3;ria e deve conter no m&#xE1;ximo n&#xFA;meros</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_7</td>
      <td style="text-align:left">Conta &#xE9; obrigat&#xF3;ria e deve conter entre e n&#xFA;meros</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_8</td>
      <td style="text-align:left">D&#xED;gito da Conta &#xE9; obrigat&#xF3;rio e deve ter apenas 1 d&#xED;gito</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_9</td>
      <td style="text-align:left">Conta do banco &#xE9; obrigat&#xF3;ria e deve conter exatamente n&#xFA;meros</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_10</td>
      <td style="text-align:left">Tipo de conta inv&#xE1;lido&quot;, &quot;Tipo da conta inv&#xE1;lido.&quot;
        or &quot;Tipo da conta do favorecido inv&#xE1;lido.</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_11</td>
      <td style="text-align:left">
        <p>Tipo de conta &apos;Entidade p&#xFA;blica&apos; &#xE9; dispon&#xED;vel
          somente para CNPJ</p>
        <p>Tipo de conta &apos;Entidade p&#xFA;blica&apos; s&#xF3; permite pessoa
          jur&#xED;dica.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_12</td>
      <td style="text-align:left">
        <p>Documento do favorecido n&#xE3;o &#xE9; um CPF nem CNPJ&quot;, &quot;CPF/CNPJ
          &#xE9; obrigat&#xF3;rio</p>
        <p>Documento n&#xE3;o &#xE9; um CPF ou CNPJ</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_13</td>
      <td style="text-align:left">
        <p>O CPF ou CNPJ est&#xE1; bloqueado</p>
        <p>Documento est&#xE1; bloqueado</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_15</td>
      <td style="text-align:left">O nome &#xE9; obrigat&#xF3;rio</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_19</td>
      <td style="text-align:left">D&#xED;gito da Ag&#xEA;ncia n&#xE3;o &#xE9; v&#xE1;lido</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_20</td>
      <td style="text-align:left">
        <p>Conta ou d&#xED;gito verificador da conta inv&#xE1;lido.</p>
        <p>D&#xED;gito verificador da conta inv&#xE1;lido.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_21</td>
      <td style="text-align:left">Conta inv&#xE1;lida.</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_22</td>
      <td style="text-align:left">Ag&#xEA;ncia n&#xE3;o existe</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_23</td>
      <td style="text-align:left">Documento n&#xE3;o existe</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_24</td>
      <td style="text-align:left">Nome informado n&#xE3;o coincide com o nome no Documento</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_26</td>
      <td style="text-align:left">Conta inv&#xE1;lida. O inicio da conta n&#xE3;o &#xE9; reconhecido como
        um tipo v&#xE1;lido.</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_27</td>
      <td style="text-align:left">CNPJ inv&#xE1;lido</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_28</td>
      <td style="text-align:left">CPF inv&#xE1;lido</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_29</td>
      <td style="text-align:left">Ag&#xEA;ncia, tipo da conta, conta ou d&#xED;gito verificador da conta
        inv&#xE1;lido.</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_30</td>
      <td style="text-align:left">
        <p>Ag&#xEA;ncia, Conta ou d&#xED;gito verificador da conta inv&#xE1;lido.</p>
        <p>Ag&#xEA;ncia, conta ou d&#xED;gito verificador da conta inv&#xE1;lido.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_33</td>
      <td style="text-align:left">Bank Code is required and must have a maximum of 3 numbers</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_34</td>
      <td style="text-align:left">This banking institution is not eligible to receive payments</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_35</td>
      <td style="text-align:left">The name must have at least 3 characters</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_41</td>
      <td style="text-align:left">Bank ISPB is required and must have exactly 8 numbers</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_42</td>
      <td style="text-align:left">This banking institution is not eligible to receive payments</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_44</td>
      <td style="text-align:left">Destination Bank Account was provided with bank code and ISPB, please
        provide only one bank info</td>
    </tr>
    <tr>
      <td style="text-align:left">DBA_45</td>
      <td style="text-align:left">Bank code or ISPB are required</td>
    </tr>
  </tbody>
</table>

