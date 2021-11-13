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

Welcome to the Leanstack API Documenation! This documentation contains endpoints and guides you need to power your hosting needs.

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
  -H "access_token: {access_key_from_dashboard}"
```

```javascript

```

> Make sure to replace `access_key_from_dashboard` with your API key.

Leanstack uses access_token to give you access to the API. You can sign up here to create your own key [developer portal](http://example.com/developers).

You can also provide a debug_id in your headers to leanstack. You can use this to debug requests if there are issues

Leanstack expects for the access key to be included in all API requests to the server in a header that looks like the following:

`access_token: {access_key_from_dashboard}`

<aside class="notice">
You must replace <code>{access_key_from_dashboard}</code> with your personal access token.
</aside>

# Domain Registration

## Domain Availability

```ruby
require "uri"
require "net/http"

url = URI("http://{base_url}/v1/enterprise/domain_availability")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access_token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request.body = "{\n    \"domain_name\" : \"tunji\",\n    \"tld\" : \"com\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("localhost", 3000)
payload = "{\n    \"domain_name\" : \"tunji\",\n    \"tld\" : \"com\"\n}"
headers = {
  'access_token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
}
conn.request("POST", "{base_url}/v1/enterprise/domain_availability", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST '{base_url}/v1/enterprise/domain_availability' \
--header 'access_token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "domain_name" : "tunji",
    "tld" : "com"
}'
```

```javascript

```

> The above command returns JSON structured like this:

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

`GET https://api.leanstack.co/v1/enterprise/domain_availability`

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

url = URI("http://localhost:3000/v1/rest/domain_suggestion")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access_token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"domain_name\" : \"tunji\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("localhost", 3000)
payload = "{\n    \"domain_name\" : \"tunji\"\n}"
headers = {
  'access_token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/rest/domain_suggestion", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'http://localhost:3000/v1/rest/domain_suggestion' \
--header 'access_token: {access_key_from_dashboard}' \
--header 'Content-Type: application/json' \
--header 'Cookie: __profilin=p%3Dt' \
--data-raw '{
    "domain_name" : "tunji"
}'
```

```javascript

```

> The above command returns JSON structured like this:

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

`GET https://api.leanstack.co/v1/enterprise/domain_suggestion`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
domain_name | true | domain name user wants to search for without the tld. e.g 'tradefair'

# Customers

## Add Customer

```ruby
require "uri"
require "net/http"

url = URI("http://localhost:3000/v1/enterprise/add_customer")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["access_token"] = "{access_key_from_dashboard}"
request["Content-Type"] = "application/json"
request["Cookie"] = "__profilin=p%3Dt"
request.body = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"postcode\": \" 100001\"\n    }\n}"

response = http.request(request)
puts response.read_body

```

```python
import http.client

conn = http.client.HTTPSConnection("localhost", 3000)
payload = "{\n    \"customer\" : {\n        \"first_name\" : \"Bob\",\n        \"last_name\" : \"Brown\",\n        \"email\" : \"bobby20@gmail.com\",\n        \"phone\" : \"090383938393\"\n    },\n    \"contact\" : {\n        \"address\" : \"My home\",\n        \"country\" : \"NG\",\n        \"city\" : \"Lagos\",\n        \"postcode\": \" 100001\"\n    }\n}"
headers = {
  'access_token': '{access_key_from_dashboard}',
  'Content-Type': 'application/json',
  'Cookie': '__profilin=p%3Dt'
}
conn.request("POST", "/v1/enterprise/add_customer", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl --location --request POST 'http://localhost:3000/v1/enterprise/add_customer' \
--header 'access_token: {access_key_from_dashboard}' \
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
        "postcode": " 100001"
    }
}'
```

```javascript

```

> The above command takes a JSON structured like this:

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
        "postcode": " 100001"
    }
}
```

> The above command returns JSON structured like this:

```json
{}

{
    "message": "Customer already exists for organisation"
}
```

This endpoint adds a customer to organisation using a request like this

### HTTP Request

`GET https://api.leanstack.co/v1/enterprise/add_customer`

### Post Parameters

Parameter | Required | Description
--------- | ------- | -----------
first_name | true | first name of customer. e.g 'Bobby'
last_name | true | last name of customer. e.g 'Brown'
email | true | email of customer. e.g 'theemail@gmail.com'
phone | true | phone number of customer (please prepend with country code). e.g '2349018191818'
address | true | address of customer. e.g 'home'
country | true | country of customer. e.g 'NG'
city | true | city of customer. e.g 'Lagos'
postcode | true | postcode of customer. e.g '100001'

<aside class="success">
When <code>message</code> is returned, it means request is not complete and client needs to make changes and request again
</aside>
