OAuth 2
==========

* **TODO:** _Introduction and a better description_

Now and example of how the OAuth 2 interation look like:

1. Get (ussually) Manually  
 `client_id`  
 `client_secret`

1. Sent User over OAuth Client:  
`GET: provider.com/oauth/authorize?`  
`client_id`  
`redirect_uri`  

1. Web ask for permission  
   $yes$   or    $no$

1. Re-direct to the uri:  
`GET: clietn.com/oauth_accept?`  
`code: foobahz`

1. Issue access token  
`POST: provider.com/oauth/access_token`  
`code: foobahz`  
`client_id: foo`  
`client_secret: bar`  

1. Get access token  
$Result:$  
``` {'access_token' : 'bazfoobahz'} ```  

1. Can do alll user will do  
`GET: /user/me/friends`  
`access_token: bazfoobahz`  

1. Response  
$Result:$  
`{'friends': [{'name': ....}]}`

