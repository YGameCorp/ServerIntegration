# Web Payment
This is the XCT Payment System on Web. User can purchase the game content by using the XCT Web Payment
## 1. Flow
![alt text](https://github.com/xctcorporation/ServerIntegration/blob/master/web_payment_flow.jpg)

1.1: User login to XCT System by using the nivi account
1.2: API get list server game. This is the HTTP GET provided by Server Game to return the list of server game 
1.3: API get list payment. This is the HTTP GET provided by Server Game to return all purchase packages which offer in the game
1.4: Pay with XCT System. XCT provide some payment method such as Card, Banking ...
1.5: API payment success. Called when user make the payment successfully

## 1. API get list server game
This is your own API to return the list of server game to XCT payment system.
- Method: HTTP GET
- Params: 
  + xct_id: id of xct account
  + sign: Used to verify the request. [Click here to know how to verify the signature](https://github.com/xctcorporation/ServerIntegration/blob/master/HowToCreateSignature.md)
- Response: return the result in json format. For example: your game has four server games. We only join in S1 and S4, in S1 we created the character and named it 'hero' and in S4 we named the character is 'warrior'. The response will be returned as below
```
{
  "status":1,
  "msg":"",
  "data":[
    {"server_name":"S1","server_id":1,"char_name":"hero", "char_id":1001, "char_level":10},
    {"server_name":"S2","server_id":2},
    {"server_name":"S3","server_id":3},
    {"server_name":"S4","server_id":4,"char_name":"warrior", "char_id":4001, "char_level":20}
  ]
}
```

## 2. API get list payment
This is your own API to return the list payment packages of your game
![alt text](https://github.com/xctcorporation/ServerIntegration/blob/master/payment_packages.png)

- Method: HTTP GET
- Response: return the result in json format. For example: the response is corresponding to the screenshot above
```
{
  "status":1,
  "msg":"",
  "data":[
    {"name":"80 Nguyen Bao","id":"80_nb","image_url":"http://xxx", "price":20000},
    {"name":"200 Nguyen Bao","id":"200_nb","image_url":"http://xxx", "price":50000},
    {"name":"400 Nguyen Bao","id":"400_nb","image_url":"http://xxx", "price":100000},
    {"name":"2000 Nguyen Bao","id":"2000_nb","image_url":"http://xxx", "price":500000},
    {"name":"4000 Nguyen Bao","id":"4000_nb","image_url":"http://xxx", "price":1000000},
    {"name":"6000 Nguyen Bao","id":"6000_nb","image_url":"http://xxx", "price":1500000},
    {"name":"20000 Nguyen Bao","id":"20000_nb","image_url":"http://xxx", "price":5000000},
    {"name":"40000 Nguyen Bao","id":"40000_nb","image_url":"http://xxx", "price":10000000}
  ]
}
```

## 3. API payment success
- This is your own API to received the payment success request from Xlauncher Server. Please build your API in GET method. When users finish the payment transaction in Xlauncher system, Xlauncher server will send the notification to your application server-side via your callback url with the following parameters.

| Name        | Description           |
| ------------- |:-------------:|
| amount      | Value of the purchase |
| app_id      | The id of your application is issued by XCT, use this parameter to classify android and ios       |
| response_time | Purchase time|
| transaction_id | id of the transaction|
| transaction_type | Type of purchase: CARD, BANK|
| currency | VN or USD |
| user_id | id of user, who make the request|
| char_id | id of character - get from API get list server game|
| server_id | id of server game - get from API get list server game|
| payment_id | id of payment package - get from API get list payment|
| order_id | order id|
| card_code | * if transaction_type = CARD, card_code = code|
| card_serial | * if transaction_type = CARD, card_serial = serial|
| card_vendor | * if transaction_type = CARD, card_vendor = name|
| sign | Used to verify the request. [Click here to know how to verify the signature](https://github.com/xctcorporation/ServerIntegration/blob/master/HowToCreateSignature.md) |

- Your API must be response the result in the JSON format as description in the table below

| Response        |JSON Format            |
| ------------- |:-------------:|
| success response      | {"status": "1", "msg":""} |
| Failure response      | {"status": "0", "msg":"reason"} |
