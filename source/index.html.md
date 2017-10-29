---
title: API Reference:

language_tabs: # must be one of https://git.io/vQNgJ
  - java
  - javascript

toc_footers:

includes:
  - errors

search: true
---

# Introdução

Bem vindo a  API da TRUSTHUB !

Aqui você poderá obter todas as informações que você precisa para conectar nas nossas soluções.
Você pode ver exemplos na area escura a diretira, e pode alterar  e pode alterar entre os tipos de linguagem pré definidas para integração.

Fique a vontade para nos conectar no caso de qualquer dificuldade.
.

# Conceitos básicos  

**API**  : API é o acrônimo de application programming interface,  especificação de interface para integração entre sistemas
			API tem como objetivo oferecer a possibilidade de estender funcionalidades básicas da plataforma, de forma a integrar com nossas soluções .
			
**Arquitetura REST** Utilizamos uma arquitetura REST, baseada 100% nos padrões HTTP
Stateless: a API não controla os estados, toda informação necessária é enviada pelo cliente.

**URLs**: cada recurso tem a sua própria e única URL, seguindo uma
   hierarquia lógica. Por exemplo: URL de um antecipacao negociada:
   https://api.trusthub.com.br/invoices/:id Métodos HTTP: todas as
   operações são realizadas usando os métodos HTTP corretos para cada
   caso, por exemplo:
   	 - GET: para consultar e ler recursos.
   	 - POST: para criar recursos.
   	 - PUT: para editar recursos.
   	 - DELETE: para eliminar recursos.
  	
  
**URL base da API**: A URL base da API, a partir da qual pode acessar todos os recursos disponíveis, é a seguinte: https://api.trusthub.com.br

**Dados em formato JSON** : Os dados são enviados e recebidos em formato JSON (JavaScript Object Notation), que é um formato baseado em texto, simples e facilmente utilizado em diferentes plataformas e linguagens

**Codificação** UTF-8 (PENDENTE ALISSON REVISAR) : Todas as solicitações (requests) e respostas (responses) utilizam codificação UTF-8.

**Formato da data e hora ISO-8601** : Todos os campos de data/hora utilizam a norma ISO-8601. Exemplo: 2014-04-24T16:37:22.032-04:00

**Gamas de IP para comunicacões**: Quando seja feito um envio de informação desde a plataforma de TRUSTHUB a os seus servidores (por exemplo desde  Webhooks), esse envío será feito desde alguma das IPs compreendidas nas seguintes gamas:
	 - 000.000.00.0 - 000.000.00.000  (Pendente Checagem do nosso IP de saida)
	 - 
**Requisitos** : Para utilizar API é necessário que se tenha familiaridade conceitos básicos utilizados no desenvolvimento de web services REST. É possível desenvolver a integração com as diferentes linguagens de programação web disponíveis  atualmente.
			Além do conhecimento técnico exigido, conhecer os conceitos básicos de negociações utilziadas na TRUSTHUB como "Nota Fiscal" ,  "XML" . O artigo abaixo sobre as entidades ásicas ajudará você a entender quais são e como se relacionam.
			
**Padrões** Nossa API segue os padrões de design e diretrizes o PAYPAL e especificação do protocolo HTTPS conforme referências abaixo.

 -   https://github.com/paypal/api-standards/blob/master/patterns.md
 - https://www.w3.org/Protocols/rfc2616/rfc2616.html

# Autenticação 

> Para autorização 

```javascript
const trusthub = require('trusthub');

let api = trusthub .authorize('trusthub');
```

![enter image description here](https://lh3.googleusercontent.com/-0QUCYoWz6sM/WfXMRd5cnaI/AAAAAAAAAAM/MVQenGq7upEGN93LgHUSnL4wtEPIiyBZACLcBGAs/s0/IMG_01.png "IMG_01.png")

Usando as suas credenciais, você garante que os seus dados só estejam disponíveis para a sua aplicação

**Como funciona?**

 - Envie as suas credenciais preenchendo [este formulário](formulario) e receba o seu token de acesso.  Use o seu access_token para operar com as APIs.
 Este código é único chamado access_token. Ele deverá ser utilizado para todas as operações que realizar com as APIs, enviando com atributo do Header da solicitação. (Pedente Alisson Request  de exemplo)
		
 - **Referências** 
	 - Referência Outh2.0  https://oauth.net/2/
	 - Bearer Token https://tools.ietf.org/html/rfc6750




# Recursos

## Notas Fiscais 

![enter image description here](https://lh3.googleusercontent.com/-Z7BoziXRnxg/WfXTD_SnhQI/AAAAAAAAAAc/32XHaN4OjykotEXx3N4i_dxdOg_KCTdFACLcBGAs/s0/IMG_02.png "IMG_02.png")

 - Este é o único serviço necessário para integrar seus clientes a TRUSTHUB.
 - Através deste serviço é possível enviar de forma muito simples as notas fiscais de seus clientes de onde será efetuado o pré cadastramento dos mesmos e de imediato já disponibilizado acesso para negociação das notas fiscais.
 - Após o envio das notas basta disponibilizar os links de acesso na nossa plataforma conforme _este exemplo_ passando seu TOKEN e identificação do cliente para que o mesmo possa negociar as notas com a TRUSTHUB de forma simples, ágil e segura.
 - Dependendo do formato mais adequado para sua solução e o relacionamento que tem que seu cliente você pode utilizar os dois processos abaixo para integração 
	 - Enviar as notas para TRUTHUB antecipadamente para todos os clientes que tem na sua aplicação agilizando o processo de abertura ou 
	 - Através de uma função de CALLBACK conforme  [este exemplo](w) identificar o aceite do cliente para com os termos de uso da TRUSTHUB no nosso link e passar a enviar as  notas.

<aside class="warning">Para uma melhor experiência do usuário e o mesmo já ser direcionado logado na nossa plataforma é importante na segunda opção que seja enviada pelo menos uma nota fiscal do mesmo de imediato. Caso contrário teremos que solicitar o cadastramento do mesmo o que não é muito legal !
</aside>			
	Após este primeiro aceite do cliente o deve ser mantido o envio rotineiro das demais notas e notas novas de seus clientes para que o mesmo as tenha para negociação na nossa plataforma
					

 - **Vamos explicar um pouco do processo que ocorre quando recebemos as notas**
	- Assim que recebemos a nota do seu cliente iremos efetuar pré cadastramento e quando o mesmo  acionar a TRUSTHUB a partir do nosso link presentes na sua plataforma iremos direciona-lo diretamente para área de negociações onde poderá serem já simuladas antecipações conforme _[este video](A)_. 
	- Por isso que é importante já enviar as notas de imediato quando identificar que seu cliente quer antecipar conosco.
	- Já no primeiro acesso do cliente iremos dar as boas vindas e notifica-lo na nossa plataforma e por email que o mesmo esta utilizando um login provisório e que deve ter sua senha alterada para posteriores acessos.
		
<aside class="success">
PRONTO !  A partir deste momento todo e qualquer acesso através do nosso link irá direcionar o cliente diretamente para fluxo de  negociações. ;)
</aside>

Para tratativas com notas fiscais o recurso a ser utilizado deverá ser :  /invoices   

 - POST/trusthub/invoices   : 
 - GET/trusthub/invoices ?invoice_key =
 - GET/trusthub/invoices ?client_key =
						
**trusthub/invoices   :**  Use este recurso para ações relacionadas e envio e busca dos dados de de notas fiscais. Como este serviço recebe o xml da nota e pode ser custoso o trafego, o mesmo deve ser compactado e será processado de forma assíncrona e em lote (BULK).

**JSON Base**
 
 - **invoices**  : Lista de chaves de notas fiscais 
	 - Tipo de Dado : Arrray(Object)
	 - Modo : Leitura / Escrita
		 - **client_key** : Chave de Identificação do cliente (Caso brasileiro CNPJ)
			 - Tipo de Dado : String(UUID)
			 - Modo : Leitura / Escrita
		 - **key** : Chave de Identificação da nota 
			 - Tipo de Dado : String(UUID)
			 - Modo : Leitura / Escrita
		 - **file**
			 - Tipo : Content-Type : text/xml 
			 - Modo  : Escrita
		 - **status** : Chave de Identificação da nota 
			 - Tipo de Dado : String(UUID)
			 - Modo : Leitura / Escrita
		 - **installments**  : Lista de  parcelas da nota fiscal.
			 - Tipo de Dado : Arrray(Object)
			 - Modo : Leitura / Escrita
				 - **document** : Numero do Documento da Parcela
					 - Tipo de Dado : String(UUID)
					 - Modo : Leitura 
				 - **maturity_date** : Data de vencimento da parcela
					 - Tipo de Dado : Date(ISO_8601)
					 - Modo : Leitura 
				 - **amount**: Valor da parcela 
					 - Tipo de Dado : String(UUID)
					 - Modo : Leitura
				 - **status**: Status da parcela
					 - Tipo de Dado : String(UUID)
					 - Modo : Leitura 


### Envio de Notas Fiscais 

```javascript

const trusthub = require('trusthub');
let api = trusthub .authorize('trusthub');
let kittens = api.invoices.post();
```


### HTTP Request

`POST/trusthub/invoices`

Use este recurso com esta ação para envio de notas fiscais. Como este serviço recebe o xml da nota e pode ser custoso o trafego, o mesmo deve ser compactado e será processado de forma assíncrona e em lote (BULK),


> Envio JSON conforme estrutura abaixo:
```json
POST /invoices
Host: api.foo.com
Content-Type: multipart/mixed; boundary=--invoice_file
Authorization: Bearer oauth2_token
Content-Length: total_content_length
Accept-Encoding: gzip, deflate

					[
"invoices": [
	{
		"cliente_key": "12345678000109",
		"invoice_key": "110000000000000000000000000000000000000000001",
		"invoice_file": Binary 
	},
 	{
		"cliente_key": "12345678000109",
		"invoice_key": "110000000000000000000000000000000000000000002",
		"invoice_file": Binary 
							}
							},
 	{
		"cliente_key": "12345678000109",
		"invoice_key": "110000000000000000000000000000000000000000003",
		"invoice_file": Binary 
							}
						}
					]

> Retorno JSON conforme estrutura abaixo:

```json
HTTP/1.1 200 OK
Content-Type: multipart/mixed; boundary=batch_111112-E=_XX11QQQYYY=
Date: Tue, 27 Jun 2017 18:56:00 GMT
Expires: Tue, 27 Jun 2017 18:56:00 GMT
Cache-Control: private, max-age=0
Content-Length: 5000

```

This endpoint retrieves all kittens.






### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>



### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten


