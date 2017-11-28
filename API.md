**Supermax API v1**

This document is not finalized and subjected to change quite frequently. If you have any questions, email hello@supermax.cool or holla at @huangkuan, @helixy on Twitter.

The base url of all the APIs is:
https://mainnet.supermax.cool/api/v1/



BLOCKS
----------
List all the blocks.

* **Method:** POST 
* **URL:** `/blocks` 
Parameters:
```json
{
  "startDate"  :"2017-10-18",
  "endDate"  :"2017-10-27",
  "miner"    :"0xmmmm1",
  "transactionCount"  :
  "startBlockNumber"  :4330000,
  "endBlockNumber"  :4330050,
  "sort"   :  {"timestamp":-1}}
}
```
You can use either use start/end_block_number or start/end_date. If you use both, the api will choose start/end_date as default.

* `POST /blocks/:blockHash or /blocks/:blockNumber`  Returns the result of web.eth.getBlock()

* `POST /blocks/:blockHash/txs or /blocks/:blockNumber/txs`  Returns the list of hashes of the transactions in that block. Notes: These do not include internal trasactions which are triggered by contracts. To get contract related transactions, please refer to /txs/ API.

