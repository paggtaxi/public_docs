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
        "num": "110300",
        "balance_debits": 3547.37,
        "unlock_value": 180.00,
        "week_debt": 180.00
      },
      "reason": {
        "message": "",
        "code": 201
      },
      "success": true
    }

*Campos:*

| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| ----------:| ----------:|
|   num         | string        | Prefixo do taxista | 110300 |
|   balance_debits         | float        | Total da dívida pendente do taxista | 3547.37 |
|   unlock_value         | float       | Este valor corresponde ao valor que o taxista deve pagar para ser liberado na semana atual para poder trabalhar na Pontual  | 180 |

