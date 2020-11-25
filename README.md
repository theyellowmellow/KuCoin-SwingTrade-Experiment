# KuCoin-SwingTrade-Experiment


## Configuration

#### Note: An api key will need to be created with "Trade Limit" permissions

| Config Parameter  |  Type |  Default | Required  |  Description |
|---|---|---|---|---|
| apiKey  |  String |  none | Yes  |  API key for account access |
| apiSecret  | String  |  none |  Yes |  Secret key for account access |
| trade  | String  |  none | Yes | Base token used for exchange (example: BTC)  |
| currency | String  | none  |  Yes | Token to be traded (example: STRAT) |
| sellValuePercent  | Integer/Float  | 4  |  No | Difference in sell price of the previous successful order or market (on startup)  | 
| buyValuePercent  |  Integer/FLoat |  4 |  No | Difference in buy price of the previous successful order or market (on startup)   | 
| volumePercent  | Integer/Float  | 4  | No  |  Percent of your tokens to be placed leveraged | 
| buyDifference  |  Integer/Float |  0 |  No |  Percent adjustment to buy orders. Positive values buy more than sells. Negative values buys less than sell | 
| extCoinBalance | Integer/Float | 0| No | Off exchange balance|
| checkInterval | Integer | 30| No | How often the bot checks state|
| slackToken | string | empty | Yes | token for sending to slack |
| slackChannel | string | empty | Yes | channel for trade notificaiton | 


The percentage values are actual percentages...not decimals. So if you want to trade 3.25% you would input 3.25 in that value. I would also not recommend going below 10 seconds for the checkInterval. Otherwise, it's possible to induce a race condition with bittrex.

## buyDifference explanation

Setting the 'volumePercent' param with a 'buyDifference' of zero places matching buys / sells. Adjusting the 'buyDifference' changes only the buying behavior. It's been much more predictable and less prone to erroneous buys / sells.

To be transparent, here's the forumla being used to calculate the buy amount:

(balance + externalCoinBalance) * volumePercent * (1/(1 - volumePercent) * 1 + buyDifference)

NOTE: I've had the best experience with higher percentages for the sell / buy Values. I currently run 6 on both


#### Example file 

```json
{
  "apiKey": "34234898u9rghk",
  "apiSecret": "238ryfiuahskuqh4ri",
  "trade": "BTC",
  "currency": "UTK",
  "sellValuePercent": 6,
  "buyValuePercent": 6,
  "volumePercent": 3,
  "buyDifference": 2,
  "extCoinBalance": 0,
  "checkInterval": 30,
  "slackToken": "",
  "slackChannel": ""
}
```
__the config file MUST be named botConfig.json__

## License
Code released under the [MIT License](https://github.com/jufkes/bittrexBot/master/LICENSE).

