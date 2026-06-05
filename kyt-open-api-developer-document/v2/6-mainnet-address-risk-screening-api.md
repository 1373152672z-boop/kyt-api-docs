# 6、Mainnet address risk screening api

Description: This API performs a preliminary risk check on an address (e.g., checking if it’s on a blacklist, if it has transacted directly or indirectly with blacklisted addresses, etc.).

Note: This api only screens for risks; it does not execute rule engine logic.

## 1、**URL** <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/risk/address/screening

## 2、**Header Parameters** <a href="#id-2.-header-parameters" id="id-2.-header-parameters"></a>

<table data-header-hidden><thead><tr><th width="193"></th><th width="119"></th><th width="125"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>Timestamp (in seconds)</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>Signature sha256("timestamp=timestamp value&#x26;secret=secretkey value")</td></tr></tbody></table>

## 3、**Request Parameters** <a href="#id-3header-can-shu" id="id-3header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="190"></th><th width="119"></th><th width="128"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>network</td><td>string</td><td>true</td><td>Mainnet name (Bitcoin、Ethereum..... details for "Support mainnet tokens")</td></tr><tr><td>address</td><td>string</td><td>true</td><td>wallet address </td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>Whether to query indirect risk transactions (default value is false)</td></tr></tbody></table>

### 4、**Return Parameters** <a href="#id-4-fan-hui-can-shu" id="id-4-fan-hui-can-shu"></a>

```json
{
    "code": 200, //200:Represents success
    "msg": "success",
    "data": {
        "unique_id": "0140......8be5", //Unique ID (used to query history)
        "risk_level": "severe", //Risk level (severe, high, medium, low, unknown)
        "risk_code": 4444, //Risk code
        "risk_source": { //Risk source
            "is_private_whitelist": false, //Whether to hit private whitelist
            "is_private_blacklist": false, //Whether to hit private blacklist
            "black_address_type": "Blackmail Scam", //Blacklist type
            "black_address_label": [ //Blacklist label
                "attacker",
                "hacker"
            ],
            "direct_risk_list":[ //List of direct risk transactions
                {
                    "black_address": "1KHw......aGbX", //Blacklist addresses for direct transactions
                    "black_address_type": "Blackmail Scam", //Type of risk
                    "tx_hash": "2bc34......b693", //Transaction hash
                    "black_address_label": [ //Blacklist label
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "indirect_risk_list":[ //List of indirect risk transactions
                {
                    "indirect_level": 2, //Indirect level
                    "black_address":"0x99......4bE1", //Blacklist of indirect transactions
                    "black_address_type": "Blackmail Scam", //Type of risk
                    "indirect_tx_list":[ //Indirect transaction hash
                        "0x74......2a90"
                        "0x56......9d4b"
                    ],
                    "black_address_label": [ //Blacklist label
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ]
        }
    }
}
```

<table data-header-hidden><thead><tr><th width="286"></th><th width="122"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Description</strong></td></tr><tr><td>code</td><td>Int</td><td><p>200: The request was successful</p><p>-2: The mainnet is not supported</p></td></tr><tr><td>message</td><td>string</td><td>Interface Request Status Description</td></tr><tr><td>unique_id</td><td>string</td><td>Unique id (identifies the current request, used to query history)</td></tr><tr><td>risk_level</td><td>string</td><td><p>Risk level（</p><p>severe</p><p>high</p><p>medium</p><p>low</p><p>none</p><p>）</p></td></tr><tr><td>risk_code</td><td>int</td><td><p>Risk code（</p><p>0: unknown</p><p>-1: Not found</p><p>4444: hit blacklist</p><p>details for "Risk_Code Instruction manual"）</p></td></tr><tr><td>risk_source</td><td>json</td><td>Risk source</td></tr><tr><td>risk_source.is_private_whitelist</td><td>boolean</td><td>Whether to hit private whitelist</td></tr><tr><td>risk_source.is_private_blacklist</td><td>boolean</td><td>Whether to hit private blacklist</td></tr><tr><td>risk_source.black_address_type</td><td>string</td><td>The blacklist type of the query address</td></tr><tr><td>risk_source.black_address_label</td><td>string</td><td>Check the blacklist label of the address</td></tr><tr><td>risk_source.direct_risk_list</td><td>jsonArray</td><td>Query address List of direct risk transactions involved</td></tr><tr><td>risk_source.indirect_risk_list</td><td>jsonArray</td><td>Query the list of indirect risk transactions that the address participates in</td></tr></tbody></table>
