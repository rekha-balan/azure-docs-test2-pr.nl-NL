---
title: Frequently Asked Questions about the Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get answers to common questions about the Bing Spell Check API on Azure.
services: cognitive-services
author: HeidiSteen
manager: jhubbard
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: conceptual
ms.date: 07/26/2017
ms.author: heidist
ms.openlocfilehash: 87b1f3ed3e0aaa9f3c3c804dc9eac3ee60b4a565
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870080"
---
# <a name="frequently-asked-questions-about-the-bing-spell-check-api"></a>Frequently Asked Questions about the Bing Spell Check API

 Find answers to commonly asked questions about concepts, code, and scenarios related to the Bing Spell Check API for Microsoft Cognitive Services on Azure.

## <a name="how-do-i-get-the-optional-client-headers-when-calling-the-bing-spell-check-api-from-javascript"></a>How do I get the optional client headers when calling the Bing Spell Check API from JavaScript?

The following headers are optional, but we recommend that you treat them as required. These headers help the Bing Spell Check API return more accurate results.

- X-Search-Location
- X-MSEdge-ClientID
- X-MSEdge-ClientIP

However, when you call the Bing Spell Check API from JavaScript, your browser's built-in security features might prevent you from accessing the values of these headers.

To resolve this issue, you can make the Bing Spell Check API request through a CORS proxy. The response from such a proxy has a `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.

It's easy to install a CORS proxy to allow the [tutorial app](tutorials/spellcheck.md) to access the optional client headers. First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/). Then enter the following command at a command prompt.

    npm install -g cors-proxy-server

Next, change the Bing Spell Check API endpoint in the HTML file to:

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/spellcheck/

Finally, start the CORS proxy with the following command:

    cors-proxy-server

Leave the command window open while you use the tutorial app; closing the window stops the proxy. In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it's the same for each request.

## <a name="next-steps"></a>Next steps

Is your question about a missing feature or functionality? Consider requesting or voting for it on the [UserVoice web site](https://cognitive.uservoice.com/).

## <a name="see-also"></a>See also

 [StackOverflow: Cognitive Services](http://stackoverflow.com/questions/tagged/microsoft-cognitive)
