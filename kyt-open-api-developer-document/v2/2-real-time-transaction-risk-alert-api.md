# 2、Real-time transaction risk alert api

Description: Supports real-time transaction monitoring for the latest transactions (within the past 24 hours) by conducting risk assessments based on transaction hashes. This includes verifying whether involved addresses are on a blacklist, checking if any transaction addresses have directly or indirectly interacted with blacklisted entities, and determining whether the transaction amount received by certain addresses exceeds AML thresholds, among other checks.

## 1、**URL** <a href="#id-1.-interface-url" id="id-1.-interface-url"></a>

GET /openapi/v2/risk/tx/check

## 2、**Header Parameters** <a href="#id-2.-header-parameters" id="id-2.-header-parameters"></a>

<table data-header-hidden><thead><tr><th width="186"></th><th width="117"></th><th width="100"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>Timestamp (in seconds)</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>Signature sha256("timestamp=timestamp value&#x26;secret=secretkey value")</td></tr></tbody></table>

## 3、**Request Parameters** <a href="#id-3.-request-parameters" id="id-3.-request-parameters"></a>

<table data-header-hidden><thead><tr><th width="187"></th><th width="117"></th><th width="104"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>tx</td><td>string</td><td>true</td><td>Transaction hash (support querying transaction hash in the last 72 hours)</td></tr><tr><td>network</td><td>string</td><td>true</td><td>Mainnet name (Bitcoin、Ethereum..... details for "Support mainnet tokens")</td></tr><tr><td>to_address</td><td>string</td><td>true</td><td>Transfer to address</td></tr><tr><td>coin</td><td>string</td><td>true</td><td>Token Name (btc、eth、trx、bnb、usdt、usdc......details for "Support mainnet tokens")</td></tr><tr><td>app_id</td><td>string</td><td>true</td><td>app id (obtained from the KYT configuration page on the WEB side)</td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>Whether to query indirect risk transactions (default value is true)</td></tr><tr><td>business_tag</td><td>string</td><td>false</td><td><p>Business type(</p><p>wallet: wallet</p><p>exchange: exchange</p><p>NFT: nft</p><p>... etc.）</p></td></tr><tr><td>kyc_status</td><td>int</td><td>false</td><td><p>KYC Status (</p><p>1: KYC certified</p><p>2: Not KYC certified</p><p>)</p></td></tr><tr><td>kyc_level</td><td>int</td><td>false</td><td><p>KYC level (</p><p>1: KYC Level 1</p><p>2: KYC Level 2</p><p>3: KYC Level 3</p><p>4: KYC Level 4</p><p>)</p></td></tr></tbody></table>

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
    "code": 200,
    "msg": "success",
    "data": { 
        "unique_id": "0140......8be5", //Unique ID (used to query historical data)
        "risk_level": "severe", //Risk level (severe, high, medium, low, none)
        "risk_code": 4444 //Risk code
        "risk_source": {
            "is_private_whitelist": false, //Whether to hit private whitelist
            "is_private_blacklist": false, //Whether to hit private blacklist
            "risk_from_address_list":[ //Risk transfer address
                { 
                    "black_address": "3E5L......44Bc",//from address
                    "black_address_type": "Blackmail Scam", //Blacklist address type
                    "black_address_label": [ //Blacklist address label
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ],
            "risk_to_address_list":[ //Risk transfer address
                { 
                    "black_address": "35AT......yzew",//to address       
                    "black_address_type": "Blackmail Scam", //Blacklist address type
                    "black_address_label": [ //Blacklist address label
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ],
            "direct_tx_from_risk_list":[ //List of direct risk transactions to the address of the transaction sender
                {
                    "black_address": "1KHw......aGbX", //Blackmail
                    "tx_hash": "2bc3......b693",
                    "black_address_type": "Blackmail Scam", //Risk type
                    "black_address_label": [ //Blacklist address label
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "direct_tx_to_risk_list":[ //List of direct risk transactions for transaction recipient addresses
                {
                    "black_address": "1KHw......aGbX", //Blacklist
                    "tx_hash": "2bc3......b693",
                    "black_address_type": "Blackmail Scam", //Risk type
                    "black_address_label": [ //Blacklist address label
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "from_indirect_risk_list":[ //Transaction Send Send Indirect Risk Transaction List
                {
                    "indirect_level": 2, //Indirect level
                    "black_address":"0x99......4bE1", //Blacklist of indirect transactions
                    "black_address_type": "Blackmail Scam", //Risk type
                    "indirect_tx_list":[ //Indirect transaction hash
                        "0x74......2a90",
                        "0x56......9d4b"
                    ],
                    "black_address_label": [ //Blacklist address label
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ],
            "to_indirect_risk_list":[ //Transaction Recipient Indirect Risk Transaction List
                {
                    "indirect_level": 2, //Indirect level
                    "black_address":"0x99......4bE1", //Blacklist of indirect transactions
                    "black_address_type": "Blackmail Scam", //Risk type
                    "indirect_tx_list":[ //Indirect transaction hash
                        "0x74......2a90",
                        "0x56......9d4b"
                    ],
                    "black_address_label": [ //Blacklist address label
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

<table data-header-hidden><thead><tr><th width="306"></th><th width="117"></th><th></th></tr></thead><tbody><tr><td><strong>Parameter name</strong></td><td><strong>Data type</strong></td><td><strong>Description</strong></td></tr><tr><td>code</td><td>Int</td><td><p>200: The request was successful</p><p>-2: The mainnet is not supported</p></td></tr><tr><td>message</td><td>string</td><td>Interface Request Status Description</td></tr><tr><td>unique_id</td><td>string</td><td>Unique id (identifies the current request, used to query history)</td></tr><tr><td>risk_level</td><td>string</td><td><p>Risk level（</p><p>severe</p><p>high</p><p>medium</p><p>low</p><p>none</p><p>）</p></td></tr><tr><td>risk_code</td><td>int</td><td><p>Risk code（</p><p>0: unknown</p><p>-1: Not found</p><p>4444: hit blacklist</p><p>details for "Risk_Code Instruction manual"</p><p>）</p></td></tr><tr><td>risk_source</td><td>jsonArray</td><td>Risk source</td></tr><tr><td>risk_source.risk_from_address_list</td><td>jsonArray</td><td>Blacklist list in transaction sender address</td></tr><tr><td>risk_source.risk_to_address_list</td><td>jsonArray</td><td>Blacklist list in transaction recipient addresses</td></tr><tr><td>risk_source.direct_tx_from_risk_list</td><td>jsonArray</td><td>List of direct risk transactions to the address of the transaction sender</td></tr><tr><td>risk_source.direct_tx_to_risk_list</td><td>jsonArray</td><td>List of direct risk transactions for transaction recipient addresses</td></tr><tr><td>risk_source.from_indirect_risk_list</td><td>jsonArray</td><td>List of indirect risk transactions to which the transaction is sent</td></tr><tr><td>risk_source.to_indirect_risk_list</td><td>jsonArray</td><td>List of indirect risk transactions for transaction receiving and sending addresses</td></tr></tbody></table>
