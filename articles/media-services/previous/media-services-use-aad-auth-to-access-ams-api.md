---
title: Access Azure Media Services API with Azure Active Directory authentication | Microsoft Docs
description: Learn about concepts and steps to take to use Azure Active Directory (Azure AD) to authenticate access to the Azure Media Services API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 08b7f50c3051c174158cff0b4c591a2b22fb4ab4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870134"
---
# <a name="access-the-azure-media-services-api-with-azure-ad-authentication"></a><span data-ttu-id="7cbe2-103">Access the Azure Media Services API with Azure AD authentication</span><span class="sxs-lookup"><span data-stu-id="7cbe2-103">Access the Azure Media Services API with Azure AD authentication</span></span>
 
<span data-ttu-id="7cbe2-104">The Azure Media Services API is a RESTful API.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-104">The Azure Media Services API is a RESTful API.</span></span> <span data-ttu-id="7cbe2-105">You can use it to perform operations on media resources by using a REST API or by using available client SDKs.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-105">You can use it to perform operations on media resources by using a REST API or by using available client SDKs.</span></span> <span data-ttu-id="7cbe2-106">Azure Media Services offers a Media Services client SDK for Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-106">Azure Media Services offers a Media Services client SDK for Microsoft .NET.</span></span> <span data-ttu-id="7cbe2-107">To be authorized to access Media Services resources and the Media Services API, you must first be authenticated.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-107">To be authorized to access Media Services resources and the Media Services API, you must first be authenticated.</span></span> 

<span data-ttu-id="7cbe2-108">Media Services supports [Azure Active Directory (Azure AD)-based authentication](../../active-directory/fundamentals/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-108">Media Services supports [Azure Active Directory (Azure AD)-based authentication](../../active-directory/fundamentals/active-directory-whatis.md).</span></span> <span data-ttu-id="7cbe2-109">The Azure Media REST service requires that the user or application that makes the REST API requests have either the **Contributor** or **Owner** role to access the resources.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-109">The Azure Media REST service requires that the user or application that makes the REST API requests have either the **Contributor** or **Owner** role to access the resources.</span></span> <span data-ttu-id="7cbe2-110">For more information, see [Get started with Role-Based Access Control in the Azure portal](../../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-110">For more information, see [Get started with Role-Based Access Control in the Azure portal](../../role-based-access-control/overview.md).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="7cbe2-111">Currently, Media Services supports the Azure Access Control service authentication model.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-111">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="7cbe2-112">However, Access Control authorization will be deprecated on June 1, 2018.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-112">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="7cbe2-113">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-113">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

<span data-ttu-id="7cbe2-114">This document gives an overview of how to access the Media Services API by using REST or .NET APIs.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-114">This document gives an overview of how to access the Media Services API by using REST or .NET APIs.</span></span>

## <a name="access-control"></a><span data-ttu-id="7cbe2-115">Access control</span><span class="sxs-lookup"><span data-stu-id="7cbe2-115">Access control</span></span>

<span data-ttu-id="7cbe2-116">For the Azure Media REST request to succeed, the calling user must have a Contributor or Owner role for the Media Services account it is trying to access.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-116">For the Azure Media REST request to succeed, the calling user must have a Contributor or Owner role for the Media Services account it is trying to access.</span></span>  
<span data-ttu-id="7cbe2-117">Only a user with the Owner role can give media resource (account) access to new users or apps.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-117">Only a user with the Owner role can give media resource (account) access to new users or apps.</span></span> <span data-ttu-id="7cbe2-118">The Contributor role can access only the media resource.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-118">The Contributor role can access only the media resource.</span></span>
<span data-ttu-id="7cbe2-119">Unauthorized requests fail, with status code of 401.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-119">Unauthorized requests fail, with status code of 401.</span></span> <span data-ttu-id="7cbe2-120">If you see this error code, check whether your user has the Contributor or Owner role assigned for the user's Media Services account.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-120">If you see this error code, check whether your user has the Contributor or Owner role assigned for the user's Media Services account.</span></span> <span data-ttu-id="7cbe2-121">You can check this in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-121">You can check this in the Azure portal.</span></span> <span data-ttu-id="7cbe2-122">Search for your media account, and then click the **Access control** tab.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-122">Search for your media account, and then click the **Access control** tab.</span></span> 

![Access control tab](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a><span data-ttu-id="7cbe2-124">Types of authentication</span><span class="sxs-lookup"><span data-stu-id="7cbe2-124">Types of authentication</span></span> 
 
<span data-ttu-id="7cbe2-125">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-125">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="7cbe2-126">**User authentication**.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-126">**User authentication**.</span></span> <span data-ttu-id="7cbe2-127">Authenticate a person who is using the app to interact with Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-127">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="7cbe2-128">The interactive application should first prompt the user for the user's credentials.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-128">The interactive application should first prompt the user for the user's credentials.</span></span> <span data-ttu-id="7cbe2-129">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-129">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="7cbe2-130">**Service principal authentication**.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-130">**Service principal authentication**.</span></span> <span data-ttu-id="7cbe2-131">Authenticate a service.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-131">Authenticate a service.</span></span> <span data-ttu-id="7cbe2-132">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-132">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs.</span></span> <span data-ttu-id="7cbe2-133">Examples are web apps, function apps, logic apps, API, and microservices.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-133">Examples are web apps, function apps, logic apps, API, and microservices.</span></span>

### <a name="user-authentication"></a><span data-ttu-id="7cbe2-134">User authentication</span><span class="sxs-lookup"><span data-stu-id="7cbe2-134">User authentication</span></span> 

<span data-ttu-id="7cbe2-135">Applications that should use the user authentication method are management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-135">Applications that should use the user authentication method are management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="7cbe2-136">This type of solution is useful when you want human interaction with the service in one of the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-136">This type of solution is useful when you want human interaction with the service in one of the following scenarios:</span></span>

- <span data-ttu-id="7cbe2-137">Monitoring dashboard for your encoding jobs.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-137">Monitoring dashboard for your encoding jobs.</span></span>
- <span data-ttu-id="7cbe2-138">Monitoring dashboard for your live streams.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-138">Monitoring dashboard for your live streams.</span></span>
- <span data-ttu-id="7cbe2-139">Management application for desktop or mobile users to administer resources in a Media Services account.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-139">Management application for desktop or mobile users to administer resources in a Media Services account.</span></span>

> [!NOTE]
> <span data-ttu-id="7cbe2-140">This authentication method should not be used for consumer-facing applications.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-140">This authentication method should not be used for consumer-facing applications.</span></span> 

<span data-ttu-id="7cbe2-141">A native application must first acquire an access token from Azure AD, and then use it when you make HTTP requests to the Media Services REST API.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-141">A native application must first acquire an access token from Azure AD, and then use it when you make HTTP requests to the Media Services REST API.</span></span> <span data-ttu-id="7cbe2-142">Add the access token to the request header.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-142">Add the access token to the request header.</span></span> 

<span data-ttu-id="7cbe2-143">The following diagram shows a typical interactive application authentication flow:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-143">The following diagram shows a typical interactive application authentication flow:</span></span> 

![Native apps diagram](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

<span data-ttu-id="7cbe2-145">In the preceding diagram, the numbers represent the flow of the requests in chronological order.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-145">In the preceding diagram, the numbers represent the flow of the requests in chronological order.</span></span>

> [!NOTE]
> <span data-ttu-id="7cbe2-146">When you use the user authentication method, all apps share the same (default) native application client ID and native application redirect URI.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-146">When you use the user authentication method, all apps share the same (default) native application client ID and native application redirect URI.</span></span> 

1. <span data-ttu-id="7cbe2-147">Prompt a user for credentials.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-147">Prompt a user for credentials.</span></span>
2. <span data-ttu-id="7cbe2-148">Request an Azure AD access token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-148">Request an Azure AD access token with the following parameters:</span></span>  

    * <span data-ttu-id="7cbe2-149">Azure AD tenant endpoint.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-149">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="7cbe2-150">The tenant information can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-150">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="7cbe2-151">Place your cursor over the name of the signed-in user in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-151">Place your cursor over the name of the signed-in user in the top right corner.</span></span>
    * <span data-ttu-id="7cbe2-152">Media Services resource URI.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-152">Media Services resource URI.</span></span> 

        <span data-ttu-id="7cbe2-153">This URI is the same for Media Services accounts that are in the same Azure environment (for example, https://rest.media.azure.net).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-153">This URI is the same for Media Services accounts that are in the same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="7cbe2-154">Media Services (native) application client ID.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-154">Media Services (native) application client ID.</span></span>
    * <span data-ttu-id="7cbe2-155">Media Services (native) application redirect URI.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-155">Media Services (native) application redirect URI.</span></span>
    * <span data-ttu-id="7cbe2-156">Resource URI for REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-156">Resource URI for REST Media Services.</span></span>
        
        <span data-ttu-id="7cbe2-157">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-157">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    <span data-ttu-id="7cbe2-158">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) using the user authentication option.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-158">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) using the user authentication option.</span></span>

3. <span data-ttu-id="7cbe2-159">The Azure AD access token is sent to the client.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-159">The Azure AD access token is sent to the client.</span></span>
4. <span data-ttu-id="7cbe2-160">The client sends a request to the Azure Media REST API with the Azure AD access token.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-160">The client sends a request to the Azure Media REST API with the Azure AD access token.</span></span>
5. <span data-ttu-id="7cbe2-161">The client gets back the data from Media Services.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-161">The client gets back the data from Media Services.</span></span>

<span data-ttu-id="7cbe2-162">For information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access the Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-162">For information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access the Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="7cbe2-163">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD access token request by using the parameters described in step 2.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-163">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD access token request by using the parameters described in step 2.</span></span> <span data-ttu-id="7cbe2-164">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-164">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="service-principal-authentication"></a><span data-ttu-id="7cbe2-165">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="7cbe2-165">Service principal authentication</span></span>

<span data-ttu-id="7cbe2-166">Applications that commonly use this authentication method are apps that run middle-tier services and scheduled jobs: web apps, function apps, logic apps, APIs, and microservices.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-166">Applications that commonly use this authentication method are apps that run middle-tier services and scheduled jobs: web apps, function apps, logic apps, APIs, and microservices.</span></span> <span data-ttu-id="7cbe2-167">This authentication method also is suitable for interactive applications in which you might want to use a service account to manage resources.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-167">This authentication method also is suitable for interactive applications in which you might want to use a service account to manage resources.</span></span>

<span data-ttu-id="7cbe2-168">When you use the service principal authentication method to build consumer scenarios, authentication typically is handled in the middle tier (through some API) and not directly in a mobile or desktop application.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-168">When you use the service principal authentication method to build consumer scenarios, authentication typically is handled in the middle tier (through some API) and not directly in a mobile or desktop application.</span></span> 

<span data-ttu-id="7cbe2-169">To use this method, create an Azure AD application and service principal in its own tenant.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-169">To use this method, create an Azure AD application and service principal in its own tenant.</span></span> <span data-ttu-id="7cbe2-170">After you create the application, give the app Contributor or Owner role access to the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-170">After you create the application, give the app Contributor or Owner role access to the Media Services account.</span></span> <span data-ttu-id="7cbe2-171">You can do this in the Azure portal, by using the Azure CLI, or with a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-171">You can do this in the Azure portal, by using the Azure CLI, or with a PowerShell script.</span></span> <span data-ttu-id="7cbe2-172">You also can use an existing Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-172">You also can use an existing Azure AD application.</span></span> <span data-ttu-id="7cbe2-173">You can register and manage your Azure AD app and service principal [in the Azure portal](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-173">You can register and manage your Azure AD app and service principal [in the Azure portal](media-services-portal-get-started-with-aad.md).</span></span> <span data-ttu-id="7cbe2-174">You also can do this by using [Azure CLI](media-services-use-aad-auth-to-access-ams-api.md) or [PowerShell](media-services-powershell-create-and-configure-aad-app.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-174">You also can do this by using [Azure CLI](media-services-use-aad-auth-to-access-ams-api.md) or [PowerShell](media-services-powershell-create-and-configure-aad-app.md).</span></span> 

![Middle-tier apps](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

<span data-ttu-id="7cbe2-176">After you create your Azure AD application, you get values for the following settings.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-176">After you create your Azure AD application, you get values for the following settings.</span></span> <span data-ttu-id="7cbe2-177">You need these values for authentication:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-177">You need these values for authentication:</span></span>

- <span data-ttu-id="7cbe2-178">Client ID</span><span class="sxs-lookup"><span data-stu-id="7cbe2-178">Client ID</span></span> 
- <span data-ttu-id="7cbe2-179">Client secret</span><span class="sxs-lookup"><span data-stu-id="7cbe2-179">Client secret</span></span> 

<span data-ttu-id="7cbe2-180">In the preceding figure, the numbers represent the flow of the requests in chronological order:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-180">In the preceding figure, the numbers represent the flow of the requests in chronological order:</span></span>
    
1. <span data-ttu-id="7cbe2-181">A middle-tier app (web API or web application) requests an Azure AD access token that has the following parameters:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-181">A middle-tier app (web API or web application) requests an Azure AD access token that has the following parameters:</span></span>  

    * <span data-ttu-id="7cbe2-182">Azure AD tenant endpoint.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-182">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="7cbe2-183">The tenant information can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-183">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="7cbe2-184">Place your cursor over the name of the signed-in user in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-184">Place your cursor over the name of the signed-in user in the top right corner.</span></span>
    * <span data-ttu-id="7cbe2-185">Media Services resource URI.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-185">Media Services resource URI.</span></span> 

        <span data-ttu-id="7cbe2-186">This URI is the same for Media Services accounts that are located in the same Azure environment (for example, https://rest.media.azure.net).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-186">This URI is the same for Media Services accounts that are located in the same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="7cbe2-187">Resource URI for REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-187">Resource URI for REST Media Services.</span></span>

        <span data-ttu-id="7cbe2-188">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-188">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    * <span data-ttu-id="7cbe2-189">Azure AD application values: the client ID and client secret.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-189">Azure AD application values: the client ID and client secret.</span></span>
    
    <span data-ttu-id="7cbe2-190">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) by using the service principal authentication option.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-190">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) by using the service principal authentication option.</span></span>

2. <span data-ttu-id="7cbe2-191">The Azure AD access token is sent to the middle tier.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-191">The Azure AD access token is sent to the middle tier.</span></span>
4. <span data-ttu-id="7cbe2-192">The middle tier sends request to the Azure Media REST API with the Azure AD token.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-192">The middle tier sends request to the Azure Media REST API with the Azure AD token.</span></span>
5. <span data-ttu-id="7cbe2-193">The middle tier gets back the data from Media Services.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-193">The middle tier gets back the data from Media Services.</span></span>

<span data-ttu-id="7cbe2-194">For more information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-194">For more information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="7cbe2-195">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using parameters described in step 1.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-195">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using parameters described in step 1.</span></span> <span data-ttu-id="7cbe2-196">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-196">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7cbe2-197">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="7cbe2-197">Troubleshooting</span></span>

<span data-ttu-id="7cbe2-198">Exception: "The remote server returned an error: (401) Unauthorized."</span><span class="sxs-lookup"><span data-stu-id="7cbe2-198">Exception: "The remote server returned an error: (401) Unauthorized."</span></span>

<span data-ttu-id="7cbe2-199">Solution: For the Media Services REST request to succeed, the calling user must be a Contributor or Owner role in the Media Services account it is trying to access.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-199">Solution: For the Media Services REST request to succeed, the calling user must be a Contributor or Owner role in the Media Services account it is trying to access.</span></span> <span data-ttu-id="7cbe2-200">For more information, see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.</span><span class="sxs-lookup"><span data-stu-id="7cbe2-200">For more information, see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.</span></span>

## <a name="resources"></a><span data-ttu-id="7cbe2-201">Resources</span><span class="sxs-lookup"><span data-stu-id="7cbe2-201">Resources</span></span>

<span data-ttu-id="7cbe2-202">The following articles are overviews of Azure AD authentication concepts:</span><span class="sxs-lookup"><span data-stu-id="7cbe2-202">The following articles are overviews of Azure AD authentication concepts:</span></span> 

- [<span data-ttu-id="7cbe2-203">Authentication scenarios addressed by Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cbe2-203">Authentication scenarios addressed by Azure AD</span></span>](../../active-directory/develop/authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [<span data-ttu-id="7cbe2-204">Add, update, or remove an application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cbe2-204">Add, update, or remove an application in Azure AD</span></span>](../../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md)
- [<span data-ttu-id="7cbe2-205">Configure and manage Role-Based Access Control by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cbe2-205">Configure and manage Role-Based Access Control by using PowerShell</span></span>](../../role-based-access-control/role-assignments-powershell.md)

## <a name="next-steps"></a><span data-ttu-id="7cbe2-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="7cbe2-206">Next steps</span></span>

* <span data-ttu-id="7cbe2-207">Use the Azure portal to [access Azure AD authentication to consume Azure Media Services API](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-207">Use the Azure portal to [access Azure AD authentication to consume Azure Media Services API](media-services-portal-get-started-with-aad.md).</span></span>
* <span data-ttu-id="7cbe2-208">Use Azure AD authentication to [access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7cbe2-208">Use Azure AD authentication to [access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

