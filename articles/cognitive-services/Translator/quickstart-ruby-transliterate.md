---
title: Translator Text convert text script with Ruby | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 56872ed6b6d7168fb1bf2c45de8104a592af34e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870556"
---
# <a name="quickstart-transliterate-text-with-ruby"></a>Quickstart: Transliterate text with Ruby

In this quickstart, you convert text in one language from one script to another using the Translator Text API.

## <a name="prerequisites"></a>Prerequisites

You'll need [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) or later to run this code.

To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).

## <a name="transliterate-request"></a>Transliterate request

The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.

1. Create a new Ruby project in your favorite code editor.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```ruby
require 'net/https'
require 'uri'
require 'cgi'
require 'json'
require 'securerandom'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the key string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'https://api.cognitive.microsofttranslator.com'
path = '/transliterate?api-version=3.0'

# Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
params = "&language=ja&fromScript=jpan&toScript=latn";

uri = URI (host + path + params)

# Transliterate "good afternoon".
text = 'こんにちは'

content = '[{"Text" : "' + text + '"}]'

request = Net::HTTP::Post.new(uri)
request['Content-type'] = 'application/json'
request['Content-length'] = content.length
request['Ocp-Apim-Subscription-Key'] = key
request['X-ClientTraceId'] = SecureRandom.uuid
request.body = content

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request (request)
end

result = response.body.force_encoding("utf-8")

json = JSON.pretty_generate(JSON.parse(result))
puts json
```

## <a name="transliterate-response"></a>Transliterate response

A successful response is returned in JSON as shown in the following example:

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a>Next steps

Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.

> [!div class="nextstepaction"]
> [Explore Ruby examples on GitHub](https://aka.ms/TranslatorGitHub?type=&language=ruby)
