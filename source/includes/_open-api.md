# Open API

## Introduction

Investec provides a simple and powerful REST API to integrate your transactional data into your business or application. This API reference provides information on available endpoints and how to interact with it.

## Authentication (OAuth2)

OAuth2 requests must be authenticated with a valid access token passed as bearer token. To use the bearer token, construct a normal HTTPS request and include an Authorization header with the value of Bearer. Signing is not required.

### Enrolment

Login to https://login.secure.investec.com and navigate to https://logindev.secure.investec.com/io/programmable-banking/cards/overview where you can enroll your user for OAuth2 and obtain your client credential ***Need to add more here***

## Create OAuth Identity

## Get Access Token

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

var urlencoded = new URLSearchParams();
urlencoded.append("grant_type", "client_credentials");
urlencoded.append("scope", "accounts");

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: urlencoded,
  redirect: 'follow'
};

fetch("https://openapi.investec.com/identity/v2/oauth2/token", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

Represents a request to obtain a "client_credentials" grant typed access token.

`POST https://openapi.investec.com/identity/v2/oauth2/token`

| HEADERS      |                                   |
|--------------|-----------------------------------|
| Content-Type | application/x-www-form-urlencoded |

| BODY      |                                   |
|--------------|-----------------------------------|
| grant_type | client_credentials |
| scope | accounts |

## Get Accounts

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://openapi.investec.com/za/pb/v1/accounts", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

Returns a list of your accounts

`GET https://openapi.investec.com/za/pb/v1/accounts`

| HEADERS      |                                   |
|--------------|-----------------------------------|
| Content-Type | application/x-www-form-urlencoded |

## Get Transactions

```ruby
require "uri"
require "net/http"

url = URI("https://openapistg.investec.com/za/pb/v1/accounts/{{accountId}}/transactions")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Content-Type"] = "application/x-www-form-urlencoded"

response = https.request(request)
puts response.read_body
```

```python
import http.client
import mimetypes
conn = http.client.HTTPSConnection("openapistg.investec.com")
payload = ''
headers = {
  'Content-Type': 'application/x-www-form-urlencoded'
}
conn.request("GET", "/za/pb/v1/accounts/{{accountId}}/transactions", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://openapistg.investec.com/za/pb/v1/accounts/{{accountId}}/transactions' \
--header 'Content-Type: application/x-www-form-urlencoded'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://openapistg.investec.com/za/pb/v1/accounts/{{accountId}}/transactions", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### HTTP Request

`GET https://openapistg.investec.com/za/pb/v1/accounts/{{accountId}}/transactions`

| HEADERS      |                                   |
|--------------|-----------------------------------|
| Content-Type | application/x-www-form-urlencoded |

### Query Parameters

Parameter | Description
--------- | ------- | -----------
include_cats | If set to true, the result will also include cats.
available | If set to false, the result will include kittens that have already been adopted.
