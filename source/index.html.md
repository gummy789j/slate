---
title: API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - go
  - python
  - javascript

toc_footers:
  - <a href='https://bitgin.freshdesk.com/support/tickets/new' target="_blank">Contact us</a>

includes:
  - exchange
  - faas
  - mine-share
 # - errors



search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the BITGIN API documentation. We offer complete Exchange, Fiat-as-a-Service, Mine Share Service APIs to suit your needs. The BITGIN API is designed to allow access to all the features of the BITGIN platform.

We have language bindings in Go, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

REST Endpoint URL: **https://api.bitgin.net**

<aside class="notice">
<strong>
You can find sample code and mock server for each connectivity option at  <a href="https://github.com/BITGIN/bitgin-api-docs">https://github.com/BITGIN/bitgin-api-docs</a>.
</strong>
</aside>


# Authentication

> To authorize, use this code:

```go
import (
  "bytes"
  "net/http"
  "strconv"
  "crypto/hmac"
  "crypto/sha256"
  "encoding/hex"
  "math/rand"
  "time"
  "fmt"
)
func sign(payload string) string {
	hash := hmac.New(sha256.New, []byte("YOUR_API_SECRET"))
	hash.Write([]byte(payload))
	signature := hex.EncodeToString(hash.Sum(nil))
	return signature
}

func randFunc() string {
	rand.Seed(time.Now().Unix())
	// 2^32
	x := rand.Int63n(4294967296)
	return fmt.Sprintf("%08x", x)
}

func main() {
  method := http.MethodPost
  path := "<path_url>"
  timestamp := strconv.FormatInt(time.Now().Unix(), 10)
  nonce := randFunc()
  payload := fmt.Sprintf("%s%s%s%s%s", method, path, nonce, timestamp, string(<request_body>))
  signature := sign(payload)
  req, _ := http.NewRequest("POST", "<endpoint_url>" + path, bytes.NewBuffer(<request_body>))
  req.Header.Set("BG-API-KEY", "YOUR_API_KEY")
  req.Header.Set("BG-API-SIGN", signature)
  req.Header.Set("BG-API-NONCE", nonce)
  req.Header.Set("BG-API-TIMESTAMP", timestamp)
  req.Header.Set("Content-Type","application/json")
}
```

```python
import time
import hmac
from requests import Request
from random import randrange

ts = int(time.time())
# 2^32
nonce = f'{randrange(0,4294967296):0>8x}'
request = Request('POST', '<endpoint_url>' + '<path_url>')
prepared = request.prepare()
signature_payload = f'{prepared.method}{prepared.path_url}{nonce}{ts}{<request_body>}'.encode()
signature = hmac.new('YOUR_API_SECRET'.encode(), signature_payload, 'sha256').hexdigest()

prepared.headers['BG-API-KEY'] = 'YOUR_API_KEY'
prepared.headers['BG-API-SIGN'] = signature
prepared.headers['BG-API-NONCE'] = nonce
prepared.headers['BG-API-TIMESTAMP'] = str(ts)
prepared.headers['Content-Type'] = "application/json"

```


```javascript

```


For authenticated requests, the following headers should be sent with the request:

- `BG-API-KEY`: Your API key
- `BG-API-SIGN`: SHA256 HMAC of the following four strings, using your API secret, as a hex string:
  - HTTP method in uppercase (e.g. `GET` or `POST`)
  - Request path, including leading slash and any URL parameters but not including the hostname (e.g. `/v1/exchange/account`)
  - Random number in the half-open interval [0,2^32) with hexadecimal system
  - Request timestamp (e.g. `1649312027`)
  - (POST only) Request body (JSON-encoded)
- `BG-API-NONCE`: Random number in the half-open interval [0,2^32-1) with hexadecimal system
- `BG-API-TIMESTAMP`: Number of seconds since Unix epoch


<aside class="notice">
<strong>
You will find a detailed example on how to authenticate <a href="https://github.com/BITGIN/bitgin-api-docs#how-to-sign-your-data-">here</a>.
</strong>
</aside>

