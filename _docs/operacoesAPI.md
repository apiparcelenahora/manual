---
title: Operações API
description: Descrição das operações possíveis com o uso da API
---

# Operações - API's Parceiros

Conforme orientação apresentada em [Arquitetura da Integração]({{ site.baseurl }}/introducao/#arquitetura-da-integração), as operações executadas em nossas API's, devem seguir a combinação URL base + endpoint da operação desejada.

# API: ConsultarDebito

A API consultar débitos, tem como objetivo realizar a consulta nos principais órgãos públicos do país. É a partir dessa API que os dados dos veículos, imóveis e etc.. são enviados para que se seja identificado os débitos do veículo/imóvel.

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v1/ConsultaDebito
        </code> Método de consulta de débitos </p>
</article>
</section>

## Corpo da requisição

Está API trabalha com um método POST, formado por 10 campos:

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

# API: CotacaoDebito

A API cotação débito, tem como objetivo consultar a simulação de valores para parcelamento (pagamento). É a partir dessa API que os dados referentes ao pedido, quantidade de parcelas e débitos selecionados são enviados para que seja determinado o valor a ser cobrado do cliente/consumidor.

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v1/CotacaoDebito
        </code> Consultar simulação de valores para parcelamento (pagamento) </p>
</article>
</section>

## Corpo da requisição

Está API trabalha com um método POST, formado por 3 campos:

```json
{
  "pedido": 0,
  "qtdParcelas": 0,
  "codFaturas": [0]
}
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`pedido`|Número de identificação do pedido.|**inteiro (int32)**|Sim|
|`qtdParcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**inteiro (int32)**|Sim|
|`codFaturas`|Número de identificação da fatura, pertencente ao pedido.|**Array de inteiros (int32)**|Não|

# Operação: Pagamento

A operação pagamento, tem como objetivo efetivar o pagamento via cartão de crédito. É a partir dessa operação que os dados referentes ao pedido (já cotado), bem como os dados de pagamento do cartão são enviados para efetivar o pagamento junto a operadora de cartão.

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v1/Pagamento
        </code> Método de consulta de débitos </p>
</article>
</section>

### Operação: ConsultarStatusPedido

A operação pagamento, tem como objetivo efetivar o pagamento via cartão de crédito. É a partir dessa operação que os dados referentes ao pedido (já cotado), bem como os dados de pagamento do cartão são enviados para efetivar o pagamento junto a operadora de cartão.

<section id="operacao">
<article class="get">
        <p>
        <code>
            <b>GET</b> /api/v1/Pagamento
        </code> Método de consulta de débitos (teste3)</p>
</article>
</section>