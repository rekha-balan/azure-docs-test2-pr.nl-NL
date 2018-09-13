---
title: Troubleshooting | Microsoft Docs
description: How to resolve issues when using Microsoft Speech Service.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: 04f3da19939d523d201d357b2b0293db1508431d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867038"
---
# <a name="troubleshooting"></a>Troubleshooting

## <a name="error-http-403-forbidden"></a>Error `HTTP 403 Forbidden`

When using speech recognition API, it returns an `HTTP 403 Forbidden` error.

### <a name="cause"></a>Cause

This error is often caused by authentication issues. Connection requests without valid `Ocp-Apim-Subscription-Key` or `Authorization` header are rejected by the service with an `HTTP 403 Forbidden` response.

If you are using subscription key for authentication, the reason could be

- the subscription key is missing or invalid
- the usage quota of the subscription key is exceeded
- the `Ocp-Apim-Subscription-Key` field is not set in the request header, when REST API is called

If you are using authorization token for authentication, the following reasons could cause the error.

- the `Authorization` header is missing in the request when using REST
- the authorization token specified in the Authorization header is invalid
- the authorization token is expired. The access token has an expiry of 10 minutes

For more information about authentication, see the [Authentication](How-to/how-to-authentication.md) page.

### <a name="troubleshooting-steps"></a>Troubleshooting steps

#### <a name="verify-that-your-subscription-key-is-valid"></a>Verify that your subscription key is valid

You can run the following command for verification. Note to replace *YOUR_SUBSCRIPTION_KEY* with your own subscription key. If your subscription key is valid, you receive in the response the authorization token as a JSON Web Token (JWT). Otherwise you get an error in response.

> [!NOTE]
> Replace `YOUR_SUBSCRIPTION_KEY` with your own subscription key.

# <a name="powershelltabpowershell"></a>[Powershell](#tab/Powershell)

```Powershell
$FetchTokenHeader = @{
  'Content-type'='application/x-www-form-urlencoded';
  'Content-Length'= '0';
  'Ocp-Apim-Subscription-Key' = 'YOUR_SUBSCRIPTION_KEY'
}

$OAuthToken = Invoke-RestMethod -Method POST -Uri https://api.cognitive.microsoft.com/sts/v1.0/issueToken -Headers $FetchTokenHeader

# show the token received
$OAuthToken

```

# <a name="curltabcurl"></a>[curl](#tab/curl)

The example uses curl on Linux with bash. If it is not available on your platform, you may need to install curl. The example should work also on Cygwin on Windows, Git Bash, zsh, and other shells.

```
curl -v -X POST "https://api.cognitive.microsoft.com/sts/v1.0/issueToken" -H "Content-type: application/x-www-form-urlencoded" -H "Content-Length: 0" -H "Ocp-Apim-Subscription-Key: YOUR_SUBSCRIPTION_KEY"
```
---

Make sure that you use the same subscription key in your application or in the REST request as that is used above.

#### <a name="verify-the-authorization-token"></a>Verify the authorization token

This step is only needed, if you use authorization token for authentication. Run the following command to verify that the authorization token is still valid. The command makes a POST request to the service, and expects a response message from the service. If you still receive HTTP `403 Forbidden` error, double-check the access token is set correctly and not expired.

> [!IMPORTANT]
> The token has an expiry of 10 minutes.
> [!NOTE]
> Replace `YOUR_AUDIO_FILE` with the path to your prerecorded audio file, and `YOUR_ACCESS_TOKEN` with the authorization token returned in the previous step.

# <a name="powershelltabpowershell"></a>[Powershell](#tab/Powershell)

```Powershell

$SpeechServiceURI =
'https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed'

# $OAuthToken is the authrization token returned by the token service.
$RecoRequestHeader = @{
  'Authorization' = 'Bearer '+ $OAuthToken;
  'Transfer-Encoding' = 'chunked'
  'Content-type' = 'audio/wav; codec=audio/pcm; samplerate=16000'
}

# Read audio into byte array
$audioBytes = [System.IO.File]::ReadAllBytes("YOUR_AUDIO_FILE")

$RecoResponse = Invoke-RestMethod -Method POST -Uri $SpeechServiceURI -Headers $RecoRequestHeader -Body $audioBytes

# Show the result
$RecoResponse

```

# <a name="curltabcurl"></a>[curl](#tab/curl)

```
curl -v -X POST "https://speech.platform.bing.com/speech/recognition/interactive/cognitiveservices/v1?language=en-us&format=detailed" -H "Transfer-Encoding: chunked" -H "Authorization: Bearer YOUR_ACCESS_TOKEN" -H "Content-type: audio/wav; codec=audio/pcm; samplerate=16000" --data-binary @YOUR_AUDIO_FILE
```

---

## <a name="error-http-400-bad-request"></a>Error `HTTP 400 Bad Request`

This reason is usually that the request body contains invalid audio data. Currently we only support WAV file.

## <a name="error-http-408-request-timeout"></a>Error `HTTP 408 Request Timeout`

The error is most likely because that no audio data is sent to the service and the service returns this error after timeout. For REST API, the audio data should be put in the request body.

## <a name="the-recognitionstatus-in-the-response-is-initialsilencetimeout"></a>The `RecognitionStatus` in the response is `InitialSilenceTimeout`

Audio data is usually the reason causing the issue. For example,

- the audio has a long silence time at the beginning. The service will stop the recognition after some number of seconds and returns `InitialSilenceTimeout`.
- the audio uses unsupported codec format, which makes the audio data be treated as silence.
