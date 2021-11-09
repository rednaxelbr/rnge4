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

Após o processamento de *cada endereço* deve ser feito um POST informando que aquele endereço foi integrado. Devem ser informados pelo menos os campos "id", "setor" e "atualizado_erp". Como em todos os PUT, é essencial que o "id" da URL seja o mesmo do JSON. Exemplo:

```bash
PUT /v2/skustocks/2801001151764 -d '{"id":"2801001151764","setor":1,"atualizado_erp":true}'
```
