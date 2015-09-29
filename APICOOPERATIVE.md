# API Cooperative

> **versão**: 1.0

> ** URL base **: https://portal.paggtaxi.com.br/api/cooperative/*{CLIENT_SECRET}*


#### /driver/{prefixo}/financial
---

* **GET**:

Recebe como paramêtro o prefixo do taxista em {prefixo} e retorna um JSON com as informações financeiras do taxista:

*Exemplo de resposta:*

    {
      "content": {
        "pk": 2491,
        "num": "110300",
        "balance_debits": "3547.37",
        "unlock_value": "180.00",
        "week_debt": "180.00"
      },
      "reason": {
        "message": "",
        "code": 201
      },
      "success": true
    }

*Campos:*

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

