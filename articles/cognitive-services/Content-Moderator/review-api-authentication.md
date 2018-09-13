---
title: Authenticate calls to Review API for Content Moderator | Microsoft Docs
description: Generate the Azure Active Directory tokens to use for authenticating Review API calls.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/19/2017
ms.author: sajagtap
ROBOTS: NOINDEX
redirect_url: /azure/cognitive-services/content-moderator/review-api
redirect_document_id: true
ms.openlocfilehash: f1e94853f790d092f6a5d7a46e4edee0b28d5855
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554908"
---
# <a name="how-to-authenticate-your-review-api-calls"></a><span data-ttu-id="f872b-103">How to Authenticate Your Review API Calls</span><span class="sxs-lookup"><span data-stu-id="f872b-103">How to Authenticate Your Review API Calls</span></span>

## <a name="introduction"></a><span data-ttu-id="f872b-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="f872b-104">Introduction</span></span>
<span data-ttu-id="f872b-105">The Review API is protected using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f872b-105">The Review API is protected using Azure Active Directory.</span></span> <span data-ttu-id="f872b-106">This section describes how you can generate the Azure Active Directory tokens to use for authenticating your review API calls.</span><span class="sxs-lookup"><span data-stu-id="f872b-106">This section describes how you can generate the Azure Active Directory tokens to use for authenticating your review API calls.</span></span>

## <a name="where-do-i-get-my-credentials"></a><span data-ttu-id="f872b-107">Where do I get my credentials?</span><span class="sxs-lookup"><span data-stu-id="f872b-107">Where do I get my credentials?</span></span>
<span data-ttu-id="f872b-108">Once you have created your team in the [review tool](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool"), navigate to the **Credentials** TAB under **Settings** as shown below to find your **Client Id** and **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="f872b-108">Once you have created your team in the [review tool](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool"), navigate to the **Credentials** TAB under **Settings** as shown below to find your **Client Id** and **Client Secret**.</span></span>

<span data-ttu-id="f872b-109">The Keys section allows you to generate the client secrets(keys) that you would need to use to authenticate while using the Review API.</span><span class="sxs-lookup"><span data-stu-id="f872b-109">The Keys section allows you to generate the client secrets(keys) that you would need to use to authenticate while using the Review API.</span></span> <span data-ttu-id="f872b-110">The secrets are time bound and can have lifetime of either 1 or 2 years.</span><span class="sxs-lookup"><span data-stu-id="f872b-110">The secrets are time bound and can have lifetime of either 1 or 2 years.</span></span>

<span data-ttu-id="f872b-111">You can generate multiple secrets(keys) to cycle through them in your production environment.</span><span class="sxs-lookup"><span data-stu-id="f872b-111">You can generate multiple secrets(keys) to cycle through them in your production environment.</span></span> <span data-ttu-id="f872b-112">The value of the secret(key) is viewable once after you generate it.</span><span class="sxs-lookup"><span data-stu-id="f872b-112">The value of the secret(key) is viewable once after you generate it.</span></span> <span data-ttu-id="f872b-113">Please remember to save the value before navigating away from the page or before generating a new secret.</span><span class="sxs-lookup"><span data-stu-id="f872b-113">Please remember to save the value before navigating away from the page or before generating a new secret.</span></span>

![Content Moderator Review API Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/images/Moderator-Review-API-Credentials.PNG)

## <a name="using-the-client-id-and-client-secret-to-authenticate"></a><span data-ttu-id="f872b-115">Using the Client Id and Client Secret to Authenticate</span><span class="sxs-lookup"><span data-stu-id="f872b-115">Using the Client Id and Client Secret to Authenticate</span></span>
<span data-ttu-id="f872b-116">Use the credentials from the previously mentioned page to generate authentication tokens for your Review API calls.</span><span class="sxs-lookup"><span data-stu-id="f872b-116">Use the credentials from the previously mentioned page to generate authentication tokens for your Review API calls.</span></span>

<span data-ttu-id="f872b-117">You can do so by either [using the interactive Postman tool](https://github.com/MicrosoftContentModerator/Docs/blob/master/UsingPostman.md) or by using code.</span><span class="sxs-lookup"><span data-stu-id="f872b-117">You can do so by either [using the interactive Postman tool](https://github.com/MicrosoftContentModerator/Docs/blob/master/UsingPostman.md) or by using code.</span></span>

<span data-ttu-id="f872b-118">The following samples show how to use the Client Id and Client Secret(key) to generate time bound tokens.</span><span class="sxs-lookup"><span data-stu-id="f872b-118">The following samples show how to use the Client Id and Client Secret(key) to generate time bound tokens.</span></span>

## <a name="request-samples"></a><span data-ttu-id="f872b-119">Request Samples</span><span class="sxs-lookup"><span data-stu-id="f872b-119">Request Samples</span></span>

#### <a name="curl"></a><span data-ttu-id="f872b-120">CURL</span><span class="sxs-lookup"><span data-stu-id="f872b-120">CURL</span></span>
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'resource=https://api.contentmoderator.cognitive.microsoft.com/review&client_id=<Your Client Id>&client_secret=<Your Client Key/Secret>&grant_type=client_credentials' "https://login.microsoftonline.com/contentmoderatorprod.onmicrosoft.com/oauth2/token"

    NodeJS Unirest
    var unirest = require("unirest");
    var req = unirest("POST", "https://login.microsoftonline.com/contentmoderatorprod.onmicrosoft.com/oauth2/token");

    req.headers({
        "content-type": "application/x-www-form-urlencoded"
    });

    req.form({
        "resource": "https://api.contentmoderator.cognitive.microsoft.com/review",
        "client_id": "< Your Client Id >",
        "client_secret": "< Your Client Key/Secret >",
        "grant_type": "client_credentials"
    });

    req.end(function (res){
        if (res.error) throw new Error(res.error);
        console.log(res.body);
    });

#### <a name="python"></a><span data-ttu-id="f872b-121">Python</span><span class="sxs-lookup"><span data-stu-id="f872b-121">Python</span></span>
    import http.client
    conn = http.client.HTTPSConnection("login.microsoftonline.com")
    payload = "resource=https%3A%2F%2Fapi.contentmoderator.cognitive.microsoft.com%2Freview&client_id=< Your Client Id >&client_secret=< Your Client Key/Secret >&grant_type=client_credentials"
    headers = {
        'content-type': "application/x-www-form-urlencoded"
    }
    conn.request("POST", "/contentmoderatorprod.onmicrosoft.com/oauth2/token", payload, headers)
    res = conn.getresponse()
    data = res.read()
    print(data.decode("utf-8"))

#### <a name="c"></a><span data-ttu-id="f872b-122">C#</span><span class="sxs-lookup"><span data-stu-id="f872b-122">C#</span></span>
    var client = new RestClient("https://login.microsoftonline.com/contentmoderatorprod.onmicrosoft.com/oauth2/token");
    var request = new RestRequest(Method.POST);
    request.AddHeader("content-type", "application/x-www-form-urlencoded");
    request.AddParameter("application/x-www-form-urlencoded", "resource=https%3A%2F%2Fapi.contentmoderator.cognitive.microsoft.com%2Freview&client_id=< Your Client Id >&client_secret=< Your Client Key/Secret >&grant_type=client_credentials", ParameterType.RequestBody);
    IRestResponse response = client.Execute(request);

## <a name="response-sample"></a><span data-ttu-id="f872b-123">Response Sample</span><span class="sxs-lookup"><span data-stu-id="f872b-123">Response Sample</span></span>
    {
        "token_type": "Bearer",
        "expires_in": "3600",
        "ext_expires_in": "0",
        "expires_on": "1476491009",
        "not_before": "1476487109",
        "resource": "https://api.contentmoderator.cognitive.microsoft.com/review",
        "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ikk2b0J3NFZ6QkhPcWxlR3JWMkFKZEE1RW1YYyIsImtpZCI6Ikk2b0J3NFZ6QkhPcWxlR3JWMkFKZEE1RW1YYyJ9.eyJhdWQiOiJodHRwOi8vd2ItcmV2aWV3LXN2YyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdjNDZiZTcwLTkyZmItNDkzMS1hNzE5LWY0MWU4NmEwMGNlOS8iLCJpYXQiOjE0NzY0ODcxMDksIm5iZiI6MTQ3NjQ4NzEwOSwiZXhwIjoxNDc2NDkxMDA5LCJhcHBpZCI6IjIxMmQyODczLTFlZDEtNDRiNi1hNGFlLTQ1MWI4MjdmODZjZCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdjNDZiZTcwLTkyZmItNDkzMS1hNzE5LWY0MWU4NmEwMGNlOS8iLCJ0aWQiOiI3YzQ2YmU3MC05MmZiLTQ5MzEtYTcxOS1mNDFlODZhMDBjZTkiLCJ2ZXIiOiIxLjAifQ.jiCrnPMWDT0Zq9NPNjlU02-NeTNrOv13ujPODXvJ8Bvu5tRWKj4sjdHP-ml9L1KXgMUZZ_JZ9N7_7vFuard6hGg1XRE-ZeIuCToihy3M10kwaTEnNDQI4SRmuYWZZfhbEQ8FnSB5EICZnDKS5gFswkDVaQAjPSNKgV12fjIocqTxPvUpbDLYr8SPWcYuUitj803CPIpK9necLH7Fuh1Un2N_KJ9lPxvG5pbQRdUY4BIuKhuPOyFWx0_aAOSUZQx7xGOsL9VXKWg74elYOxcXL2gbqIEy1CA_tRyKhB_pJhB_4UcWpAEeP-v8ODpXiIqHWBuOImCarquGxY6STIaV1g"
    }

<span data-ttu-id="f872b-124">The POST token response specifies the token expiration detail.</span><span class="sxs-lookup"><span data-stu-id="f872b-124">The POST token response specifies the token expiration detail.</span></span> <span data-ttu-id="f872b-125">The expires_in property expresses the value in seconds.</span><span class="sxs-lookup"><span data-stu-id="f872b-125">The expires_in property expresses the value in seconds.</span></span> <span data-ttu-id="f872b-126">For example, the value "3600" denotes that the access token will expire in one hour from the time the response was generated.</span><span class="sxs-lookup"><span data-stu-id="f872b-126">For example, the value "3600" denotes that the access token will expire in one hour from the time the response was generated.</span></span> <span data-ttu-id="f872b-127">Partners may choose to cache the token until the token expiry time to avoid getting the token every time.</span><span class="sxs-lookup"><span data-stu-id="f872b-127">Partners may choose to cache the token until the token expiry time to avoid getting the token every time.</span></span>

## <a name="using-the-token"></a><span data-ttu-id="f872b-128">Using the Token</span><span class="sxs-lookup"><span data-stu-id="f872b-128">Using the Token</span></span>
<span data-ttu-id="f872b-129">You can now use the token while making the review API calls by sending the access_token in the header:</span><span class="sxs-lookup"><span data-stu-id="f872b-129">You can now use the token while making the review API calls by sending the access_token in the header:</span></span>

    Header name: authorization
    Header value: Bearer <Your access token>

## <a name="helpful-links"></a><span data-ttu-id="f872b-130">Helpful Links</span><span class="sxs-lookup"><span data-stu-id="f872b-130">Helpful Links</span></span>
[<span data-ttu-id="f872b-131">How to get an Azure AD security token</span><span class="sxs-lookup"><span data-stu-id="f872b-131">How to get an Azure AD security token</span></span>](https://msdn.microsoft.com/en-us/library/partnercenter/dn974935.aspx "How to get an Azure AD token")

