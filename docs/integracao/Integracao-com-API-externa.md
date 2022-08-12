---
stoplight-id: cmulevoiikwjw
tags: [Integração]
---

# Integração com API externa

## Integrações disponíveis

|id_vendor|Nome da API|
|---------|-----------|
|bling|Bling|
|cigam|CIGAM|
|correios|Correios|
|getnet|Getnet|
|googlemaps|Google Maps|
|ifood|iFood|
|ipwhois|IPWHOIS|
|jadlog|Jadlog|
|magalu|Magalu|
|mercadolivre|Mercado Livre|
|neogrid|Neogrid|
|olist|Olist|
|pagarme|Pagar.me|
|pagseguro|PagSeguro|
|core|Plataforma Core|
|plugboleto|PlugBoleto|
|plugnotas|PlugNotas|
|receitaws|ReceitaWS|
|shopify|Shopify|
|tray|Tray Commerce|
|vtex|VTEX|
|webprice|WebPrice|
|woocommerce|WooCommerce|

## Exportação

Cada recurso de cada integração possui um ID. Por exemplo, o recurso `Requisicao` da CIGAM tem o ID 174. Para enviar o que estiver na fila de exportação deve-se usar o comando (devidamente autenticado com o token):

```bash
curl -g -s -X PUT 'https://homolog.rnge.com.br:8091/v2/integrationexports/174'\
  -d '{"id":174}'\
  -H 'Authorization: Bearer {token}'
```


## Comandos

Em alguns casos existem comandos "avulsos" que podem ser chamados conforme a necessidade. Por exemplo, para verificar se há novas assinaturas recorrentes do PagSeguro deve-se usar o comando (devidamente autenticado com o token):

```bash
curl -g -s -X POST 'https://homolog.rnge.com.br:8091/v2/integrationwebhooks/pagseguro/verificacao'\
  -d '{"dias":30}'\
  -H 'Authorization: Bearer {token}'

curl -g -s -X POST 'https://homolog.rnge.com.br:8091/v2/integrationwebhooks/cigam/requisicao'\
  -d '{"ID_ACAO":1}'\
  -H 'Authorization: Bearer {token}'

```


## Webhooks

Alguns fornecedores chamam webhooks quando alguns eventos ocorrem. Por exemplo, o Mercado Livre chama o seguinte webhook quando uma encomenda é enviada:

```bash
curl -g -s -X POST 'https://homolog.rnge.com.br:8091/v2/webhooks/mercadolivre'
```
