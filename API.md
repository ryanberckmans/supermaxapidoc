**Supermax API v1 draft**

This document is not finalized and subjected to change quite frequently. If you have any questions, email hello@supermax.cool or holla at [@huangkuan](https://twitter.com/huangkuan), [@helixy](https://twitter.com/helixy) on Twitter.

The base url of all the APIs is:
https://app.supermax.cool/supermax/api/v1

All the data after block 4000000 or Jul 9th, 2017 08:52:47PM(UTC) is fully synced in our database. We're in the process of adding historical data into our database as well.

----------
1. List all the blocks based on given parameters. You can filter the result by date range, transaction counts per block and miner. Amazing, right?! :)
* **Http request:** POST `/blocks` 
* **Parameters:**
```json
{
  "startDate":"2017-10-18",
  "endDate":"2017-10-27",
  "miner":"0xmmmm1",
  "transactionCount": {"$gte":3000},
  "startBlockNumber":4330000,
  "endBlockNumber":4330050,
  "sort":{"transactionCount":-1}
}
```
* **Response:** 
```json
{
  "blocks":[{         
    "_id": "5a1afa055f5575dc214412fe",
    "author": "0xea674fdde714fd979de3edf0f56aa9716b898ec8",
    "difficulty": 1466994161559713,
    "extraData": "0x65746865726d696e652d6173696135",
    "gasLimit": 6712392,
    "gasUsed": 3902260,
    "hash": "0x479c6910f4a991e3ee9677083ca96169dc1a03a1a3682e0667c4db19f693aadb",
    "logsBloom": "0x000000a40050405",
    "miner": "0xEA674fdDe714fd979de3EdF0F56AA9716B898ec8",
    "mixHash": "0xd9af06293b2a2c50f78ef84ea364c4b1bedad491e2762fb958fdcbfead4f6965",
    "nonce": "0x7485a7d003b24aec",
    "number": 4418999,
    "parentHash": "0xa46a750f55d227bd1887fa173c6fefc4e52db84149da56f06e5281bfcaa18421",
    "receiptsRoot": "0x3b66067eaabd6f73600672f47d3f4653a9528948c5e32ce7c37339bd21bccc3d",
    "sealFields": [
        "0xa0d9af06293b2a2c50f78ef84ea364c4b1bedad491e2762fb958fdcbfead4f6965",
        "0x887485a7d003b24aec"
    ],
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": 16991,
    "stateRoot": "0xfa9866b0041488a5aa6428dce48b17d233bc2382dd698ad9575559501b9279db",
    "timestamp": 1508825437,
    "totalDifficulty": 1.2690805494178584e+21,
    "transactions": [
        "0x66b2eac9e5bc5db708d1636098d7de569f2219811adce19d4d529dfa433216e0"
        ],
    "transactionsRoot": "0x463e35698926f8476f971c936e36f00c65fbe5f7bfdb11ba054b8f9ecf43573e",
    "uncles": [],
    "transactionCount": 79
  }]
}
```
* **Example:** 
```
curl -X POST https://app.supermax.cool/supermax/api/v1/blocks -H 'authorization: hello@world.com:eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImhlbGxvQHdvcmxkLmNvbSIsIl9pZCI6IjVhMTBjMzllNTQ2ZWZiMDc1MWEwYWUzYyIsImlhdCI6MTUxMTA1MDE4NH0.oIe738oMRmez_NI5U4-w9L0LiCjkssJ6f9KtbX9_N_k' -H 'cache-control: no-cache' -H 'content-type: application/json' -d '{"startDate":"2017-11-24","endDate":"2017-11-25"}'
```
* **Notes:**
You can use either use startBlockNumber/endBlockNumber or startDate/endDate. If you use both, the api will choose startDate/endDate as default.
----------
2. List all the transactions of a given token. People could use this API to analyze the past and ongoing ICOs, to track the distribution of their own tokens within their network. We're also thinking about having a push service where any time there is a new transaction of your token, the data will be pushed to a webhook defined by you. Get in touch if you dig it!.

* **Http request:** POST `/tokens/:tokenAddress/txs` 
* **Parameters:**
```json
{
  "startDate":"2017-11-24",
  "endDate":"2017-11-25",
  "quantity": {"$gte":3.0},
  "fromWallet":"0x7fe2b88f2e4858de375832fbf54ac7cf1a78ca51",
  "toWallet": "0x835779b32e558a3fdef94d443523b984e3d1551",
}
```
* **Response:** 
```json
{
  "txs": [{
          "_id":"5a18b26788776d13d99ac67a",
          "blockHash":"0xdf59ba4b93175cc2112aa9f5a31d2f85349ee0ff3d58c230701a950c035827e1",
          "blockNumber":4616114,
          "blockTimestamp":1511567968,
          "transactionHash":"0x473d37964e903e93ea25200822208c8bde1d5755e2ec2d418d754968e39bbd1d",
          "quantity":"299.99",
          "tokenAddress":"0xa74476443119A942dE498590Fe1f2454d7D4aC0d",
          "fromWallet":"0x7fe2b88f2e4858de375832fbf54ac7cf1a78ca51",
          "toWallet":"0x835779b32e558a3fdef94d443523b984e3d1551"
        }]

}
```
* **Example:** 
```
curl -X POST https://app.supermax.cool/supermax/api/v1/tokens/0xa74476443119A942dE498590Fe1f2454d7D4aC0d/txs -H 'authorization: hello@world.com:eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImhlbGxvQHdvcmxkLmNvbSIsIl9pZCI6IjVhMTBjMzllNTQ2ZWZiMDc1MWEwYWUzYyIsImlhdCI6MTUxMTA1MDE4NH0.oIe738oMRmez_NI5U4-w9L0LiCjkssJ6f9KtbX9_N_k' -H 'cache-control: no-cache' -H 'content-type: application/json' -d '{"startDate":"2017-11-24","endDate":"2017-11-25"}'
```
----------
3. Get a list of supported erc20 tokens.
* **Http request:** POST `/tokens`
* **Parameters:** `None`
* **Response:** 
```json
{
  "tokens": [{
              "_id": "5a1b99d999d437329bdd21f8",
              "address": "0x1F573D6Fb3F13d689FF844B4cE37794d79a7FF1C",
              "currencyCode": "BNT",
              "name": "Bancor Network",
              "description": "Bancor Protocol is a standard for a new generation of cryptocurrencies called Smart Tokens"
            },
            {
              "_id": "5a1b99d999d437329bdd21f8",
              "address": "0x1F573D6Fb3F13d689FF844B4cE37794d79a7FF1C",
              "currencyCode": "BNT",
              "name": "Bancor Network",
              "description": "Bancor Protocol is a standard for a new generation of cryptocurrencies called Smart Tokens"
            }]
}
```
* **Example:**
```
curl -X POST https://app.supermax.cool/supermax/api/v1/tokens  -H 'authorization: hello@world.com:eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9eyJlbWFpbCI6ImhlbGxvQHdvcmxkLmNvbSIsIl9pZCI6IjVhMTBjMzllNTQ2ZWZiMDc1MWEwYWUzYyIsImlhdCI6MTUxMTA1MDE4NH0.oIe738oMRmez_NI5U4-w9L0LiCjkssJ6f9KtbX9_N_k' -H 'cache-control: no-cache' -H 'content-type: application/json'
```
* **Notes:**
We will keep updating this list. If you want us to include your token, send us an email.