# 8、Risk\_Code Instruction manual

Simple codes are categorized as: blacklisted hits, indirectly risky trades, unknowns, not found, and so on;

Other complex codes are made up of "classification + transaction direction + transaction exposure type + risk level" stitched together in sequence.

## 1、Simple code <a href="#id-1.hit-blacklist-and-unknown-code" id="id-1.hit-blacklist-and-unknown-code"></a>

| **code** | **name**                       |
| -------- | ------------------------------ |
| 4444     | Black Address                  |
| 0        | none                           |
| -1       | not found                      |
| -2       | network or coin is not support |
| 1        | Private White Address          |
| 444      | Private Blacklist Address      |
| 4400     | Direct Risk                    |
| 4401     | Indirect Risk Level 1          |
| 4402     | Indirect Risk Level 2          |
| 4403     | Indirect Risk Level 3          |
| 4404     | Indirect Risk Level 4          |
| 4405     | Indirect Risk Level 5          |

## 2、Trading directions code <a href="#id-2.trading-directions-code" id="id-2.trading-directions-code"></a>

| **Code** | **Name**  |
| -------- | --------- |
| 21       | sending   |
| 22       | receiving |

## 3、Trading directions code <a href="#id-3.trading-directions-code" id="id-3.trading-directions-code"></a>

| **Code** | **Name** |
| -------- | -------- |
| 11       | direct   |
| 12       | indirect |

## 4、Risk level code <a href="#id-4.risk-level-code" id="id-4.risk-level-code"></a>

| **Code** | **Name** |
| -------- | -------- |
| 45       | severe   |
| 44       | high     |
| 43       | medium   |
| 42       | low      |
| 41       | none     |

## 5、Blacklist categories code <a href="#id-5.policy-categories-code" id="id-5.policy-categories-code"></a>

| **code** | **Name**                               |
| -------- | -------------------------------------- |
| 3000     | Big Money                              |
| 3001     | Decentralized Exchange                 |
| 3002     | Centralized Exchange                   |
| 3003     | Custody Wallet                         |
| 3004     | Merchant Service                       |
| 3005     | Suspected Money Laundering             |
| 3006     | Mining                                 |
| 3007     | Other Smart Contract                   |
| 3008     | Infrastructure as a Service            |
| 3009     | Token Smart Contract                   |
| 3010     | High Risk Exchange                     |
| 3011     | High Risk Jurisdiction                 |
| 3012     | Lending Contract                       |
| 3013     | Mining Pool                            |
| 3014     | ICO                                    |
| 3015     | Blackmail Scam                         |
| 3016     | Tumbler Mixer                          |
| 3017     | Sextortion                             |
| 3018     | Darknet Market                         |
| 3019     | Child Exploitation                     |
| 3020     | Fake Charity                           |
| 3021     | Fake Exchange                          |
| 3022     | Fake Giveaway                          |
| 3023     | Fake Token                             |
| 3024     | Fake Miner                             |
| 3025     | Fake Investment                        |
| 3026     | Fake Wallet Address                    |
| 3027     | Ponzi Scheme                           |
| 3028     | Trafficking in Human Beings and Organs |
| 3029     | Fake Shop                              |
| 3030     | Betting or Gambling                    |
| 3031     | Illegal Sale and Distribution          |
| 3032     | Illegal Org                            |
| 3033     | Protocol Privacy                       |
| 3034     | Ransomware/Virus                       |
| 3035     | Sanctions                              |
| 3036     | Stolen Crypto                          |
| 3037     | Terrorist Financing                    |
| 3038     | USA Political Blacklist                |
| 3039     | Etherscan\_AddedBlackList              |
| 3040     | Mainnet\_AddedBlackList                |
| 3041     | Cryptoassets-related Cards             |
| 3042     | DeFi Smart Contract                    |
| 3043     | NFT Smart Contract                     |





