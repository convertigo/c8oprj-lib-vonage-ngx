# lib_Vonage_Ngx
This is the Convertigo connector to Vonage API for SMS, Viber, Whatsapp, Facebook Messenger and MMS messaging services. The library also provides APIs for Video Components.

More information on Vonage APIs can be found here:

https://www.vonage.co.uk/communications-apis/?icmp=mainnav_products_communicationsapis


## Installation
In your Convertigo Studio, Use file->import->Convertigo Project and paste

    lib_Vonage_Ngx=https://github.com/convertigo/c8oprj-lib-vonage-ngx.git

In the Project Remote Url field

## Usage for messaging APIs
The Library provides sequences you can use to in your apps to send SMS, and other messages.

### Configuring symbols
This library needs 2 symbols :

|Symbol    | usage                   |
|------------| ------------------------|
|lib_Vonage_Ngx.apiKey  | The Api Key you can find in the https://dashboard.nexmo.com/ dashboard |
|lib_Vonage_Ngx.apiSecret.secret | The API Secret you can find in the same place. |

Configure these symbols to the correct value you find in the Vonage API dashboard

https://dashboard.nexmo.com/

### Sequences

Youc can use the following sequences in your project :

|sequence    | usage                   |
|------------| ------------------------|
|sendSMS     | send a SMS to anyone    |
|sendWhatspp | send a WhatsApp Message |

## Usage for Video APIs
The library provides APIs as sequences and Shared Components you can use in you apps. It also provides a sample app you can use to see how to use each of these.

### Global Symbols
The library need some global symbols to be configured. 

|Symbol    | usage                   |
|------------| ------------------------|
|lib_Vonage_Ngx.video.apiKey	| the Api key you can find in the https://tokbox.com/account/#/ for a given project |
|lib_Vonage_Ngx.video.apiSecret.secret	| the Api secret you also find  on this page |
|lib_Vonage_Ngx.video.project| The Vonage video project named you created |


### Sequences

You can use the following sequences in your project to create sessions, tokens and retrieve API keys.

|sequence    | usage                   |
|------------| ------------------------|
|ApiCreateVideoSession     | Creates a video session and returns it. Usually the session is saved in a FullSync database|
|ApiGetVideoApiKey         | Useful to get the Video API key on the client as the Video components needs it |
|ApiGetVideoToken          | Generates a token for the Video components.  |

### Shared Component

You can use the _VonageVideo_ shared component in your apps. This will handle automatically the Video publishing and Video subscriber mode. 

|Shared Component variable    | usage                   |
|------------| ------------------------|
|SessionId     | The session id. You can get it using the _ApiCreateVideoSession_ sequence |
|token     | The token. Aloso you can get it using the _ApiGetVideoToken_ sequence |
|apiKey     | Your Vonage video api key. This is usually configured as global symbol on Convertigo Server. You can use the _ApiGetVideoApiKey_ to get it from the Convertigo  Server |
|mode     | The connection mode. can be 'publisher', 'subscriber' or 'moderator' |

### Standard workflow

The usual workflow for using the video components is :

* Use the _ApiCreateVideoSession_ sequence to get a session id. This will call all the necessary Vonage APIs to get you one
* You can use a FullSync database to store this session ID as it will have to be shared by other users.
* Then use the _ApiGetVideoToken_ to get a PUBLISHER token or a SUBSCRIBER token on this session.
* Use the utility _ApiGetVideoApiKey_ to get on your client the Api Key configured as symbol on the Convertigo server.
* Insert the _VonageVideo_ shared component in one you pages passing all the necessary value for the components variable. be sure to use a PUBLISHER token for publisher mode and a SUBSCRIBER token for a subscriber mode.
* Enjoy : )
  
### The sample App

The library come with a sample App. This demonstrates how to create session, how to store them in a FullSync database, how to launch subscriber or publisher pages to handle video sessions.
