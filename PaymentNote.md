# How to use Xlauncher Payment System Flexible 

## 1. What's the problem
XCTCorp is one of the famous publisher in Vietnam. We already have published many games such as action game, role playing game, card battle ... We used to be facing in different payment scenarios when connect and publish these games. A payment scenarios means the action when user purchase the digital goods in game. 
For example, In somes game, users can use their money to buy coins - a digital money in game - or to buy some special items. 
How to adapt the payment process in this payment scenarios? How to know when user want to buy coins or buy special items?
This document will be help you to resolve this problem

## 2. My Solution
Let me reuse the example above. A game provide two payment packages for user, let's name it a "package_coin" and "package_item"

- package_coin: purchase 0.99$ and get 100 coin
- package_item: purchase 0.99$ and get a valuable item, for example, a cup of tea

Let me remind you the payment process
- Step 1: user choice the payment package in your game
- Step 2: your game create "the payment extra data (PED)" and call the function showPaymentScreen in SDK
- Step 3: user confirm the payment
- Step 4: Xlaucher client send the payment receipt with your PED to Xlauncher server
- Step 5: Xlaucher server process payment and "callback the result" to your server game

That's all

Let's focus two important steps, "create the payment extra data" and "callback the result".
In step 2, PED is your customized data, you can build PED whatever you want.
Hey, Come back to the example above. I will demo how to use the PED to classify the package_coin and package_item.
We need some additional information to demo. An user who make the purchase in game is named "Peter".
My PED will be contructed by formatting below
PED = base64( username + | + 
