
## Description of URL
All URL is going to use the HTTP method GET, there will be two types of URLs the Type 1 URL will contain the password and user as part of the URL command, the type 2 URL won't contain the password and user, therefore it will need a different method of authentication first. 

### CGI path
The two types of URLs will have different CGI format, these are defined in the firmware and cannot be changed, the Type 1 URL will have `/cgi-bin/` and Type 2 will have `/cgi-bin/cmd/`.

Type 1 URL:
```bash
http://ip:port/cgi-bin/system?USER=xxxx&PWD=xxxx&CMD
```
Type 2 URL:
```Bash
http://ip:port/cgi-bin/cmd/system?CMD
```

### Format of URL
Type 1 URL is considered not secure, although they are very simple and every CGI will support them 
```Bash
http://ip:port/cgi-bin/CGI?USER=admin&PWD=123456&CMD1=VALUE1&CMD2
```
where  

* `IP`: the device IPv4 address.  
* `port`: the device's HTTP port. If it is 80, the port could be omitted.  
* `CGI`: CGI Program like system, mpeg4, encoder, update,...   
* `CMD1=VALUE1`: write command to set the VALUE1 to device's configuration associated with CMD1.  
* `CMD2`: a read command to get the device's configuration associated with CMD2.  

Type 2 URL is more secure than Type 1 since the password and user are encrypted int he HTTP transaction, but not all CGI support this type or URL
```Bash
http://ip:port/cgi-bin/cmd/CGI?CMD1=VALUE1&CMD2
```
The structure is pretty much the same, the only difference is in the CGI path in this case we use `/cgi-bin/cmd/` instead of `/cgi-bin/`

### Multi-channel encoders
In this case, we have two different URLs, one will be the Router URL and the other will be the Video server URL, the visual difference is that the Video server URL will have a parameter `CHANNEL` right after the user and password and it is used to identify the channel we are targeting. The router URL will look just like the URLs we mentioned before

#### Format of the Router URL
```Bash
http://ip:port/cgi-bin/CGI?USER=Admin&PWD=123456&CMD1=VALUE1&CMD2
```
or
```Bash
http://ip:port/cgi-bin/cmd/CGI?CMD1=VALUE1&CMD2
```

#### Format of the Video Server URL
```Bash
http://ip:port/cgi-bin/CGI?USER=Admin&PWD=123456&CHANNEL=n&CMD1=VALUE1&CMD2
```
or
```Bash
http://ip:port/cgi-bin/cmd/CGI?CHANNEL=n&CMD1=VALUE1&CMD2
```
Where the `n` in the parameter `CHANNEL` will be the channel ID

### Quard encoder or 2CH video server
These commands are the same as the Multi-channel encoder, but instead of the router URL we will call it the Global URL, the Global URL won't have the parameter `CHANNEL` on it, but the video server URL will have that parameter and will behave as the multi-channel encoder.
>  most of quard encoders and 2CH video server are EOL by now 2020.

## URL Return message

The return message follows the HTTP standard, there are two parts to the message, these two parts are sent in one or two TCP packets  ( depending on the firmware implementation). The first par is the HTTP status header and the second part is the return message.

| HTTP 1.0 header| HTTP 1.1 header|
|:-----------------:|:----------------:|
|HTTP/1.0 200 OK\r\n|HTTP/1.1 200 OK\r\n
Content-type: text/plain\n\n|Content-Type: text/plain\r\n|
WAN_TYPE='1'\n|Content-Length: 13\r\n|
||\r\n|
||WAN_TYPE='1'\n|

### HTTP Status Header

The format of the HTTP status code

```BASh
HTTP/1.0 <HTTP_CODE> <HTTP_TEXT>\r\n
```

the most common codes will be:  

| HTTP code| HTTP Text    | Description             |
|:--------:|:------------:|:-----------------------:|
| 200      | OK           | Valid URL Command       |
| 400      | Unauthorized | Error in authentication |
| 401      | Not Found    | General Error           |

### Return message

There are five types of return message: 

1. **CMD='VALUE'**  
2. **OK: CMD='VALUE'**  
3. **OK**  
4. **ERROR: CMD='VALUE'**  
5. **ERROR: Descriptions of Error**  

> the HTTP 200 code will be return in type 4 and 5 messages, but they are an error message, so it is important to keep that in mind and not use the HTTP code as a validator.

#### 1. `CMD='VALUE'`

Used in the READ type of commands, the response will be the CMD value  on the request URL and a given value withing ' ', if the request contains more than one CMD the answer will list all the CMD 

Return Message for `URL WAN_TYPE&WAN_IP` is:
```Bash
WAN_TYPE='1'
WAN_IP='192.168.0.100'
```

#### 2. `OK: CMD='VALUE'`
Used in the WRITE URL command. If the VALUE is correct, the command will be echoed back with OK: tag, follow by the CMD send and the given value within ' '. If more than one value is given the return message of every URL will be displayed. 

Return Message for `URL WAN_TYPE=1&WAN_IP=192.168.1.100` is
```Bash
OK: WAN_TYPE='1'
OK: WAN_IP='192.168.0.100'
```

#### 3. `OK`
Used in the ACTION URL command like `SAVE`, `REBOOT`, `FACTORY_DEFAULT`, etc. There is no value returned for this command. 

Return Message for `URL REBOOT` is
```Bash
OK
```

#### 4. `ERROR: CMD='VALUE'`
Used in the WRITE URL command when the input argument is incorrect. the device will echo the URL command and incorrect given value. If there is more than one URL in the URL command, the return message will display all the commands, and values.

Return Message of the URL `WAN_TYPE=0` where the range of `WAN_TYPE` is `1~3`:
```Bash
ERROR: WAN_TYPE='1'
```
It shows the current WAN_TYPE setting in the device is 1.
Return Message for `URL WAN_TYPE=0&WAN_IP=192.168.1.100` is:
```Bash
ERROR: WAN_TYPE='1'
OK: WAN_IP='192.168.0.100'
```
The `WAN_TYPE` setting is incorrect so `WAN_TYPE` configuration is not updated, however, the `WAN_IP` setting is updated successfully.

#### 5. ERROR: Description of error

This is an error message display when the type 4 ERROR: CMD='VALUE' is not enough, bellow some of the most common errors:

|Description of Error    |  Description |
|:----------------------:|:------------:|
|missing `USER/PWD`	 | The USER or PWD command was not found in the Type1 URL|
|bad account/password| The user account name or password is incorrect in the Type1 URL.|
|missing `CHANNEL`	 | The CHANNEL command was not found |
|bad `CHANNEL=n`	     | The channel n Video Server is not active in the Multi-Channel Encoder device or the channel n is out of range in the Multi-Channel Encoder device.|
|CMD not found	     | The device does not support this CMD|
|CMD is write-only	 | The CMD is write only in the device |
|CMD is read-only	 | The CMD is read-only in the device  |
|not authorized	     | The CMD is not allowed to be executed because of the lower login level.|
|invalid parameters	 | The input argument is incorrect in the Write-Only Command and Write Operation with a list index, like MOTION_CONFIG in ENCODER CGI|
|no command	         | There is no URL command in the URI.|
|firmware image	     | Firmware image file is corrupted or MD5 check error in firmware upgrade URLs|
|firmware version	 | Firmware version mismatches in firmware upgrade URLs|
|firmware type	     | Firmware Type error (AC/NB mismatches) in firmware upgrade URLs|
|config image	     | Configuration file is corrupted|
|oem image	         | OEM image file is corrupted|
|profile image	     | Camera Profile image file is corrupted |
|profile ID	         | Profile ID mismatches in profile upgrade URLs |
|PTZ Image	         | PTZ image file is corrupted |
|8051DNX Image	     | 8051DNX image file is corrupted|
|8051THX Image	     |8051THX image file is corrupted|
|internal error <more description>|	There is an error internally. There might be more description of the error|

## Valid Character in the URL Commands
The valid characters will depend on which part of the URL are they.

### Valid Characters in the Login Name

1. Only *A~Z*, *a~z*, 0~9, minus sign (-), underscore (_), period (.), $ and @ are allowed.  
2. The first character is allowed to *A~Z* or *a~z*.  

### Valid Characters in Login Password 

1. Printable characters: Started from ASCII code $0x21$ to $0x7E$, with the exception of these 10 reserved characters which are not allowed  `':', '#', '?', '/', '\', '%', '&', ''', '"', ','`  

### Valid Characters in Network Name
1. Only ASCII *A~Z*, *a~z*, 0~9, minus sign (-), underscore (_), and period (.) are allowed.  
2. No blank or space characters are permitted as part of a name.  
3. The last character must not be a minus sign, underscore, or period.  
4. The first character is allowed to either a letter or a digit.  
5. No NULL string is allowed.  

### General  rule of Valid Characters in URI
1. Only ASCII *A~Z*, *a~z*, 0~9, minus sign (-), underscore (_), period (.), and space ( ) characters are allowed.  
2. The last character must not be a minus sign, underscore, period, or space.  
3. The first character is allowed to either a letter or a digit.  
4. NULL string is allowed.  