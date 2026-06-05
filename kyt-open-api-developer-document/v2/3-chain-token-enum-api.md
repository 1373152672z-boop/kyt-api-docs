# 3、Chain token enum api

Description: Get the chain and token names supported by the openapi interface.

## 1、**URL** <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/data/enum

## 2、**Header Parameters** <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="187"></th><th width="120"></th><th width="102"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>Timestamp (in seconds)</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>Signature sha256("timestamp=timestamp value&#x26;secret=secretkey value")</td></tr></tbody></table>

## 3、**Request Parameters** <a href="#id-3header-can-shu" id="id-3header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="185"></th><th width="122"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr></tbody></table>

## 4、**Return Parameters** <a href="#id-4.-return-parameters" id="id-4.-return-parameters"></a>

```json
{
    "code": 200,
    "msg": "success",
    "data": { 
        "network_coin_list": [
            {
                "coin_list": [ //List of supported tokens
                    "BTC"
                ],
                "network": "Bitcoin" //Mainnet
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
                    "USDT"
                ],
                "network": "TRON"
            },
            {
                "coin_list": [
                    "BNB",
                    "USDT",
                    "USDC"
                ],
                "network": "BNB"
            },
            {
                "coin_list": [
                    "MATIC",
                    "USDT",
                    "USDC"
                ],
                "network": "POLYGON"
            },
            ......
        ]
    }
}
```

[<br>](https://docs.trustformer.ai/kyt-api-developer-document/v2/2-real-time-transaction-risk-alert-interface)
