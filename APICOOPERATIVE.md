# API Cooperative

> **versão**: 2.0

> **URL base**: https://portal.paggtaxi.com.br/api/cooperative/{CLIENT_SECRET}

* [1 - Capturando dados financeiros do taxista](#financial)
* [2 - Validação de e-vouchers para corridas](#evoucher)
* [3 - Telefones de taxistas](#phones)
    * [3.1 - Listar telefones](#phones_list)
    * [3.2 - Adicionar ou editar um telefone](#phones_add)
    * [3.3 - Editar um telefone](#phones_edit)
    * [3.4 - Deletar um telefone](#phones_delete)

#### <a name="financial"></a>/driver/{ID}/financial

---

* **GET**:

>Recebe como paramêtro o ID do taxista em {ID} e retorna um JSON com as informações financeiras do taxista:

*Requisição*:

  https://portal.paggtaxi.com.br/api/cooperative/Iia41sdr1/driver/1324/financial

*Resposta:*

    {
        "content": {
            "num": "100000",
            "balance_debits": 3547.37,
            "unlock_value": 180.00,
            "week_debt": 180.00,
            "total_debits": 360.00,
            "suspended": false,
            "ride_suspended": false,
            "deleted": true,
        },
        "reason": {
            "message": "",
            "code": 201
        },
        "success": true
    }

*Campos:*

| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***num***         | string        | Prefixo do taxista | 100000 |
|   ***balance_debits***         | float        | Total da dívida pendente do taxista | 3547.37 |
|   ***unlock_value***         | float       | Este valor corresponde ao valor que o taxista deve pagar para ser liberado na semana atual para poder trabalhar na Pontual  | 180 |
|   ***week_debt***         | float       | Valor que o taxista está devendo da semana atual  | 180 |
|   ***total_debits***         | float       | Valor total da semana atual e da dívida de desbloqueio  | false |
|   ***suspended***         | boolean       | Taxista está suspenso de cobranças?  | 380 |
|   ***ride_suspended***         | boolean       | Taxista está suspenso para pegar corridas por excesso de dívidas?  | false |
|   ***deleted***         | boolean       | Taxista deletado da Paggtaxi?  | true |


---

#### <a name="evoucher"></a>/validate-voucher/

* **POST**:

> - Recebe um POST com o voucher e a OS da corrida, se a OS for informada associa a corrida ao voucher, assim esse voucher não poderá ser validado em outra corrida novamente.
> - ***content-type***: *application/x-www-form-urlencoded*

*Requisição*:

    {
        'service_order': '200055',
        'evoucher': 'vouch'
    }

| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***service_order***         | string        | Ordem de serviço da corrida | 200055 |
|   ***evoucher***         | string        | Voucher único (5 letras) ou avulso (4 letras) para ser validado | vouch |


*Resposta com* ***SUCESSO***:

    {
        "content": {
          "status": true,
          "evoucher": "vouch",
          "verify": "eiai",
          "company": "Paggtaxi",
          "service_order": "848468",
          "password": "dc310f3fd6e3c31e41767a072c27322f",
          "user_name": "Alan Albuquerque"
        },
        "reason": {
          "message": "Voucher validado com sucesso.",
          "code": 201
        },
        "success": true
    }


| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***verify***         | string        | Voucher de retorno que deve ser utilizado na corrida | eiai |
|   ***company***         | string        | Nome da empresa do voucher | Paggtaxi |
|   ***password***         | string        | Senha do passageiro (encriptografado) | dc310f3fd6e3c31e41767a072c27322f |

``` * demais campos já especificados anteriormente. ```

*Resposta com* ***ERRO***:

    {
        "content": {
            "evoucher": "vouch"
        },
        "reason": {
            "message": "Funcionário sem limite",
            "code": 200
        },
        "success": false
    }



---

#### <a name="phones"></a>/driver/{ID}/phones




<a name="phones_list"></a>
* **GET**:

> -Recebe como paramêtro o ID do taxista em {ID} e retorna um JSON com os telefones do taxista:

*Resposta com* ***SUCESSO***:

    {
      "content": {
        "phones": [
          {
            "name": "Alan Albuquerque",
            "created": "2014-12-05T19:26:04.602468",
            "phone": "99999999",
            "main": true,
            "ddd": "21",
            "secondary": false
          },
          {
            "name": "Alan Albuquerque",
            "created": "2014-12-23T08:15:45.163294",
            "phone": "22222222",
            "main": false,
            "ddd": "21",
            "secondary": false
          }
        ],
        "driver_id": "1234"
      },
      "reason": {
        "message": "",
        "code": 201
      },
      "success": true
    }


| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***name***         | string        | Nome do contato dono do telefone | Alan Albuquerque |
|   ***secondary***         | boolean        | Se o telefone é o telefone alternativo to taxista (só pode ter um e pode não ter nenhum) | false |
|   ***main***         | boolean        | Se o telefone é o telefone o principal to taxista (só pode ter um e deve ter pelo menos um) | true |

``` * demais campos são auto explicativos. ```



<a name="phones_add"></a>
* **POST**:

> - Recebe um POST para cadastrar ou editar um telefone de taxista.
> - ***content-type***: *application/x-www-form-urlencoded*

*Requisição*:

    {
        'name': 'Alan Albuquerque',
        'phone': '4799999999',
        'main': 'true',
        'secondary': 'false'
    }

| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***name***         | string        | Nome do contato dono do telefone | Alan Albuquerque |
|   ***phone***         | string        | DDD e telefone, se o telefone informado já existir entra em modo de edição dos outros campos (para editar o número de telefone use o PUT). | 4799999999 |
|   ***main***         | boolean        | Se o telefone é o telefone o principal to taxista (só pode ter um e deve ter pelo menos um) | true |
|   ***secondary***         | boolean        | Se o telefone é o telefone alternativo to taxista (só pode ter um e pode não ter nenhum) | false |


*Resposta com* ***SUCESSO***:

    {
      "content": {
        "phone": "99999999",
        "driver_id": "1234",
        "name": "Alan Albuquerque",
        "created": "2015-09-30T09:33:30.003276",
        "secondary": false,
        "main": true,
        "ddd": "47"
      },
      "reason": {
        "message": "",
        "code": 201
      },
      "success": true
    }

*Resposta com* ***ERRO***:

    {
      "content": {
        "driver_id": "1234"
      },
      "reason": {
        "message": "O telefone 478908787 é inválido.",
        "code": 200
      },
      "success": false
    }



<a name="phones_edit"></a>
#### /driver/{ID}/phones/{PHONE}

* **PUT**:

> - Recebe um PUT para editar um telefone de taxista e recebe como paramêtro em PHONE o telefone a ser editado.
> - ***content-type***: *application/x-www-form-urlencoded*

*Requisição*:

    {
        'name': 'Alan Albuquerque',
        'phone': '4788888888',
        'main': 'true',
        'secondary': 'false'
    }

| Campo         | Tipo          | Descrição  | Exemplo    |
| ------------- |:-------------:| :----------| ----------:|
|   ***name***         | string        | Nome do contato dono do telefone | Alan Albuquerque |
|   ***phone***         | string        | DDD e telefone, se o telefone informado já existir entra em modo de edição dos outros campos (para editar o número de telefone use o PUT). | 4799999999 |
|   ***main***         | boolean        | Se o telefone é o telefone o principal to taxista (só pode ter um e deve ter pelo menos um) | true |
|   ***secondary***         | boolean        | Se o telefone é o telefone alternativo to taxista (só pode ter um e pode não ter nenhum) | false |


*Resposta com* ***SUCESSO***:

    {
      "content": {
        "phone": "88888888",
        "driver_id": "1234",
        "name": "Alan Albuquerque",
        "created": "2015-09-30T09:33:30.003276",
        "secondary": false,
        "main": true,
        "ddd": "47"
      },
      "reason": {
        "message": "",
        "code": 201
      },
      "success": true
    }

*Resposta com* ***ERRO***:

    {
      "content": {
        "driver_id": "1234"
      },
      "reason": {
        "message": "O telefone 478908787 é inválido.",
        "code": 200
      },
      "success": false
    }


<a name="phones_delete"></a>
* **DELETE**:

> - Deleta um telefone de taxista e recebe como paramêtro em PHONE o telefone a ser deletado.

*Resposta com* ***SUCESSO***:

    {
        "content": {
            "phone": "22222222",
            "driver_id": "1234",
            "name": "Alan Albuquerque",
            "created": "2014-12-23T08:15:45.163294",
            "secondary": false,
            "main": false,
            "ddd": "21"
        },
        "reason": {
            "message": "",
            "code": 201
        },
            "success": true
    }


*Resposta com* ***ERRO***:

    {
        "content": {
            "phone": "99999999",
            "driver_id": "1234",
            "name": "Alan Albuquerque",
            "created": "2015-09-30T09:33:30.003276",
            "secondary": false,
            "main": true,
            "ddd": "47"
        },
        "reason": {
            "message": "Não é possível remover celulares principais.",
            "code": 200
        },
            "success": false
    }

#### <a name="photo"></a>/driver/{ID}/photo/{SIZE}

---

* **GET**:

>Recebe como paramêtro o ID do taxista em {ID} e retorna a foto do perfil do taxista do tamanho especificado em {SIZE}.

*Requisição*:

  https://portal.paggtaxi.com.br/api/cooperative/Iia41sdr1/driver/1324/photo/medium

*Capo SIZE:*


| Campo         | Dimensões |
| ------------- |:-------------:|
|   ***small***         | 90x90 pixels        |
|   ***medium***         | 260x260 pixels        |
|   ***original***         | Tamanho original no momento do upload        |


---
