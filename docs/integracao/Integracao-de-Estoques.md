---
tags: [Integração]
---

# Integração de Estoques

## Leitura

Para buscar os estoques modificados num determinado prédio é preciso passar o filtro `pendente_erp` true no GET v2/skustocks. O processo precisa ser executado uma vez para cada prédio. Exemplo:

```bash
GET v2/skustocks?filter={"pendente_erp":true, "id_predio": 1}
GET v2/skustocks?filter={"pendente_erp":true, "id_predio": 2}
GET v2/skustocks?filter={"pendente_erp":true, "id_predio": 3}
(...)
GET v2/skustocks?filter={"pendente_erp":true, "id_predio": 9999}
```

Após o processamento de *cada endereço* deve ser feito um POST informando que aquele endereço foi integrado. Devem ser informados pelo menos os campos "id" e "atualizado_erp". Como em todos os PUT, é essencial que o "id" da URL seja o mesmo do JSON. Exemplo:

```bash
PUT /v2/skustocks/2801001151764 -d '{"id":"2801001151764", "atualizado_erp":true}'
```

## Gravação

Durante a transição do controle de estoque do ERP legado para o WMS da Rednaxel pode ser necessário atualizar periodicamente o estoque no WMS. Para isso deve-se fazer um `POST v2/skustocks` passando um array "integracao" contendo até 2000 registros de inventário. Exemplo de JSON:

```json
{
    "id_predio": 20,
    "integracao": [
        {
            "id": 9900200100077898,
            "cod_sku": 77898,
            "capacidade": 30,
            "quantidade": 1
        },
        {
            "id": 9900200100016924,
            "cod_sku": 16924,
            "capacidade": 30,
            "quantidade": 27
        },
        {
            "id": 9900200100021318,
            "cod_sku": 21318,
            "capacidade": 50,
            "quantidade": 66
        },
        {
            "id": 9900200100124719,
            "cod_sku": 124719,
            "capacidade": 120,
            "quantidade": 112
        },
        {
            "id": 9900200100118041,
            "cod_sku": 118041,
            "capacidade": 10,
            "quantidade": 10
        },
        {
            "id": 9900200100112808,
            "cod_sku": 112808,
            "capacidade": 18,
            "quantidade": 15
        }
    ]
}
```