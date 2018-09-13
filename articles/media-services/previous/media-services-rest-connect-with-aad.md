---
title: Use Azure AD authentication to access Azure Media Services API with REST | Microsoft Docs
description: Learn how to access Azure Media Services API with Azure Active Directory authentication by using REST.
services: media-services
documentationcenter: ''
author: willzhan
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/26/2017
ms.author: willzhan;juliako;johndeu
ms.openlocfilehash: ed78d6c6d4c695b841dbfbf917cd1681adc44ee7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966365"
---
# <a name="use-azure-ad-authentication-to-access-the-azure-media-services-api-with-rest"></a><span data-ttu-id="74559-103">Use Azure AD authentication to access the Azure Media Services API with REST</span><span class="sxs-lookup"><span data-stu-id="74559-103">Use Azure AD authentication to access the Azure Media Services API with REST</span></span>

<span data-ttu-id="74559-104">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="74559-104">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="74559-105">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="74559-105">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="74559-106">The interactive application should first prompt the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="74559-106">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="74559-107">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span><span class="sxs-lookup"><span data-stu-id="74559-107">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="74559-108">**Service principal authentication** authenticates a service.</span><span class="sxs-lookup"><span data-stu-id="74559-108">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="74559-109">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span><span class="sxs-lookup"><span data-stu-id="74559-109">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

    <span data-ttu-id="74559-110">This tutorial shows you how to use Azure AD **service principal** authentication to access AMS API with REST.</span><span class="sxs-lookup"><span data-stu-id="74559-110">This tutorial shows you how to use Azure AD **service principal** authentication to access AMS API with REST.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="74559-111">**Service principal** is the recommended best practice for most applications connecting to Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="74559-111">**Service principal** is the recommended best practice for most applications connecting to Azure Media Services.</span></span> 

<span data-ttu-id="74559-112">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="74559-112">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74559-113">Get the authentication information from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="74559-113">Get the authentication information from the Azure portal</span></span>
> * <span data-ttu-id="74559-114">Get the access token using Postman</span><span class="sxs-lookup"><span data-stu-id="74559-114">Get the access token using Postman</span></span>
> * <span data-ttu-id="74559-115">Test the **Assets** API using the access token</span><span class="sxs-lookup"><span data-stu-id="74559-115">Test the **Assets** API using the access token</span></span>


> [!IMPORTANT]
> <span data-ttu-id="74559-116">Currently, Media Services supports the Azure Access Control services authentication model.</span><span class="sxs-lookup"><span data-stu-id="74559-116">Currently, Media Services supports the Azure Access Control services authentication model.</span></span> <span data-ttu-id="74559-117">However, Access Control authentication will be deprecated June 1, 2018.</span><span class="sxs-lookup"><span data-stu-id="74559-117">However, Access Control authentication will be deprecated June 1, 2018.</span></span> <span data-ttu-id="74559-118">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="74559-118">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74559-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74559-119">Prerequisites</span></span>

- <span data-ttu-id="74559-120">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="74559-120">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
- <span data-ttu-id="74559-121">[Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="74559-121">[Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="74559-122">Review the [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) article.</span><span class="sxs-lookup"><span data-stu-id="74559-122">Review the [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) article.</span></span>
- <span data-ttu-id="74559-123">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in this article.</span><span class="sxs-lookup"><span data-stu-id="74559-123">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in this article.</span></span> 

    <span data-ttu-id="74559-124">In this tutorial, we are uring **Postman** but any REST tool would be suitable.</span><span class="sxs-lookup"><span data-stu-id="74559-124">In this tutorial, we are uring **Postman** but any REST tool would be suitable.</span></span> <span data-ttu-id="74559-125">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span><span class="sxs-lookup"><span data-stu-id="74559-125">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span></span> 

## <a name="get-the-authentication-information-from-the-azure-portal"></a><span data-ttu-id="74559-126">Get the authentication information from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="74559-126">Get the authentication information from the Azure portal</span></span>

### <a name="overview"></a><span data-ttu-id="74559-127">Overview</span><span class="sxs-lookup"><span data-stu-id="74559-127">Overview</span></span>

<span data-ttu-id="74559-128">To access Media Services API, you need to collect the following data points.</span><span class="sxs-lookup"><span data-stu-id="74559-128">To access Media Services API, you need to collect the following data points.</span></span>

|<span data-ttu-id="74559-129">Setting</span><span class="sxs-lookup"><span data-stu-id="74559-129">Setting</span></span>|<span data-ttu-id="74559-130">Example</span><span class="sxs-lookup"><span data-stu-id="74559-130">Example</span></span>|<span data-ttu-id="74559-131">Description</span><span class="sxs-lookup"><span data-stu-id="74559-131">Description</span></span>|
|---|-------|-----|
|<span data-ttu-id="74559-132">Azure Active Directory tenant domain</span><span class="sxs-lookup"><span data-stu-id="74559-132">Azure Active Directory tenant domain</span></span>|<span data-ttu-id="74559-133">microsoft.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="74559-133">microsoft.onmicrosoft.com</span></span>|<span data-ttu-id="74559-134">Azure AD as a Secure Token Service (STS) endpoint is created using the following format: https://login.microsoftonline.com/{your-aad-tenant-name.onmicrosoft.com}/oauth2/token.</span><span class="sxs-lookup"><span data-stu-id="74559-134">Azure AD as a Secure Token Service (STS) endpoint is created using the following format: https://login.microsoftonline.com/{your-aad-tenant-name.onmicrosoft.com}/oauth2/token.</span></span> <span data-ttu-id="74559-135">Azure AD issues a JWT in order to access resources (an access token).</span><span class="sxs-lookup"><span data-stu-id="74559-135">Azure AD issues a JWT in order to access resources (an access token).</span></span>|
|<span data-ttu-id="74559-136">REST API endpoint</span><span class="sxs-lookup"><span data-stu-id="74559-136">REST API endpoint</span></span>|https://amshelloworld.restv2.westus.media.azure.net/api/|<span data-ttu-id="74559-137">This is the endpoint against which all Media Services REST API calls in your application are made.</span><span class="sxs-lookup"><span data-stu-id="74559-137">This is the endpoint against which all Media Services REST API calls in your application are made.</span></span>|
|<span data-ttu-id="74559-138">Client ID (Application ID)</span><span class="sxs-lookup"><span data-stu-id="74559-138">Client ID (Application ID)</span></span>|<span data-ttu-id="74559-139">f7fbbb29-a02d-4d91-bbc6-59a2579259d2</span><span class="sxs-lookup"><span data-stu-id="74559-139">f7fbbb29-a02d-4d91-bbc6-59a2579259d2</span></span>|<span data-ttu-id="74559-140">Azure AD application (client) ID.</span><span class="sxs-lookup"><span data-stu-id="74559-140">Azure AD application (client) ID.</span></span> <span data-ttu-id="74559-141">The client ID is required to get the access token.</span><span class="sxs-lookup"><span data-stu-id="74559-141">The client ID is required to get the access token.</span></span> |
|<span data-ttu-id="74559-142">Client Secret</span><span class="sxs-lookup"><span data-stu-id="74559-142">Client Secret</span></span>|<span data-ttu-id="74559-143">+mUERiNzVMoJGggD6aV1etzFGa1n6KeSlLjIq+Dbim0=</span><span class="sxs-lookup"><span data-stu-id="74559-143">+mUERiNzVMoJGggD6aV1etzFGa1n6KeSlLjIq+Dbim0=</span></span>|<span data-ttu-id="74559-144">Azure AD application keys (client secret).</span><span class="sxs-lookup"><span data-stu-id="74559-144">Azure AD application keys (client secret).</span></span> <span data-ttu-id="74559-145">The client secret is required to get the access token.</span><span class="sxs-lookup"><span data-stu-id="74559-145">The client secret is required to get the access token.</span></span>|

### <a name="get-aad-auth-info-from-the-azure-portal"></a><span data-ttu-id="74559-146">Get AAD auth info from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="74559-146">Get AAD auth info from the Azure portal</span></span>

<span data-ttu-id="74559-147">To get the information, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="74559-147">To get the information, follow these steps:</span></span>

1. <span data-ttu-id="74559-148">Log in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74559-148">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="74559-149">Navigate to your AMS instance.</span><span class="sxs-lookup"><span data-stu-id="74559-149">Navigate to your AMS instance.</span></span>
3. <span data-ttu-id="74559-150">Select **API access**.</span><span class="sxs-lookup"><span data-stu-id="74559-150">Select **API access**.</span></span>
4. <span data-ttu-id="74559-151">Click on **Connect to Azure Media Services API with service principal**.</span><span class="sxs-lookup"><span data-stu-id="74559-151">Click on **Connect to Azure Media Services API with service principal**.</span></span>

    ![API access](./media/connect-with-rest/connect-with-rest01.png)

5. <span data-ttu-id="74559-153">Select an existing **Azure AD application** or create a new one (shown below).</span><span class="sxs-lookup"><span data-stu-id="74559-153">Select an existing **Azure AD application** or create a new one (shown below).</span></span>

    > [!NOTE]
    > <span data-ttu-id="74559-154">For the Azure Media REST request to succeed, the calling user must have a **Contributor** or **Owner** role for the Media Services account it is trying to access.</span><span class="sxs-lookup"><span data-stu-id="74559-154">For the Azure Media REST request to succeed, the calling user must have a **Contributor** or **Owner** role for the Media Services account it is trying to access.</span></span> <span data-ttu-id="74559-155">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control).</span><span class="sxs-lookup"><span data-stu-id="74559-155">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control).</span></span>

    <span data-ttu-id="74559-156">If you need to create a new AD app, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="74559-156">If you need to create a new AD app, follow these steps:</span></span>
    
    1. <span data-ttu-id="74559-157">Press **Create New**.</span><span class="sxs-lookup"><span data-stu-id="74559-157">Press **Create New**.</span></span>
    2. <span data-ttu-id="74559-158">Enter a name.</span><span class="sxs-lookup"><span data-stu-id="74559-158">Enter a name.</span></span>
    3. <span data-ttu-id="74559-159">Press **Create New** again.</span><span class="sxs-lookup"><span data-stu-id="74559-159">Press **Create New** again.</span></span>
    4. <span data-ttu-id="74559-160">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="74559-160">Press **Save**.</span></span>

    ![API access](./media/connect-with-rest/new-app.png)

    <span data-ttu-id="74559-162">The new app shows up on the page.</span><span class="sxs-lookup"><span data-stu-id="74559-162">The new app shows up on the page.</span></span>

6. <span data-ttu-id="74559-163">Get the **Client ID** (Application ID).</span><span class="sxs-lookup"><span data-stu-id="74559-163">Get the **Client ID** (Application ID).</span></span>
    
    1. <span data-ttu-id="74559-164">Select the application.</span><span class="sxs-lookup"><span data-stu-id="74559-164">Select the application.</span></span>
    2. <span data-ttu-id="74559-165">Get the **Client ID** from the window on the right.</span><span class="sxs-lookup"><span data-stu-id="74559-165">Get the **Client ID** from the window on the right.</span></span> 

    ![API access](./media/connect-with-rest/existing-client-id.png)<span data-ttu-id="74559-167">.</span><span class="sxs-lookup"><span data-stu-id="74559-167">.</span></span>

7.  <span data-ttu-id="74559-168">Get the application's **Key** (client secret).</span><span class="sxs-lookup"><span data-stu-id="74559-168">Get the application's **Key** (client secret).</span></span> 

    1. <span data-ttu-id="74559-169">Click the **Manage application** button (notice that the Client ID info is under **Application ID**).</span><span class="sxs-lookup"><span data-stu-id="74559-169">Click the **Manage application** button (notice that the Client ID info is under **Application ID**).</span></span> 
    2. <span data-ttu-id="74559-170">Press **Keys**.</span><span class="sxs-lookup"><span data-stu-id="74559-170">Press **Keys**.</span></span>
    
        ![API access](./media/connect-with-rest/manage-app.png)
    3. <span data-ttu-id="74559-172">Generate the app key (client secret) by filling in **DESCRIPTION** and **EXPIRES** and pressing **Save**.</span><span class="sxs-lookup"><span data-stu-id="74559-172">Generate the app key (client secret) by filling in **DESCRIPTION** and **EXPIRES** and pressing **Save**.</span></span>
    
        <span data-ttu-id="74559-173">Once the **Save** button is pressed, the key value appears.</span><span class="sxs-lookup"><span data-stu-id="74559-173">Once the **Save** button is pressed, the key value appears.</span></span> <span data-ttu-id="74559-174">Copy the key value before leaving the blade.</span><span class="sxs-lookup"><span data-stu-id="74559-174">Copy the key value before leaving the blade.</span></span>

    ![API access](./media/connect-with-rest/connect-with-rest03.png)

<span data-ttu-id="74559-176">You can add values for AD connection parameters to your web.config or app.config file, to later use in your code.</span><span class="sxs-lookup"><span data-stu-id="74559-176">You can add values for AD connection parameters to your web.config or app.config file, to later use in your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74559-177">The **Client key** is an important secret and should be properly secured in a key vault or encrypted in production.</span><span class="sxs-lookup"><span data-stu-id="74559-177">The **Client key** is an important secret and should be properly secured in a key vault or encrypted in production.</span></span>

## <a name="get-the-access-token-using-postman"></a><span data-ttu-id="74559-178">Get the access token using Postman</span><span class="sxs-lookup"><span data-stu-id="74559-178">Get the access token using Postman</span></span>

<span data-ttu-id="74559-179">This section shows how to use **Postman** to execute a REST API that returns a JWT Bearer Token (access token).</span><span class="sxs-lookup"><span data-stu-id="74559-179">This section shows how to use **Postman** to execute a REST API that returns a JWT Bearer Token (access token).</span></span> <span data-ttu-id="74559-180">To call any Media Services REST API, you need to add the "Authorization" header to the calls, and add the value of "Bearer *your_access_token*" to each call (as shown in the next section of this tutorial).</span><span class="sxs-lookup"><span data-stu-id="74559-180">To call any Media Services REST API, you need to add the "Authorization" header to the calls, and add the value of "Bearer *your_access_token*" to each call (as shown in the next section of this tutorial).</span></span> 

1. <span data-ttu-id="74559-181">Open **Postman**.</span><span class="sxs-lookup"><span data-stu-id="74559-181">Open **Postman**.</span></span>
2. <span data-ttu-id="74559-182">Select **POST**.</span><span class="sxs-lookup"><span data-stu-id="74559-182">Select **POST**.</span></span>
3. <span data-ttu-id="74559-183">Enter the URL that includes your tenant name using the following format: the tenant name should end with **.onmicrosoft.com** and the URL should end with **oauth2/token**:</span><span class="sxs-lookup"><span data-stu-id="74559-183">Enter the URL that includes your tenant name using the following format: the tenant name should end with **.onmicrosoft.com** and the URL should end with **oauth2/token**:</span></span> 

    https://login.microsoftonline.com/{your-aad-tenant-name.onmicrosoft.com}/oauth2/token

4. <span data-ttu-id="74559-184">Select the **Headers** tab.</span><span class="sxs-lookup"><span data-stu-id="74559-184">Select the **Headers** tab.</span></span>
5. <span data-ttu-id="74559-185">Enter the **Headers** information using the "Key/Value" data grid.</span><span class="sxs-lookup"><span data-stu-id="74559-185">Enter the **Headers** information using the "Key/Value" data grid.</span></span> 

    ![Data Grid](./media/connect-with-rest/headers-data-grid.png)

    <span data-ttu-id="74559-187">Alternatively, click **Bulk Edit** link on the right of the Postman window and paste the following code.</span><span class="sxs-lookup"><span data-stu-id="74559-187">Alternatively, click **Bulk Edit** link on the right of the Postman window and paste the following code.</span></span>

        Content-Type:application/x-www-form-urlencoded
        Keep-Alive:true

6. <span data-ttu-id="74559-188">Press the **Body** tab.</span><span class="sxs-lookup"><span data-stu-id="74559-188">Press the **Body** tab.</span></span>
7. <span data-ttu-id="74559-189">Enter the body information using the "Key/Value" data grid (replace the client ID and secret values).</span><span class="sxs-lookup"><span data-stu-id="74559-189">Enter the body information using the "Key/Value" data grid (replace the client ID and secret values).</span></span> 

    ![Data Grid](./media/connect-with-rest/data-grid.png)

    <span data-ttu-id="74559-191">Alternatively, click **Bulk Edit** on the right of the Postman window and paste the following body (replace the client ID and secret values):</span><span class="sxs-lookup"><span data-stu-id="74559-191">Alternatively, click **Bulk Edit** on the right of the Postman window and paste the following body (replace the client ID and secret values):</span></span>

        grant_type:client_credentials
        client_id:{Your Client ID that you got from your AAD Application}
        client_secret:{Your client secret that you got from your AAD Application's Keys}
        resource:https://rest.media.azure.net

8. <span data-ttu-id="74559-192">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="74559-192">Press **Send**.</span></span>

    ![get token](./media/connect-with-rest/connect-with-rest04.png)

<span data-ttu-id="74559-194">The returned response contains the **access token** that you need to use to access any AMS APIs.</span><span class="sxs-lookup"><span data-stu-id="74559-194">The returned response contains the **access token** that you need to use to access any AMS APIs.</span></span>

## <a name="test-the-assets-api-using-the-access-token"></a><span data-ttu-id="74559-195">Test the **Assets** API using the access token</span><span class="sxs-lookup"><span data-stu-id="74559-195">Test the **Assets** API using the access token</span></span>

<span data-ttu-id="74559-196">This section shows how to access the **Assets** API using **Postman**.</span><span class="sxs-lookup"><span data-stu-id="74559-196">This section shows how to access the **Assets** API using **Postman**.</span></span>

1. <span data-ttu-id="74559-197">Open **Postman**.</span><span class="sxs-lookup"><span data-stu-id="74559-197">Open **Postman**.</span></span>
2. <span data-ttu-id="74559-198">Select **GET**.</span><span class="sxs-lookup"><span data-stu-id="74559-198">Select **GET**.</span></span>
3. <span data-ttu-id="74559-199">Paste the REST API endpoint (for example, https://amshelloworld.restv2.westus.media.azure.net/api/Assets)</span><span class="sxs-lookup"><span data-stu-id="74559-199">Paste the REST API endpoint (for example, https://amshelloworld.restv2.westus.media.azure.net/api/Assets)</span></span>
4. <span data-ttu-id="74559-200">Select the **Authorization** tab.</span><span class="sxs-lookup"><span data-stu-id="74559-200">Select the **Authorization** tab.</span></span> 
5. <span data-ttu-id="74559-201">Select **Bearer Token**.</span><span class="sxs-lookup"><span data-stu-id="74559-201">Select **Bearer Token**.</span></span>
6. <span data-ttu-id="74559-202">Paste the token that was created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="74559-202">Paste the token that was created in the previous section.</span></span>

    ![get token](./media/connect-with-rest/connect-with-rest05.png)

    > [!NOTE]
    > <span data-ttu-id="74559-204">The Postman UX could be different between a Mac and PC.</span><span class="sxs-lookup"><span data-stu-id="74559-204">The Postman UX could be different between a Mac and PC.</span></span> <span data-ttu-id="74559-205">If the Mac version does not have the "Bearer Token" option in the **Authentication** section dropdown, you should add the **Authorization** header manually on the Mac client.</span><span class="sxs-lookup"><span data-stu-id="74559-205">If the Mac version does not have the "Bearer Token" option in the **Authentication** section dropdown, you should add the **Authorization** header manually on the Mac client.</span></span>

   ![Auth header](./media/connect-with-rest/auth-header.png)

7. <span data-ttu-id="74559-207">Select **Headers**.</span><span class="sxs-lookup"><span data-stu-id="74559-207">Select **Headers**.</span></span>
5. <span data-ttu-id="74559-208">Click **Bulk Edit** link on the right the Postman window.</span><span class="sxs-lookup"><span data-stu-id="74559-208">Click **Bulk Edit** link on the right the Postman window.</span></span>
6. <span data-ttu-id="74559-209">Paste the following headers:</span><span class="sxs-lookup"><span data-stu-id="74559-209">Paste the following headers:</span></span>

        x-ms-version:2.15
        Accept:application/json
        Content-Type:application/json
        DataServiceVersion:3.0
        MaxDataServiceVersion:3.0

7. <span data-ttu-id="74559-210">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="74559-210">Press **Send**.</span></span>

<span data-ttu-id="74559-211">The returned response contains the assets that are in your account.</span><span class="sxs-lookup"><span data-stu-id="74559-211">The returned response contains the assets that are in your account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74559-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="74559-212">Next steps</span></span>

* <span data-ttu-id="74559-213">Try this sample code in [Azure AD Authentication for Azure Media Services Access: Both via REST API](https://github.com/willzhan/WAMSRESTSoln)</span><span class="sxs-lookup"><span data-stu-id="74559-213">Try this sample code in [Azure AD Authentication for Azure Media Services Access: Both via REST API](https://github.com/willzhan/WAMSRESTSoln)</span></span>
* [<span data-ttu-id="74559-214">Upload files with .NET</span><span class="sxs-lookup"><span data-stu-id="74559-214">Upload files with .NET</span></span>](media-services-dotnet-upload-files.md)
