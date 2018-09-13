---
title: Bing Text To Speech API in Microsoft Cognitive Services | Microsoft Docs
description: Use the Bing Text to Speech API to provide real-time text to speech conversion in a variety of voices and languages
services: cognitive-services
author: priyaravi20
manager: yanbo
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 03/16/2017
ms.author: prrajan
ms.openlocfilehash: 3ff46f3fdf14c57bf8781d7a553eb42e85ddf4cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564475"
---
# <a name="bing-text-to-speech-api"></a>Bing Text To Speech API

## <a name="Introduction"> Introduction</a>
With the Bing Text to Speech API your application can send HTTP requests to a cloud server, where text is instantly synthesized into human sounding speech, and returned as an audio file.  The API can be used in many different contexts to provide real-time text to speech conversion in a variety of different voices and languages.  

## <a name="VoiceSynReq"> Voice Synthesis Request</a>

### <a name="Subscription">Authorization Tokens</a>
Every request requires a JSON Web Token (JWT) access token. The JWT access token is passed through in the Speech request header. The token has an expiry time of 10 minutes. See [Get Started for Free](https://www.microsoft.com/cognitive-services/en-US/sign-up?ReturnUrl=/cognitive-services/en-us/subscriptions?productId=%2fproducts%2fBing.Speech.Preview) for information about subscribing and obtaining API keys used to retrieve valid JWT access tokens.

The API key is passed to the token service, for example:

```
POST https://api.cognitive.microsoft.com/sts/v1.0/issueToken
Content-Length: 0
```

The required header for token access is:

Name    | Format    | Description, Example and Use
---------|---------|--------
Ocp-Apim-Subscription-Key | ASCII   | Your subscription key.

The token service returns the JWT access token as text/plain. Then the JWT is passed as a Base64 access_token to the Speech endpoint as an Authorization header prefixed with the string Bearer, for example:

`Authorization: Bearer [Base64 access_token]`

Clients must use the following endpoint to access the text to speech service: 

`https://speech.platform.bing.com/synthesize` 

>[!NOTE]
>Until you have acquired an access token with your subscription key as described above this link will generate a 403 Response Error.

### <a name="Http">HTTP Headers</a>
HTTP headers for the request include:

Header   |Value  |Comments 
---------|---------|---------
Content-Type     |    application/ssml+xml     |      The input content type   
X-Microsoft-OutputFormat     |  **1)** ssml-16khz-16bit-mono-tts, **2)** raw-16khz-16bit-mono-pcm, **3)** audio-16khz-16kbps-mono-siren, **4)** riff-16khz-16kbps-mono-siren **5)** riff-16khz-16bit-mono-pcm **6)** audio-16khz-128kbitrate-mono-mp3, **7)** audio-16khz-64kbitrate-mono-mp3, **8)** audio-16khz-32kbitrate-mono-mp3 |       The output audio format  
X-Search-AppId     |    A GUID (hex only, no dashes)     |     An ID that uniquely identifies the client application. This can be Store ID for Apps. If one is not available, the ID may be user generated per-application.     
X-Search-ClientID     |     A GUID (hex only, no dashes)    |    An ID that uniquely identifies application instance per-installation.     
User-Agent     |     Application name    |     Application name is required and must be less than 255 characters.    

### <a name="InputParam">Input Parameters</a>
Inputs to the Bing Text to Speech API are expressed as HTTP query parameters. Parameters in the POST body are treated as Speech Synthesis Markup Language (SSML) content. Refer to the [SSML W3C Specification](http://www.w3.org/TR/speech-synthesis/) for a description of the markup used to control aspects of speech such as the language and gender of the speaker.
The following is a complete list of recognized input parameters:  

Parameter   |Description | Values 
---------|---------|----------
VoiceType | Indicates the preferred gender of the voice to speak the synthesized text. | Female, Male 
VoiceName | Indicates the processor-specific voice name used to speak the synthesized text. | See [Supported Locales and Voice Fonts](#SupLocales)
Locale | Indicates the language used to speak the synthesized text. | See [Supported Locales and Voice Fonts](#SupLocales)  
OutputFormat | Indicates the audio format the text will be synthesized into | SSML16Khz16BitMonoTTS, Raw16khz16bitMonoPCM, Audio16khz16kbpsMonoSiren, Riff16khz16kbpsMonoSiren, Riff16khz16bitMonoPcm, Audio16khz128kbitrateMonoMp3, Audio16khz64kbitrateMonoMp3, Audio16khz32kbitrateMonoMp3 
RequestUri | Indicates the URI of the Internet resource associated with the request | 
AuthorizationToken | Token used to validate the transaction | 
Text | The text to be synthesized. | **Note**: Unsafe characters should be escaped following the W3C URL specifications ([http://www.w3.org/Addressing/URL/url-spec.txt](http://www.w3.org/Addressing/URL/url-spec.txt)).

>[!NOTE]
>Requests with more than one instance of any parameter will result in an HTTP 400 error response.

###  <a name="SampleVoiceOR">Example Voice Output Request</a>
The following is an example of a voice output request:  
 
```
POST /synthesize
HTTP/1.1
Host: speech.platform.bing.com
Content-Type: audio/wav; samplerate=8000

X-Microsoft-OutputFormat: riff-8khz-8bit-mono-mulaw
Content-Type: text/plain; charset=utf-8
Host: speech.platform.bing.com
Content-Length: 197

<speak version='1.0' xml:lang='en-US'><voice xml:lang='en-US' xml:gender='Female' name='Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)'>Microsoft Bing Voice Output API</voice></speak>
```
 
## <a name="VoiceOutResponse"> Voice Output Responses</a>
The Bing Text to Speech API uses HTTP POST to send audio back to the client. The API response contains the audio stream and the codec and will match the requested output format. The maximum amount of audio returned for a given request must not exceed 15 seconds. 
 
#### <a name="SuccessfulRecResponse"> Successful Synthesis Response</a>
Example JSON response for a successful voice search. The comments and formatting of the JSON below is for example reasons only. Indentation spaces, smart quotes, comments, etc. are omitted from the actual response. 
```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: audio/x-wav 

Response audio payload       
```
 
#### <a name="RecFailure"> Synthesis Failure</a>

Example JSON response for a voice synthesis query failure.

```
HTTP/1.1 400 XML parser error
Content-Type: text/xml
Content-Length: 0
```
 
### <a name="ErrorResponse"> Error Responses</a>

Error   | Description 
---------|---------
**HTTP/400 Bad Request** | Will be returned if a required parameter is missing, empty or null, or if the value passed to either a required or optional parameter is invalid. The “Invalid” response includes passing a string value that is longer than the allowed length. A brief description of the problematic parameter will be included.  
**HTTP/401 Unauthorized** | Will be returned if the request is not authorized. 
**HTTP/413 RequestEntityTooLarge**  | Will be returned if the SSML input is larger than what is supported. 
**HTTP/502 BadGateway** | Network related problem or a server side issue. 

#### <a name="example-error-response"></a>Example Error Response.
```
HTTP/1.0 400 Bad Request
Content-Length: XXX
Content-Type: text/plain; charset=UTF-8

Voice name not supported
```

## <a name="SampleApp">Sample Application</a>
See the [Visual C#.NET Text to Speech sample application](https://github.com/Microsoft/Cognitive-Speech-TTS/blob/master/Samples-Http/CSharp/TTSProgram.cs) for implementation details.  

## <a name="SupLocales">Supported Locales and Voice Fonts</a>

Supported locales and related voice fonts include:

Locale | Gender | Service name mapping 
---------|--------|------------
ar-EG*   |   Female  | "Microsoft Server Speech Text to Speech Voice (ar-EG, Hoda)"
de-DE    |   Female  | "Microsoft Server Speech Text to Speech Voice (de-DE, Hedda)" 
de-DE    |   Male    | "Microsoft Server Speech Text to Speech Voice (de-DE, Stefan, Apollo)" 
en-AU    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-AU, Catherine)" 
en-CA    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-CA, Linda)"
en-GB    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-GB, Susan, Apollo)"
en-GB    |     Male  | "Microsoft Server Speech Text to Speech Voice (en-GB, George, Apollo)"
en-IN    |     Male  | "Microsoft Server Speech Text to Speech Voice (en-IN, Ravi, Apollo)"  
en-US    |Female|"Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)"
en-US    |Male|"Microsoft Server Speech Text to Speech Voice (en-US, BenjaminRUS)"
es-ES    |Female|"Microsoft Server Speech Text to Speech Voice (es-ES, Laura, Apollo)"
es-ES    |Male|"Microsoft Server Speech Text to Speech Voice (es-ES, Pablo, Apollo)"
es-MX|Male|"Microsoft Server Speech Text to Speech Voice (es-MX, Raul, Apollo)"
fr-CA|Female|"Microsoft Server Speech Text to Speech Voice (fr-CA, Caroline)"
fr-FR|Female|"Microsoft Server Speech Text to Speech Voice (fr-FR, Julie, Apollo)"
fr-FR|Male|"Microsoft Server Speech Text to Speech Voice (fr-FR, Paul, Apollo)"
hi-IN|Female|"Microsoft Server Speech Text to Speech Voice (hi-IN, Kalpana, Apollo)"
it-IT|Male|"Microsoft Server Speech Text to Speech Voice (it-IT, Cosimo, Apollo)"
ja-JP|Female|"Microsoft Server Speech Text to Speech Voice (ja-JP, Ayumi, Apollo)"
ja-JP|Male|"Microsoft Server Speech Text to Speech Voice (ja-JP, Ichiro, Apollo)"
ko-KR|Female|"Microsoft Server Speech Text to Speech Voice (ko-KR,HeamiRUS)"
pt-BR|Male|"Microsoft Server Speech Text to Speech Voice (pt-BR, Daniel, Apollo)"
ru-RU|Female|"Microsoft Server Speech Text to Speech Voice (ru-RU, Irina, Apollo)"
ru-RU|Male|"Microsoft Server Speech Text to Speech Voice (ru-RU, Pavel, Apollo)"
zh-CN|Female|"Microsoft Server Speech Text to Speech Voice (zh-CN, HuihuiRUS)"
zh-CN|Female|"Microsoft Server Speech Text to Speech Voice (zh-CN, Yaoyao, Apollo)"
zh-CN|Male|"Microsoft Server Speech Text to Speech Voice (zh-CN, Kangkang, Apollo)"
zh-HK|Female|"Microsoft Server Speech Text to Speech Voice (zh-HK, Tracy, Apollo)"
zh-HK|Male|"Microsoft Server Speech Text to Speech Voice (zh-HK, Danny, Apollo)"
zh-TW|Female|"Microsoft Server Speech Text to Speech Voice (zh-TW, Yating, Apollo)"
zh-TW|Male|"Microsoft Server Speech Text to Speech Voice (zh-TW, Zhiwei, Apollo)"
 *ar-EG supports Modern Standard Arabic (MSA)

## <a name="TrouNSupport"> Troubleshooting and Support</a>

Post all questions and issues to the [Bing Speech Service](https://social.msdn.microsoft.com/Forums/en-US/home?forum=SpeechService) MSDN Forum, with complete detail, such as: 
* An example of the full request string.
* If applicable, the full output of a failed request, which includes log IDs.
* The percentage of requests that are failing.

