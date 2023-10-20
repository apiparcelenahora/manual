---
layout: page
title: Visão geral - API Parceiros
permalink: /introducao/
---

# Visão geral - API Parceiros

O objetivo desta documentação é orientar sobre a integração da API Wynk, descrevendo as funcionalidades, os métodos utilizados, informações a serem enviadas/recebidas,além de prover exemplos.

Para executar as operações da nossa API Parceiros, é necessário o uso do nosso **TOKEN** de acesso. Caso você ainda não possua, um cadastro junto ao nosso sistema, entre em contato com o nosso suporte.

Caso você já possua cadastro, você deverá usar seu login e e-mail para geração do **TOKEN** de acesso, utilizando o verbo HTTP **POST** junto ao nosso endpoint, conforme exemplo abaixo:

{% include alert.html type="info" title="Endereço endpoint" content="http://api.parcelenahora.com.br/login/v1/login" %}

```
---
{
  "email": "",
  "senha": ""
}
---
```
## Arquitetura da integração

O modelo utilizado na integração das nossas APIs é baseado na utilização de uma única URL:

{% include alert.html type="info" title="URL base" content="http://api.parcelenahora.com.br/" %}

Onde para se executar uma determinada operaçãoção é necessário seguir os seguintes passos:

1. Combinar a URL base do ambiente com o **_endpoint_** da operação desejada. Ex.: http://api.parcelenahora.com.br/**v1/v1-2/operacaoDesejada/**.
2. Enviar a requisição para a URL combinada (base+operação desejada) utilizando o verbo (método) HTTP adequado à operação.

### Exemplos de verbos (métodos) HTML

|Método HTTP|Descrição|
|---|---|
|**GET**|Método utilizado para solicitação de representação de um recurso específico. Utilizado para obtenção de dados existentes. Ex.: consultar status de uma transação.|
|**POST**|Método utilizado para criação de um novo recurso. Utilizado para submeter uma entidade a um recurso específico. Ex.: realizar uma cotação|

Nas operações realizadas em nossas API, todo e qualquer envio de requisição irá retornar um código de [Status HTTP]({{ site.baseurl }}/docs/codigosRetorno), indicando se a operação foi realizado com sucesso ou não.

## Glossário 

Para facilitar o entendimento da nossa API, listamos abaixo um pequeno glossário com os principais termos relacionados as operações em nossa API:

|Termo|Descrição|
|---|---|
|**CDA**|É um título emitido pelo governo que comprova a dívida do contribuinte, seu número é utilizado para identificação de uma determinada dívida.|
|**Holder Name**|É o nome do titular do cartão, o seu portador.|
|**Inscrição Imóvel**|Também conhecido como Inscrição do IPTU, é o identificador do estabelecimento/casa, junto ao cadastro imobiliário do município.|
|**Pedido**|É o número identificador da transação ou consulta, realizada pelo cliente, junto ao nosso sistema.|
|**Security Code**|É o código de segurança do cartão (CVV), composto usualmente de 3 dígitos.|
|**Taxas de serviço**|Valor cobrado pelos órgãos para realizações de pequenos seviços (emplacamento e etc).|
|**Valor Wynk**|É o valor referente ao desconto obtido pelo cliente a partir de sua pontuação junto a Wynk.|

## UF's, Órgãos e débitos suportados

A versão atual da API Parceiros possui suporte ás seguintes UF's, Órgãos e Débitos

| UF      | Órgãos            | Débitos retornados                  |
|---------|-------------------|-------------------------------------|
| `AC`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `AL`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                 |
| `AM`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                            |
| `AP`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `BA`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `CE`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `DF`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO / IPTU` |
| `ES`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `GO`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                              |
| `MA`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `MG`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                             |
| `MS`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `MT`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `PA`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `PB`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `PE`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `PI`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                 |
| `PR`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                  |
| `RJ`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `RN`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `RO`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `RR`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `RS`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `SC`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                               |
| `SP`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |
| `TO`      | `DETRAN / SEFAZ`    | `MULTAS / IPVA / LICENCIAMENTO`                                |

