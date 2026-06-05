# 10、Sample Code

## 1、Call the Support chain tokens enum api <a href="#id-1-call-the-v2-address-risk-detection-interface" id="id-1-call-the-v2-address-risk-detection-interface"></a>

**1.1 cURL**

{% code overflow="wrap" %}
```
curl --location 'https://openapi.trustformer.info/openapi/v2/data/enum?api_key=a087......bb6f' \
--header 'sign: 8a96......1911' \
--header 'timestamp: 1687788140'
```
{% endcode %}

**api-response**

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "network_coin_list": [
            {
                "coin_list": [
                    "BTC"
                ],
                "network": "Bitcoin"
            },
            {
                "coin_list": [
                    "ETH",
                    "USDT",
                    "USDC"
                ],
                "network": "Ethereum"
            },
            {
                "coin_list": [
                    "TRX",
                    "USDT",
                    "USDC"
                ],
                "network": "TRON"
            },
            {
                "coin_list": [
                    "BNB",
                    "USDT",
                    "USDC"
                ],
                "network": "BSC"
            },
            {
                "coin_list": [
                    "MATIC",
                    "POL",
                    "USDT",
                    "USDC"
                ],
                "network": "POLYGON"
            },
            {
                "coin_list": [
                    "AVAX",
                    "USDT",
                    "USDC"
                ],
                "network": "AVALANCHE-C"
            },
            {
                "coin_list": [
                    "LTC"
                ],
                "network": "Litecoin"
            },
            {
                "coin_list": [
                    "DOGE"
                ],
                "network": "Dogecoin"
            }
        ]
    }
}
```

**1.2 Python**

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.trustformer.info/openapi/v2/data/enum?api_key=a087......bb6f"

payload = {}
headers = {
  'sign': '8a96......1911',
  'timestamp': '1687788140'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**1.3 Golang**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io"
)

func main() {
  url := "https://openapi.trustformer.info/openapi/v2/data/enum?api_key=a087......bb6f"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("sign", "8a96......1911")
  req.Header.Add("timestamp", "1687788140")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}



## 2、Call the Blacklist address detection api <a href="#id-1-call-the-v2-address-risk-detection-interface" id="id-1-call-the-v2-address-risk-detection-interface"></a>

**2.1 cURL**

{% code overflow="wrap" %}
```javascript
curl --location 'https://openapi.trustformer.info/openapi/v2/risk/address/blacklist?api_key=21bb.....7259e&address=3HQJ9ta7TmYNRjkby3nbMGdHzNCCiXs3Ui' \
--header 'timestamp: 1677148682' \
--header 'sign: bba4......4461'
```
{% endcode %}

**api-response**

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "unique_id": "abe6d14326abbc1ffafde3b6534c4203ae201aef90638c038e4f47d1f95e3a29",
        "risk_level": "severe",
        "risk_code": 4444,
        "risk_source": {
            "is_private_blacklist": false,
            "is_private_whitelist": false,
            "private_blacklist_name": "",
            "black_address_type": "Terrorist Financing",
            "black_address_label": [
                "Hamas Donation Campaigns",
                "Israel",
                "NBCTF",
                "Terrorist Financing"
            ]
        }
    }
}
```

**2.2 Python**

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.trustformer.info/openapi/v2/risk/address/blacklist?api_key=21bb......7259e&address=3HQJ9ta7TmYNRjkby3nbMGdHzNCCiXs3Ui"

payload = {}
headers = {
  'timestamp': '1677148682',
  'sign': 'bba4......4461'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**2.3 Golang**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io"
)

func main() {
  url := "https://openapi.trustformer.info/openapi/v2/risk/address/blacklist?api_key=21bb.....7259e&address=3HQJ9ta7TmYNRjkby3nbMGdHzNCCiXs3Ui"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("timestamp", "1677148682")
  req.Header.Add("sign", "bba4......4461")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}

## 3、Call the V2 address risk alert api <a href="#id-1-call-the-v2-address-risk-detection-interface" id="id-1-call-the-v2-address-risk-detection-interface"></a>

**Python**&#x20;

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.trustformer.info/openapi/v2/risk/address/check?api_key=a0876......bb6f&network=Ethereum&address=0x53......a920b&coin=eth&app_id=6491......21qa&address_role=to"

payload = {}
headers = {
  'sign': '8a96......1911',
  'timestamp': '1697788140'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**Golang**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://openapi.trustformer.info/openapi/v2/risk/address/check?api_key=a0876......bb6f&network=Ethereum&address=0x53......a920b&coin=eth&app_id=6491......21qa&address_role=to"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("sign", "8a96......1911")
  req.Header.Add("timestamp", "1697788140")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}

## 3、Call the V2 transaction risk alert api <a href="#id-2-call-the-v2-version-of-the-transaction-risk-detection-interface" id="id-2-call-the-v2-version-of-the-transaction-risk-detection-interface"></a>

**Python**

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.trustformer.info/openapi/v2/risk/tx/check?api_key=a087......bb6f&tx=0x04......548df&network=ethereum&to_address=0x17......a10d&coin=usdt&app_id=1425......2w8d"

payload = {}
headers = {
  'sign': '8a96......1911',
  'timestamp': '1697788140'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**Golang**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://openapi.trustformer.info/openapi/v2/risk/tx/check?api_key=a087......bb6f&tx=0x04......548df&network=ethereum&to_address=0x17......a10d&coin=usdt&app_id=1425......2w8d"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("sign", "8a96......1911")
  req.Header.Add("timestamp", "1697788140")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}
