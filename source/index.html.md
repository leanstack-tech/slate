---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  
includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Leanstack API
---

# Introduction

Welcome to the Leanstack API Documentation! This documentation contains endpoints and guides you need to power your hosting needs.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'net/http'

request = Net::HTTP::Post.new(url)
request["Authorization"] = "{access_key_from_dashboard}"
```

```python

```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "access-token: {access_key_from_dashboard}"
```

```javascript

```

> Make sure to replace `access_key_from_dashboard` with your API key.

Leanstack uses access-token to give you access to the API. You can sign up here to create your own key [developer portal](https://leanstack.co/enterprise/signup) and retrieve your keys from the settings area. For test requests use sandbox key, for live requests use live keys.

You can also provide a debug-id in your headers to leanstack. You can use this to debug requests if there are issues

Leanstack expects for the access key to be included in all API requests to the server in a header that looks like the following:

`access-token: {access_key_from_dashboard}`

<aside class="notice">
You must replace <code>{access_key_from_dashboard}</code> with your personal access token.
</aside>

# Customers

## Add Customer

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/customer")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"post_code\": \" 100001\"\n    }\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"post_code\": \" 100001\"\n    }\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/customer", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/customer' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "customer" : {
        "first_name" : "Bob",
        "last_name" : "Brown",
        "email" : "bobby20@gmail.com",
        "phone" : "090383938393"
    },
    "contact" : {
        "address" : "My home",
        "country" : "NG",
        "city" : "Lagos",
        "post_code": " 100001"
    }
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
    "customer" : {
        "first_name" : "Bob",
        "last_name" : "Brown",
        "email" : "bobby20@gmail.com",
        "phone" : "090383938393"
    },
    "contact" : {
        "address" : "My home",
        "country" : "NG",
        "city" : "Lagos",
        "post_code": " 100001"
    }
}
```

> the above endpoint returns JSON structured like this:

```json
{}

{
    "message": "Customer already exists for organisation"
}
```

This endpoint adds a customer to organisation using a request like this. Please set country as NG until more country support is added

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/customer`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
first_name | true | first name of customer. e.g 'Bob'
last_name | true | last name of customer. e.g 'Brown'
email | true | email of customer. e.g 'theemail@gmail.com'
phone | true | phone number of customer (please prepend with country code). e.g '2349018191818'
address | true | address of customer. e.g 'home'
country | true | country of customer. e.g 'NG'
city | true | city of customer. e.g 'Lagos'
post_code | true | postcode of customer. e.g '100001'

<aside class="success">
When <code>message</code> is returned, it means request is not complete and client needs to make changes and request again
</aside>

## Edit Customer

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/customer/{customer_id}")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Patch.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"post_code\": \" 100001\"\n    }\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"post_code\": \" 100001\"\n    }\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("PATCH", "/v1/enterprise/customer/200", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request PATCH 'https://api.leanstack.co/v1/enterprise/customer/200' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "customer" : {
        "first_name" : "Bob",
        "last_name" : "Brown",
        "email" : "bobby20@gmail.com",
        "phone" : "090383938393"
    },
    "contact" : {
        "address" : "My home",
        "country" : "NG",
        "city" : "Lagos",
        "post_code": " 100001"
    }
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
    "customer" : {
        "first_name" : "Bob",
        "last_name" : "Brown",
        "email" : "bobby20@gmail.com",
        "phone" : "090383938393"
    },
    "contact" : {
        "address" : "My home",
        "country" : "NG",
        "city" : "Lagos",
        "post_code": " 100001"
    }
}
```

> the above endpoint returns JSON structured like this:

```json
{}

{
    "message": "Customer does not exist for organisation"
}
```

This endpoint edits customer information using a request like this. Please set country as NG until more country support is added

### HTTP Request

`PATCH https://api.leanstack.co/v1/enterprise/customer/{customer_id}`

### Patch Parameters

Parameter | Required | Description
--------- | ------- | -----------
first_name | true | first name of customer. e.g 'Bobby'
last_name | true | last name of customer. e.g 'Brown'
email | true | email of customer. e.g 'theemail@gmail.com'
phone | true | phone number of customer (please prepend with country code). e.g '2349018191818'
address | true | address of customer. e.g 'home'
country | true | country of customer. e.g 'NG'
city | true | city of customer. e.g 'Lagos'
post_code | true | postcode of customer. e.g '100001'

<aside class="success">
When <code>message</code> is returned, it means request is not complete and client needs to make changes and request again
</aside>


## Show Customers

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/customers")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"query\" : \"trial\",\n    \"pagination\" : {\n \"page\" : 2,\n        \"page_size\" : 4\n    }\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n    \"query\" : \"trial\",\n    \"pagination\" : {\n        \"page\" : 2,\n        \"page_size\" : 4\n    }\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/customers", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/customers' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "query" : "trial",
    "pagination" : {
        "page" : 2,
        "page_size" : 4
    }
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
    "query" : "oduro",
    "pagination" : {
        "page" : 2,
        "page_size" : 4
    }
}
```

> the above endpoint returns a JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "first_name": "Trial",
            "last_name": "Pro",
            "phone": "234814116058",
            "email": "trial@gmail.com",
            "created_at": "2019-01-05T13:04:33.000Z"
        }
    ],
    "meta_data": {
        "query": "trial",
        "total_count": 5,
        "total_pages": 2,
        "page": 2,
        "page_size": 4
    }
}
```

> the above endpoint returns JSON structured like this:

This endpoint returns a list of customers belonging to organisation

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/customers`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
query | false | use this field to filter results
pagination['page'] | false | what page to return
pagination['page_size'] | false | size of data to return


## Get customer information

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/customer/{customer_id}")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["access-token"] = "{access_key_from_dashboard}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
}
conn.request("GET", "/v1/enterprise/customer/{customer_id}", headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://api.leanstack.co/v1/enterprise/customer/{customer_id}' \
--header 'access-token: {access_key_from_dashboard}' \
```

```javascript

```

> the above endpoint returns JSON structured like this:

```json
{
  "id": 1,
  "customer": {
    "first_name": "benk",
    "last_name": "thomas",
    "email": "benkthomas@gmail.com",
    "phone": "09019191919"
  },
  "contact": {
    "address": "home",
    "country": "NG",
    "city": "lagos",
    "post_code": "100001"
  }
}
```

This endpoint returns details for a specific customer id

### HTTP Request

`GET https://api.leanstack.co/v1/enterprise/customer/{customer_id}`

# Domains

## Domain Availability

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain_availability")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request.body = "{\n    \"domain_name\" : \"tunji\",\n    \"tld\" : \"com\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n    \"domain_name\" : \"tunji\",\n    \"tld\" : \"com\"\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
}
conn.request("POST", "https://api.leanstack.co/v1/enterprise/domain_availability", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/domain_availability' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "domain_name" : "tunji",
    "tld" : "com"
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
    "domain_name" : "tunji",
    "tld" : "com"
}
```

> the above endpoint returns JSON structured like this:

```json
{
    "tld_available": true,
    "dollar_price": "5",
    "naira_price": "3000",
    "domain_name_available": true
}

{
    "tld_available": true,
    "dollar_price": "5",
    "naira_price": "3000",
    "domain_name_available": false
}

{
    "tld_available": false
}
```

This endpoint checks for domain availability.

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain_availability`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
domain_name | true | domain name user wants to search for without the tld. e.g 'tradefair'
tld | true | the tld accompanying the domain name e.g 'com', 'ca'.

<aside class="success">
If request returns both <code>tld_available</code>  and <code>domain_name_available</code> as true, it means domain name is available for purchase
</aside>


## Domain Suggestion

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/rest/domain_suggestion")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"domain_name\" : \"tunji\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n    \"domain_name\" : \"tunji\"\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/rest/domain_suggestion", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/rest/domain_suggestion' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "domain_name" : "tunji"
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:
```json
{
    "domain_name" : "tunji"
}
```

> the above endpoint returns JSON structured like this:

```json
[
    {
        "domain_name": "yourtunji",
        "tld": "com",
        "dollar_price": "4.9",
        "naira_price": "4000"
    },
    {
        "domain_name": "tunjiclub",
        "tld": "com",
        "dollar_price": "4.9",
        "naira_price": "4000"
    },
    {
        "domain_name": "tunji",
        "tld": "tech",
        "dollar_price": "41",
        "naira_price": "15000"
    }
]
```

This endpoint checks for domain suggestions.

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain_suggestion`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
domain_name | true | domain name user wants to search for without the tld. e.g 'tradefair'

## Domain Order

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain/order")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"domain_name\" : \"blastedomains\",\n    \"tld\" : \"com\",\n    \"duration\" : 1,\n    \"customer_id\": 316,\n    \"domain_privacy\": false\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{https://api.leanstack.co/v1/enterprise/domain/order")
payload = "{\n    \"domain_name\" : \"testdomain\",\n    \"tld\" : \"com\",\n    \"duration\" : 1,\n    \"customer_id\": 316,\n    \"domain_privacy\": false\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
}
conn.request("POST", "https://api.leanstack.co/v1/enterprise/domain/order", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/domain/order' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "domain_name" : "testdomain",
    "tld" : "com",
    "duration" : 1,
    "customer_id": 316,
    "domain_privacy": false
}'
```

```javascript

```

> the above endpoint takes JSON structured like this:

```json
{
    "domain_name" : "testdomain",
    "tld" : "com",
    "duration" : 1,
    "customer_id": 316,
    "domain_privacy": false
}
```

> the above endpoint returns JSON structured like this:

```json
{
    "message": "Customer not found"
}

[
  {
    "status": "success",
    "domain_name": "testdomain.com"
  }
]

[
  {
    "status": "incomplete",
    "message": "Could not be completed automatically, request routed to support for completion"
    "domain_name": "testdomain.com"
  }
]
```

This endpoint orders a domain for a customer.

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain/order`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
domain_name | true | domain name user wants to search for without the tld. e.g 'tradefair'
tld | true | the tld accompanying the domain name e.g 'com', 'ca'.
customer_id | true | the id of the customer the domain should be provisioned for
duration | true | the number of years required
domain_privacy | true | is domain privacy required for domain

## Show Domains

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domains")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n  \"domain_name\" : \"trek\",\n  \"customer_id\": 312,\n  \"pagination\": {\n    \"page\": 2,\n    \"page_size\": 3\n  }\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n  \"domain_name\" : \"trek\",\n  \"customer_id\": 312,\n  \"pagination\": {\n    \"page\": 2,\n    \"page_size\": 3\n  }\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/domains", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/domains' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
  "domain_name" : "trek",
  "customer_id": 312,
  "pagination": {
    "page": 2,
    "page_size": 3
  }
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
  "domain_name" : "trek",
  "customer_id": 312,
  "pagination": {
    "page": 2,
    "page_size": 3
  }
}
```

> the above endpoint returns a JSON structured like this:

```json
{
    "data": [
        {
            "id": 5,
            "current_status": "1",
            "domain_name": "ourwalkers.com",
            "expiry": "2022-12-02T09:59:53.000Z",
            "created_at": "2021-12-02T09:59:53.898Z",
            "customer_id": 312
        },
        {
            "id": 4,
            "current_status": "1",
            "domain_name": "finalwalkers.com",
            "expiry": "2022-12-02T09:57:09.000Z",
            "created_at": "2021-12-02T09:57:09.747Z",
            "customer_id": 312
        },
        {
            "id": 3,
            "current_status": "1",
            "domain_name": "thewalkersorganisation.com",
            "expiry": "2022-12-02T09:50:48.000Z",
            "created_at": "2021-12-02T09:50:48.828Z",
            "customer_id": 312
        }
    ],
    "meta_data": {
        "query": "",
        "total_count": 3,
        "total_pages": 1,
        "page": 1,
        "page_size": 20
    }
}
```

> the above endpoint returns JSON structured like this:

This endpoint returns a list of domains belonging to organisation, you can filter by customer_id or by domain_name (domain name does not have to be in full)

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domains`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
domain_name | false | use this field to filter results
customer_id | false | use this field to filter results
pagination['page'] | false | what page to return
pagination['page_size'] | false | size of data to return

## Get domain information

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain/{domain_id}")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["access-token"] = "{access_key_from_dashboard}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
}
conn.request("GET", "/v1/enterprise/domain/{domain_id}", headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://api.leanstack.co/v1/enterprise/domain/{domain_id}' \
--header 'access-token: {access_key_from_dashboard}' \
```

```javascript

```

> the above endpoint returns JSON structured like this:

```json
{
    "domain_name": "friskhouse.com",
    "current_status": "InActive - Order Locked In Processing.",
    "registrar_lock": null,
    "expiry": "2022-12-06T08:08:27.000Z",
    "customer_id": 311,
    "customer_name": "Bob Brown",
    "nameservers": {
        "ns1": "ns1.sedoparking.com",
        "ns2": "ns2.sedoparking.com",
        "ns3": null,
        "ns4": null
    }
}
```

This endpoint returns details for a specific domain id

### HTTP Request

`GET https://api.leanstack.co/v1/enterprise/domain/{domain_id}`


## Update Domain nameservers

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain/{domain_id}/nameservers")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n  \"ns1\": \"ns1@sedoparking.com\",\n  \"ns2\": \"ns2@sedoparking.com\",\n  \"ns3\": \"ns3@sedoparking.com\",\n  \"ns4\": \"ns4@sedoparking.com\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload = "{\n  \"ns1\": \"ns1@sedoparking.com\",\n  \"ns2\": \"ns2@sedoparking.com\",\n  \"ns3\": \"ns3@sedoparking.com\",\n  \"ns4\": \"ns4@sedoparking.com\"\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/domain/{domain_id}/nameservers", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/domain/{domain_id}/nameservers' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
  "ns1": "ns1@sedoparking.com",
  "ns2": "ns2@sedoparking.com",
  "ns3": "ns3@sedoparking.com",
  "ns4": "ns4@sedoparking.com"
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
  "ns1": "ns1@sedoparking.com",
  "ns2": "ns2@sedoparking.com",
  "ns3": "ns3@sedoparking.com",
  "ns4": "ns4@sedoparking.com"
}
```

> the above endpoint returns JSON structured like this:

```
{}
```

This endpoint updates nameservers for a domain

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain{domain_id}/nameservers`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
ns1 | true | nameserver 1
ns2 | true | nameserver 2
ns3 | false | nameserver 3
ns4 | false | nameserver 4

## Update Domain Registrar Lock

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain/{domain_id}/registrar_lock")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access-token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n  \"enable_registrar_lock\": true\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
payload="{\n  \"enable_registrar_lock\": true\n}"
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/domain/{domain_id}/registrar_lock", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'https://api.leanstack.co/v1/enterprise/domain/{domain_id}/registrar_lock' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
  "enable_registrar_lock": true
}'
```

```javascript

```

> the above endpoint takes a JSON structured like this:

```json
{
  "enable_registrar_lock": true
}

{
  "enable_registrar_lock": false
}
```

> the above endpoint returns JSON structured like this:

```
{}
```

This endpoint updates registrar lock status for a domain

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain{domain_id}/registrar_lock`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
enable_registrar_lock | true | set registrar lock to true or false

## Get Domain Secret

```ruby
require "uri"
require "net/http"

url = URI("https://api.leanstack.co/v1/enterprise/domain/{domain_id}/domain_secret")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["access-token"] = "{access_key_from_dashboard}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("{host_url}")
headers = {
  'access-token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("GET", "/v1/enterprise/domain/{domain_id}/domain_secret", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request GET 'https://api.leanstack.co/v1/enterprise/domain/{domain_id}/domain_secret' \
--header 'access-token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
```

```javascript

```


```

> the above endpoint returns JSON structured like this:

```json

{
    "secret": "f`BvdTx7ka"
}
```

This endpoint returns domain secret for a domain

### HTTP Request

`POST https://api.leanstack.co/v1/enterprise/domain{domain_id}/domain_secret`


