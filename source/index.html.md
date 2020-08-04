---
title: Eliodoro Staging API - v0.1.2
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
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="eliodoro-staging-api-with-api-keys-2">Eliodoro Staging API with API keys - 2 v1.0.2</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

API for comunication from Elidoro to the world in staging phase

Base URLs:

* <a href="https://api-gateway-qp76dmqroq-uc.a.run.app">https://api-gateway-qp76dmqroq-uc.a.run.app</a>

# Authentication

* API Key (api_key)
    - Parameter Name: **key**, in: query. 

<h1 id="eliodoro-staging-api-with-api-keys-2-payments">payments</h1>

Object that represent a payment for certain debt and that Eliodoro uses to inform to your debtors.

## Create or modify a new payment document

<a id="opIdcreate_update_payment_payments_create_post"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://api-gateway-qp76dmqroq-uc.a.run.app/payments \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

```http
POST https://api-gateway-qp76dmqroq-uc.a.run.app/payments HTTP/1.1
Host: api-gateway-qp76dmqroq-uc.a.run.app
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "payment_amount": 0,
  "payment_date": "2019-08-24T14:15:22Z",
  "payment_method": "string",
  "period_id": "string",
  "product_id": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('https://api-gateway-qp76dmqroq-uc.a.run.app/payments',
{
  method: 'POST',
  body: inputBody,
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
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api-gateway-qp76dmqroq-uc.a.run.app/payments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://api-gateway-qp76dmqroq-uc.a.run.app/payments', headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','https://api-gateway-qp76dmqroq-uc.a.run.app/payments', array(
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
URL obj = new URL("https://api-gateway-qp76dmqroq-uc.a.run.app/payments");
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
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api-gateway-qp76dmqroq-uc.a.run.app/payments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /payments`

Create or modify a payment object for one specific debt.

- **product_id**: Each debt has to be referenced by its product_id.
- **period_id**: The id that you use to reference the period of the debt.
- **payment_date**: The moment of the payment.
- **payment_amount**: How much the debtor has paid.
- **payment_method**: The method the debtor used to pay you.

> Body parameter

```json
{
  "payment_amount": 0,
  "payment_date": "2019-08-24T14:15:22Z",
  "payment_method": "string",
  "period_id": "string",
  "product_id": "string"
}
```

<h3 id="create-or-modify-a-new-payment-document-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[Payment](#schemapayment)|true|none|
|» payment_amount|body|integer|false|none|
|» payment_date|body|string(date-time)|false|none|
|» payment_method|body|string|false|none|
|» period_id|body|string|true|none|
|» product_id|body|string|true|none|

> Example responses

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="create-or-modify-a-new-payment-document-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The payment was updated succesfully|[Message](#schemamessage)|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|The payment was created succesfully|[Message](#schemamessage)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The debt was not found|[Message](#schemamessage)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
api_key
</aside>

## Delete a Payment object

<a id="opIddelete_paymentpayments_destroy_delete"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://api-gateway-qp76dmqroq-uc.a.run.app/payments \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

```http
DELETE https://api-gateway-qp76dmqroq-uc.a.run.app/payments HTTP/1.1
Host: api-gateway-qp76dmqroq-uc.a.run.app
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "period_id": "string",
  "product_id": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('https://api-gateway-qp76dmqroq-uc.a.run.app/payments',
{
  method: 'DELETE',
  body: inputBody,
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
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api-gateway-qp76dmqroq-uc.a.run.app/payments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.delete('https://api-gateway-qp76dmqroq-uc.a.run.app/payments', headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','https://api-gateway-qp76dmqroq-uc.a.run.app/payments', array(
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
URL obj = new URL("https://api-gateway-qp76dmqroq-uc.a.run.app/payments");
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
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://api-gateway-qp76dmqroq-uc.a.run.app/payments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /payments`

Delete one payment object created previously for one specific debt.

- **product_id**: Each debt has to be referenced by its product_id.
- **period_id**: The id that you use to reference the period of the debt.

> Body parameter

```json
{
  "period_id": "string",
  "product_id": "string"
}
```

<h3 id="delete-a-payment-object-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[PaymentBase](#schemapaymentbase)|true|none|
|» period_id|body|string|true|none|
|» product_id|body|string|true|none|

> Example responses

> 200 Response

```json
{
  "message": "string"
}
```

<h3 id="delete-a-payment-object-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The payment was succesfully deleted|[Message](#schemamessage)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The debt or payment was not found|[Message](#schemamessage)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
api_key
</aside>

# Schemas

<h2 id="tocS_HTTPValidationError">HTTPValidationError</h2>
<!-- backwards compatibility -->
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

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|detail|[[ValidationError](#schemavalidationerror)]|false|none|none|

<h2 id="tocS_Message">Message</h2>
<!-- backwards compatibility -->
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

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|true|none|none|

<h2 id="tocS_Payment">Payment</h2>
<!-- backwards compatibility -->
<a id="schemapayment"></a>
<a id="schema_Payment"></a>
<a id="tocSpayment"></a>
<a id="tocspayment"></a>

```json
{
  "payment_amount": 0,
  "payment_date": "2019-08-24T14:15:22Z",
  "payment_method": "string",
  "period_id": "string",
  "product_id": "string"
}

```

Payment

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|payment_amount|integer|false|none|none|
|payment_date|string(date-time)|false|none|none|
|payment_method|string|false|none|none|
|period_id|string|true|none|none|
|product_id|string|true|none|none|

<h2 id="tocS_PaymentBase">PaymentBase</h2>
<!-- backwards compatibility -->
<a id="schemapaymentbase"></a>
<a id="schema_PaymentBase"></a>
<a id="tocSpaymentbase"></a>
<a id="tocspaymentbase"></a>

```json
{
  "period_id": "string",
  "product_id": "string"
}

```

PaymentBase

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|period_id|string|true|none|none|
|product_id|string|true|none|none|

<h2 id="tocS_ValidationError">ValidationError</h2>
<!-- backwards compatibility -->
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

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|loc|[string]|true|none|none|
|msg|string|true|none|none|
|type|string|true|none|none|

