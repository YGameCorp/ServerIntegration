# Create the signature from request parameters

- This is the sample how to create the signature from request parameters. For example, we have some parameters below

		amount=0.99&app_id=ea2d5a18ebbd43871103b502f804db79&response_time=2017-01-10 17:11:33&transaction_id=43093285&transaction_type=CARD&currency=VND&game_order=1147277470600214&user_id=217&order_id=ffc9447c6c45b1d1a6ecbdfbd3a1aa21&card_code=xxxxxxxx&card_serial=yyyyyyy&card_vendor=viettel

- Step 1: sort the name of parameters by A → Z

		amount > app_id > card_code > card_serial > card_vendor > currency > game_order > order_id > response_time > transaction_id > transaction_type > user_id

- Step 2: get the values from ordered parameters. We have the final String

		values = 0.99ea2d5a18ebbd43871103b502f804db79xxxxxxxxyyyyyyyviettelVND1147277470600214ffc9447c6c45b1d1a6ecbdfbd3a1aa212017-01-10 17:11:3343093285CARD217

- Step 3: create the signature

```
sign = md5( values + appSecret )
* appSecret: the secret key of your application is issued by XCT

For example:
var appSecret = "ff9af584ad6c9328930f3925f2c973f0"
sign = md5 ( values + appSecret ) = 16f97f19fe1ded03bb3e175b19a0709e
```
