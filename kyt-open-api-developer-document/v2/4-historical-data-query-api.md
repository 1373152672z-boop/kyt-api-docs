# 4、Historical data query api

Description: Query historical data records according to the unique\_id returned by the alert interface

## 1、**URL** <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/risk/data/push

## 2、**Header Parameters** <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="176"></th><th width="111"></th><th width="121"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>Timestamp (in seconds)</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>Signature sha256("timestamp=timestamp value&#x26;secret=secretkey value")</td></tr></tbody></table>

## 3、**Request Parameters** <a href="#id-3header-can-shu" id="id-3header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="178"></th><th width="112"></th><th width="119"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>unique_id</td><td>string</td><td>true</td><td>Unique id</td></tr></tbody></table>

## 4、 **Response Parameters** <a href="#id-4.-return-parameters" id="id-4.-return-parameters"></a>

```json
{
    "code": 200,
    "msg": "success",
    "data": { 
        "risk_data": {
            "unique_id": "0140......8be5", //Unique id
            "risk_level": "severe", //Risk level (severe, high, medium, low, none)
            "risk_code": 4444 //Risk code
            "risk_source": {
                "is_private_whitelist": false, //Whether to hit private whitelist
                "risk_from_address_list":[ //Risk transfer address
                    { 
                        "black_address":"3E5L......44Bc",//from address
                        "black_address_type": "Blackmail Scam", //Blacklist address type
                        "black_address_label": [ //Blacklist address label
                            "attacker",
                            "hacker"
                        ],
                    },
                    ......
                ],
                .......
            }
        }
    }
}
```

| **Parameter name** | **Data type** | **Description** |
| ------------------ | ------------- | --------------- |
| risk\_data         | json          | History details |
