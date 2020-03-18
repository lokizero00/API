
#   Api Docs(Chinese simplified document)

## 1. open-api Catalog (example：cmc.imoex.top/api/*)
-   [Assets of currency](#1)
-	[Ticker of market pair](#2)
-	[Order book of market pair](#3)
-	[Trades of market pair](#4)


---
### <span id="1">Assets of currency</span>

1. Interface address: /v1/assets
2. Interface specification: (GET) The assets endpoint is to provide a detailed summary for each currency available on the exchange


|parameter|	Fill in type|	Explain|
|--------|--------|--------|
||	|	|

Return value:

    {
    	"comm": {
    		"name": "comm",
    		"unified_cryptoasset_id": null,
    		"can_withdraw": true,
    		"can_deposit": true,
    		"min_withdraw": "40.000",
    		"max_withdraw": "416667.000",
    		"maker_fee": "0.001",
    		"taker_fee": "0.001"
    	},
    	"BCH": {
    		"name": "Bitcoin Cash",
    		"unified_cryptoasset_id": 1831,
    		"can_withdraw": true,
    		"can_deposit": true,
    		"min_withdraw": "0.018",
    		"max_withdraw": "600.000",
    		"maker_fee": "0.002",
    		"taker_fee": "0.002"
    	}
    }

Explain：
**name**：Full name of cryptocurrency<br>
**unified_cryptoasset_id**：Unique ID of cryptocurrency assigned by Unifified Cryptoasset ID<br>
**can_withdraw**：Identififies whether withdrawals are enabled or disabled<br>
**can_deposit**：Identififies whether deposits are enabled or disabled<br>
**min_withdraw**：Identififies the single minimum withdraw amount of a cryptocurrency<br>
**max_withdraw**：Identififies the single maximum withdraw amount of a cryptocurrency<br>
**maker_fee**：Fees applied when liquidity is added to the order book<br>
**taker_fee**：Fees applied when liquidity is removed from the order book<br>

---
### <span id="2">Ticker of market pair</span>

1. Interface address:/v1/ticker
2. Interface specification:(GET) The ticker endpoint is to provide a 24-hour pricing and volume summary for each market pair available on the exchange

|parameter|	Fill in type|	Explain|
|------------|--------|-----------------------------|
||||



Return value:

    {
    	"btcusdt": {
    		"name": "btcusdt",
    		"base_id": "1",
    		"quote_id": "825",
    		"last_price": "5003.971400",
    		"base_volume": "145752517.103805",
    		"quote_volume": "30034.375379"
    	},
    	"xrgusdm": {
    		"name": "xrgusdm",
    		"base_id": "",
    		"quote_id": "",
    		"last_price": "0.556900",
    		"base_volume": "702605.831685",
    		"quote_volume": "1267723.079304"
    	}
    }

Explain：
**name**：Full name of cryptocurrency <br>
**base_id**：The quote pair Unifified Cryptoasset ID<br>
**quote_id**：The base pair Unifified Cryptoasset ID<br>
**last_price**：The price of the last executed order<br>
**base_volume**：24 hour trading volume in base pair volume<br>
**quote_volume**：24 hour trading volume in quote pair volume<br>

---
### <span id="3">Order book of market pair</span>

1. Interface address:/v1/orderBook/market_pair
2. Interface Description: (GET) The order book endpoint is to provide a complete level 2 order book (arranged by best asks/bids) with full depth returned for a given market pair

|parameter|	Fill in type|	Explain|
|------------|--------|-----------------------------|
|market_pair|	Must fill|	A pair such as LTC_BTC|

Return value:

    {
    	"asks": [
    		[9400, 0.0971]
    	],
    	"bids": [
    		[5021.7492, 0.1362]
    	],
    	"timestamp": "1584341474"
    }

Explain：
**timestamp**：Unix timestamp in milliseconds for when the last updated time occurred<br>
**bids**：An array containing 2 elements. The offer price and quantity for each bid order<br>
**asks**：An array containing 2 elements. The ask price and quantity for each ask order<br>

---
###  <span id="4">Trades of market pair</span>

1. Interface address:/v1/trades/market_pair
2. Interface specification:(GET) The trades endpoint is to return data on all recently completed trades for a given market pair

|parameter|	Fill in type|	Explain|
|------------|--------|-----------------------------|
|market_pair|	Must fill|	A pair such as LTC_BTC|
|type|	Must fill|	Query buy side or sell side only|

Return value:

    [{
    	"price": "5016.182200",
    	"type": "sell",
    	"trade_id": "21211432",
    	"base_volume": "2161.974528",
    	"quote_volume": "0.431000",
    	"trade_timestamp": "1584341940"
    }, {
    	"price": "5016.293800",
    	"type": "sell",
    	"trade_id": "21211431",
    	"base_volume": "4225.224267",
    	"quote_volume": "0.842300",
    	"trade_timestamp": "1584341940"
    }]

Explain：
**trade_id**：A unique ID associated with the trade for the currency pair transaction Note: Unix timestamp does not qualify as trade_id <br>
**price**：Transaction price in base pair volume<br>
**base_volume**：Transaction amount in base pair volume<br>
**quote_volume**：Transaction amount in quote pair volume<br>
**trade_timestamp**：Unix timestamp in milliseconds for when the transaction occurred<br>
**type**：Used to determine whether or not the transaction originated as a buy or sell.Buy – Identififies an ask was removed from the order book. Sell –Identififies a bid was removed from the order book<br>
