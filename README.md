# Introdução

Essa SDK foi construída com o intuito de torná-la flexível, de forma que todos possam utilizar todas as features, de todas as versões de API.

Você pode acessar a documentação oficial do Pagar.me acessando esse [link](https://docs.pagar.me).

## Index

- [Instalação](#instalação)
- [Configuração](#configuração)
- [Transações](#transações)
- [Criando uma transação](#criando-uma-transação)
- [Capturando uma transação](#capturando-uma-transação)
- [Estornando uma transação](#estornando-uma-transação)
  - [Estornando uma transação parcialmente](#estornando-uma-transação-parcialmente)
  - [Estornando uma transação com split](#estornando-uma-transação-com-split)
- [Retornando transações](#retornando-transações)
- [Retornando uma transação](#retornando-uma-transação)
- [Retornando recebíveis de uma transação](#retornando-recebíveis-de-uma-transação)
- [Retornando um recebível de uma transação](#retornando-um-recebível-de-uma-transação)
- [Retornando o histórico de operações de uma transação](#retornando-o-histórico-de-operações-de-uma-transação)
- [Retornando eventos de uma transação](#retornando-eventos-de-uma-transação)
- [Calculando Pagamentos Parcelados](#calculando-pagamentos-parcelados)
- [Testando pagamento de boletos](#testando-pagamento-de-boletos)
- [Cartões](#cartões)
  - [Criando cartões](#criando-cartões)
  - [Retornando cartões](#retornando-cartões)
  - [Retornando um cartão](#retornando-um-cartão)
- [Planos](#planos)
  - [Criando planos](#criando-planos)
  - [Retornando planos](#retornando-planos)
  - [Retornando um plano](#retornando-um-plano)
  - [Atualizando um plano](#atualizando-um-plano)
- [Assinaturas](#assinaturas)
  - [Criando assinaturas](#criando-assinaturas)
  - [Split com assinatura](#split-com-assinatura)
  - [Retornando uma assinatura](#retornando-uma-assinatura)
  - [Retornando assinaturas](#retornando-assinaturas)
  - [Atualizando uma assinatura](#atualizando-uma-assinatura)
  - [Cancelando uma assinatura](#cancelando-uma-assinatura)
  - [Transações de assinatura](#transações-de-assinatura)
  - [Pulando cobranças](#pulando-cobranças)
- [Postbacks](#postbacks)
  - [Retornando postbacks](#retornando-postbacks)
  - [Retornando um postback](#retornando-um-postback)
  - [Reenviando um Postback](#reenviando-um-postback)
  - [Validando uma requisição de postback](#validando-uma-requisição-de-postback)
- [Saldo do recebedor principal](#saldo-do-recebedor-principal)
- [Operações de saldo](#operações-de-saldo)
  - [Histórico das operações](#histórico-das-operações)
  - [Histórico de uma operação específica](#histórico-de-uma-operação-específica)
- [Recebível](#recebível)
  - [Retornando recebíveis](#retornando-recebíveis)
  - [Retornando um recebível](#retornando-um-recebível)
- [Transferências](#transferências)
  - [Criando uma transferência](#criando-uma-transferência)
  - [Retornando transferências](#retornando-transferências)
  - [Retornando uma transferência](#retornando-uma-transferência)
  - [Cancelando uma transferência](#cancelando-uma-transferência)
- [Antecipações](#antecipações)
  - [Criando uma antecipação](#criando-uma-antecipação)
  - [Obtendo os limites de antecipação](#obtendo-os-limites-de-antecipação)
  - [Confirmando uma antecipação building](#confirmando-uma-antecipação-building)
  - [Cancelando uma antecipação pending](#cancelando-uma-antecipação-pending)
  - [Deletando uma antecipação building](#deletando-uma-antecipação-building)
  - [Retornando antecipações](#retornando-antecipações)
- [Contas bancárias](#contas-bancárias)
  - [Criando uma conta bancária](#criando-uma-conta-bancária)
  - [Retornando uma conta bancária](#retornando-uma-conta-bancária)
  - [Retornando contas bancárias](#retornando-contas-bancárias)
- [Recebedores](#recebedores)
  - [Criando um recebedor](#criando-um-recebedor)
  - [Retornando recebedores](#retornando-recebedores)
  - [Retornando um recebedor](#retornando-um-recebedor)
  - [Atualizando um recebedor](#atualizando-um-recebedor)
  - [Saldo de um recebedor](#saldo-de-um-recebedor)
  - [Operações de saldo de um recebedor](#operações-de-saldo-de-um-recebedor)
  - [Operação de saldo específica de um recebedor](#operação-de-saldo-específica-de-um-recebedor)
- [Clientes](#clientes)
  - [Criando um cliente](#criando-um-cliente)
  - [Retornando clientes](#retornando-clientes)
  - [Retornando um cliente](#retornando-um-cliente)
- [Links de pagamento](#links-de-pagamento)
  - [Criando um link de pagamento](#criando-um-link-de-pagamento)
  - [Retornando links de pagamento](#retornando-links-de-pagamento)
  - [Retornando um link de pagamento](#retornando-um-link-de-pagamento)
  - [Cancelando um link de pagamento](#cancelando-um-link-de-pagamento)

## Instalação

Instale a biblioteca utilizando o comando:

```shell
$ pip install pagarme-python
```

## Configuração

Para incluir a biblioteca em seu projeto, basta fazer o seguinte:

```python
import pagarme

pagarme.authentication_key('SUA_API_KEY')
```

## Transações

Nesta seção será explicado como utilizar transações no Pagar.me com essa biblioteca.

### Criando uma transação

```python
  transaction = pagarme.transaction.create({
	"amount": "21000",
    "card_number": "4111111111111111",
    "card_cvv": "123",
    "card_expiration_date": "0922",
    "card_holder_name": "Morpheus Fishburne",
    "customer": {
      "external_id": "#3311",
      "name": "Morpheus Fishburne",
      "type": "individual",
      "country": "br",
      "email": "mopheus@nabucodonozor.com",
      "documents": [
        {
          "type": "cpf",
          "number": "30621143049"
        }
      ],
      "phone_numbers": ["+5511999998888", "+5511888889999"],
      "birthday": "1965-01-01"
    },
    "billing": {
      "name": "Trinity Moss",
      "address": {
        "country": "br",
        "state": "sp",
        "city": "Cotia",
        "neighborhood": "Rio Cotia",
        "street": "Rua Matrix",
        "street_number": "9999",
        "zipcode": "06714360"
      }
    },
    "shipping": {
      "name": "Neo Reeves",
      "fee": "1000",
      "delivery_date": "2000-12-21",
      "expedited": True,
      "address": {
        "country": "br",
        "state": "sp",
        "city": "Cotia",
        "neighborhood": "Rio Cotia",
        "street": "Rua Matrix",
        "street_number": "9999",
        "zipcode": "06714360"
      }
    },
    "items": [
      {
        "id": "r123",
        "title": "Red pill",
        "unit_price": "10000",
        "quantity": "1",
        "tangible": True
      },
      {
        "id": "b123",
        "title": "Blue pill",
        "unit_price": "10000",
        "quantity": "1",
        "tangible": True
      }
    ]
  })

  print(transaction)
```

### Capturando uma transação

```python
  transactionCapture = pagarme.transaction.capture(
      'ID_TRANSAÇÃO_OU_TOKEN',
      {"amount": "Valor a ser capturado"}
  )

  print(transactionCapture)
```

### Estornando uma transação

```python
  transactionRefund = pagarme.transaction.refund(
      'ID_TRANSAÇÃO',
      {"amount": "Valor a ser estornado"}
  )

  print(transactionRefund)
```

Esta funcionalidade também funciona com estornos parciais, ou estornos com split. Por exemplo:

#### Estornando uma transação parcialmente

```python
pagarme.transaction.refund(
    'ID_TRANSACAO',
    {"amount": "Valor a ser estornado parcialmente"}
)
```

#### Estornando uma transação com split

```python
pagarme.transaction.refund(
    'ID_TRANSACAO',
    {
        "amount": "Valor a ser estornado",
        "split_rules": [
            {
                "id": "sr_cj41w9m4d01ta316d02edaqav",
                "amount": "60000",
                "recipient_id": "re_cj2wd5ul500d4946do7qtjrvk"
            },
            {
                "id": "sr_cj41w9m4e01tb316dl2f2veyz",
                "amount": "11000",
                "recipient_id": "re_cj2wd5u2600fecw6eytgcbkd0",
                "charge_processing_fee": "true"
            }
        ]
    }
)
```

### Retornando Transações

```python
  transactions = pagarme.transaction.find_all()

  print(transactions)
```

### Retornando uma transação 

```python
  transaction = pagarme.transaction.find_by({"id":"ID_TRANSAÇÃO"})

  print(transaction)
```

### Retornando recebíveis de uma transação

```python
  transactionPayables = pagarme.transaction.payables('ID_TRANSAÇÃO')

  print(transactionPayables)
```

### Retornando um recebível de uma transação

```python
  transactionPayable  = pagarme.transaction.specific_payable('ID_TRANSAÇÃO', "ID_DO_RECEBIVEL")

  print(transactionPayable)
```

### Retornando o histórico de operações de uma transação

```python
  transactionOperations = pagarme.transaction.operations('ID_TRANSAÇÃO')

  print(transactionOperations)
```

### Retornando eventos de uma transação 

```python
  transacionEvents = pagarme.transaction.events("ID_TRANSAÇÃO")

  print(transactionEvents)
```

### Calculando pagamentos parcelados

Essa rota não é obrigatória para uso. É apenas uma forma de calcular pagamentos parcelados com o Pagar.me.

Para fins de explicação, utilizaremos os seguintes valores:

`amount`: 1000, `free_installments`: 4, `max_installments`: 12, `interest_rate`: 3

O parâmetro `free_installments` decide a quantidade de parcelas sem juros. Ou seja, se ele for preenchido com o valor `4`, as quatro primeiras parcelas não terão alteração em seu valor original.

Nessa rota, é calculado juros simples, efetuando o seguinte calculo:

valorTotal = valorDaTransacao * ( 1 + ( taxaDeJuros * numeroDeParcelas ) / 100 )

Então, utilizando os valores acima, na quinta parcela, a conta ficaria dessa maneira:

valorTotal = 1000 * (1 + (3 * 5) / 100)

Então, o valor a ser pago na quinta parcela seria de 15% da compra, totalizando 1150.

Você pode usar o código abaixo caso queira utilizar essa rota:

```python
  transactionCalculate = pagarme.transaction.calculate_installments_amount({
      "amount": "10000",
      "free_installments": "1",
      "interest_rate": "13",
      "max_installments": "3"
    })
  })

  print(transactionCalculate)
```

### Testando pagamento de boletos

```python
  transactionPayBoleto = pagarme.transaction.pay_boleto(
      "ID_TRANSAÇÃO",
      {"status": "paid"}
  )

  print(transactionPayBoleto)
```


## Cartões

Sempre que você faz uma requisição através da nossa API, nós guardamos as informações do portador do cartão, para que, futuramente, você possa utilizá-las em novas cobranças, ou até mesmo implementar features como one-click-buy.


### Criando Cartões

```python
  card = pagarme.card.create({
      "card_expiration_date": "1122",
      "card_number": "4018720572598048",
      "card_cvv": "123",
      "card_holder_name": "Cersei Lannister"
  })

  print(card)
```

### Retornando cartões

```python
  cards = pagarme.card.find_all()

  print(cards)
```

### Retornando um cartão

```python
  card = pagarme.card.find_by({"id": "card_id"})

  print(card)
```

## Planos

Representa uma configuração de recorrência a qual um cliente consegue assinar.
É a entidade que define o preço, nome e periodicidade da recorrência

### Criando planos

```python
  plan = pagarme.plan.create({
      "amount": "15000",
      "days": "30",
      "name": "Curso com o Alto Pardal"
  })

  print(plan)
```

### Retornando planos

```python
  pagarme.plan.find_all()
```

### Retornando um plano

```python
  pagarme.plan.find_by({"id":"PLAN_ID"})
```

### Atualizando um plano

```python
  pagarme.plan.update(
    "plan_id",
    {
        "name": "Esgrima com Syrio Forel",
        "trial_days": "7"
    })
```

## Assinaturas

### Criando assinaturas

```python
  pagarme.subscription.create({
      "card_id": "card_cj6qvosem04w3nu6dm20nu8od",
      "customer":{
          "email":"jorah.mormont@gameofthrones.com",
          "name":"Sir Jorah Mormont",
          "document_number":"18152564000105",
          "address":{
              "zipcode":"04571020",
              "neighborhood":"Cidade Moncoes",
              "street":"R. Dr. Geraldo Campos Moreira",
              "street_number":"240"
          },
          "phone": {
              "number":"987654321",
              "ddd":"11"
          }
      },
      "payment_method": "credit_card",
      "plan_id": "201836",
      "postback_url": "http://requestb.in/zyn5obzy"
  })
```

### Split com assinatura

```python
  pagarme.subscription.create({
      "card_id": "card_cj6qvosem04w3nu6dm20nu8od",
      "customer":{
          "email":"aardvark.silva@gmail.com",
          "name":"Sir Jorah Mormont",
          "document_number":"18152564000105",
          "address":{
              "zipcode":"04571020",
              "neighborhood":"Cidade Moncoes",
              "street":"R. Dr. Geraldo Campos Moreira",
              "street_number":"240"
          },
          "phone": {
              "number":"987654321",
              "ddd":"11"
          }
      },
      "split_rules":[
          {
              "recipient_id": "re_cj6p5tpqj0bp3oi6euostjng1",
              "percentage": "25"
          },
          {
              "recipient_id": "re_cj6cbuz041cs5mx6dx2fh5asx",
              "percentage": "75"
          }
      ],
      "payment_method": "credit_card",
      "plan_id": "201836",
      "postback_url": "http://requestb.in/zyn5obzy"
  })
```


### Retornando uma assinatura

```python
  pagarme.subscription.find_by({"id": "ID_DA_SUBSCRIPTION"})
```


### Retornando assinaturas

```python
  pagarme.subscription.find_all()
```


### Atualizando uma assinatura

```python
  pagarme.subscription.update(
      "subscription_id",
      {
          "card_id": "card_cj6p5853z0coko66e7h767986",
          "payment_method": "credit_card",
          "plan_id": "201836"
      }
  )
```

### Cancelando uma assinatura

```python
  pagarme.subscription.cancel("ID_DA_SUBSCRIPTION")
```

### Transações de assinatura
```python
  pagarme.subscription.transactions("ID_DA_SUBSCRIPTION")
```

### Pulando cobranças

```python
  pagarme.subscription.settle_charges("ID_DA_SUBSCRIPTION")
```

## Postbacks

Ao criar uma transação ou uma assinatura você tem a opção de passar o parâmetro postback_url na requisição. Essa é uma URL do seu sistema que irá então receber notificações a cada alteração de status dessas transações/assinaturas.

Para obter informações sobre postbacks, 3 informações serão necessárias, sendo elas: `model`, `model_id` e `postback_id`.

`model`: Se refere ao objeto que gerou aquele POSTback. Pode ser preenchido com o valor `transaction` ou `subscription`.

`model_id`: Se refere ao ID do objeto que gerou ao POSTback, ou seja, é o ID da transação ou assinatura que você quer acessar os POSTbacks.

`postback_id`: Se refere à notificação específica. Para cada mudança de status de uma assinatura ou transação, é gerado um POSTback. Cada POSTback pode ter várias tentativas de entregas, que podem ser identificadas pelo campo `deliveries`, e o ID dessas tentativas possui o prefixo `pd_`. O campo que deve ser enviado neste parâmetro é o ID do POSTback, que deve ser identificado pelo prefixo `po_`. 

### Retornando postbacks

```python
  pagarme.transaction.postbacks("ID_DA_TRANSAÇÃO")
```

### Retornando um postback

```python
  pagarme.transaction.specific_postback("transaction_id", "postback_id")
```

### Reenviando um Postback

```python
  pagarme.transaction.postback_redeliver("transaction_id", "postback_id")
```

### Validando uma requisição de postback

```python
  pagarme.postback.validate("signature", "payload", "api_key")
```

## Saldo do recebedor principal

Para saber o saldo de sua conta, você pode utilizar esse código:

```python
  pagarme.balance.default_recipient_balance()
```

Observação: o código acima serve somente de exemplo para que o processo de validação funcione. Recomendamos que utilize ferramentas fornecidas por bibliotecas ou frameworks para recuperar estas informações de maneira mais adequada.

## Operações de saldo

Com este objeto você pode acompanhar todas as movimentações financeiras ocorridas em sua conta Pagar.me.

### Histórico das operações

```python
  pagarme.balance_operation.find_all()
```

### Histórico específico de uma operação

```python
  pagarme.balance_operation.find_by({"id": "balance_operation_id"})
```

## Recebível

Objeto contendo os dados de um recebível. O recebível (payable) é gerado automaticamente após uma transação ser paga. Para cada parcela de uma transação é gerado um recebível, que também pode ser dividido por recebedor (no caso de um split ter sido feito).

### Retornando recebíveis

```python
  pagarme.payable.find_all()
```

### Retornando um recebível

```python
  pagarme.payable.find_by({"id": "payable_id"})
```

## Transferências
Transferências representam os saques de sua conta.

### Criando uma transferência

```python
  transfer = pagarme.transfer.create({
      'amount': '10000',
      'recipient_id': 'RECIPIENT_ID'
  })
```

### Retornando transferências

```python
  pagarme.transfer.find_all()
```

### Retornando uma transferência

```python
  pagarme.transfer.find_by({"id": "TRANSFER_ID"})
```

### Cancelando uma transferência

```python
  pagarme.transfer.cancel("TRANSFER_ID")
```

## Antecipações

Para entender o que são as antecipações, você deve acessar esse [link](https://docs.pagar.me/docs/overview-antecipacao).

### Criando uma antecipação

```python
  bulk_anticipation = pagarme.bulk_anticipation.create('RECIPIENT_ID', {
    'payment_date': '1462999741870',
    'timeframe': 'start',
    'requested_amount': '100000'
  })
```

### Obtendo os limites de antecipação

```python
bulk_anticipation_data = {
    'payment_date': 1503921427000,
    'timeframe': 'start'
}

default_recipient_id = pagarme.recipient.default_recipient()['test'] #test ou live
limits = pagarme.bulk_anticipation.limits(default_recipient_id,  bulk_anticipation_data)
```

### Confirmando uma antecipação building

```python
  default_recipient_id = pagarme.recipient.default_recipient()['test'] #test ou live
  confirm_bulk_anticipation = pagarme.bulk_anticipation.confirm(default_recipient_id, "bulk_anticipation_id")
```

### Cancelando uma antecipação pending

```python
  canceled_bulk_anticipation = pagarme.bulk_anticipation.cancel(recipient['id'], bulk_anticipation['id'])
```

### Deletando uma antecipação building

```python
  default_recipient_id = pagarme.recipient.default_recipient()['test'] #test ou live
  delete_bulk_anticipation = pagarme.bulk_anticipation.delete(default_recipient_id, "bulk_anticipation_id")
```

### Retornando antecipações

```python
  default_recipient_id = pagarme.recipient.default_recipient()['test']
  bulk_anticipations = pagarme.bulk_anticipation.find_all(default_recipient_id)
```

## Contas bancárias

Contas bancárias identificam para onde será enviado o dinheiro de futuros pagamentos.

### Criando uma conta bancária

```python
  bank_account_data = {
      'agencia': '0932',
      'agencia_dv': '5',
      'bank_code': '341',
      'conta': '58054',
      'conta_dv': '1',
      'document_number': '26268738888',
      'legal_name': 'HOUSE TARGARYEN'
  }

  bank_account = pagarme.bank_account.create(bank_account_data)
```

### Retornando uma conta bancária

```python
  pagarme.bank_account.find_by({"id":"bank_account_id"})
```

### Retornando contas bancárias

```python
  pagarme.bank_account.find_all()
```

## Recebedores

Para dividir uma transação entre várias entidades, é necessário ter um recebedor para cada uma dessas entidades. Recebedores contém informações da conta bancária para onde o dinheiro será enviado, e possuem outras informações para saber quanto pode ser antecipado por ele, ou quando o dinheiro de sua conta será sacado automaticamente.

### Criando um recebedor

```python
  params = {
      'anticipatable_volume_percentage': '80',
      'automatic_anticipation_enabled': 'true',
      'transfer_day': '5',
      'transfer_enabled': 'true',
      'transfer_interval': 'weekly',
      'bank_account':{
          'agencia': '0932',
          'agencia_dv': '5',
          'bank_code': '341',
          'conta': '58054',
          'conta_dv': '1',
          'document_number': '26268738888',
          'legal_name': 'HOUSE TARGARYEN'
      }
  }

  recipient = pagarme.recipient.create(params)
```

### Retornando recebedores

```python
  pagarme.recipient.find_all()
```

### Retornando um recebedor

```python
  pagarme.recipient.find_by({"id":"recipient_id"})
```

### Atualizando um recebedor

```python
  pagarme.recipient.update_recipient(
    "recipient_id",
    {
        "anticipatable_volume_percentage": "80",
        "bank_account_id": "17365100"
    }
  )
```

### Saldo de um recebedor

```python
  pagarme.recipient.recipient_balance("recipient_id")
```

### Operações de saldo de um recebedor

```python
  pagarme.recipient.recipient_balance_operation("recipient_id")
```

### Operação de saldo específica de um recebedor

```python
  balance_operation = pagarme.recipient.recipient_balance_operation_id("recipient_id", "operation_id")
```

## Clientes

Clientes representam os usuários de sua loja, ou negócio. Este objeto contém informações sobre eles, como nome, e-mail e telefone, além de outros campos.

### Criando um cliente

```python
  customer_data = {
    'external_id': '#123456789',
    'name': 'João das Neves',
    'type': 'individual',
    'country': 'br',
    'email': 'joaoneves@norte.com',
    'documents': [
      {
        'type': 'cpf',
        'number': '11111111111'
      }
    ],
    'phone_numbers': ['+5511999999999', '+5511888888888'],
    'birthday': '1985-01-01'
  }

  customer = pagarme.customer.create(customer_data)
```

### Retornando clientes

```python
  pagarme.customer.find_all()
```

### Retornando um cliente

```python
  pagarme.customer.find_by({"id": "customer_id"})
```

## Links de pagamento

### Criando um link de pagamento

```python
paymentLink = pagarme.paymentLinks.create({
    'amount' : 10000,
    'items' : {
        {
            'id' : '1',
            'title' : "Fighter's Sword",
            'unit_price' : 4000,
            'quantity' : 1,
            'tangible' : true,
            'category' : 'weapon',
            'venue' : 'A Link To The Past',
            'date' : '1991-11-21'
        },
        {
            'id' : '2',
            'title' : 'Kokiri Sword',
            'unit_price' : 6000,
            'quantity' : 1,
            'tangible' : true,
            'category' : 'weapon',
            'venue' : "Majora's Mask",
            'date' : '2000-04-27'
        },
    },
    'payment_config' : {
        'boleto' : {
            'enabled' : true,
            'expires_in' : 20
        },
        'credit_card' : {
            'enabled' : true,
            'free_installments' : 4,
            'interest_rate' : 25,
            'max_installments' : 12
        },
        'default_payment_method' : 'boleto'
    },
    'max_orders' : 1,
    'expires_in' : 60
})
```

### Retornando links de pagamento

```python
paymentLinks = pagarme.payment_link.find_all()
```

### Retornando um link de pagamento

```python
paymentLink = pagarme.payment_link.find_by_id('id_link_de_pagamento')
```

### Cancelando um link de pagamento

```python
paymentLink = pagarme.payment_link.cancel('id_link_de_pagamento')
```

## Support
Caso você tenha algum problema ou sugestão crie uma issue [here](https://github.com/pagarme/pagarme-python/issues).

## License

Clique [aqui](LICENSE).
