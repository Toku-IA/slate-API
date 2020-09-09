---
title: REST API de Toku. v0.3.0
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2
generator: widdershins v4.0.1

---

<h1 id="rest-api-de-toku-">REST API de Toku. v0.3.0</h1>

> Scrollea hacia abajo para ejemplos de código, requests y respuestas. Selecciona un lenguaje para ejemplos de código desde uno de los _tabs_ arriba o desde el menú de navegación de tu móvil.

¡Bienvenido a Toku.! 🤖 🚀

En esta documentación encontrarás lo necesario para utilizar nuestra API (Application Programming Interfaces), la cual es la interfaz para la integración del servicio prestado por Eliodoro junto con las aplicaciones y programas de nuestros clientes.

Toda la API de Toku. entrega respuestas en JSON con códigos HTTP para decir el éxito de la operación. En los _requests_ debes incluir el `Content-Type` como `application/json` y por ende, el body debe ser un JSON correcto.

Todas las request deben ser hechas con este url base:

> Base URLs:

> https://api.toku.cl

# Autenticación

Puedes comunicarte con nuestra API una vez que te hayas registrado con nosotros y te hayamos compartido una API Key, la cual debes poner en cada una de las llamadas hacia nosotros como se describe a continuación:

* API Key (api_key)
    - Nombre del parámetro: **x-api-key**, in: header. 

<h1 id="rest-api-de-toku--pagos-">Pagos 💳</h1>

Los objetos _Payment_ representan el **pago** hecho de una **deuda** que está registrada con nosotros.

## Crear o Modificar un Pago

<a id="opIdcreate_update_payment_payments_create_post"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X POST https://api.toku.cl/payments \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
POST https://api.toku.cl/payments HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/payments',
{
  method: 'POST',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.post 'https://api.toku.cl/payments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
})

r = requests.post('https://api.toku.cl/payments', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','https://api.toku.cl/payments', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/payments");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.toku.cl/payments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /payments`

Crear o modificar un objeto **pago** asociado a una **deuda** en específico.

> Parámetros en Body

```json
{
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}
```

<h3 id="crear-o-modificar-un-pago-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[Payment](#schemapayment)| Si  ||
|» payment_amount|body|integer|  No |El monto que se pagó de la deuda.|
|» payment_date|body|string(date-time)|  No |Fecha y hora en la cual se registro el pago de la deuda en su sistema. Debe estar en formato [ISO 8601](https://www.w3.org/TR/NOTE-datetime).|
|» payment_method|body|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|

#### Descripciones detalladas

**» payment_date**: Fecha y hora en la cual se registro el pago de la deuda en su sistema. Debe estar en formato [ISO 8601](https://www.w3.org/TR/NOTE-datetime).
 Puede ser sólo la fecha (2020-08-26) o como timestamp (2020-08-26T12:06:34Z), ten en consideración que se asumirá hora UTC en tanto no especifiques lo contrario.

#### Valores posibles

|Parámetro|Valor|
|---|---|
|» payment_method|PAC|
|» payment_method|PAT|
|» payment_method|WebPay|
|» payment_method|Transference|
|» payment_method|Other|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="crear-o-modificar-un-pago-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|El pago fue creado con éxito.|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

## Modificar Pago

<a id="opIdModificar_Pago_payments_update_put"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X PUT https://api.toku.cl/payments \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
PUT https://api.toku.cl/payments HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/payments',
{
  method: 'PUT',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.put 'https://api.toku.cl/payments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
})

r = requests.put('https://api.toku.cl/payments', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('PUT','https://api.toku.cl/payments', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/payments");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://api.toku.cl/payments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /payments`

Modificar un objeto **pago** asociado a una **deuda** en específico.

> Parámetros en Body

```json
{
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}
```

<h3 id="modificar-pago-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[Payment](#schemapayment)| Si  ||
|» payment_amount|body|integer|  No |El monto que se pagó de la deuda.|
|» payment_date|body|string(date-time)|  No |Fecha y hora en la cual se registro el pago de la deuda en su sistema. Debe estar en formato [ISO 8601](https://www.w3.org/TR/NOTE-datetime).|
|» payment_method|body|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|

#### Descripciones detalladas

**» payment_date**: Fecha y hora en la cual se registro el pago de la deuda en su sistema. Debe estar en formato [ISO 8601](https://www.w3.org/TR/NOTE-datetime).
 Puede ser sólo la fecha (2020-08-26) o como timestamp (2020-08-26T12:06:34Z), ten en consideración que se asumirá hora UTC en tanto no especifiques lo contrario.

#### Valores posibles

|Parámetro|Valor|
|---|---|
|» payment_method|PAC|
|» payment_method|PAT|
|» payment_method|WebPay|
|» payment_method|Transference|
|» payment_method|Other|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="modificar-pago-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

## Borrar un objeto Payment

<a id="opIddelete_payment_payments_destroy_delete"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X DELETE https://api.toku.cl/payments \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
DELETE https://api.toku.cl/payments HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/payments',
{
  method: 'DELETE',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.delete 'https://api.toku.cl/payments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
})

r = requests.delete('https://api.toku.cl/payments', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','https://api.toku.cl/payments', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/payments");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://api.toku.cl/payments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /payments`

Elimina un objeto **pago** creado anteriormente para una **deuda** en específico.

> Parámetros en Body

```json
{
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}
```

<h3 id="borrar-un-objeto-payment-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[PaymentDelete](#schemapaymentdelete)| Si  ||
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="borrar-un-objeto-payment-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

<h1 id="rest-api-de-toku--deudas-">Deudas 💰</h1>

Los objetos _Debt_ representan una **deuda** que algún deudor tiene con el cliente. Este objeto es la principal fuente de información para que Eliodoro determine la mejor hora y canal por el cual contactarse con dicho deudor, así que procura darnos al menos el email y el número de telefono para sacarle el mayor provecho a nuestro servicio y a Eliodoro 😉.

## Crear o Modificar Deuda

<a id="opIdCrear_o_Modificar_Deuda_debts_post"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X POST https://api.toku.cl/debts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
POST https://api.toku.cl/debts HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/debts',
{
  method: 'POST',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.post 'https://api.toku.cl/debts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
})

r = requests.post('https://api.toku.cl/debts', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','https://api.toku.cl/debts', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/debts");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.toku.cl/debts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /debts`

Crea o modifica un objeto **deuda** la cual representa una unidad a la cual Eliodoro debe contactar. 

Mientras más datos ingreses, es más probable que Eliodoro pueda responder más preguntas de sus deudores.

> Parámetros en Body

```json
{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}
```

<h3 id="crear-o-modificar-deuda-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[Debt](#schemadebt)| Si  ||
|» car_brand|body|string|  No |Marca de auto asociada a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» car_model|body|string|  No |Modelo de auto asociado a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» debt_amount|body|integer|  No |El monto de la deuda en pesos chilenos sin puntos. Por ejemplo, 10000.|
|» debtor_name|body|string|  No |Nombre con el cual nos referiremos al deudor, aquí puedes personalizarlo todo lo que quieras. Entrégalo como nombre propio: Juan Nieves.|
|» debtor_rut|body|string|  No |Rut del deudor sin puntos ni guión. Por ejemplo, si el rut es 12.345.678-K, entonces entrégalo así: 12345678K.|
|» default_reason|body|string|  No |Contiene la razón de rechazo de la deuda con la primera letra en mayúsculas.|
|» email|body|string|  No |Correo del deudor a contactar.|
|» link_pat|body|string|  No |Link para inscribir (o actualizar) el pago automático con tarjeta (o PAT). Debe ser un url válido, por lo que debe comenzar con `http://` o `https://`.|
|» link_payment|body|string|  No |Link de pago para el deudor específico. Se recomienda que sea único para que haya seguimiento de este link. Debe partir con `http://` o `https://`.|
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» phone_number|body|string|  No |Número de teléfono del deudor a contactar. Este número debe ser de celular dado los canales con los que nos comunicamos. Se admite sólo el siguiente formato: '+56987654321'.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|
|» regular_payment_method|body|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|

#### Valores posibles

|Parámetro|Valor|
|---|---|
|» regular_payment_method|PAC|
|» regular_payment_method|PAT|
|» regular_payment_method|WebPay|
|» regular_payment_method|Transference|
|» regular_payment_method|Other|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="crear-o-modificar-deuda-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|La deuda fue creada con éxito.|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

## Modificar Deuda

<a id="opIdModificar_Deuda_debts_put"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X PUT https://api.toku.cl/debts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
PUT https://api.toku.cl/debts HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/debts',
{
  method: 'PUT',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.put 'https://api.toku.cl/debts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
})

r = requests.put('https://api.toku.cl/debts', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('PUT','https://api.toku.cl/debts', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/debts");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://api.toku.cl/debts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /debts`

Modifica un objeto **deuda** la cual representa una unidad a la que Eliodoro debe contactar.

> Parámetros en Body

```json
{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}
```

<h3 id="modificar-deuda-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[Debt](#schemadebt)| Si  ||
|» car_brand|body|string|  No |Marca de auto asociada a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» car_model|body|string|  No |Modelo de auto asociado a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» debt_amount|body|integer|  No |El monto de la deuda en pesos chilenos sin puntos. Por ejemplo, 10000.|
|» debtor_name|body|string|  No |Nombre con el cual nos referiremos al deudor, aquí puedes personalizarlo todo lo que quieras. Entrégalo como nombre propio: Juan Nieves.|
|» debtor_rut|body|string|  No |Rut del deudor sin puntos ni guión. Por ejemplo, si el rut es 12.345.678-K, entonces entrégalo así: 12345678K.|
|» default_reason|body|string|  No |Contiene la razón de rechazo de la deuda con la primera letra en mayúsculas.|
|» email|body|string|  No |Correo del deudor a contactar.|
|» link_pat|body|string|  No |Link para inscribir (o actualizar) el pago automático con tarjeta (o PAT). Debe ser un url válido, por lo que debe comenzar con `http://` o `https://`.|
|» link_payment|body|string|  No |Link de pago para el deudor específico. Se recomienda que sea único para que haya seguimiento de este link. Debe partir con `http://` o `https://`.|
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» phone_number|body|string|  No |Número de teléfono del deudor a contactar. Este número debe ser de celular dado los canales con los que nos comunicamos. Se admite sólo el siguiente formato: '+56987654321'.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|
|» regular_payment_method|body|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|

#### Valores posibles

|Parámetro|Valor|
|---|---|
|» regular_payment_method|PAC|
|» regular_payment_method|PAT|
|» regular_payment_method|WebPay|
|» regular_payment_method|Transference|
|» regular_payment_method|Other|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="modificar-deuda-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

## Eliminar Deuda

<a id="opIdEliminar_Deuda_debts_delete"></a>

> Ejemplos de código

```shell
# You can also use wget
curl -X DELETE https://api.toku.cl/debts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-api-key: API_KEY'

```

```http
DELETE https://api.toku.cl/debts HTTP/1.1
Host: api.toku.cl
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-api-key':'API_KEY'
};

fetch('https://api.toku.cl/debts',
{
  method: 'DELETE',
  body: JSON.stringify(inputBody),
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'x-api-key' => 'API_KEY'
}

result = RestClient.delete 'https://api.toku.cl/debts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import json
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-api-key': 'API_KEY'
}

body = json.dumps({
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
})

r = requests.delete('https://api.toku.cl/debts', data = body,  headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'x-api-key' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','https://api.toku.cl/debts', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("https://api.toku.cl/debts");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://api.toku.cl/debts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /debts`

Elimina un objeto **deuda** junto con las interacciones que hayan sucedido bajo esta **deuda** con el deudor.

> Parámetros en Body

```json
{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}
```

<h3 id="eliminar-deuda-parameters">Parámetros</h3>

|Nombre|En|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|body|body|[Debt](#schemadebt)| Si  ||
|» car_brand|body|string|  No |Marca de auto asociada a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» car_model|body|string|  No |Modelo de auto asociado a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|» debt_amount|body|integer|  No |El monto de la deuda en pesos chilenos sin puntos. Por ejemplo, 10000.|
|» debtor_name|body|string|  No |Nombre con el cual nos referiremos al deudor, aquí puedes personalizarlo todo lo que quieras. Entrégalo como nombre propio: Juan Nieves.|
|» debtor_rut|body|string|  No |Rut del deudor sin puntos ni guión. Por ejemplo, si el rut es 12.345.678-K, entonces entrégalo así: 12345678K.|
|» default_reason|body|string|  No |Contiene la razón de rechazo de la deuda con la primera letra en mayúsculas.|
|» email|body|string|  No |Correo del deudor a contactar.|
|» link_pat|body|string|  No |Link para inscribir (o actualizar) el pago automático con tarjeta (o PAT). Debe ser un url válido, por lo que debe comenzar con `http://` o `https://`.|
|» link_payment|body|string|  No |Link de pago para el deudor específico. Se recomienda que sea único para que haya seguimiento de este link. Debe partir con `http://` o `https://`.|
|» period_id|body|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|» phone_number|body|string|  No |Número de teléfono del deudor a contactar. Este número debe ser de celular dado los canales con los que nos comunicamos. Se admite sólo el siguiente formato: '+56987654321'.|
|» product_id|body|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|
|» regular_payment_method|body|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|

#### Valores posibles

|Parámetro|Valor|
|---|---|
|» regular_payment_method|PAC|
|» regular_payment_method|PAT|
|» regular_payment_method|WebPay|
|» regular_payment_method|Transference|
|» regular_payment_method|Other|

> Ejemplos de respuesta

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="eliminar-deuda-responses">Respuestas</h3>

|Status|Significado|Descripción|Esquema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Operación realizada con éxito|[Message](#schemamessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Falta de credenciales.|[HTTPError](#schemahttperror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Falta de permisos. No tienes por qué estar ahi 👀.|[HTTPError](#schemahttperror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|El recurso no fue encontrado.|[HTTPError](#schemahttperror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Superaste el número máximos de request permitidos, espera un poquito.|[HTTPError](#schemahttperror)|

<aside class="warning">
Para llevar a cabo esta operación, debes estar autenticado, lo que significa que debes seguir uno de estos métodos: 
api_key
</aside>

# Esquemas

<h2 id="tocS_Debt">Debt</h2>

<a id="schemadebt"></a>
<a id="schema_Debt"></a>
<a id="tocSdebt"></a>
<a id="tocsdebt"></a>

```json
{
  "car_brand": "string",
  "car_model": "string",
  "debt_amount": 1,
  "debtor_name": "El Juan Nieves",
  "debtor_rut": "12345678K",
  "default_reason": "string",
  "email": "string",
  "link_pat": "https://www.google.cl",
  "link_payment": "https://www.google.cl",
  "period_id": "202008",
  "phone_number": "+56987658765",
  "product_id": "9897af7987d9245d",
  "regular_payment_method": "PAC"
}

```

Debt

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|car_brand|string|  No |Marca de auto asociada a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|car_model|string|  No |Modelo de auto asociado a la deuda. **Nota**: Esta variable fue construida específicamente para la industria de seguros de auto.|
|debt_amount|integer|  No |El monto de la deuda en pesos chilenos sin puntos. Por ejemplo, 10000.|
|debtor_name|string|  No |Nombre con el cual nos referiremos al deudor, aquí puedes personalizarlo todo lo que quieras. Entrégalo como nombre propio: Juan Nieves.|
|debtor_rut|string|  No |Rut del deudor sin puntos ni guión. Por ejemplo, si el rut es 12.345.678-K, entonces entrégalo así: 12345678K.|
|default_reason|string|  No |Contiene la razón de rechazo de la deuda con la primera letra en mayúsculas.|
|email|string|  No |Correo del deudor a contactar.|
|link_pat|string|  No |Link para inscribir (o actualizar) el pago automático con tarjeta (o PAT). Debe ser un url válido, por lo que debe comenzar con `http://` o `https://`.|
|link_payment|string|  No |Link de pago para el deudor específico. Se recomienda que sea único para que haya seguimiento de este link. Debe partir con `http://` o `https://`.|
|period_id|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|phone_number|string|  No |Número de teléfono del deudor a contactar. Este número debe ser de celular dado los canales con los que nos comunicamos. Se admite sólo el siguiente formato: '+56987654321'.|
|product_id|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|
|regular_payment_method|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|

<h2 id="tocS_HTTPError">HTTPError</h2>

<a id="schemahttperror"></a>
<a id="schema_HTTPError"></a>
<a id="tocShttperror"></a>
<a id="tocshttperror"></a>

```json
{
  "code": 0,
  "message": "string"
}

```

HTTPError

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|code|integer| Si  ||
|message|string| Si  ||

<h2 id="tocS_HTTPValidationError">HTTPValidationError</h2>

<a id="schemahttpvalidationerror"></a>
<a id="schema_HTTPValidationError"></a>
<a id="tocShttpvalidationerror"></a>
<a id="tocshttpvalidationerror"></a>

```json
{
  "detail": [
    {
      "loc": [
        "string"
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}

```

HTTPValidationError

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|detail|[[ValidationError](#schemavalidationerror)]|  No ||

<h2 id="tocS_Message">Message</h2>

<a id="schemamessage"></a>
<a id="schema_Message"></a>
<a id="tocSmessage"></a>
<a id="tocsmessage"></a>

```json
{
  "message": "string"
}

```

Message

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|message|string| Si  ||

<h2 id="tocS_Payment">Payment</h2>

<a id="schemapayment"></a>
<a id="schema_Payment"></a>
<a id="tocSpayment"></a>
<a id="tocspayment"></a>

```json
{
  "payment_amount": 10000,
  "payment_date": "2020-08-16T19:20:30-04:00",
  "payment_method": "PAC",
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}

```

Payment

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|payment_amount|integer|  No |El monto que se pagó de la deuda.|
|payment_date|string(date-time)|  No |Fecha y hora en la cual se registro el pago de la deuda en su sistema. Debe estar en formato [ISO 8601](https://www.w3.org/TR/NOTE-datetime).<br /> Puede ser sólo la fecha (2020-08-26) o como timestamp (2020-08-26T12:06:34Z), ten en consideración que se asumirá hora UTC en tanto no especifiques lo contrario.|
|payment_method|[PaymentMethod](#schemapaymentmethod)|  No |Método ocupado por el deudor para realizar el pago.|
|period_id|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|product_id|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|

<h2 id="tocS_PaymentDelete">PaymentDelete</h2>

<a id="schemapaymentdelete"></a>
<a id="schema_PaymentDelete"></a>
<a id="tocSpaymentdelete"></a>
<a id="tocspaymentdelete"></a>

```json
{
  "period_id": "202008",
  "product_id": "9897af7987d9245d"
}

```

PaymentDelete

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|period_id|string| Si  |El ID que usas para referenciar el periodo de la deuda que nos has dado. Debe estar en formato AAAAMM, sólo se admiten 6 caracteres.|
|product_id|string| Si  |El ID con el que reconoces la deuda (o el producto adeudado) que nos has dado. Largo permitido: 1 - 256 caracteres.|

<h2 id="tocS_PaymentMethod">PaymentMethod</h2>

<a id="schemapaymentmethod"></a>
<a id="schema_PaymentMethod"></a>
<a id="tocSpaymentmethod"></a>
<a id="tocspaymentmethod"></a>

```json
"PAC"

```

PaymentMethod

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|PaymentMethod|string|  No |Método ocupado por el deudor para realizar el pago.|

#### Valores numerados

|Propiedad|Valor|
|---|---|
|PaymentMethod|PAC|
|PaymentMethod|PAT|
|PaymentMethod|WebPay|
|PaymentMethod|Transference|
|PaymentMethod|Other|

<h2 id="tocS_ValidationError">ValidationError</h2>

<a id="schemavalidationerror"></a>
<a id="schema_ValidationError"></a>
<a id="tocSvalidationerror"></a>
<a id="tocsvalidationerror"></a>

```json
{
  "loc": [
    "string"
  ],
  "msg": "string",
  "type": "string"
}

```

ValidationError

### Propiedades

|Nombre|Tipo|Requerido|Descripción|
|---|---|---|---|---|
|loc|[string]| Si  ||
|msg|string| Si  ||
|type|string| Si  ||

