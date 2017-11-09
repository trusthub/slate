---
title: API Reference

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

Aqui você poderá obter todas as informações que precisa para de conectar nas nossas soluções.
Você pode ver exemplos na área escura a direita e pode alternar os exemplos entre os tipos de linguagem pré definidas para integração.

Fique a vontade para nos contactar no tenha qualquer dificuldade través do [desenvolvimento@trusthub.com.br](desenvolvimento@trusthub.com.br).

Se pretende se tornar um parceiro por favor entrar em contato com [contato@trusthub.com.br](contato@trusthub.com.br) para mais informações.


# Conceitos básicos  

**API**  : API é o acrônimo de application programming interface,  especificação de interface para integração entre sistemas. Tem como objetivo oferecer a possibilidade de estender funcionalidades básicas da plataforma, de forma a integrar com nossas soluções.
			
**Arquitetura REST** Utilizamos uma arquitetura REST, baseada 100% nos padrões HTTP

 - Stateless: a API não controla os estados, toda informação necessária é enviada pelo cliente.
 - URLs : cada recurso tem a sua própria e única URL, seguindo uma
   hierarquia lógica. Por exemplo: URL de notas fiscais:
   [https://api.trusthub.com.br/invoices/](https://api.trusthub.com.br/invoices/) 
 - Métodos HTTP: todas as operações são realizadas usando os métodos HTTP corretos para cada
   caso, por exemplo:
   	 - GET: para consultar e ler recursos.
   	 - POST: para criar recursos.
   	 - PUT: para editar recursos.
   	 - DELETE: para eliminar recursos.
  
**URL base da API**: A URL base da API, a partir da qual pode acessar todos os recursos disponíveis, é a seguinte:  https://api.trusthub.com.br
	
**Dados em formato JSON** : Os dados são enviados e recebidos em formato JSON (JavaScript Object Notation), que é um formato baseado em texto, simples e facilmente utilizado em diferentes plataformas e linguagens

**Codificação** UTF-8  : Todas as solicitações (requests) e respostas (responses) utilizam codificação UTF-8.

**Formato da data e hora ISO-8601** : Todos os campos de data/hora utilizam a norma ISO-8601. Exemplo: 2017-04-24T16:37:22.032-04:00

**Gamas de IP para comunicacões**: Quando for feito envio de informação desde a plataforma de TRUSTHUB a os seus servidores (por exemplo caso de Webhooks), esse envio será feito desde alguma das IPs compreendidas nas seguintes gamas:

	   189.125.22.110  

**Requisitos** : Para utilizar API é necessário que se tenha familiaridade conceitos básicos utilizados no desenvolvimento de web services REST. É possível desenvolver a integração com as diferentes linguagens de programação web disponíveis  atualmente.
			Além do conhecimento técnico exigido, conhecer os conceitos básicos de negociações utilziadas na TRUSTHUB como "Nota Fiscal" ,  "XML" . O artigo abaixo sobre as entidades ásicas ajudará você a entender quais são e como se relacionam.
			
**Padrões** Nossa API segue os padrões de design e diretrizes o PAYPAL e especificação do protocolo HTTPS conforme referências abaixo.

 - https://github.com/paypal/api-standards/blob/master/patterns.md
 - https://www.w3.org/Protocols/rfc2616/rfc2616.html

**Homlogações** Para ambiente de homologação use o sufixo "hom" na URL base conforme segue:   

	https://api-hom.trusthub.com.br/integration/invoices/v1/

Neste ambiente constam todos serviços que serão disponibilizados no ambiente de produção de homologação somente sendo restringido o volume de transações. Para este ambiente deve ser utilizado TOKEN publico abaixo:

	99f0e2361ccbf5dca644e78ba6038316 


# Autenticação 

> Autenticação 

```java
request.addHeader("Authorization", "Bearer " + "99f0e2361ccbf5dca644e78ba6038316");
```

![enter image description here](https://raw.githubusercontent.com/maikelwgo/slate/master/source/images/IMG_01.png)


Usando as suas credenciais, você garante que os seus dados só estejam disponíveis para a sua aplicação.

**Como funciona?**

 - Para  credenciais no ambiente de produção entre em contato através da nossa área comercial [comercial@srmasset.com.br](comercial@srmasset.com.br) para cadastramento de sua plataforma  e receba o seu token de acesso.  Use o seu access_token para operar com as APIs.
Ele deverá ser utilizado para todas as operações que realizar com as APIs, enviando com atributo do Header da solicitação.
		
 - **Referências** 
	 - Referência Outh2.0  [https://oauth.net/2/](https://oauth.net/2/)
	 - Bearer Token [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)



# Recursos

## Envio de Notas Fiscais 

![enter image description here](https://lh3.googleusercontent.com/-a01IWyWouGc/WgRC65ckc1I/AAAAAAAAAA4/FDsGxHCrvLE5W8T4azpU1Bc-gAiLTuFBwCLcBGAs/s0/IMG_02.png "IMG_02.png")

 - Este é o único serviço necessário para integrar seus clientes para antecipação na TRUSTHUB.
 - Através deste serviço é possível enviar de forma muito simples as notas fiscais de seus clientes de onde será efetuado o pré cadastramento dos mesmos e de imediato já disponibilizando acesso para negociação das notas fiscais.
 - Após o envio das notas basta disponibilizar os links de acesso na nossa plataforma conforme conforme scripts que serão encaminhados pós cadastramento para que o mesmo possa negociar as notas com a TRUSTHUB de forma simples, ágil e segura.
 - Dependendo do formato mais adequado para sua solução e o relacionamento que tem que seu cliente você pode utilizar os dois processos abaixo para integração 
	 - Enviar as notas para TRUTHUB antecipadamente para todos os clientes que estão na sua plataforma agilizando o processo de abertura de conta do mesmo.
	 - Encaminhar as notas no momento do acionamento do link. Neste caso o usuário será direcionado porém terá que aguardar o carregamento das notas.

<aside class="warning">Para uma melhor experiência do usuário e o mesmo já ser direcionado logado na nossa plataforma é importante na segunda opção que seja enviada pelo menos uma nota fiscal do mesmo de imediato. Caso contrário teremos que solicitar o cadastramento do mesmo o que não é muito legal !
</aside>			
	Após este primeiro aceite do cliente o deve ser mantido o envio rotineiro das demais notas e notas novas de seus clientes para que o mesmo as tenha para negociação na nossa plataforma.
					

 - **Vamos explicar um pouco do processo que ocorre quando recebemos as notas**
	- Assim que recebemos a nota do seu cliente iremos efetuar pré cadastramento e quando o mesmo  acionar a TRUSTHUB a partir do nosso link presentes na sua plataforma iremos direciona-lo diretamente para área de negociações onde poderá serem já simuladas antecipações.
	- Por isso que é importante já enviar as notas de imediato quando identificar que seu cliente deseja antecipar conosco ou antes mesmo.
	- Já no primeiro acesso do cliente iremos dar as boas vindas e notifica-lo na nossa plataforma e por e-mail que o mesmo esta utilizando um login provisório e que deve ter sua senha alterada para posteriores acessos.
		
<aside class="success">
PRONTO !  A partir deste momento todo e qualquer acesso através do nosso link irá direcionar o cliente diretamente para fluxo de  negociações. ;) 
</aside>

Para tratativas de envio de invoices deve ser utilizado recurso conforme URL e exemplos como segue:	

`POST  https://api.hom.trusthub.com.br/invoices/v1/`

> Sample Request

```java

HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
File arquivo = new File("c:/srm-config/queue.properties");
multipartEntity.addPart("file_name", new FileBody(arquivo, contentType, arquivo.getName()));
multipartEntity.setContentType(contentType);
multipartEntity.setCharset(Charset.forName(charset));
multipartEntity.setBoundary(boundary);
request.setEntity(multipartEntity.build());
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + "99f0e2361ccbf5dca644e78ba6038316");
HttpResponse response = client.execute(request);


```

 Através deste recurso é possível o envio das notas fiscais de clientes. 

<aside class="warning">Importante salientar que os envios de arquivos de notas devem ser compactados através de padrão .zip de forma a otimizar o envio de informações.
</aside>		


## Consulta de Notas Fiscais por Chave

> Sample Request

```java
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + "99f0e2361ccbf5dca644e78ba6038316");
HttpResponse response = client.execute(request);
```

> Sample Response

```java
{
     "client_key" : "12345678909",
     "key" : "100-123",
     "status" : "PROCCESSED",
     "installments" : [
          {
                "document" : "100-123/1",
                "maturity_date" : "20171030103500",
                "amount" : "100.40",
                "status" : ""
          },
          {
                "document" : "100-123/2",
                "maturity_date" : "20171030113500",
                "amount" : "100.40",
                "status" : ""
          }
     ]
}

```

 Este recurso retorna informações de notas fiscais de uma determinada chave.


### HTTP Request

Consulta de notas fiscais por Chave 

`GET  https://api.hom.trusthub.com.br/invoices/v1/999999`




## Consulta de Notas Fiscais Por Parâmetros

> Sample Request

```java
//Requisição
HttpClient client = HttpClientBuilder.create().build();
HttpPost request = new HttpPost(url);
request.addHeader("charset", charset);
request.addHeader("Content-Type", contentType.getMimeType() + ";boundary=" + boundary + "; charset=" + charset);
request.addHeader("Accept", contentType.getMimeType());
request.addHeader("enctype", contentType.getMimeType());
request.addHeader("Authorization", "Bearer " + "99f0e2361ccbf5dca644e78ba6038316");
HttpResponse response = client.execute(request);
```

> Sample Response

```java
[
     {
          "client_key" : "12345678909",
          "key" : "100-123",
          "status" : "PROCCESSED",
          "installments" : [
                {
                     "document" : "100-123/1",
                     "maturity_date" : "20171030103500",
                     "amount" : "100.40",
                     "status" : ""
                },
                {
                     "document" : "100-123/2",
                     "maturity_date" : "20171030113500",
                     "amount" : "100.40",
                     "status" : ""
                }
          ]
     },
     {
          "client_key" : "12345678909",
          "key" : "215-321",
          "status" : "PROCCESSED",
          "installments" : [
                {
                     "document" : "215-321/1",
                     "maturity_date" : "20171030103500",
                     "amount" : "100.40",
                     "status" : ""
                },
                {
                     "document" : "215-321/2",
                     "maturity_date" : "20171030113500",
                     "amount" : "100.40",
                     "status" : ""
                }
          ]
     }
]


```
 Este EndPoint retorna informações de notas fiscais 
 de uma ou mais notas de acordo com parâmetros informados.


### HTTP Request

Consulta de notas fiscais por Chave 

`GET  https://api.hom.trusthub.com.br/invoices/v1/1/1`



Consulta de notas fiscais por Parametros

`GET  https://api.hom.trusthub.com.br/invoices/v1`

### URL Parameters

Parameter | Description
--------- | -----------
client_id | Id do cliente das notas em questão. No caso de notas brasileiras informar o CNPJ do cliente.
expire_date | Data de vencimento da duplicata da nota fiscal.
status | Status de negociação da duplicata da nota fiscal.

