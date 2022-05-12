---
title: Operações API
description: Descrição das operações possíveis com o uso da API
---

# Operações - API's Parceiros

Conforme orientação apresentada em [Arquitetura da Integração]({{ site.baseurl }}/introducao/#arquitetura-da-integração), as operações executadas em nossas API's, devem seguir a combinação URL base + endpoint da operação desejada.

# API: ConsultarDebito

A API consultar débitos, tem como objetivo realizar a consulta nos principais órgãos públicos do país. É a partir dessa API que os dados dos veículos, imóveis e etc.. são enviados para que se seja identificado os débitos do veículo/imóvel.

Está API opera com uma requisição POST, formada por 10 campos.

## Requisição POST - ConsultaDebito

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v2/ConsultaDebito
        </code> Método de consulta de débitos </p>
</article>
</section>

## Corpo da requisição - ConsultaDebito


1. JSON
```json
{
  "cpf": "string",
  "uf": "string",
  "placa": "string",
  "renavam": "string",
  "inscricaoImovel": "string",
  "numeroGuia": "string",
  "numeroLancamento": "string",
  "numeroParcelamento": "string",
  "numeroCDA": "string",
  "tipoDebito": 0
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/ConsultaDebito' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "cpf": "string",
  "uf": "string",
  "placa": "string",
  "renavam": "string",
  "inscricaoImovel": "string",
  "numeroGuia": "string",
  "numeroLancamento": "string",
  "numeroParcelamento": "string",
  "numeroCDA": "string",
  "tipoDebito": 0
}'
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`cpf`|Cpf do titular do débito.|**string**|Não|
|`uf`|UF a qual pertence o débito.|**string**|Não|
|`placa`|Placa identificadora do veículo.|**string**|Não|
|`renavam`|Renavam identificador do veículo.|**string**|Não|
|`inscricaoImovel`|Numeração referente a identificação do imóvel junto a fazenda. | **string** |Não|
|`numeroGuia`|Número de identificação da guia de pagamento.|**string**|Não|
|`numeroLancamento`|Número de identificação do lançamento.|**string**|Não|
|`numeroParcelamento`|Número do parcelamento junto ao órgão.|**string**|Não|
|`numeroCDA`|Número de identificação da dívida junto ao governo.|**string**|Não|
|`tipoDebito`|Número de identificação do pagamento na adquirente.|**enum** (Array [7]) |Sim|

## Exemplo de aplicação da requisição - ConsultaDebito

```
 {
  "Cpf": "00000000000",
  "Uf": "GO",
  "Placa": "jkt3433",
  "Renavam": "928392818"
}
```

# API: CotacaoDebito

A API cotação débito, tem como objetivo consultar a simulação de valores para parcelamento (pagamento). É a partir dessa API que os dados referentes ao pedido, quantidade de parcelas e débitos selecionados são enviados para que seja determinado o valor a ser cobrado do cliente/consumidor.

Está API opera com uma requisição POST, formada por 3 campos.

## Requisição POST - CotacaoDebito

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v2/CotacaoDebito
        </code> Consultar simulação de valores para parcelamento (pagamento) </p>
</article>
</section>

## Corpo da requisição - CotacaoDebito

1. JSON
```json
{
  "pedido": 0,
  "qtdParcelas": 0,
  "codFaturas": [0]
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/CotacaoDebito' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "pedido": 1000,
  "qtdParcelas": 2,
  "codFaturas": [
    0
  ]
}'
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`pedido`|Número de identificação do pedido.|**integer (int32)**|Sim|
|`qtdParcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**integer (int32)**|Sim|
|`codFaturas`|Número de identificação da fatura, pertencente ao pedido.|**Array de integers (int32)**|Não|

## Exemplo de aplicação da requisição - CotacaoDebito

```
{
 "Pedido": 3453,
 "QtdParcelas": 2,
 "CodFaturas": [1,2,3,4]
}
```

# API: Fatura

A API Fatura, tem como objetivo atualizar o status de uma dada fatura, pertencente a um pedido. 

Está API opera com uma requisição POST, formada por 4 campos.

## Requisição POST - AtualizarLiquidacao

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v2/AtualizarLiquidacao
        </code> Método de consulta de fatura </p>
</article>
</section>

## Corpo da requisição - AtualizarLiquidacao

1. JSON
```json
{
  "cod_Fat": 0,
  "autenticacao": "string",
  "bancoLiquidacao": "string",
  "dataLiquidacao": "2022-05-12T14:31:49.439Z"
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/Fatura/AtualizarLiquidacao' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "cod_Fat": 0,
  "autenticacao": "string",
  "bancoLiquidacao": "string",
  "dataLiquidacao": "2022-05-12T14:31:49.439Z"
}'
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`cod_Fat`|Número de identificação da fatura (código).|**integer (int32)**|Sim|
|`autenticacao`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**string**|Não|
|`bancoLiquidacao`|Identificação do banco onde foi efetuada a liquidação (nome do banco).|**string**|Não|
|`dataLiquidacao`|Número de identificação da fatura, pertencente ao pedido.|**string (%date-time)**|Não|

## Exemplo de aplicação da requisição - AtualizarLiquidacao

```
{
  "Cod_fat": 3453,
  "Autenticacao": "JASDASDJASJDAJSD",
  "BancoLiquidacao": "ITAU SA",
  "DataLiquidacao": "2022-04-29"
}
```

# API: Pagamento

A API pagamento, trabalha com 3 requisições,possuindo como objetivo efetivar o pagamento via cartão de crédito e realizar consultas. É a partir dessa operação que os dados referentes ao pedido (já cotado), bem como os dados de pagamento do cartão são enviados para efetivar o pagamento junto a operadora de cartão.

## Requisição POST - Pagamento

Está requisição é formada por 12 campos.

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v2/Pagamento
        </code> Permite o pagamento da dívida </p>
</article>
</section>

### Corpo da requisição - Pagamento

1. JSON
```json
{
  "cdFaturas": [
    "string"
  ],
  "parcelas": "string",
  "valorPagCartao": "string",
  "valorWynk": "string",
  "email": "string",
  "celular": "string",
  "securityCode": "string",
  "creditCardNumber": "string",
  "monthYear": "string",
  "holderName": "string",
  "cpfcnpj": "string",
  "telefone": "string"
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/Pagamento' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "cdFaturas": [
    "string"
  ],
  "parcelas": "string",
  "valorPagCartao": "string",
  "valorWynk": "string",
  "email": "string",
  "celular": "string",
  "securityCode": "string",
  "creditCardNumber": "string",
  "monthYear": "string",
  "holderName": "string",
  "cpfcnpj": "string",
  "telefone": "string"
}'
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`cdFaturas`|Numeração identificadora da fatura.|**Array de string's**|Não|
|`parcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**string**|Não|
|`valorPagCartao`|Valor pago pelo cliente ao final de sua cotação (valor total).|**string**|Não|
|`valorWynk`|Valor pago pelo cliente a partir da Wynk.|**string**|Não|
|`email`|Endereço de e-mail para cobrança do cartão do cliente. | **string** |Não|
|`celular`|Número de telefone(celular) do cliente.|**string**|Não|
|`securityCode`|Código de segurança do cartão do cliente.|**string**|Não|
|`creditCardNumber`|Numeração do cartão do cliente.|**string**|Não|
|`monthYear`|Mês e ano do vencimento do cartão do cliente.|**string**|Não|
|`holderName`|Nome do portador do cartão.|**string**|Não|
|`cpfcnpj`|CPF ou CNPJ do portado do cartão.|**string**|Não|
|`telefone`|Número de telefone do cliente.|**string**|Não|

## Exemplo de aplicação da requisição - Pagamento

```
{
 "cdFaturas": [1,2,3,4],
 "parcelas": "2",
 "valorPagCartao": "12.00",
 "valorWynk": "12.00",
 "email": "wynk@gmail.com",
 "celular": "61992234523",
 "securityCode": "123123123",
 "creditCardNumber": "4534534",
 "monthYear": "092022",
 "holderName": "holder name",
 "cpfcnpj": "02321123422"
 "telefone": "61899234864",
}
```

## Requisição GET - ConsultarStatusPedido

Essa requisição é composta por um único parâmetro e tem como objetivo consultar o código de barra de uma dada fatura. 

<section id="operacao">
<article class="get">
        <p>
        <code>
            <b>GET</b> /api/v2/Pagamento/ConsultarStatusPedido
        </code> Consultar o status do pedido</p>
</article>
</section>

### Exemplo da requisição - ConsultarStatusPedido

1. Curl
```
curl -X 'GET' \
  'https://api.parcelenahora.com.br/api/v2/Pagamento/ConsultarStatusPedido' \
  -H 'accept: application/json'
```

2. Request URL
```
https://api.parcelenahora.com.br/api/v2/Pagamento/ConsultarStatusPedido
```

3. JSON
```
{
  "CodigoPedido": 4
}
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`CodigoPedido`|Numeração identificadora do pedido.|**integer (int32)**|Não|

## Requisição GET - BuscarCodBarraFatura

Essa requisição é composta por um único parâmetro e tem como objetivo consultar o código de barra de uma dada fatura. 

<section id="operacao">
<article class="get">
        <p>
        <code>
            <b>GET</b> /api/v2/Pagamento/BuscarCodBarraFatura
        </code> Buscar o codigo de Barra da Fatura</p>
</article>
</section>

### Exemplo da requisição - BuscarCodBarraFatura

1. Curl
```
curl -X 'GET' \
  'https://api.parcelenahora.com.br/api/v2/Pagamento/BuscarCodBarraFatura?CodigoFatura=2' \
  -H 'accept: */*'
```

2. Request URL
```
https://api.parcelenahora.com.br/api/v2/Pagamento/BuscarCodBarraFatura?CodigoFatura=2
```

3. JSON
```
{
  "CodigoFatura": 2
}
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`CodigoFatura`|Numeração identificadora da fatura.|**integer (int32)**|Não|
