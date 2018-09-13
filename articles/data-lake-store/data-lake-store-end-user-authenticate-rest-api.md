---
title: 'End-user authentication: REST API with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory using REST API
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 7b339c989a21abff34b885a8cba219aba701ca79
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864967"
---
# <a name="end-user-authentication-with-data-lake-store-using-rest-api"></a><span data-ttu-id="ef63e-103">End-user authentication with Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="ef63e-103">End-user authentication with Data Lake Store using REST API</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-end-user-authenticate-python.md)
> * [Using REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
>  

<span data-ttu-id="ef63e-108">In this article, you learn about how to use the REST API to do end-user authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ef63e-108">In this article, you learn about how to use the REST API to do end-user authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="ef63e-109">For service-to-service authentication with Data Lake Store using REST API, see [Service-to-service authentication with Data Lake Store using REST API](data-lake-store-service-to-service-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="ef63e-109">For service-to-service authentication with Data Lake Store using REST API, see [Service-to-service authentication with Data Lake Store using REST API](data-lake-store-service-to-service-authenticate-rest-api.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef63e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ef63e-110">Prerequisites</span></span>

* <span data-ttu-id="ef63e-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="ef63e-111">**An Azure subscription**.</span></span> <span data-ttu-id="ef63e-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef63e-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ef63e-113">**Create an Azure Active Directory "Native" Application**.</span><span class="sxs-lookup"><span data-stu-id="ef63e-113">**Create an Azure Active Directory "Native" Application**.</span></span> <span data-ttu-id="ef63e-114">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ef63e-114">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

* <span data-ttu-id="ef63e-115">**[cURL](http://curl.haxx.se/)**.</span><span class="sxs-lookup"><span data-stu-id="ef63e-115">**[cURL](http://curl.haxx.se/)**.</span></span> <span data-ttu-id="ef63e-116">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="ef63e-116">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="end-user-authentication"></a><span data-ttu-id="ef63e-117">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="ef63e-117">End-user authentication</span></span>
<span data-ttu-id="ef63e-118">End-user authentication is the recommended approach if you want a user to log in to your application using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef63e-118">End-user authentication is the recommended approach if you want a user to log in to your application using Azure AD.</span></span> <span data-ttu-id="ef63e-119">Your application is able to access Azure resources with the same level of access as the logged-in user.</span><span class="sxs-lookup"><span data-stu-id="ef63e-119">Your application is able to access Azure resources with the same level of access as the logged-in user.</span></span> <span data-ttu-id="ef63e-120">The user needs to provide their credentials periodically in order for your application to maintain access.</span><span class="sxs-lookup"><span data-stu-id="ef63e-120">The user needs to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="ef63e-121">The result of having the end-user login is that your application is given an access token and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="ef63e-121">The result of having the end-user login is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="ef63e-122">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span><span class="sxs-lookup"><span data-stu-id="ef63e-122">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="ef63e-123">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span><span class="sxs-lookup"><span data-stu-id="ef63e-123">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="ef63e-124">You can use two different approaches for end-user login.</span><span class="sxs-lookup"><span data-stu-id="ef63e-124">You can use two different approaches for end-user login.</span></span>

<span data-ttu-id="ef63e-125">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span><span class="sxs-lookup"><span data-stu-id="ef63e-125">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="ef63e-126">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ef63e-126">Perform the following steps:</span></span>

1. <span data-ttu-id="ef63e-127">Through your application, redirect the user to the following URL:</span><span class="sxs-lookup"><span data-stu-id="ef63e-127">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<REDIRECT-URI> needs to be encoded for use in a URL. So, for https://localhost, use `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    <span data-ttu-id="ef63e-130">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="ef63e-130">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="ef63e-131">You will be redirected to authenticate using your Azure login.</span><span class="sxs-lookup"><span data-stu-id="ef63e-131">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="ef63e-132">Once you successfully log in, the response is displayed in the browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="ef63e-132">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="ef63e-133">The response will be in the following format:</span><span class="sxs-lookup"><span data-stu-id="ef63e-133">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>

2. <span data-ttu-id="ef63e-134">Capture the authorization code from the response.</span><span class="sxs-lookup"><span data-stu-id="ef63e-134">Capture the authorization code from the response.</span></span> <span data-ttu-id="ef63e-135">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="ef63e-135">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown in the following snippet:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > In this case, the \<REDIRECT-URI> need not be encoded.
   > 
   > 

3. <span data-ttu-id="ef63e-137">The response is a JSON object that contains an access token (for example, `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (for example, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="ef63e-137">The response is a JSON object that contains an access token (for example, `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (for example, `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="ef63e-138">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span><span class="sxs-lookup"><span data-stu-id="ef63e-138">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}

4. <span data-ttu-id="ef63e-139">When the access token expires, you can request a new access token using the refresh token, as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="ef63e-139">When the access token expires, you can request a new access token using the refresh token, as shown in the following snippet:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="ef63e-140">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef63e-140">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="ef63e-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef63e-141">Next steps</span></span>
<span data-ttu-id="ef63e-142">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using REST API.</span><span class="sxs-lookup"><span data-stu-id="ef63e-142">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using REST API.</span></span> <span data-ttu-id="ef63e-143">You can now look at the following articles that talk about how to use the REST API to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ef63e-143">You can now look at the following articles that talk about how to use the REST API to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="ef63e-144">Account management operations on Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="ef63e-144">Account management operations on Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="ef63e-145">Data operations on Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="ef63e-145">Data operations on Data Lake Store using REST API</span></span>](data-lake-store-data-operations-rest-api.md)

