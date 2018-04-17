---
title: TrustHub - API Reference

language_tabs: 
  - java

toc_footers:
  - <a href='https://www.trusthub.com.br'>www.trusthub.com.br</a>

includes:
  - errors

search: true
---

# Introdução

Bem vindo a  API da **TRUSTHUB** ! 

Aqui você poderá obter todas as informações que precisa para se conectar nas nossas soluções.
Você pode ver exemplos na área escura a direita e pode alternar os exemplos entre os tipos de linguagem pré definidas para integração.

Fique a vontade para nos contatar caso tenha qualquer dificuldade através do *desenvolvimento@trusthub.com.br*.

Se pretende se tornar um parceiro e acessar nosso ambiente de produção favor, entrar em contato com *contato@trusthub.com.br* para mais informações.


# Conceitos básicos  

**API**  : API é o acrônimo de application programming interface,  especificação de interface para integração entre sistemas. Tem como objetivo oferecer a possibilidade de estender funcionalidades básicas da plataforma, de forma a integrar com nossas soluções.
			
**Arquitetura REST** Utilizamos uma arquitetura REST, baseada 100% nos padrões HTTP.

 - Stateless: a API não controla os estados, toda informação necessária é enviada pelo cliente.
 - URLs : cada recurso tem a sua própria e única URL, seguindo uma
   hierarquia lógica. Por exemplo:  URL de notas fiscais:
   [https://api.trusthub.com.br/integration/invoices/](https://api.trusthub.com.br/integration/invoices/) 
 - Métodos HTTP: todas as operações são realizadas usando os métodos HTTP de acordo com cada intuito, por exemplo:
   	 - GET: para consultar e ler recursos.
   	 - POST: para criar recursos.
   	 - PUT: para editar recursos.
   	 - DELETE: para eliminar recursos.
  
**URL base da API**: A URL base da API, a partir da qual pode acessar todos os recursos disponíveis em produção, é a seguinte:  [https://api.trusthub.com.br/integration](https://api.trusthub.com.br/integration)
	
**Dados em formato JSON** : Os dados são enviados e recebidos em formato JSON (JavaScript Object Notation), que é um formato baseado em texto, simples e facilmente utilizado em diferentes plataformas e linguagens

**Codificação** UTF-8  : Todas as solicitações (requests) e respostas (responses) utilizam codificação UTF-8.

**Formato da data e hora ISO-8601** : Todos os campos de data/hora utilizam a norma ISO-8601. Exemplo: 2017-04-24T16:37:22.032-04:00

**Gamas de IP para comunicacões**: Quando for feito envio de informação a partir da plataforma de TRUSTHUB a os seus servidores (por exemplo caso de Webhooks), esse envio será feito desde alguma dos IPs compreendidas nas seguintes gamas:

	 189.125.22.110  

**Requisitos** : Para utilizar API é necessário que se tenha familiaridade conceitos básicos utilizados no desenvolvimento de web services REST. É possível desenvolver a integração com as diferentes linguagens de programação web disponíveis  atualmente.
			Além do conhecimento técnico exigido, é útil estar familiarizado com conceitos básicos de negociações utilizados na TRUSTHUB como "Nota Fiscal" ,  "XML" , "Duplicata", "Antecipação de recebíveis". 
			
**Padrões** Nossa API segue os padrões de design e diretrizes utilizados pelo PAYPAL e especificação do protocolo HTTPS conforme referências abaixo.

 - [https://github.com/paypal/api-standards/blob/master/patterns.md](https://github.com/paypal/api-standards/blob/master/patterns.md)
 - [https://www.w3.org/Protocols/rfc2616/rfc2616.html](https://www.w3.org/Protocols/rfc2616/rfc2616.html)

**Homlogações** Para ambiente de homologação use o sufixo "hom" na URL base conforme segue:   

 - [https://api-hom.trusthub.com.br/integration/invoices/v1/](https://api-hom.trusthub.com.br/integration/invoices/v1/)

Neste ambiente de homologação constam todos serviços que serão disponibilizados em produção, somente sendo restringido o volume de transações. Para este ambiente deve ser utilizado TOKEN público de homologações abaixo. 

	99f0e2361ccbf5dca644e78ba6038316 


# Autenticação 

> Autenticação 

```java
request.addHeader("Authorization", "Bearer " + "99f0e2361ccbf5dca644e78ba6038316");
```

![enter image description here](https://raw.githubusercontent.com/maikelwgo/slate/master/source/images/IMG_01.png)


Usando as suas credenciais, você garante que os seus dados só estejam disponíveis para a sua aplicação.

**Como funciona?**

 - Para  credenciais no ambiente de produção entre em contato através da nossa área comercial *contato@srmasset.com.br* para cadastramento de sua plataforma  e receba o seu token de acesso.  Use o seu access_token para operar com nossas API´s.
Ele deverá ser utilizado para todas as operações a serem realizadas, enviando com atributo do Header da solicitação conforme exemplo.
		
 - **Referências** 
	 - Referência Outh2.0  [https://oauth.net/2/](https://oauth.net/2/)
	 - Bearer Token [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)



# Recursos

## TrustHub Parcele+
TrustHub Parcele+ é uma solução da TrustHub oferecida para facilitar o crédito a Sacados, com a forma de pagamento através de boletos parcelados. Assim, com as vendas realizadas através desta opção de pagamento, é possível realizar a antecipação de crédito de forma rápida, ágil e segura para todos os Cedentes e Marketplace parceiros.

O fluxo dos pedidos inicia com a simulação de crédito para financiamento do valor total do pedido. Quando o Sacado escolher a melhor forma de pagamento, os dados do pedido, do Cedente e  do Sacado, são enviados e devidamente analisados pelas validações de negócio da TrustHub. Com base nessa análise detalhada, a TrustHub envia um retorno de liberação de crédito, aprovando ou rejeitando o mesmo.

Quando um pedido é aprovado, ele é acompanhado do inicio ao fim através dos recursos oferecidos pela API. Assim que recebidas todas as notas fiscais do pedido ele entrará para fila de antecipação de crédito ao Cedente e inicia-se o fluxo operacional do produto THPAR.


### Simular Pagamentos
O serviço de simulação é o serviço primário de integração com a API TrustHub para recebimento de simulações de crédito e gestão de pedidos online, facilitando a integração entre o Cedente TrustHub e, com ou sem o intermédio de um Marketplace. Através desse serviço é possível enviar os dados de identificação do Marketplace ou Cedente e o valor total do pedido, com base nesses dados básicos é realizada uma simulação de crédito e financiamento para o Sacado(comprador).

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/simulation`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
merchantDocument | Identificador do Marketplace ou e-commerce(Cedente).| STRING (30) | S
amount | Valor bruto total do pedido, incluindo taxa de entrega, descontos e demais valores relacionados. | DECIMAL (15,2) | S
clients | Para cada Cliente do Marketplace que tiver itens dentro da simulação, deve ser enviado o CPF/CNPJ deste Cliente neste parâmetro. | ARRAY | S
[clients] clientDocument | Para cada Cliente do Marketplace que tiver itens dentro da simulação, deve ser enviado o CPF/CNPJ deste Cliente neste parâmetro. Ou, em caso de e-commerce, enviar neste parâmetro o mesmo valor enviado no parâmetro merchantDocument | STRING (30) | S
[clients] amount | Para cara Cliente, também deve ser enviado o valor total dos pedidos destes isoladamente.  |DECIMAL (15,2) | S

> Sample Request

```java

{
  "merchantDocument" : "12589656/0001-01",
  "amount" : 200.52,
  "clients" : [
                {
                               "clientDocument":"158965852-96",
                               "amount" : 200.52
                }
  ]
}

```

**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de identificação do status da requisição do serviço.	| INTEGER	| S
responseStatus	|  Descrição do código de identificação do status.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S
simulation	| Lista com os dados de simulação: taxa de juros, valor bruto total (sem juros), condições de parcelamento possíveis, valor total atualizado (com juros). | ARRAY	| S
[simulation] taxAmount | Valor calculado do juros a aplicar sobre o valor bruto(amount) do pedido. | DECIMAL(15,2) | S  
[simulation] amount | Valor bruto do pedido, sem juros. | DECIMAL(15,2)|S
[simulation] amountWithTax | Valor bruto final do pedido, com juros. | DECIMAL(15,2)|S
[simulation] installments | Lista com as simulações de pagamento do pedido. Cada ID contém os seus dados individuais de parcelamento e valores respectivos. | ARRAY	| S
[installments] ID* | Índice da(s) condição(ões) de pagamento(s) geradas(s) através de regras internas da TrustHub. | INTEGER | S
[installments] installment	| Identificador do título(parcela).	| INTEGER	| S
[installments] amount	| Valor bruto total do título(parcela).	| DECIMAL (15,2)	| S


> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success",
    "responseStatusMessage": "",
    "simulation": [
        {
            "taxAmount": 20.05,
            "amount": 200.52,
            "amountWithTax": 220.57,
            "installments": [
                {
                    "1": [
                        {
                            "installment": 1,
                            "amount": 220.57
                        }
                    ]
                },
                {
                    "2": [
                        {
                            "installment": 1,
                            "amount": 110.29
                        },
                        {
                            "installment": 2,
                            "amount": 110.28
                        }
                    ]
                },
                {
                    "3": [
                        {
                            "installment": 1,
                            "amount": 73.53
                        },
                        {
                            "installment": 2,
                            "amount": 73.52
                        },
                        {
                            "installment": 3,
                            "amount": 73.52
                        }
                    ]
                },
                {
                    "4": [
                        {
                            "installment": 1,
                            "amount": 55.15
                        },
                        {
                            "installment": 2,
                            "amount": 55.14
                        },
                        {
                            "installment": 3,
                            "amount": 55.14
                        },
                        {
                            "installment": 4,
                            "amount": 55.14
                        }
                    ]
                },
                {
                    "5": [
                        {
                            "installment": 1,
                            "amount": 44.13
                        },
                        {
                            "installment": 2,
                            "amount": 44.11
                        },
                        {
                            "installment": 3,
                            "amount": 44.11
                        },
                        {
                            "installment": 4,
                            "amount": 44.11
                        },
                        {
                            "installment": 5,
                            "amount": 44.11
                        }
                    ]
                },
                {
                    "6": [
                        {
                            "installment": 1,
                            "amount": 36.77
                        },
                        {
                            "installment": 2,
                            "amount": 36.76
                        },
                        {
                            "installment": 3,
                            "amount": 36.76
                        },
                        {
                            "installment": 4,
                            "amount": 36.76
                        },
                        {
                            "installment": 5,
                            "amount": 36.76
                        },
                        {
                            "installment": 6,
                            "amount": 36.76
                        }
                    ]
                },
                {
                    "7": [
                        {
                            "installment": 1,
                            "amount": 31.51
                        },
                        {
                            "installment": 2,
                            "amount": 31.51
                        },
                        {
                            "installment": 3,
                            "amount": 31.51
                        },
                        {
                            "installment": 4,
                            "amount": 31.51
                        },
                        {
                            "installment": 5,
                            "amount": 31.51
                        },
                        {
                            "installment": 6,
                            "amount": 31.51
                        },
                        {
                            "installment": 7,
                            "amount": 31.51
                        }
                    ]
                },
                {
                    "8": [
                        {
                            "installment": 1,
                            "amount": 27.58
                        },
                        {
                            "installment": 2,
                            "amount": 27.57
                        },
                        {
                            "installment": 3,
                            "amount": 27.57
                        },
                        {
                            "installment": 4,
                            "amount": 27.57
                        },
                        {
                            "installment": 5,
                            "amount": 27.57
                        },
                        {
                            "installment": 6,
                            "amount": 27.57
                        },
                        {
                            "installment": 7,
                            "amount": 27.57
                        },
                        {
                            "installment": 8,
                            "amount": 27.57
                        }
                    ]
                },
                {
                    "9": [
                        {
                            "installment": 1,
                            "amount": 24.57
                        },
                        {
                            "installment": 2,
                            "amount": 24.5
                        },
                        {
                            "installment": 3,
                            "amount": 24.5
                        },
                        {
                            "installment": 4,
                            "amount": 24.5
                        },
                        {
                            "installment": 5,
                            "amount": 24.5
                        },
                        {
                            "installment": 6,
                            "amount": 24.5
                        },
                        {
                            "installment": 7,
                            "amount": 24.5
                        },
                        {
                            "installment": 8,
                            "amount": 24.5
                        },
                        {
                            "installment": 9,
                            "amount": 24.5
                        }
                    ]
                },
                {
                    "10": [
                        {
                            "installment": 1,
                            "amount": 22.12
                        },
                        {
                            "installment": 2,
                            "amount": 22.05
                        },
                        {
                            "installment": 3,
                            "amount": 22.05
                        },
                        {
                            "installment": 4,
                            "amount": 22.05
                        },
                        {
                            "installment": 5,
                            "amount": 22.05
                        },
                        {
                            "installment": 6,
                            "amount": 22.05
                        },
                        {
                            "installment": 7,
                            "amount": 22.05
                        },
                        {
                            "installment": 8,
                            "amount": 22.05
                        },
                        {
                            "installment": 9,
                            "amount": 22.05
                        },
                        {
                            "installment": 10,
                            "amount": 22.05
                        }
                    ]
                },
                {
                    "11": [
                        {
                            "installment": 1,
                            "amount": 20.07
                        },
                        {
                            "installment": 2,
                            "amount": 20.05
                        },
                        {
                            "installment": 3,
                            "amount": 20.05
                        },
                        {
                            "installment": 4,
                            "amount": 20.05
                        },
                        {
                            "installment": 5,
                            "amount": 20.05
                        },
                        {
                            "installment": 6,
                            "amount": 20.05
                        },
                        {
                            "installment": 7,
                            "amount": 20.05
                        },
                        {
                            "installment": 8,
                            "amount": 20.05
                        },
                        {
                            "installment": 9,
                            "amount": 20.05
                        },
                        {
                            "installment": 10,
                            "amount": 20.05
                        },
                        {
                            "installment": 11,
                            "amount": 20.05
                        }
                    ]
                },
                {
                    "12": [
                        {
                            "installment": 1,
                            "amount": 18.39
                        },
                        {
                            "installment": 2,
                            "amount": 18.38
                        },
                        {
                            "installment": 3,
                            "amount": 18.38
                        },
                        {
                            "installment": 4,
                            "amount": 18.38
                        },
                        {
                            "installment": 5,
                            "amount": 18.38
                        },
                        {
                            "installment": 6,
                            "amount": 18.38
                        },
                        {
                            "installment": 7,
                            "amount": 18.38
                        },
                        {
                            "installment": 8,
                            "amount": 18.38
                        },
                        {
                            "installment": 9,
                            "amount": 18.38
                        },
                        {
                            "installment": 10,
                            "amount": 18.38
                        },
                        {
                            "installment": 11,
                            "amount": 18.38
                        },
                        {
                            "installment": 12,
                            "amount": 18.38
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Registrar Pedido
O serviço de registro de pedidos é responsável por registrar a requisição de compra dentro da TrustHub. Os dados do Sacado, bem como do pedido do mesmo, são recebidos, registrados e, em cima destes, é feito uma análise detalhada que, posteriormente retornará ao Marketplace/Cedente a confirmação do pedido, ou seja, o aceite do financiamento e a liberação de crédito para o Sacado efetuar sua compra com sucesso.

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/submit`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
orderID	| Identificador do pedido gerado pelo Marketplace/Cedente	| STRING  (200)	| S
amount	| Valor final do pedido.	| DECIMAL (15,2)	| S
installments	| Quantidade de títulos de pagamento selecionados pelo Sacado.	| INTEGER	| S
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING  (30)	| S
merchantDocumentType	| Identificador do dado do valor recebido no parâmetro: merchantDocument.	| STRING  (30)	| S
clientDocument	| Identificador do vendedor do item: Cedente.	| STRING  (200)	| S
clientDocumentType	| Identificador do dado do valor recebido no parâmetro: clientDocument	| STRING  (30)	| S
miniCart	| Objeto com os dados essenciais do pedido: Dados do comprador, endereço de entrega e cobrança, itens do carrinho e demais tributos e descontos.	|OBJECT	|S
buyer	| Objeto com os dados básicos do Sacado.	| OBJECT| S
[buyer] firstName	| **Sacado PJ**: Recebe a razão social completa neste parâmetro. **Sacado PF**: Recebe o primeiro nome. | STRING  (200)	| S
[buyer] lastName	| **Sacado PJ**: Enviar vazio. **Sacado PF**: Sobrenome do Sacado.	| STRING  (200)	| N
[buyer] document	| Número do documento cadastrado no parceiro (Marketplace/Cedente).	| STRING  (30)	| S
[buyer] documentType	| Identificador do dado do valor recebido no parâmetro: buyer – document.	| STRING  (30)	| S
[buyer] email	| Email de contato do Sacado.	| STRING  (200)	| S
[buyer] phone	| Telefone principal do Sacado.	| STRING  (30)	| S
billingAddress	| Objeto com os dados do endereço de cobrança do Sacado.	|  OBJECT | S
[billingAddress] country	| Sigla do país do endereço de cobrança.	| STRING  (3)*	| S
[billingAddress] street	| Descrição da localização do endereço de cobrança.	| STRING  (300)	| S
[billingAddress] number	| Número do endereço de cobrança.	| INTEGER	| S
[billingAddress] complement	| Complemento do endereço de cobrança.	| STRING  (300)	| N
[billingAddress] neighborhood	| Bairro do endereço de cobrança.	| STRING  (300)	| S
[billingAddress] postalCode	| Código Postal/CEP do endereço de cobrança.	| STRING  (20)	| S
[billingAddress] city	| Cidade do endereço de cobrança.	| STRING  (100)	| S
[billingAddress] state	| Estado do endereço de cobrança.	| STRING  (100)	| S
shippingAddress	| Objeto com os dados do endereço de entrega do Sacado.	| OBJECT | S
[shippingAddress] country	| País do endereço de entrega.	| STRING  (3)*	| S
[shippingAddress] street| Descrição da localização do endereço de entrega.	| STRING  (300)	| S
[shippingAddress] number	| Número do endereço de entrega.	| INTEGER	| S
[shippingAddress] complement	| Complemento do endereço de entrega.	| STRING  (300)	| N
[shippingAddress] neighborhood	| Bairro do endereço de entrega.	| STRING  (300)	| S
[shippingAddress] postalCode	| Código Postal/CEP do endereço de entrega.	| STRING  (20)	| S
[shippingAddress] city	| Cidade do endereço de entrega.	| STRING  (100)	| S
[shippingAddress] state	| Estado do endereço de entrega.	| STRING  (100)	| S
Items	| Lista de items do pedido realizado pelo Sacado.	| LIST| S
[items] id	| Identificador do item do pedido do Cedente.	| STRING  (200)	| S
[items] name	| Descrição do item do pedido do Cedente.	| STRING  (300)	| S
[items] price	| Valor bruto unitário do item.	| DECIMAL (15,2)	| S
[items] quantity	| Quantidade do item.	| INTEGER	| S
[items] itemDiscount	| Valor bruto de desconto do item.	| DECIMAL (15,2)	| S
shippingAmount	| Valor bruto total da taxa de entrega.	| DECIMAL (15,2)	| N
taxAmount	| Valor bruto total de juros do financiamento TrustHub.	| DECIMAL (15,2)	| N
otherFees | Valor bruto total de outras taxas cobradas no pedido.	| DECIMAL (15,2)	| N
orderDiscount | Valor bruto total de descontos do pedido.	| DECIMAL (15,2)	| N
deviceFingerprint	| Identificador antifraude.	| STRING  (200)	| N

> Sample Request

```java
{
       "Id": "123456",
       "orderId": "v32478982vtx-01",
       "amount": 4307.23,
       "installments": 3,
       "merchantDocument": "88.256.695/0001-18",
       "merchantDocumentType": "CNPJ",
       "clientDocument": "88.256.695/0001-18",
       "clientDocumentType": "CNPJ",
       "miniCart": {
             "buyer": {
                    "firstName": "John",
                    "lastName": "Doe",
                    "document": "012.345.678-90",
                    "documentType": "CPF",
                    "email": "john@doe.com",
                    "phone": "+55 (21) 98765-4321"
             },
             "billingAddress": {
                    "country": "BRA",
                    "street": "Rua Praia de Botafogo",
                    "number": "518",
                    "complement": "2o. andar",
                    "neighborhood": "Botafogo",
                    "postalCode": "22250-040",
                    "city": "Rio de Janeiro",
                    "state": "RJ"
             },
             "shippingAddress": {
                    "country": "BRA",
                    "street": "Rua Praia de Botafogo",
                    "number": "518",
                    "complement": "2o. andar",
                    "neighborhood": "Botafogo",
                    "postalCode": "22250-040",
                    "city": "Rio de Janeiro",
                    "state": "RJ"
             },
             "items": [
                    {
                           "id": "132981",
                           "name": "Some useful product",
                           "price": 2134.9,
                           "quantity": 2,
                           "itemDiscount": 5
                    },
                    {
                           "id": "123242",
                           "name": "Some useless product",
                           "price": 21.98,
                           "quantity": 1,
                           "itemDiscount": 1
                    }
             ]
        },
        "shippingAmount": 11.44,
        "taxAmount": 10.01,
        "otherFees" : 0,
        "orderDiscount" : 0,
        "deviceFingerprint": "1234567890" 
}

```
**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de saída da requisição.	| INTEGER	| S
responseStatus	| Descrição do código de saída da requisição.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S

> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success",
    "responseStatusMessage": ""
}
```

### Consultar Pedido
O serviço de Consulta é responsável pelo envio do status atual do pedido que está sendo analisado pela TrustHub. 

**HTTP Request**

`GET  https://api-hom.trusthub.com.br/integration/order/v1/search/{merchantDocument}/{orderId}`

**Parâmetros de Entrada**


**URL Parameters**

Parameter | Description | Example
--------- | ----------- | -----------
orderId | Identificador do pedido. | v32478982vtx-01
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING  (30)	| S

**URL Entrada** :  `http://api-hom.trusthub.com.br/integration/order/v1/search/88256695000118/v32478982vtx-01`


**Parâmetros de Saída**


**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
orderID	| Identificador do pedido gerado pelo Marketplace/Cedente	| STRING (200)	| S
status	| Descrição do status geral do pedido	| STRING (200)	| S
tracking	| Descrição do status do pedido no Marketplace/Cedente	| STRING (200)	| S
amount	| Valor bruto total do pedido.	| DECIMAL (15,2)	| S
installments	| Quantidade de títulos de pagamento selecionados pelo Sacado.	| INTEGER	| S
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING (30)	| S
clientDocument	| Identificador do vendedor do item: Cedente.	| STRING (200)	| S
miniCart	| Objeto com os dados essenciais do pedido: Dados do comprador, endereço de entrega e cobrança, itens do carrinho e demais tributos e descontos.	| OBJECT	| S
buyer	| Objeto com os dados básicos do Sacado.	| OBJECT| S
[buyer] firstName	| **Sacado PJ**: Recebe a razão social completa neste parâmetro. **Sacado PF**: Recebe o primeiro nome. | STRING  (200)	| S
[buyer] lastName	| **Sacado PJ**: Enviar vazio. **Sacado PF**: Sobrenome do Sacado.	| STRING  (200)	| N
[buyer] document	| Número do documento cadastrado no parceiro (Marketplace/Cedente). 	| STRING (30)	| S
[buyer] email	| Email de contato do Sacado.	| STRING (200)	| S
Items	| Lista de items do pedido realizado pelo Sacado.	| LIST| S
[items] id	| Identificador do item do pedido do Cedente.	| STRING (200)	| S
[items] status	| Descrição do status do item do pedido.	| STRING (200)	| S
shippingAmount	| Valor bruto total da taxa de entrega.	| DECIMAL (15,2)	| N
taxAmount	| Valor bruto total de juros do financiamento TrustHub.	| DECIMAL (15,2)	| N
otherFees | Valor bruto total de outras taxas cobradas no pedido.	| DECIMAL (15,2)	| N
orderDiscount | Valor bruto total de descontos do pedido.	| DECIMAL (15,2)	| N
deviceFingerprint	| Identificador antifraude.	| STRING  (200)	| N

**Status | Monitoramento do Pedido**

Source | Status | Description 
--------- | ----------- | ---------
PEDIDO | RECEBIDO | Pedido recebido com sucesso. Iniciado processo de verificação dos dados.
PEDIDO | REJEITADO_PESSOA_FISICA| Pedido rejeitado automaticamente: Pessoa Física.
PEDIDO | REJEITADO_PAIS_DIFERENTE_BRASIL| Pedido rejeitado automaticamente: País do Sacado diferente de Brasil.
PEDIDO | REJEITADO_DIVERGENCIA_VALORES| Pedido rejeitado automaticamente: Valor calculado do pedido diverge do valor recebido.
PEDIDO | REJEITADO_CLIENTE_NAO_CADASTRADO | Pedido rejeitado automaticamente: Cliente não cadastrado.
PEDIDO | AGUARDANDO_APROVACAO | Aguardando a análise do Cedente e Sacado.
PEDIDO | APROVADO | Cedente e Sacado analisados automaticamente com sucesso.
PEDIDO | REJEITADO_APROVACAO | Cedente e Sacado analisados, porém com restrições de cadastro ou crédito.
PEDIDO | AGUARDANDO_APROVACAO_MANUAL | Aguardando a aprovação manual do pedido, por regras de negócio internas da TrustHub.
PEDIDO | REJEITADO_PARCEIRO| Pedido recebido com sucesso, porém com Marketplace/Cedente ou E-commerce não registrado na base da TrustHub.
PEDIDO | REJEITADO_CANCELADO_SACADO| Pedido cancelado pelo Sacado. Retorno de confirmação do cancelamento recebido pela TrustHub.
PEDIDO | REJEITADO_NOTA_FISCAL| Pedido rejeitado por divergências na Nota Fiscal.
TRACKING | CONFIRMADO | Pedido confirmado. Preparando para entrega.		
TRACKING | EM_TRANSITO | Pedido em rota de entrega.
TRACKING | ENTREGUE | Pedido entregue com sucesso.
TRACKING | REJEITADO | Pedido cancelado/rejeitado por motivos diversos.
NOTA_FISCAL | AGUARDANDO_NOTA_FISCAL | Aguardando Nota Fiscal para conferência de dados do pedido.
NOTA_FISCAL | NOTA_FISCAL_RECEBIDA | Nota Fiscal Recebida. Iniciado o processo de conferência da Nota Fiscal.
NOTA_FISCAL | NOTA_FISCAL_DIVERGENTE| Nota Fiscal com divergências.							
NOTA_FISCAL | NOTA_FISCAL_NAO_AUTORIZADA| Nota Fiscal não autorizada pela SEFAZ.		
NOTA_FISCAL | CONCORDANTE| Nota Fiscal concordante(sem divergências). Pedido confirmado. Aguardando para o inicio do processo operacional.
OPERACAO | INICIADO_PROCESSO_PAGAMENTO | Operação criada. Iniciado o processo operacional.
OPERACAO | AGUARDANDO_ASSINATURA_CONTRATOS | Aguardando a assinatura dos contratos Operacionais.
OPERACAO | AGUARDANDO_PAGAMENTO | Aguardando pagamento da Operação.										
OPERACAO | PEDIDO_PAGO | Operação paga com sucesso.

> Sample Response

```java
{   
    "orderId": "v32478982vtx-01",
    "status" : "",
    "tracking" : "",
    "amount": 4307.23,
    "installments": 3,
    "merchantDocument": "88.256.695/0001-18",
    "clientDocument": "88.256.695/0001-18",
    "miniCart": {
                   "buyer": {
                             "firstName": "MARCELO",
                             "lastName": "DOMES",
                             "document": "012.345.678-90",
                             "email": "marcelo@domes.com"
                   },
                   "items": [
                             {
                              "id": "132981",                          
                             },
                             {
                               "id": "123242",
                             }
                   ],
    "status" : "",
    "idOperation" : "",
    "statusOperation" : "",
    "shippingAmount": 11.44,
    "taxAmount": 10.01,
    "otherFees" : 0,
    "orderDiscount" : 0,
    "deviceFingerprint": "1234567890"
    }
}   
```

### Enviar Nota Fiscal do Pedido (arquivo)
Serviço utilizado para o envio dos arquivos xml das notas fiscais do pedido.

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/invoice/file`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
orderId	| Identificador do pedido gerado pelo Marketplace/Cedente	| STRING (200)	| S
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING  (30)	| S
zipName	| Nome do arquivo com a(s) nota(s) fiscal(is).	| STRING (200)	| S
zipData	| Arquivo zip convertido em STRING BASE64.	| STRING Base64	| S
invoices	| Lista de relação para vínculo entre o arquivo e o item.	| ARRAY	| S
[invoice] itemId |  Identifica*do*r do item do pedido.	| STRING (200)	| S
[invoice] fileName| Nome do arquivo xml contido dentro do arquivo zip.	| STRING (200)	| S

> Sample Request

```java
{
                "orderId": "v32478982vtx-01",
                "zipName" : "teste.zip",
                "zipData" : "",
                "fileNames" : [
                               {
                               "itemId" : "1",
                               "fileName" : "41170617047083000177550010000246841002246804-nfe.xml"
                               }
                ]
}
```

**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de saída da requisição.	| INTEGER	| S
responseStatus	| Descrição do código de saída da requisição.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S

> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success",
    "responseStatusMessage": ""
}
```
### Enviar Nota Fiscal do Pedido (chave de acesso)
Serviço utilizado para o envio da chave de acesso das notas fiscais do pedido.

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/invoice/key`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
orderId	| Identificador do pedido gerado pelo Marketplace/Cedente	| STRING (200)	| S
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING  (30)	| S
invoices | Lista de gestão das notas fiscais do pedido.	| LIST | S
[invoices] itemId| Identificador do item do pedido.	| STRING (200)	| S
[invoices] accessKey | Chave de acesso da nota fiscal vinculada ao item do pedido.	| STRING (200)	| S

> Sample Request

```java
{
    "orderId": "v32478982vtx-01",
    "invoices" : [
                   {
                   "itemId" : "1",
                   "accessKey" : "51171006116723000722550010000014861291207052"
                   },
                   {           
                   "itemId" : "1",
                   "accessKey" : "85975556546132321110000021500002465620244515"
                   }
    ]
}
```

**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de saída da requisição.	| INTEGER	| S
responseStatus	| Descrição do código de saída da requisição.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S

> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success",
    "responseStatusMessage": ""
}
```

### Atualizar Status Tracking
O serviço de atualização do status Tracking é responsável pelo recebimento da atualização de status do pedido no Marketplace/Cedente.

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/tracking`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
orderId	| Identificador do pedido gerado pelo Marketplace/Cedente	| STRING (200)	| S
merchantDocument	| Identificador do Marketplace ou Cliente. **Qual enviar?** Se a integração se dá através de um Marketplace, deve-se enviar os dados deste. Porém, quando a integração se dá diretamente do e-commerce do Cliente, sem um Marketplace de integração, deve-se enviar os dados do Cliente.	| STRING  (30)	| S
invoices | Lista de gestão das notas fiscais do pedido.	| LIST | S
Status	| Status do Marketplace/Cedente. Status permitidos: CONFIRMED, SHIPPED, COMPLETED, DECLINED	| STRING (30)	| S
Date	| Data/hora da atualização do status	| STRING (aaaa-MM-dd hh:mm)	| S
complement	| Descrição complementar ao status 	| ARRAY| N


> Sample Request

```java
{
  "orderId" : "12345678909",
  "merchantDocument": "88.256.695/0001-18",
  "status" : "CONFIRMED",
  "date" : "2018-01-10",
  "complement" : ""
}
```

**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de saída da requisição.	| INTEGER	| S
responseStatus	| Descrição do código de saída da requisição.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S

> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success",
    "responseStatusMessage": ""
}
```

### Consultar Limite de Crédito Sacado
Serviço utilizado para recebimento do limite de crédito atual disponível para o Sacado.

**HTTP Request**

`POST  https://api-hom.trusthub.com.br/integration/order/v1/credit-limit-buyer`

**Parâmetros de Entrada**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
buyerDocument | Número do documento do Sacado. 	| STRING (200)	| S
buyerDocumentType | Identificador do dado do valor recebido no parâmetro: buyerDocument.	| STRING (30)	| S

> Sample Request

```java
{
    "buyerdDocument": "08941084000170",
    "buyerDocumentType": "CNPJ"
}
```

**Parâmetros de Saída**

**URL Parameters**

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
responseCode	| Código de saída da requisição.	| INTEGER	| S
responseStatus	| Descrição do código de saída da requisição.	| STRING (200)	| S
responseStatusMessage	| Descrição adicional da TrustHub para o retorno.	| STRING (200)	| S
currentCreditLimit | Valor do limite de crédito atual do Sacado.	| DECIMAL (15,2)	| S

> Sample Response

```java
{
    "responseCode": 200,
    "responseStatus": "Success"
    "responseStatusMessage": "",
    "currentCreditLimit": 10000
}
```

## Envio de Notas Fiscais 

![enter image description here](https://lh3.googleusercontent.com/-a01IWyWouGc/WgRC65ckc1I/AAAAAAAAAA4/FDsGxHCrvLE5W8T4azpU1Bc-gAiLTuFBwCLcBGAs/s0/IMG_02.png "IMG_02.png")

 - Este é o único serviço necessário para integrar seus clientes para antecipação na TRUSTHUB.
 - Através deste serviço é possível enviar de forma muito simples as notas fiscais de seus clientes de onde será efetuado o pré cadastramento dos mesmos e de imediato já disponibilizando acesso para negociação das notas fiscais.
 - Após o envio das notas basta disponibilizar os links de acesso na nossa plataforma conforme scripts que serão encaminhados pós cadastramento para que o mesmo possa negociar as notas com a TRUSTHUB de forma simples, ágil e segura.
 - Dependendo do formato mais adequado para sua solução e o relacionamento que tem que seu cliente você pode utilizar os três processos abaixo para integração 
	 - Enviar as notas para TRUTHUB antecipadamente para todos os clientes que estão na sua plataforma agilizando o processo de abertura de conta do mesmo.
	 - Encaminhar as notas no momento do acionamento do link. Neste caso o usuário será direcionado porém terá que aguardar o carregamento das notas.
	 - Envio do email do cliente juntamente com as notas para que possamos cadastrar as notas, o cliente e enviar email para o mesmo com as instruções para acessar a plataforma.

<aside class="warning">Para uma melhor experiência do usuário e o mesmo já ser direcionado logado na nossa plataforma é importante na segunda opção que seja enviada pelo menos uma nota fiscal do mesmo de imediato. Caso contrário teremos que solicitar o cadastramento do mesmo o que não é muito legal ;)
E lembre-se que só serão aceitas notas com vencimento superior a data atual.
</aside>			
	Após este primeiro aceite do cliente deve ser mantido o envio rotineiro das demais notas e notas novas ( não necessita enviar o email ) para que o mesmo as tenha para negociação na nossa plataforma.
					

 - **Vamos explicar um pouco do processo que ocorre quando recebemos as notas**
	- Assim que recebemos a nota do seu cliente iremos efetuar pré cadastramento e quando o mesmo  acionar a nossa plataforma a partir do link presentes na sua plataforma iremos direciona-lo diretamente para área de negociações onde já poderá simular as antecipações.
	- Por isso é importante já enviar email e as notas de imediato quando identificar que seu cliente deseja antecipar conosco ou antes mesmo.
	- Já no primeiro acesso do cliente iremos dar as boas vindas e notifica-lo na nossa plataforma e por e-mail que o mesmo esta utilizando um login provisório e que deve ter sua senha alterada para posteriores acessos.
		
<aside class="success">
PRONTO !  A partir deste momento todo e qualquer acesso através do nosso link irá direcionar o cliente diretamente para fluxo de  negociações. ;) 
</aside>

Para tratativas de envio de invoices deve ser utilizado recurso conforme umas das duas URLs e exemplos como segue:	

 - Via Multipart: `POST  https://api-hom.trusthub.com.br/integration/invoices/v1/`
 - Via Json: `POST  https://api-hom.trusthub.com.br/integration/invoices/v1/json/`


Parameter | Tipo Envio | Description | Format | Required
--------- | ----------- | ----------- | --------- | -----------
Token 	| Todos | Use o seu access_token para operar com nossas API´s.	| STRING	| S
email	| Todos | Email que o cliente será cadastrado.	| STRING (200)	| N
fileName	| Json | Nome do arquivo zip que contem as notas.	| STRING (200)	| S
fileData	| Json | Arquivo zip na base 64.	| Base 64	| S


> Sample Request Multipart

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String url = "https://api-hom.trusthub.com.br/integration/invoices/v1/";
List<NameValuePair> postParameters = new ArrayList<>();
postParameters.add(new BasicNameValuePair("email", "emailcadastro@teste.com"));
URIBuilder uriBuilder = new URIBuilder(url);
uriBuilder.addParameters(postParameters);
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(uriBuilder.build());
String charset = "UTF-8";
ContentType contentType = ContentType.MULTIPART_FORM_DATA.withCharset(Charset.forName(charset));
String boundary = UUID.randomUUID().toString();
MultipartEntityBuilder multipartEntity = MultipartEntityBuilder.create();
ByteArrayOutputStream baos = new ByteArrayOutputStream();
ZipOutputStream zos = new ZipOutputStream(baos);
ZipEntry ze = new ZipEntry("c:/temp/teste_api/Fatura_OK.xml");
zos.putNextEntry(ze);
zos.closeEntry();
multipartEntity.addBinaryBody("teste.zip", baos.toByteArray(), contentType, "teste.zip");
multipartEntity.setContentType(contentType);
multipartEntity.setCharset(Charset.forName(charset));
multipartEntity.setBoundary(boundary);
request.setEntity(multipartEntity.build());
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
HttpResponse response = client.execute(request);


```

> Sample Request Json

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String url = "https://api-hom.trusthub.com.br/integration/invoices/v1/json/";
byte[] data = arquivo.getBytes();
JObject uploadFile = new JObject();
uploadFile.set("fileName", arquivo.getOriginalFilename());
uploadFile.set("fileData", Base64.encodeBase64String(data));
uploadFile.set("email", "emailcadastro@teste.com");
String charset = "UTF-8";
ContentType contentType = ContentType.APPLICATION_JSON.withCharset(Charset.forName(charset));
String boundary = UUID.randomUUID().toString();
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
StringEntity params = new StringEntity(uploadFile.toString()); //Json
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
request.setEntity(params);
HttpResponse response = client.execute(request);


```

 Através deste recurso é possível o envio das notas fiscais de clientes. 

<aside class="warning">Importante salientar que os envios de arquivos de notas devem ser compactados através de padrão ".zip" de forma a otimizar o envio de informações. E as notas devem terminarem com a extensão ".XML". Cada ".ZIP" deve conter ".XMLs" (Notas) de um único cedente.
</aside>			

## Consulta de Notas Fiscais por Chave

> Sample Request

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String chave = "INSERIR_CHAVE_AQUI";
HttpClient client = HttpClientBuilder.create().build();
HttpGet request = new HttpGet("https://api-hom.trusthub.com.br/integration/invoices/v1" + chave);
String charset = "UTF-8";
ContentType contentType = ContentType.APPLICATION_JSON.withCharset(Charset.forName(charset));
String boundary = "---------------" + UUID.randomUUID().toString();
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
HttpResponse response = client.execute(request);
```

> Sample Response

```java
{  
   "client_key":"99999999999999",
   "key":"000011111-250",
   "installments":[  
      {  
         "document":"000011111",
         "maturity_date":"20180301000000",
         "amount":9975.2100,
         "status":"ENVIADO",
		 "liquidation_date":"20180301000000",
		 "transmission_date":"20180301000000"
      },
	  {  
         "document":"000022222",
         "maturity_date":"20180302000000",
         "amount":8875.2100,
         "status":"ENVIADO",
		 "liquidation_date":"20180301000000",
		 "transmission_date":"20180301000000"
      }
   ]
}

```

 Através deste recurso é possível retornar informações de notas fiscais de uma determinada chave.
 
Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
Token 	| Use o seu access_token para operar com nossas API´s.	| STRING	| S
chave	| Chave que identifica a nota.	| STRING	| S


### HTTP Request

Consulta de notas fiscais por Chave 

`GET  https://api-hom.trusthub.com.br/integration/invoices/v1/999999`




## Consulta de Notas Fiscais Por Parâmetros

> Sample Request

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String cnpj = "INSERIR_CNPJ_AQUI";
String dataInicial = "INSERIR_DATA_INICIAL_AQUI";
String dataFinal = "INSERIR_DATA_FINAL_AQUI";
String idStatus = "INSERIR_ID_STATUS_AQUI";
String paginaInicial = "INSERIR_PAG_INICIAL_AQUI";
String paginaFim = "INSERIR_PAG_FIM_AQUI";
HttpClient client = HttpClientBuilder.create().build();
HttpGet request = new HttpGet("https://api-hom.trusthub.com.br/integration/invoices/v1/" + cnpj + "/" + dataInicial + "/" + dataFinal + "/" + idStatus + "/" + paginaInicial + "/" + paginaFim);
String charset = "UTF-8";
ContentType contentType = ContentType.APPLICATION_JSON.withCharset(Charset.forName(charset));
String boundary = "---------------" + UUID.randomUUID().toString();
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
HttpResponse response = client.execute(request);
```

> Sample Response

```java
{  
   "arrayInstallments":[  
      {  
         "client_key":"99999999999999",
         "key":"000000001-007",
         "installments":[  
            {  
               "document":"000000001",
               "maturity_date":"20180301000000",
               "amount":5.0000,
               "status":"EM ANÁLISE",
			   "liquidation_date":"20180301000000",
			   "transmission_date":"20180301000000"
            }
         ]
      },
      {  
         "client_key":"99999999999999",
         "key":"000000006-008",
         "installments":[  
            {  
               "document":"000000046",
               "maturity_date":"20180215000000",
               "amount":5.0000,
               "status":"EM ANÁLISE",
			   "liquidation_date":"20180301000000",
			   "transmission_date":"20180301000000"
            },
            {  
               "document":"000000901",
               "maturity_date":"20180210000000",
               "amount":90.0000,
               "status":"EM ANÁLISE",
			   "liquidation_date":"20180301000000",
			   "transmission_date":"20180301000000"
            }
         ]
      }
   ],
   "pagination":{  
      "page_size":20,
      "total_regs":"3",
      "pages":1,
      "from_page":1,
      "to_page":100
   }
}


```
 Através deste recurso é possível retornar informações de uma ou mais notas de acordo com parâmetros informados.
 Importante salientar que este recurso trabalha com paginação no formato de *Path Parameter*  onde o primeiro parâmetro é o inicio do registro da paginação e o segundo o fim do registro da paginação desejada.


### HTTP Request

Consulta de notas fiscais por Parametros.

`GET  https://api-hom.trusthub.com.br/integration/invoices/v1/{cnpj}/{dataInicial}/{dataFinal}/{idStatus}/{paginaInicial}/{paginaFim}`


### URL Parameters

O padrão de data para ser enviada deve ser: AAAA-MM-DD.

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
Token 	| Use o seu access_token para operar com nossas API´s.	| STRING	| S
cnpj | Id do cliente das notas em questão. No caso de notas brasileiras informar o CNPJ do cliente.	| STRING	| S
dataInicial | Data inicial de vencimento da duplicata da nota fiscal.	| STRING	| S
dataFinal | Data final de vencimento da duplicata da nota fiscal.	| STRING	| S
idStatus | Status da duplicata.	| INTEGER	| S

## Cadastrar Cliente

> Sample Request

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String cnpj = "INSERIR_CNPJ_AQUI";
JObject cedente = new JObject();
cedente.set("cnpj", "INSERIR_CNPJ_AQUI");
cedente.set("email", "INSERIR_EMAIL_AQUI");
String url = "https://api-hom.trusthub.com.br/integration/invoices/v1/register/";
String charset = "UTF-8";
ContentType contentType = ContentType.APPLICATION_JSON.withCharset(Charset.forName(charset));
String boundary = UUID.randomUUID().toString();
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
StringEntity params = new StringEntity(cedente.toString());
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
request.setEntity(params);
HttpResponse response = client.execute(request);
```

> Sample Response

```java
{  
   "mensagem":"Request successfully.",
   "sucesso":true
}


```
 Cadastro cliente pelo CNPJ e email. Assim que recebemos a requisição, iremos processar o cadastramento do cliente, caso seja encontradas todas as informações necessárias estaremos enviando um email de boas vindas com as informações para operar na plataforma.


### HTTP Request

`POST  https://api-hom.trusthub.com.br/integration/invoices/v1/register/`


### URL Parameters

Parameter | Description | Format | Required
--------- | ----------- | --------- | -----------
Token 	| Use o seu access_token para operar com nossas API´s.	| STRING	| S
cnpj | CNPJ do cliente que será cadastrado.	| STRING	| S
email | Email que o cliente será cadastrado.	| STRING (200)	| S

## Login Automático

> Sample Request

```java
String TOKEN_PARCEIRO = "99f0e2361ccbf5dca644e78ba6038316";
String cnpj = "INSERIR_CNPJ_AQUI";
String erpCode = "INSERIR_AQUI_O_ERP_CODE_DO_PARCEIRO";
JObject p = new JObject();
p.set("erp-code", erpCode);
p.set("cnpj-cliente", cnpj);
String url = "https://api-hom.trusthub.com.br/integration/invoices/v1/generate-token/";
String charset = "UTF-8";
ContentType contentType = ContentType.APPLICATION_JSON.withCharset(Charset.forName(charset));
String boundary = UUID.randomUUID().toString();
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
StringEntity params = new StringEntity(p.toString());
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + TOKEN_PARCEIRO);
request.setEntity(params);
HttpResponse response = client.execute(request);
```

> Sample Response

```java
{  
   "temporary-token":"MzM3YzM0MzQzNjMzMzYzMjM2MzYzMDMwMzAzMTMwMzk3YzRlN2MzMjMwMzEzODMwMzEzMTM3MzEzNDM0MzIzMjM1MzEzNTM0MzA="
}


```
 O login automático se dar através de um token gerado pela Trusthub que tem validade de uso.
 O processo se dar em duas etapas:
 - Chamar o serviço de geração de token https://api-hom.trusthub.com.br/integration/invoices/v1/generate-token/;
 - Com o token retornado deve-se acessar o portal passando o token gerado no fim da url do portal. https://hom.trusthub.com.br/trusthub-antecipacao-web/#/redirect-logged-user/{temporary-token}

 No momento do acesso com o token na aplicação, caso o cliente não esteja cadastrado, estaremos cadastrando o mesmo e redirecionando o mesmo logado.
 
 Exemplo de botão de Login: [http://hom.trusthub.com.br/HTML-API/box.html](http://hom.trusthub.com.br/HTML-API/box.html)
