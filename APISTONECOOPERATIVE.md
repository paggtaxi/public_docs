# API Stone - Cooperativa

> **versão**: 1.0

> **URL**: https://portal.paggtaxi.com.br


> OBS.: Assume-se que somente a resposta com status 201 e/ou com o campo "success" como "true" tenha sido executada com êxito.

## Criar nova corrida:

### /api/stone/{{CLIENT_NOT_SECRET}}/add-transaction/

> MÉTODO: POST
> CONTENT-TYPE: application/json

> Exemplo:

    {
        "amount": "100.00", // Valor da corrida (R$ 1.100,10 enviar "1100.10")
        "payment_type": "credit", // Tipo da forma de pagamento (credit ou debit)
        "created_at": "2016-01-12T11:00:27", // Data e hora nesse formato (iso) que a transação foi realizada. (yyyy-mm-ddThh:mm:ss)
        "expected_on": "2016-01-02",  // Data nesse formato que a transação será repassada pela Stone para a Paggtaxi. (yyyy-mm-dd)
        "seller_id": "000000000000", // CPF do taxista sem pontos ou traços
        "transaction_id": "e44ba8fa9ce411e5ace5c4e9840db4a3", // ID da Transação
        "authorization_code": "56489", // Código de autorização da transação
        "ride_id": "321654", // OS da Corrida
        "card_number": "31231239****" // Número do cartão
    }

> Campos obrigatórios:
  - seller_id
  - payment_type
  - created_at
  - transaction_id
  - amount
  - expected_on
  - card_number
  - authorization_code

> Retorno de sucesso:

    {
      "reason": {
        "message": "Transação recebida com sucesso",
        "code": 201
      },
      "success": true
    }

> Retorno com erro:

    {
      "reason": {
        "message": {
          "amount": "Este campo é obrigatório."
        },
        "code": 200
      },
      "success": false
    }



## Estornar corrida:

### /api/stone/{{CLIENT_NOT_SECRET}}/reverse-transaction/

> MÉTODO: POST
> CONTENT-TYPE: application/json

> Exemplo:

    {
        "transaction_id": "e44ba8fa9ce411e5ace5c4e9840db3tr", // ID da Transação
        "seller_id": "00000000000" // CPF do taxista
    }

> Campos obrigatórios:
  - seller_id
  - transaction_id

> Retorno com erro:

    {
      "reason": {
        "message": "Transação não existe ou não pertence ao CPF informado",
        "code": 201
      },
      "success": true
    }