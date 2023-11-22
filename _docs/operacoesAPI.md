---
title: Operações API
description: Descrição das operações possíveis com o uso da API
---

# Operações - API's Parceiros

Conforme orientação apresentada em [Arquitetura da Integração]({{ site.baseurl }}/introducao/#arquitetura-da-integração), as operações executadas em nossas API's, devem seguir a combinação URL base + endpoint da operação desejada.

# API: ConsultarDebito

A API consultar débitos, tem como objetivo realizar a consulta nos principais órgãos públicos do país. É a partir dessa API que os dados dos veículos, imóveis e etc.. são enviados para que se seja identificado os débitos do veículo/imóvel. Obtendo-se como resposta, os débitos e suas principais descrições.

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
  "iduser": 0,
  "inscricaoImovel": "string",
  "numeroGuia": "string",
  "numeroLancamento": "string",
  "numeroParcelamento": "string",
  "numeroCDA": "string",
  "tipoDebito": 0,
  "email": "string",
  "telefone": "string"
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/ConsultaDebito' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "cpf": "string",
  "uf": "string",
  "placa": "string",
  "renavam": "string",
  "iduser": 0,
  "inscricaoImovel": "string",
  "numeroGuia": "string",
  "numeroLancamento": "string",
  "numeroParcelamento": "string",
  "numeroCDA": "string",
  "tipoDebito": 0,
  "email": "string",
  "telefone": "string"
}'
```

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`cpf`|Cpf do titular do débito.|**string**|Sim|
|`uf`|UF a qual pertence o débito.|**string**|Sim|
|`placa`|Placa identificadora do veículo.|**string**|Sim|
|`renavam`|Renavam identificador do veículo.|**string**|Sim|
|`iduser`| ID identificador do usuário.|**integer (int32)**|Não|
|`inscricaoImovel`|Numeração referente a identificação do imóvel junto a fazenda. | **string** |Não|
|`numeroGuia`|Número de identificação da guia de pagamento.|**string**|Não|
|`numeroLancamento`|Número de identificação do lançamento.|**string**|Não|
|`numeroParcelamento`|Número do parcelamento junto ao órgão.|**string**|Não|
|`numeroCDA`|Número de identificação da dívida junto ao governo.|**string**|Não|
|`tipoDebito`|Número de identificação do pagamento na adquirente.|**enum** (Array [7]) |Não|
|`email`|Email válido de contato, do portador do cartão.|**string**|Sim|
|`telefone`|Número de telefone válido de contato, do portador do cartão.|**string**|Sim|

## Exemplo de aplicação da requisição - ConsultaDebito

```
 {
  "cpf": "12345678901",
  "uf": "DF",
  "placa": "AAA0123",
  "renavam": "12345678901",
  "inscricaoImovel": "",  
  "telefone":"61123456789",
  "email":"exemplo@exemplo.com"
}
```

## Resposta da requisição - ConsultaDebito

```json
{
  "success": true,
  "message": "string",
  "data": {
    "pedido": 0,
    "debitos": [
      {
        "codFatura": 0,
        "codDebito": 0,
        "codNsu": "string",
        "vencimento": "string",
        "valor": "string",
        "codBarras": "string",
        "exigivel": 0,
        "descricao": "string"
      }
    ]
  }
}
```

### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|---|
|`pedido`|Número identificador do pedido/consulta.|**integer (int32)**|
|`codFatura`|Código da fatura para pagamento do débito.|**integer (int32)**|
|`codDebito`|Código identificador do débito.|**integer (int32)**|
|`codNsu`|Número sequencial único para identificar a transação.|**string**|
|`vencimento`|Data de vencimento para pagamento do débito.|**string**|
|`valor`| Valor do débito.|**string**|
|`codBarras`|Código de barras para pagamento da fatura. | **string** |
|`descricao`|Descrição do débito a ser pago.|**string**|


### Schema

<p><img src="assets\imgs\retorno-consulta-debito-generic-result.png" class="schema" alt="imagem"></p>

<!-- ![imagem](assets\imgs\retorno-consulta-debito-generic-result.png) -->

# API: ConsultaPlaca

A API consulta placa, tem como objetivo consultar a existência de registro para placa informada pelo usuário. Em caso positivo, a API retorna os dados do veículo pertencente a placa. A partir desses dados, será possível realizar a consulta de débitos para o veículo, sem que o usuário precise inserir outras informações, além da placa.

Está API opera com uma requisição POST, formada por 1 campo.

## Requisição POST - ConsultaPlaca

<section id="operacao">
<article class="post">
        <p>
        <code>
            <b>POST</b> /api/v2/ConsultaPlaca
        </code> Método de consulta por Placa </p>
</article>
</section>

## Corpo da requisição - ConsultaPlaca

1. JSON
```json
{
  "placa": "string"
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/ConsultaPlaca' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "placa": "string"
}'
```

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`placa`|Placa identificadora do veículo.|**string**|Sim|

## Exemplo de aplicação da requisição - ConsultaPlaca

```
{
  "PLACA": "jkt3433"
}
```

## Resposta da requisição - ConsultaPlaca

```json
{
  "success": true,
  "message": "string",
  "data": {
    "solitacao": {
      "dado": "string",
      "numeroresposta": "string",
      "tempo": "string",
      "mensagem": "string",
      "horario": "string"
    },
    "resposta": {
      "placa": "string",
      "chassi": "string",
      "renavam": "string",
      "marcaModelo": "string",
      "ano_fabricacao": "string",
      "anoModelo": "string",
      "cor": "string",
      "combustivel": "string",
      "uf": "string"
    }
  }
}
```
### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|---|
|`placa`|Placa identificadora do veículo.|**string**|
|`chassi`|Numeração identificadora do chassi do veículo.|**string**|
|`renavam`|Renavam identificador do veículo.|**string**|
|`marcaModelo`|Modelo e marca do veículo.|**string**|
|`ano_fabricacao`|Ano de fabricação do veículo.|**string**|
|`anoModelo`|Ano do modelo do veículo.|**string**|
|`cor`|Cor original do veículo.|**string**|
|`combustivel`|Tipo de combustível utilizado no veículo.|**string**|
|`uf`|UF a qual pertence o veículo (varia de acordo com as transferências de UF).|**string**|

### Schema

<p><img src="assets\imgs\retorno-placa-generic-result.png" class="schema" alt="imagem"></p>

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
  "codFaturas": [0],
  "cBandeira":3
}
```
2. CURL
```json
curl -X 'POST' \
  'https://api.parcelenahora.com.br/api/v2/CotacaoDebito' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "pedido": 0,
  "qtdParcelas": 0,
  "codFaturas": [
    0
  ],
  "cBandeira": 3
}'
```

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`pedido`|Número de identificação do pedido.|**integer (int32)**|Sim|
|`qtdParcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**integer (int32)**|Sim|
|`codFaturas`|Número de identificação da fatura, pertencente ao pedido.|**Array de integers (int32)**|Sim|
|`cBandeira`|Identificador da bandeira, pertencente ao cartão utilizado na cotação.|**integer (int32)**|Não|

**OBS:** O parâmetro [cBandeira], embora seja opcional, deve sempre que possível ser preenchido. Caso o mesmo não seja, a API irá fornecer apenas as parcelas no intervalo de 1 a 12x. Atualmente, é possível alcançar um maior número de parcelas a depender da bandeira utilizada. Os valores atribúidos a esse parâmetro, devem seguir a tabela abaixo:

|cBandeira (valor)|Bandeira|Intervalo de Parcelas Retornadas|
|:----:|:----:|:----:|
|`3`| Visa | 1x a 24x|
|`2`| Mastercard| 1x a 21x|
|`1`| Todas as demas (default)| 1x a 12x|


## Exemplo de aplicação da requisição - CotacaoDebito

```
{
  "Pedido": 3453,
  "QtdParcelas": 2,
  "CodFaturas": [1,2,3,4]
}
```

## Resposta da requisição - CotacaoDebito

```json
{
  "success": true,
  "message": "string",
  "data": {
    "erros": [
      "string"
    ],
    "isValid": true,
    "messagem": "string",
    "codigoMessagem": 0,
    "retorno": {
      "principal": 0,
      "simumacaoParcelas": [
        {
          "parcela": 0,
          "valor": 0,
          "tipoOperacao": "string",
          "valorTotal": 0,
          "cet": 0
        }
      ],
      "valorTarifa": 0
    },
    "problemaDeInfraestrutura": true,
    "warning": true,
    "cd_cupom": 0
}
```

### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|---|
|`parcela`|Quantidade de parcelas selecionadas.|**integer (int32)**|
|`valor`|Valor da parcela.|**string**|
|`valorTotal`|Número sequencial único para identificar a transação.|**string**|
|`cet`|Custo efetivo total.|**string**|



### Schema

<p><img src="assets\imgs\retorno-simulacao-generic-result.png" class="schema" alt="imagem"></p>

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

#### Descrição dos dados enviados como parâmetro:

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

## Resposta da requisição - AtualizarLiquidacao

```json
{
  "success": true,
  "message": "string",
  "data": {
    "cod_Fat": 0,
    "autenticacao": "string",
    "bancoLiquidacao": "string",
    "dataLiquidacao": "2022-05-19T18:22:02.989Z"
  }
}
```

### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|---|
|`cod_Fat`|Identificador da fatura liquidada.|**integer (int32)**|
|`autenticacao`|Código comprovante da liquidação do boleto junto ao banco.|**string**|
|`bancoLiquidacao`|Nome do banco o qual foi realizada a liquidação.|**string**|
|`dataLiquidacao`|Data que ocorreu a liquidação .|**string (date-time)**|


### Schema

<p><img src="assets\imgs\fatura-liquidada-model-generic-result.png" class="schema" alt="imagem"></p>

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

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`cdFaturas`|Numeração identificadora da fatura.|**Array de string's**|Sim|
|`parcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**string**|Sim|
|`valorPagCartao`|Valor pago pelo cliente ao final de sua cotação (valor total).|**string**|Sim|
|`valorWynk`|Valor pago pelo cliente a partir da Wynk.|**string**|Sim|
|`email`|Endereço de e-mail para cobrança do cartão do cliente. | **string** |Sim|
|`celular`|Número de telefone(celular) do cliente.|**string**|Sim|
|`securityCode`|Código de segurança do cartão do cliente.|**string**|Sim|
|`creditCardNumber`|Numeração do cartão do cliente.|**string**|Sim|
|`monthYear`|Mês e ano do vencimento do cartão do cliente.|**string**|Sim|
|`holderName`|Nome do portador do cartão.|**string**|Sim|
|`cpfcnpj`|CPF ou CNPJ do portado do cartão.|**string**|Sim|
|`telefone`|Número de telefone do cliente.|**string**|Sim|

#### Observações para execução da chamada :

1. É necessário passar o número real de parcelas, a API opera verificando a quantidade de parcela selecionada e o valor cobrado, valores diferentes da cotaçãorealizada, anteriormente, pode cominar em erros.
2. O valor total a ser cobrado no cartão, deve ter os centavos separados por "," (vírgula) e não ponto. Assim como o parâmetro valorWynk.
3. O parãmetro valorWynk, deve ser enviado sempre zerado: 00,00. No momento, essa opção não está mais disponível.
4. O número do cartão deve ser enviado sem espaços ou máscara.
5. O campo monthyear segue o padrão MMAA.

### Exemplo de aplicação da requisição - Pagamento

```
{
 "cdFaturas": [1,2,3,4],
 "parcelas": "2",
 "valorPagCartao": "12,00",
 "valorWynk": "12,00",
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

### Resposta da requisição - Pagamento

```json
{
  "success": true,
  "message": "string",
  "data": {
    "mensagem": "string",
    "pedido": 0,
    "transacao": 0,
    "transacaoWynk": 0
  }
}
```

#### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|---|
|`pedido`|Código identificador do pedido.|**integer (int32)**|
|`transacao`|Código identificador da transação.|**integer (int32)**|
|`transacaoWynk`|Código identificador da transação Wynk .|**integer(int32)**|


#### Schema

<p><img src="assets\imgs\pagamento-generic-result.png" class="schema" alt="imagem"></p>

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
|`CodigoPedido`|Numeração identificadora do pedido.|**integer (int32)**|Sim|

### Resposta da requisição - ConsultarStatusPedido

```json
{
  "success": true,
  "message": "string",
  "data": {
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
}
```

#### Descrição dos dados retornados:

|Propriedade|Descrição|Tipo|
|---|---|---|
|`cdFaturas`|Numeração identificadora da fatura.|**Array de string's**|
|`parcelas`|Numeração referente a quantidade de parcelas selecionadas para pagamento.|**string**|
|`valorPagCartao`|Valor pago pelo cliente ao final de sua cotação (valor total).|**string**|
|`valorWynk`|Valor pago pelo cliente a partir da Wynk.|**string**|
|`email`|Endereço de e-mail para cobrança do cartão do cliente. | **string** |
|`celular`|Número de telefone(celular) do cliente.|**string**|
|`securityCode`|Código de segurança do cartão do cliente.|**string**|
|`creditCardNumber`|Numeração do cartão do cliente.|**string**|
|`monthYear`|Mês e ano do vencimento do cartão do cliente.|**string**|
|`holderName`|Nome do portador do cartão.|**string**|
|`cpfcnpj`|CPF ou CNPJ do portado do cartão.|**string**|
|`telefone`|Número de telefone do cliente.|**string**|


#### Schema

<p><img src="assets\imgs\pagamento-debito-model-generic-result.png" class="schema" alt="imagem"></p>

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

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`CodigoFatura`|Numeração identificadora da fatura.|**integer (int32)**|Sim|


# API: Recibo

A API recibo, trabalha com 2 requisições,possuindo como objetivo gerar o recibo de pagamento, do pedido efetuado pelo cliente. É a partir dessa operação que os dados referentes ao cliente, bem como os dados de pagamento do cartão e os débitos parcelados são reunidos para apresentação de um recibo único ao cliente.

## Requisição GET - ReciboPedido

Está requisição é formada por 1 campo. A principal diferença dessa requisição para a requisição de recibo por faturas está no fato dela retornar os dados do portador do cartão, como: telefone, e-mail e cpf, por exemplo. Uma visão geral do pedido feito.

<section id="operacao">
<article class="get">
        <p>
        <code>
            <b>GET</b> /api/v2/Recibo/ReciboPedido
        </code> Método consulta Recibo por Pedido </p>
</article>
</section>

### Exemplo da requisição - ReciboPedido

1. Curl
```
curl -X 'GET' \
  'https://api.parcelenahora.com.br/api/v2/Recibo/ReciboPedido=2' \
  -H 'accept: application/json'
```

2. Request URL
```
https://api.parcelenahora.com.br/api/v2/Recibo/ReciboPedido=2
```

3. JSON
```
{
  "COD_PEDIDO": "2"
}
```

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`COD_PEDIDO`|Numeração identificadora do pedido.|**string**|Sim|


### Resposta da requisição - ReciboPedido

```json
{
  "success": true,
  "message": "string",
  "data": {
    "comPedido": [
      {
        "cdped": "string",
        "dtped": "string",
        "cdddochavests": "string",
        "dstelefone": "string",
        "dsemail": "string",
        "dscpfcnpj": "string",
        "nrvalorfat": "string",
        "nrvalortotal": "string",
        "qtparcela": "string",
        "nrvalorparcela": "string",
        "nrvalortaxa": "string",
        "dsplaca": "string",
        "dsrenavam": "string",
        "dscpfcnpjprop": "string",
        "dsmarcamodelo": "string",
        "dscor": "string",
        "dsnomeprop": "string",
        "dsempresauf": "string",
        "cdusuario": "string",
        "dsterminalpdv": "string",
        "dspagamentoguid": "string",
        "nrvalorfacilitadora": "string",
        "cdemp": "string",
        "dsanomodelo": "string",
        "dschassi": "string",
        "nrvalretcredtotal": "string",
        "cdempret": "string",
        "cdter": "string",
        "nrvalcustoadqtotal": "string",
        "nrperctaxa": "string",
        "qtcartoes": "string",
        "nrvalcomissaovendedor": "string",
        "nrperccomissaovendedor": "string",
        "nrpercretcredenciado": "string",
        "nrperccustoadquirencia": "string",
        "nrvallucroliquido": "string",
        "nrvalimposto": "string",
        "cdempadq": "string",
        "dsiporigem": "string",
        "cdusupedalteracao": "string",
        "dtpedalteracao": "string",
        "dsjustificativa": "string",
        "cdddochavecanal": "string",
        "cdempsubadq": "string",
        "cdcupom": "string",
        "comdetdominReference": "string",
        "comempresaReference": "string",
        "comempresA1Reference": "string",
        "comcupomdescontoReference": "string",
        "comempresA2Reference": "string",
        "xmlns": "string",
        "text": "string"
      }
    ]
  }
}
```

## Requisição GET - ReciboFaturaPagasPedido

Está requisição é formada por 1 campo. E difere da requisição do recibo por pedido, dado seu retorno visar as faturas que foram pagas no pedido. 

<section id="operacao">
<article class="get">
        <p>
        <code>
            <b>GET</b> /api/v2/Recibo/ReciboFaturaPagasPedido
        </code> Método de consulta recibo Faturas Pagas Por Pedido </p>
</article>
</section>

### Exemplo da requisição - ReciboFaturaPagasPedido

1. Curl
```
curl -X 'GET' \
  'https://api.parcelenahora.com.br/api/v2/Recibo/ReciboFaturaPagasPedido?CodigoPedido=2' \
  -H 'accept: application/json'
```

2. Request URL
```
https://api.parcelenahora.com.br/api/v2/Recibo/ReciboFaturaPagasPedido?CodigoPedido=2
```

3. JSON
```
{
  "COD_PEDIDO": "2"
}
```

#### Descrição dos dados enviados como parâmetro:

|Propriedade|Descrição|Tipo|Obrigatório|
|---|---|---|---|
|`COD_PEDIDO`|Numeração identificadora do pedido.|**string**|Sim|


### Resposta da requisição - ReciboFaturaPagasPedido

```json
{
  "success": true,
  "message": "string",
  "data": {
    "confatura": [
      {
        "cdfat": "string",
        "cdped": "string",
        "dtfat": "string",
        "dsrenavam": "string",
        "dsplaca": "string",
        "dsdescricao": "string",
        "nrvalor": "string",
        "dsidentificador": "string",
        "cdddochavests": "string",
        "dsindentdetran": "string",
        "dsautoinfracao": "string",
        "dsanolicenciamento": "string",
        "dtvencimento": "string",
        "nrvalormulta": "string",
        "nrvalormora": "string",
        "nrvaloroutros": "string",
        "nrvalorpago": "string",
        "nrvalordevido": "string",
        "nrvalortotal": "string",
        "dtdata": "string",
        "nrvalorservico": "string",
        "dsquantidade": "string",
        "dtparcelamento": "string",
        "nrqtdparcela": "string",
        "nrvalorparcelamento": "string",
        "nrnumparcela": "string",
        "dsorgao": "string",
        "dscodinfracao": "string",
        "nrvalordesconto": "string",
        "nrvalorcorrecao": "string",
        "cdddochavetipo": "string",
        "nrvalordebito": "string",
        "dscodbarras": "string",
        "dtvalidade": "string",
        "dslinhaarq": "string",
        "nrvalortaxa": "string",
        "dtliquidacao": "string",
        "dsbancoliquidacao": "string",
        "dsautenticacao": "string",
        "nrvalorfacilitadora": "string",
        "dslinhadigitavel": "string",
        "dsretornoapi": "string",
        "nrvalretcredenciado": "string",
        "cdusufatalteracao": "string",
        "dtfatalteracao": "string",
        "cdrec": "string",
        "comdetdominReference": "string",
        "comdetdomiN1Reference": "string",
        "compedidoReference": "string"
      }
    ]
  }
}
```
