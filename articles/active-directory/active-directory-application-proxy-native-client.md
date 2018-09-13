---
title: Publish native client apps - Azure AD | Microsoft Docs
description: Covers how to enable native client apps to communicate with Azure AD Application Proxy Connector to provide secure remote access to your on-premises apps.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: kgremban
ms.openlocfilehash: 49e9903df6e902e4b2a20b8d6f47fdd8b584b85f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553868"
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="d6ffa-103">How to enable native client apps to interact with proxy Applications</span><span class="sxs-lookup"><span data-stu-id="d6ffa-103">How to enable native client apps to interact with proxy Applications</span></span>
<span data-ttu-id="d6ffa-104">Azure Active Directory Application Proxy is widely used to publish browser applications such as SharePoint, Outlook Web Access and custom line of business applications.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-104">Azure Active Directory Application Proxy is widely used to publish browser applications such as SharePoint, Outlook Web Access and custom line of business applications.</span></span> <span data-ttu-id="d6ffa-105">It can also be used to publish native client apps, which differ from web apps because they get installed on a device.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-105">It can also be used to publish native client apps, which differ from web apps because they get installed on a device.</span></span> <span data-ttu-id="d6ffa-106">This is done by supporting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-106">This is done by supporting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relationship between end users, Azure Active Directory, and published applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="d6ffa-108">The recommended method to publish such applications is to use the Azure AD Authentication Library, which takes care of all the authentication hassle and supports many different client environments.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-108">The recommended method to publish such applications is to use the Azure AD Authentication Library, which takes care of all the authentication hassle and supports many different client environments.</span></span> <span data-ttu-id="d6ffa-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d6ffa-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="d6ffa-110">The process for accomplishing this is as follows:</span><span class="sxs-lookup"><span data-stu-id="d6ffa-110">The process for accomplishing this is as follows:</span></span>

## <a name="step-1-publish-your-application"></a><span data-ttu-id="d6ffa-111">Step 1: Publish your application</span><span class="sxs-lookup"><span data-stu-id="d6ffa-111">Step 1: Publish your application</span></span>
<span data-ttu-id="d6ffa-112">Publish your proxy application as you would any other application, assign users and give them premium or basic licenses.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-112">Publish your proxy application as you would any other application, assign users and give them premium or basic licenses.</span></span> <span data-ttu-id="d6ffa-113">For more information see  [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d6ffa-113">For more information see  [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="d6ffa-114">Step 2: Configure your application</span><span class="sxs-lookup"><span data-stu-id="d6ffa-114">Step 2: Configure your application</span></span>
<span data-ttu-id="d6ffa-115">Configure your native application as follows:</span><span class="sxs-lookup"><span data-stu-id="d6ffa-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="d6ffa-116">Sign in to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-116">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="d6ffa-117">Select the Active Directory icon on the left menu, and then select your directory.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-117">Select the Active Directory icon on the left menu, and then select your directory.</span></span>
3. <span data-ttu-id="d6ffa-118">On the top menu, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-118">On the top menu, click **Applications**.</span></span> <span data-ttu-id="d6ffa-119">If no apps have been added to your directory, this page will only show the **Add an App** link.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-119">If no apps have been added to your directory, this page will only show the **Add an App** link.</span></span> <span data-ttu-id="d6ffa-120">Click on the link, or alternatively you can click on the **Add** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-120">Click on the link, or alternatively you can click on the **Add** button on the command bar.</span></span>
4. <span data-ttu-id="d6ffa-121">On the **What do you want to do** page, click on the link to **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-121">On the **What do you want to do** page, click on the link to **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="d6ffa-122">On the **Tell us about your application** page, specify a name for your application and choose **Native client application**.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-122">On the **Tell us about your application** page, specify a name for your application and choose **Native client application**.</span></span> <span data-ttu-id="d6ffa-123">Click the arrow icon to continue.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-123">Click the arrow icon to continue.</span></span>
6. <span data-ttu-id="d6ffa-124">On the **Application information** page, provide the **Redirect URI** for the native client application, then click the checkmark to finish.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-124">On the **Application information** page, provide the **Redirect URI** for the native client application, then click the checkmark to finish.</span></span>

<span data-ttu-id="d6ffa-125">Your application has been added, and you will be taken to the Quick Start page for your application.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-125">Your application has been added, and you will be taken to the Quick Start page for your application.</span></span>

## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="d6ffa-126">Step 3: Grant access to other applications</span><span class="sxs-lookup"><span data-stu-id="d6ffa-126">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="d6ffa-127">Enable the native application to be exposed to other applications in your directory:</span><span class="sxs-lookup"><span data-stu-id="d6ffa-127">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="d6ffa-128">On the top menu, click **Applications**, select the new native application, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-128">On the top menu, click **Applications**, select the new native application, and then click **Configure**.</span></span>
2. <span data-ttu-id="d6ffa-129">Scroll down to the **permissions to other applications** section.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-129">Scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="d6ffa-130">Click on the **Add application** button and select the proxy application that you want to grant the native application access to, and click the check mark in the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-130">Click on the **Add application** button and select the proxy application that you want to grant the native application access to, and click the check mark in the bottom right corner.</span></span> <span data-ttu-id="d6ffa-131">From the **Delegated Permissions** drop-down menu, select the new permission.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-131">From the **Delegated Permissions** drop-down menu, select the new permission.</span></span>

![Permissions to other applications screenshot - add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-native-client/delegate_native_app.png)

## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="d6ffa-133">Step 4: Edit the Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="d6ffa-133">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="d6ffa-134">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following:</span><span class="sxs-lookup"><span data-stu-id="d6ffa-134">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following:</span></span>

        // Acquire Access Token from AAD for Proxy Application
        AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<TenantId>");
        AuthenticationResult result = authContext.AcquireToken("< Frontend Url of Proxy App >",
                                                        "< Client Id of the Native app>",
                                                        new Uri("< Redirect Uri of the Native App>"),
                                                        PromptBehavior.Never);

        //Use the Access Token to access the Proxy Application
        HttpClient httpClient = new HttpClient();
        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
        HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");

<span data-ttu-id="d6ffa-135">The variables should be replaced as follows:</span><span class="sxs-lookup"><span data-stu-id="d6ffa-135">The variables should be replaced as follows:</span></span>

* <span data-ttu-id="d6ffa-136">**TenantId** can be found in the GUID in the URL of the application's **Configuration** page, right after “/Directory/”.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-136">**TenantId** can be found in the GUID in the URL of the application's **Configuration** page, right after “/Directory/”.</span></span>
* <span data-ttu-id="d6ffa-137">**Frontend URL** is the front end URL you entered in the Proxy Application and can be found on the **Configuration** page of the proxy app.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-137">**Frontend URL** is the front end URL you entered in the Proxy Application and can be found on the **Configuration** page of the proxy app.</span></span>
* <span data-ttu-id="d6ffa-138">**Client Id** of the native app can be found on the **Configure** page of the native application.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-138">**Client Id** of the native app can be found on the **Configure** page of the native application.</span></span>
* <span data-ttu-id="d6ffa-139">**Redirect URI of the native app** can be found on the **Configure** page of the native application.</span><span class="sxs-lookup"><span data-stu-id="d6ffa-139">**Redirect URI of the native app** can be found on the **Configure** page of the native application.</span></span>

![New native application configure page screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-native-client/new_native_app.png)

<span data-ttu-id="d6ffa-141">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d6ffa-141">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span>

## <a name="see-also"></a><span data-ttu-id="d6ffa-142">See also</span><span class="sxs-lookup"><span data-stu-id="d6ffa-142">See also</span></span>
* [<span data-ttu-id="d6ffa-143">Publish applications using your own domain name</span><span class="sxs-lookup"><span data-stu-id="d6ffa-143">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="d6ffa-144">Enable conditional access</span><span class="sxs-lookup"><span data-stu-id="d6ffa-144">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="d6ffa-145">Working with claims aware applications</span><span class="sxs-lookup"><span data-stu-id="d6ffa-145">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)
* [<span data-ttu-id="d6ffa-146">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="d6ffa-146">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)

<span data-ttu-id="d6ffa-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="d6ffa-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>



