---
title: Publish native client apps - Azure AD | Microsoft Docs
description: Covers how to enable native client apps to communicate with Azure AD Application Proxy Connector to provide secure remote access to your on-premises apps.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/31/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 85a7b133655a3b1e4ca60c28e695e3057b293fdc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856533"
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="190e2-103">How to enable native client apps to interact with proxy applications</span><span class="sxs-lookup"><span data-stu-id="190e2-103">How to enable native client apps to interact with proxy applications</span></span>

<span data-ttu-id="190e2-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps that are configured with the Azure AD Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="190e2-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps that are configured with the Azure AD Authentication Library (ADAL).</span></span> <span data-ttu-id="190e2-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span><span class="sxs-lookup"><span data-stu-id="190e2-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="190e2-106">Application Proxy supports native client apps by accepting Azure AD issued tokens sent in the header.</span><span class="sxs-lookup"><span data-stu-id="190e2-106">Application Proxy supports native client apps by accepting Azure AD issued tokens sent in the header.</span></span> <span data-ttu-id="190e2-107">The Application Proxy service performs authentication on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="190e2-107">The Application Proxy service performs authentication on behalf of the users.</span></span> <span data-ttu-id="190e2-108">This solution does not use application tokens for authentication.</span><span class="sxs-lookup"><span data-stu-id="190e2-108">This solution does not use application tokens for authentication.</span></span> 

![Relationship between end users, Azure Active Directory, and published applications](./media/application-proxy-configure-native-client-application/richclientflow.png)

<span data-ttu-id="190e2-110">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span><span class="sxs-lookup"><span data-stu-id="190e2-110">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="190e2-111">Application Proxy fits into the [Native Application to Web API scenario](../develop/authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="190e2-111">Application Proxy fits into the [Native Application to Web API scenario](../develop/authentication-scenarios.md#native-application-to-web-api).</span></span> 

<span data-ttu-id="190e2-112">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="190e2-112">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="190e2-113">Step 1: Publish your application</span><span class="sxs-lookup"><span data-stu-id="190e2-113">Step 1: Publish your application</span></span>
<span data-ttu-id="190e2-114">Publish your proxy application as you would any other application and assign users to access your application.</span><span class="sxs-lookup"><span data-stu-id="190e2-114">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="190e2-115">For more information, see [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="190e2-115">For more information, see [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="190e2-116">Step 2: Configure your application</span><span class="sxs-lookup"><span data-stu-id="190e2-116">Step 2: Configure your application</span></span>
<span data-ttu-id="190e2-117">Configure your native application as follows:</span><span class="sxs-lookup"><span data-stu-id="190e2-117">Configure your native application as follows:</span></span>

1. <span data-ttu-id="190e2-118">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="190e2-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="190e2-119">Navigate to **Azure Active Directory** > **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="190e2-119">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="190e2-120">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="190e2-120">Select **New application registration**.</span></span>
4. <span data-ttu-id="190e2-121">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span><span class="sxs-lookup"><span data-stu-id="190e2-121">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Create a new app registration](./media/application-proxy-configure-native-client-application/create.png)
5. <span data-ttu-id="190e2-123">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="190e2-123">Select **Create**.</span></span>

<span data-ttu-id="190e2-124">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](../develop/quickstart-v1-integrate-apps-with-azure-ad.md).</span><span class="sxs-lookup"><span data-stu-id="190e2-124">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](../develop/quickstart-v1-integrate-apps-with-azure-ad.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="190e2-125">Step 3: Grant access to other applications</span><span class="sxs-lookup"><span data-stu-id="190e2-125">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="190e2-126">Enable the native application to be exposed to other applications in your directory:</span><span class="sxs-lookup"><span data-stu-id="190e2-126">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="190e2-127">Still in **App registrations**, select the new native application that you just created.</span><span class="sxs-lookup"><span data-stu-id="190e2-127">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="190e2-128">Select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="190e2-128">Select **Required permissions**.</span></span>
3. <span data-ttu-id="190e2-129">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="190e2-129">Select **Add**.</span></span>
4. <span data-ttu-id="190e2-130">Open the first step, **Select an API**.</span><span class="sxs-lookup"><span data-stu-id="190e2-130">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="190e2-131">Use the search bar to find the Application Proxy app that you published in the first section.</span><span class="sxs-lookup"><span data-stu-id="190e2-131">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="190e2-132">Choose that app, then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="190e2-132">Choose that app, then click **Select**.</span></span> 

   ![Search for the proxy app](./media/application-proxy-configure-native-client-application/select_api.png)
6. <span data-ttu-id="190e2-134">Open the second step, **Select permissions**.</span><span class="sxs-lookup"><span data-stu-id="190e2-134">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="190e2-135">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="190e2-135">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Grant access to proxy app](./media/application-proxy-configure-native-client-application/select_perms.png)
8. <span data-ttu-id="190e2-137">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="190e2-137">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="190e2-138">Step 4: Edit the Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="190e2-138">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="190e2-139">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span><span class="sxs-lookup"><span data-stu-id="190e2-139">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = await authContext.AcquireTokenAsync("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="190e2-140">The variables in the sample code should be replaced as follows:</span><span class="sxs-lookup"><span data-stu-id="190e2-140">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="190e2-141">**Tenant ID** can be found in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="190e2-141">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="190e2-142">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span><span class="sxs-lookup"><span data-stu-id="190e2-142">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="190e2-143">**External URL** is the front-end URL you entered in the Proxy Application.</span><span class="sxs-lookup"><span data-stu-id="190e2-143">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="190e2-144">To find this value, navigate to the **Application proxy** section of the proxy app.</span><span class="sxs-lookup"><span data-stu-id="190e2-144">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="190e2-145">**App ID** of the native app can be found on the **Properties** page of the native application.</span><span class="sxs-lookup"><span data-stu-id="190e2-145">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="190e2-146">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span><span class="sxs-lookup"><span data-stu-id="190e2-146">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>

<span data-ttu-id="190e2-147">Once the ADAL is edited with these parameters, your users should be able to authenticate to native client apps even when they're outside of the corporate network.</span><span class="sxs-lookup"><span data-stu-id="190e2-147">Once the ADAL is edited with these parameters, your users should be able to authenticate to native client apps even when they're outside of the corporate network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="190e2-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="190e2-148">Next steps</span></span>

<span data-ttu-id="190e2-149">For more information about the native application flow, see [Native application to web API](../develop/authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="190e2-149">For more information about the native application flow, see [Native application to web API](../develop/authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="190e2-150">Learn about setting up [Single sign-on for Application Proxy](application-proxy-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="190e2-150">Learn about setting up [Single sign-on for Application Proxy](application-proxy-single-sign-on.md)</span></span>
