# 1、 Address deposit｜withdraw risk alert api

Description: Support wallet address deposit or withdraw transaction scenarios, pre-detect address risks (e.g., whether it is blacklisted, whether it has directly or indirectly blacklisted transactions, etc.).

## 1、**URL** <a href="#id-1.-interface-url" id="id-1.-interface-url"></a>

GET /openapi/v2/risk/address/check

## 2、**Header Parameters** <a href="#id-2.-header-parameters" id="id-2.-header-parameters"></a>

<table data-header-hidden><thead><tr><th width="177"></th><th width="122"></th><th width="109"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>Timestamp (in seconds)</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>Signature sha256("timestamp=timestamp value&#x26;secret=secretkey value")</td></tr></tbody></table>

## 3、**Request Parameters** <a href="#id-3.-request-parameters" id="id-3.-request-parameters"></a>

<table data-header-hidden><thead><tr><th width="194"></th><th width="116"></th><th width="116"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>network</td><td>string</td><td>true</td><td>Mainnet name (Bitcoin、Ethereum..... details for "Support mainnet tokens")</td></tr><tr><td>address</td><td>string</td><td>true</td><td>Wallet address</td></tr><tr><td>address_role</td><td>string</td><td>true</td><td><p>Address role（</p><p>from: Transfer out address；</p><p>to: Transfer to address</p><p>）</p></td></tr><tr><td>coin</td><td>string</td><td>true</td><td>Token Name (btc、eth、trx、bnb、usdt、usdc......details for "Support mainnet tokens")</td></tr><tr><td>app_id</td><td>string</td><td>true</td><td>app id (obtained from the KYT configuration page on the WEB side)</td></tr><tr><td>value</td><td>float64</td><td>false</td><td>Token value</td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>Whether to query indirect risk transactions (default value is true)</td></tr><tr><td>business_tag</td><td>string</td><td>false</td><td><p>Business type(</p><p>wallet: wallet</p><p>exchange: exchange</p><p>NFT: nft</p><p>... etc.）</p></td></tr><tr><td>kyc_status</td><td>int</td><td>false</td><td><p>KYC Status (</p><p>1: KYC certified</p><p>2: Not KYC certified</p><p>)</p></td></tr><tr><td>kyc_level</td><td>int</td><td>false</td><td><p>KYC level (</p><p>1: KYC Level 1</p><p>2: KYC Level 2</p><p>3: KYC Level 3</p><p>4: KYC Level 4</p><p>)</p></td></tr></tbody></table>

## 4、**Response Parameters** <a href="#id-4.-return-parameters" id="id-4.-return-parameters"></a>

API key expired or invalid, interface returned:

```
{
    "code": -1,
    "data": {},
    "message": "api_key is invalid"
}
```

The apikey and secrectkey have been verified successfully and returned normally:

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

<table data-header-hidden><thead><tr><th width="293"></th><th width="122"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Description</strong></td></tr><tr><td>code</td><td>Int</td><td><p>200: The request was successful</p><p>-2: The mainnet is not supported</p></td></tr><tr><td>message</td><td>string</td><td>Interface Request Status Description</td></tr><tr><td>unique_id</td><td>string</td><td>Unique id (identifies the current request, used to query history)</td></tr><tr><td>risk_level</td><td>string</td><td><p>Risk level（</p><p>severe</p><p>high</p><p>medium</p><p>low</p><p>none</p><p>）</p></td></tr><tr><td>risk_code</td><td>int</td><td><p>Risk code（</p><p>0: unknown</p><p>-1: Not found</p><p>4444: hit blacklist</p><p>details for "Risk_Code Instruction manual"）</p></td></tr><tr><td>risk_source</td><td>json</td><td>Risk source</td></tr><tr><td>risk_source.is_private_whitelist</td><td>boolean</td><td>Whether to hit private whitelist</td></tr><tr><td>risk_source.is_private_blacklist</td><td>boolean</td><td>Whether to hit private blacklist</td></tr><tr><td>risk_source.black_address_type</td><td>string</td><td>The blacklist type of the query address</td></tr><tr><td>risk_source.black_address_label</td><td>string</td><td>Check the blacklist label of the address</td></tr><tr><td>risk_source.direct_risk_list</td><td>jsonArray</td><td>Query address List of direct risk transactions involved</td></tr><tr><td>risk_source.indirect_risk_list</td><td>jsonArray</td><td>Query the list of indirect risk transactions that the address participates in</td></tr></tbody></table>
