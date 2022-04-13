# Exchange

## Account

### Get account

> Requst

```
GET /v1/exchange/account
```


> Response

```json
{
    "success": true,
    "data": {
        "id": "ad122e63-9112-499e-be60-1997f9455f6b",
        "email": "bitgin@bitgin.com",
        "kyc_level": 2,
        "referral_codes": [ 
            "KIJ83L",
            "MLIDSE"
        ],
        "referrer_code": "KLD3DJ"
    }
}

```

<p style="color:red">Requires authentication.</p>



Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | ID of account |
| email | string | Email of account |
| kyc_level | integer | KYC (Know Your Customer) level|
| referral_codes | string array | Referral codes (e.g. You can give your referral code to other users to sign up.) |
| referrer_code | string | Referrer code (e.g. The referral code that you acquire from other user.)  |

</br>


## Wallet

### Get balances


> Requst

```
GET /v1/exchange/wallet/balance?currency={currency}
```


> Response

```json
{
    "success": true,
    "data": [
        {
            "currency": "BTC",
            "total": 0.45,
            "available": 0.45,
            "locked": 0
        }
    ]
}

```


<p style="color:red">Requires authentication.</p>



Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | optional, if the field is empty, it will return all balances information as default. (e.g. BTC, ETH, USDT, TWD)|

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | BTC, ETH, USDT, TWD |
| total | float | total ammount |
| available | float | amount available|
| locked | float |  amount locked  |


</br>

### Get deposit addresses

> Requst

```
GET /v1/exchange/wallet/address/deposit?currency={currency}&chain={chain}
```


> Response

```json
{
    "success": true,
    "data": [
        {
            "chain": "Tron",
            "address": "TXHzvoDBPaG7YbSgb3zdoosJK4x4Kmf2J2"
        },
        {
            "chain": "Ethereum",
            "address": "0xB76204882Fbef161428588560b48dB570A9d42Bb"
        }
    ]
}

```


<p style="color:red">Requires authentication.</p>



Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | BTC, ETH, USDT|
| chain | string | optional (e.g. Bitcoin, Ethereum, Tron)|

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| chain | string | Bitcoin, Ethereum, Tron |
| address | string |  |

</br>


### Get saved addresses

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/wallet/address/saved?currency={currency}&chain={chain}
```


> Response

```json
{
    "success": true,
    "data": [
        {
            "id": "c3422e63-4512-499e-be60-1948f945346b",
            "name": "Binance",
            "chain": "Ethereum",
            "currency": "ETH",
            "address": "0xB76204882Fbef161428588560b48dB570A9d42Bb"
        }
    ]
}

```

Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | BTC, ETH, USDT |
| chain | string | optional (e.g. Bitcoin, Ethereum, Tron)|

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | |
| name | string |  |
| chain | string | Bitcoin, Ethereum, Tron |
| currency | string | BTC, ETH, USDT |
| address | string |  |


</br>


### Get deposit history

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/wallet/history/deposit?currency={currency}&start_time={start_time}&end_time={end_time}
```


> Response

```json
{
    "success": true,
    "data": [
        {
            "id": "c82b7de8-c654-4d9e-b84e-022b52c189bb",
            "status": "completed",
            "currency": "USDT",
            "chain": "Tron",
            "amount": "1500",
            "fee": "0",
            "fee_currency": "USDT",
            "txid": "ba2f799dd1607a0d118dd9320019ea9ca7e42492760e76abbeb27b29f6404cf7",
            "sentTime": "2022-02-03T22:02:37.048913+08:00",
            "completedTime": "2022-02-03T22:05:37.048913+08:00"
        },
        {
            "id": "c82b7de8-c654-4d9e-b84e-022b52c189bb",
            "status": "completed",
            "currency": "TWD",
            "chain": null,
            "amount": "20000",
            "fee": "0",
            "fee_currency": "TWD",
            "txid": null,
            "sentTime": "2022-02-03T22:02:37.048913+08:00",
            "completedTime": "2022-02-03T22:05:37.048913+08:00"
        }
    ]
}

```

Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | optional, if the field is empty, it will return all deposit history as default. (e.g. BTC, ETH, USDT, TWD)|
| start_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |
| end_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | |
| status | string | completed, rejected, amlscreenignored, blacklistignored, waitingconfirmation|
| currency | string | BTC, ETH, USDT, TWD |
| chain | string | Bitcoin, Ethereum, Tron |
| amount | float | total amount |
| fee | float |  |
| fee_currency | string | BTC, ETH, USDT, TWD  |
| txid | string | transaction hash |
| sentTime | string | when the deposit was sent|
| completedTime | string | when the deposit was completed |

</br>


### Get withdrawal history

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/wallet/history/withdrawal?currency={currency}&start_time={start_time}&end_time={end_time}
```


> Response

```json
{
    "success": true,
    "data": [
        {
            "id": "c82b7de8-c654-4d9e-b84e-022b52c189bb",
            "status": "completed",
            "currency": "USDT",
            "chain": "Tron",
            "amount": "1500",
            "fee": "0",
            "fee_currency": "USDT",
            "txid": "ba2f799dd1607a0d118dd9320019ea9ca7e42492760e76abbeb27b29f6404cf7",
            "sentTime": "2022-02-03T22:02:37.048913+08:00",
            "completedTime": "2022-02-03T22:05:37.048913+08:00"
        },
        {
            "id": "c82b7de8-c654-4d9e-b84e-022b52c189bb",
            "status": "pending",
            "currency": "TWD",
            "chain": null,
            "amount": "20000",
            "fee": "0",
            "fee_currency": "TWD",
            "txid": null,
            "sentTime": "2022-02-03T22:02:37.048913+08:00",
            "completedTime": null
        }
    ]
}

```

Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | optional, if the field is empty, it will return all withdrawal history as default. (e.g. BTC, ETH, USDT, TWD)|
| start_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |
| end_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | |
| status | string | completed, rejected, sent, pending, waitingapproval, approved, bankverifying, cancel, failed|
| currency | string | BTC, ETH, USDT, TWD |
| chain | string | Bitcoin, Ethereum, Tron |
| amount | float | total amount |
| fee | float |  |
| fee_currency | string | BTC, ETH, USDT, TWD  |
| txid | string | transaction hash |
| sentTime | string | when the withdrawal was sent|
| completedTime | string | when the withdrawal was completed |


</br>


## Markets

### Get markets

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/markets?market={market}
```

> Response

```json
{
    "success": true,
    "data": [
        {
            "market": "BTCTWD",
            "base_currency": "BTC",
            "quote_currency": "TWD",
            "price_increment": 0.25,
            "size_increment": 0.0001,
            "max_order_size": 5,
            "min_order_size": 0.000001,
            "fee_rate": 0.01
        }
    ]
}


```

Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| market | string | optional, if the field is empty, it will return all market information as default. (e.g. BTCTWD, ETHTWD, USDTTWD)|

</br>

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| market | string |  BTCTWD, ETHTWD, USDTTWD|
| base_currency | string | BTC, ETH, USDT |
| quote_currency | string | TWD|
| price_increment | float |  |
| size_increment | float |  |
| max_order_size | float |  maximum size of each order.  |
| min_order_size | float |  minimum size of each order.  |
| fee_rate | float | |
| ask | float | |
| bid | float | |


</br>


## Currencies

### Get currencies

Get supported currencies.

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/currencies?currency={currency}
```

> Response

```json
{
    "success": true,
    "data": [
        {
            "currency":"USDT",
            "supported_chains": [
                {
                    "chain": "Ethereum",
                    "withdrawal_fee": 16,
                    "min_withdrawal_size": 5
                },
                {
                    "chain": "Tron",
                    "withdrawal_fee": 1,
                    "min_withdrawal_size": 5
                }
            ]
        }
     ]
}



```

Request Parameters

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string | optional, if the field is empty, it will return all currencies information as default. (e.g. BTC, ETH, USDT, TWD)|

</br>

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| currency | string |  BTC, ETH, USDT, TWD |
| chain | string | Bitcoin, Ethereum, Tron |
| withdrawal_fee | float | fee per withdrawal |
| min_withdrawal_size | float | minimum size per withdrawal |

</br>


## Trade

### Get trades history

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/trade/history?market={market}&start_time={start_time}&end_time={end_time}
```

> Response

```json
{
    "success": true,
    "data": [
        {
            "id": "b3422e63-9112-499e-be60-1997f9455f6b",
            "market": "USDTTWD",
            "side": "buy",
            "price": 29.03,
            "size": 1000,
            "fee": 0,
            "fee_rate": 0,
            "fee_currency": "USDT",
            "timestamp": "2022-02-10T12:08:07.590928Z"
        }
    ]
}


```

Request Parameters 

| Field | Type  | Description |
| :---  | :---  | :---        |
| market | string | optional, if the field is empty, it will return all trade history as default. (e.g. BTCTWD, ETHTWD, USDTTWD)|
| start_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |
| end_time | integer | Unix timestamp, the number of seconds elapsed since January 1, 1970 UTC |

</br>

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | trade id |
| market | string  | BTCTWD, ETHTWD, USDTTWD |
| side | string  | buy, sell |
| price | float | price of the transation|
| size | float | total amount of the transation|
| fee | float | fee per transaction|
| fee_rate | float | |
| fee_currency | string | Bitcoin, Ethereum, Tron, TWD |
| time | string | when the transaction was completed |


</br>


### Get quotation

Get quotation for transaction.

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/trade/quote
```
```json
{
    "market": "USDTTWD",
    "side": "buy",
    "base_amount": 1000,
}
```


> Response


```json
{
    "success": true,
    "data": {
        "id": "ad122e63-9112-499e-be60-1997f9455f6b",
        "market": "USDTTWD",
        "side": "buy",
        "price": 29.03,
        "base_amount": 1000,
        "quote_amount": 29030,
        "fee": 0,
        "fee_rate": 0,
        "fee_currency": "USDT",
        "created_at": "2022-02-10T12:05:07.590928Z",
        "expired_at": "2022-02-10T12:10:07.590928Z",
    }
}
```


Payload 

| Field | Type  | Description |
| :---  | :---  | :---        |
| market | string | BTCTWD, ETHTWD, USDTTWD|
| side | string | buy, sell|
| base_amount | string | total amount you want to buy/sell (e.g. USDT, ETH, BTC)|
| quote_amount | string | total amount you want to buy/sell (e.g. TWD)|

<aside class="notice">
    NOTE: You have to provide base_amount <strong>OR</strong> quote_amount <strong>(only pick one of two)</strong> to ask for quotation.
</aside>

</br>

Response Format

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | quotation id |
| market | string  | BTCTWD, ETHTWD, USDTTWD |
| side | string  | buy, sell |
| price | float | current price |
| base_amount | float | total amount you want to buy/sell (e.g. USDT, ETH, BTC) |
| quote_amount | float | total amount you want to buy/sell (e.g. TWD) |
| fee | float | fee per transaction|
| fee_rate | float | |
| fee_currency | string | Bitcoin, Ethereum, Tron, TWD |
| created_at | string | when the quotation was created |
| expired_at | string | when the quotation expires |

<aside class="notice">
    NOTE: For complete the transaction, you can use <strong>Accept quotation API</strong> to transaction by using the quotation id.
</aside>

</br>


### Accept quotation

Accept quotation for transaction. 

<p style="color:red">Requires authentication.</p>

> Requst

```
GET /v1/exchange/trade/quote/accept
```
```json
{
    "id": "ad122e63-9112-499e-be60-1997f9455f6b"
}
```


> Response


```json
{
    "success": true
}
```


Payload 

| Field | Type  | Description |
| :---  | :---  | :---        |
| id | string | quotation id  |

<aside class="notice">
    NOTE: You can complete transaction with quotation id which is from <strong>Get quotation API
    </strong> by using <strong>Accept quotation API</strong>
</aside>
