# Risk Code Description

A single `risk_code` may represent: blacklist hit, indirect risk transaction, unknown, not found, etc.

Other composite `risk_code` values are constructed by concatenating the following elements in order:

> **Risk Type + Transaction Direction + Transaction Exposure Type + Risk Level**

These correspond to the configuration displayed on the KYT system rule engine page.

***

### 1. Single `risk_code`

| Code  | Description                                                 | Name                             |
| ----- | ----------------------------------------------------------- | -------------------------------- |
| 4444  | Blacklist hit                                               | Black Address                    |
| 0     | Unknown                                                     | none                             |
| -1    | Not found                                                   | not found                        |
| -2    | Unsupported mainnet or token                                | network or coin is not supported |
| 1     | Private whitelist hit                                       | Private White Address            |
| 444   | Private blacklist hit                                       | Private Blacklist Address        |
| 4400  | Direct risk                                                 | Direct Risk                      |
| >4400 | Indicates indirect risk when the value is greater than 4400 | Indirect Risk                    |

***

### 2. Transaction Direction Code

| Code | Name (CN) | Name (EN) |
| ---- | --------- | --------- |
| 21   | 转出        | sending   |
| 22   | 转入        | receiving |

***

### 3. Transaction Exposure Type Code

| Code | Name (CN) | Name (EN) |
| ---- | --------- | --------- |
| 11   | 直接        | direct    |
| 12   | 间接        | indirect  |

***

### 4. Risk Level Code

| Code | Name (CN) | Name (EN) |
| ---- | --------- | --------- |
| 45   | 极高风险      | severe    |
| 44   | 高风险       | high      |
| 43   | 中风险       | medium    |
| 42   | 低风险       | low       |
| 41   | 未知        | none      |

***

### 5. Risk Type Code

| Code | Name (EN)                              |
| ---- | -------------------------------------- |
| 3000 | Big Money                              |
| 3001 | Decentralized Exchange                 |
| 3002 | Centralized Exchange                   |
| 3003 | Custody Wallet                         |
| 3004 | Merchant Service                       |
| 3005 | Suspected Money Laundering             |
| 3006 | Mining                                 |
| 3007 | Other Smart Contract                   |
| 3008 | Infrastructure as a Service            |
| 3009 | Token Smart Contract                   |
| 3010 | High Risk Exchange                     |
| 3011 | High Risk Jurisdiction                 |
| 3012 | Lending Contract                       |
| 3013 | Mining Pool                            |
| 3014 | ICO                                    |
| 3015 | Blackmail Scam                         |
| 3016 | Tumbler Mixer                          |
| 3017 | Sextortion                             |
| 3018 | Darknet Market                         |
| 3019 | Child Exploitation                     |
| 3020 | Fake Charity                           |
| 3021 | Fake Exchange                          |
| 3022 | Fake Giveaway                          |
| 3023 | Fake Token                             |
| 3024 | Fake Miner                             |
| 3025 | Fake Investment                        |
| 3026 | Fake Wallet Address                    |
| 3027 | Ponzi Scheme                           |
| 3028 | Trafficking in Human Beings and Organs |
| 3029 | Fake Shop                              |
| 3030 | Betting or Gambling                    |
| 3031 | Illegal Sale and Distribution          |
| 3032 | Illegal Organization                   |
| 3033 | Protocol Privacy                       |
| 3034 | Ransomware / Virus                     |
| 3035 | Sanctions                              |
| 3036 | Stolen Crypto                          |
| 3037 | Terrorist Financing                    |
| 3038 | USA Political Blacklist                |
| 3039 | Etherscan\_AddedBlackList              |
| 3040 | Mainnet\_AddedBlackList                |
| 3041 | Cryptoassets-related Cards             |
| 3042 | DeFi Smart Contract                    |
| 3043 | NFT Smart Contract                     |
