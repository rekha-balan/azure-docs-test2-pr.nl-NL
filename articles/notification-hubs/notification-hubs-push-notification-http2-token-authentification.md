---
title: Token-based (HTTP/2) Authentication for APNS in Azure Notification Hubs | Microsoft Docs
description: This topic explains how to leverage the new token authentication for APNS
services: notification-hubs
documentationcenter: .net
author: dimazaid
manager: kpiteira
editor: spelluru
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: ca86130e9c184576fc44119190d6224a363c6561
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867007"
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="0dc56-103">Token-based (HTTP/2) Authentication for APNS</span><span class="sxs-lookup"><span data-stu-id="0dc56-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="0dc56-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0dc56-104">Overview</span></span>
<span data-ttu-id="0dc56-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span><span class="sxs-lookup"><span data-stu-id="0dc56-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="0dc56-106">The key benefits of using the new protocol include:</span><span class="sxs-lookup"><span data-stu-id="0dc56-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="0dc56-107">Token generation is relatively hassle free (compared to certificates)</span><span class="sxs-lookup"><span data-stu-id="0dc56-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="0dc56-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span><span class="sxs-lookup"><span data-stu-id="0dc56-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="0dc56-109">Payloads can now be up to 4 KB</span><span class="sxs-lookup"><span data-stu-id="0dc56-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="0dc56-110">Synchronous feedback</span><span class="sxs-lookup"><span data-stu-id="0dc56-110">Synchronous feedback</span></span>
-   <span data-ttu-id="0dc56-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span><span class="sxs-lookup"><span data-stu-id="0dc56-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="0dc56-112">Using this new mechanism can be done in two steps in a few minutes:</span><span class="sxs-lookup"><span data-stu-id="0dc56-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="0dc56-113">Obtain the necessary information from the Apple Developer Account portal</span><span class="sxs-lookup"><span data-stu-id="0dc56-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="0dc56-114">Configure your notification hub with the new information</span><span class="sxs-lookup"><span data-stu-id="0dc56-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="0dc56-115">Notification Hubs is now all set to use the new authentication system with APNS.</span><span class="sxs-lookup"><span data-stu-id="0dc56-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="0dc56-116">Note that if you migrated from using certificate credentials for APNS:</span><span class="sxs-lookup"><span data-stu-id="0dc56-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="0dc56-117">the token properties overwrite your certificate in our system,</span><span class="sxs-lookup"><span data-stu-id="0dc56-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="0dc56-118">but your application continues to receive notifications seamlessly.</span><span class="sxs-lookup"><span data-stu-id="0dc56-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="0dc56-119">Obtaining authentication information from Apple</span><span class="sxs-lookup"><span data-stu-id="0dc56-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="0dc56-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span><span class="sxs-lookup"><span data-stu-id="0dc56-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="0dc56-121">Key Identifier</span><span class="sxs-lookup"><span data-stu-id="0dc56-121">Key Identifier</span></span>
<span data-ttu-id="0dc56-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span><span class="sxs-lookup"><span data-stu-id="0dc56-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="0dc56-123">Application Identifier & Application Name</span><span class="sxs-lookup"><span data-stu-id="0dc56-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="0dc56-124">The application name is available via the App IDs page in the Developer Account.</span><span class="sxs-lookup"><span data-stu-id="0dc56-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="0dc56-125">The application identifier is available via the membership details page in the Developer Account.</span><span class="sxs-lookup"><span data-stu-id="0dc56-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="0dc56-126">Authentication token</span><span class="sxs-lookup"><span data-stu-id="0dc56-126">Authentication token</span></span>
<span data-ttu-id="0dc56-127">The authentication token can be downloaded after you generate a token for your application.</span><span class="sxs-lookup"><span data-stu-id="0dc56-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="0dc56-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="0dc56-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="0dc56-129">Configuring your notification hub to use token-based authentication</span><span class="sxs-lookup"><span data-stu-id="0dc56-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="0dc56-130">Configure via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0dc56-130">Configure via the Azure portal</span></span>
<span data-ttu-id="0dc56-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span><span class="sxs-lookup"><span data-stu-id="0dc56-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="0dc56-132">There is a new property – *Authentication Mode*.</span><span class="sxs-lookup"><span data-stu-id="0dc56-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="0dc56-133">Selecting Token allows you to update your hub with all the relevant token properties.</span><span class="sxs-lookup"><span data-stu-id="0dc56-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="0dc56-134">Enter the properties you retrieved from your Apple developer account,</span><span class="sxs-lookup"><span data-stu-id="0dc56-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="0dc56-135">choose your application mode (Production or Sandbox)</span><span class="sxs-lookup"><span data-stu-id="0dc56-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="0dc56-136">click Save to update your APNS credentials.</span><span class="sxs-lookup"><span data-stu-id="0dc56-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="0dc56-137">Configure via Management API (REST)</span><span class="sxs-lookup"><span data-stu-id="0dc56-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="0dc56-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span><span class="sxs-lookup"><span data-stu-id="0dc56-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="0dc56-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span><span class="sxs-lookup"><span data-stu-id="0dc56-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="0dc56-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="0dc56-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="0dc56-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="0dc56-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dc56-142">Token-based authentication requires an API version of: **2017-04 or later**.</span><span class="sxs-lookup"><span data-stu-id="0dc56-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="0dc56-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span><span class="sxs-lookup"><span data-stu-id="0dc56-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="0dc56-144">Configure via the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0dc56-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="0dc56-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="0dc56-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="0dc56-146">Here’s a code sample illustrating the correct usage:</span><span class="sxs-lookup"><span data-stu-id="0dc56-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="0dc56-147">Reverting to using certificate-based authentication</span><span class="sxs-lookup"><span data-stu-id="0dc56-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="0dc56-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span><span class="sxs-lookup"><span data-stu-id="0dc56-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="0dc56-149">That action overwrites the previously stored credentials.</span><span class="sxs-lookup"><span data-stu-id="0dc56-149">That action overwrites the previously stored credentials.</span></span>
