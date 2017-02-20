# ServerIntegration

1. Get User Information

..1. Flow
	
	![alt tag](https://github.com/xctcorporation/ServerIntegration/blob/master/get_user_info.png)
	
..2. Description 

1. Game Client calls a Xlauncher function, then SDK show up the Login UI.

2. Xlauncher Client sends a login request to Xlauncher server to validate the user info.

3. Xlauncher Client  receives the user info and accessToken from Xlauncher server.

4. Xlauncher Client transfer the accessToken and user info to Game Client in order to notify there is a user login to game.

5. Game Client create a login request with the accessToken and send it to Game Server.

6. Game Server get the user information by sending the request to Xlauncher server API with the accessToken as a parameter.

7. Game Server receives User information from the Xlauncher Server.
8. Game Client receives Login Response and let the user join game.

	1.3 Xlauncher server API
- When users login or register to Xlauncher system successfully, The access token will be passed from Xlauncher system to your client. Access token is used to get the user information from your server-side.  
- To send a message, your Game Server issues a POST request.

URL: https://api.nivi.vn/v1/user/user_info

If you build in the TEST MODE, use the domain:
URL: https://devsdk.nivi.vn:9101/v1/user/user_info	
