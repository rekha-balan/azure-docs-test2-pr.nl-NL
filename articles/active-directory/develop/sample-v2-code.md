---
title: Azure Active Directory code samples | Microsoft Docs
description: Provides an index of available Azure Active Directory (V2 endpoint) code samples, organized by scenario.
services: active-directory
documentationcenter: dev-center-name
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2018
ms.author: celested
ms.reviewer: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 0be97bfbbaafd6045fd36be57d85e917f0325779
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867735"
---
# <a name="azure-active-directory-code-samples-v2-endpoint"></a><span data-ttu-id="4980f-103">Azure Active Directory code samples (V2 endpoint)</span><span class="sxs-lookup"><span data-stu-id="4980f-103">Azure Active Directory code samples (V2 endpoint)</span></span>

<span data-ttu-id="4980f-104">You can use Microsoft Azure Active Directory (Azure AD) to:</span><span class="sxs-lookup"><span data-stu-id="4980f-104">You can use Microsoft Azure Active Directory (Azure AD) to:</span></span>

- <span data-ttu-id="4980f-105">Add authentication and authorization to your web applications and web APIs.</span><span class="sxs-lookup"><span data-stu-id="4980f-105">Add authentication and authorization to your web applications and web APIs.</span></span>
- <span data-ttu-id="4980f-106">Require an access token to access a protected web API.</span><span class="sxs-lookup"><span data-stu-id="4980f-106">Require an access token to access a protected web API.</span></span>

<span data-ttu-id="4980f-107">This article briefly describes and provides you with links to samples for the Azure AD V2 endpoint.</span><span class="sxs-lookup"><span data-stu-id="4980f-107">This article briefly describes and provides you with links to samples for the Azure AD V2 endpoint.</span></span> <span data-ttu-id="4980f-108">These samples show you how it's done, along with code snippets that you can use in your applications.</span><span class="sxs-lookup"><span data-stu-id="4980f-108">These samples show you how it's done, along with code snippets that you can use in your applications.</span></span> <span data-ttu-id="4980f-109">On the code sample page, you'll find detailed readme topics that help with requirements, installation, and set up.</span><span class="sxs-lookup"><span data-stu-id="4980f-109">On the code sample page, you'll find detailed readme topics that help with requirements, installation, and set up.</span></span> <span data-ttu-id="4980f-110">Comments within the code are there to help you understand the critical sections.</span><span class="sxs-lookup"><span data-stu-id="4980f-110">Comments within the code are there to help you understand the critical sections.</span></span>

> [!NOTE]
> <span data-ttu-id="4980f-111">If you are interested in V1 samples, see [Azure AD code samples (V1 endpoint)](sample-v1-code.md).</span><span class="sxs-lookup"><span data-stu-id="4980f-111">If you are interested in V1 samples, see [Azure AD code samples (V1 endpoint)](sample-v1-code.md).</span></span>

<span data-ttu-id="4980f-112">To understand the basic scenario for each sample type, see [App types for the Azure Active Directory v2.0 endpoint](v2-app-types.md).</span><span class="sxs-lookup"><span data-stu-id="4980f-112">To understand the basic scenario for each sample type, see [App types for the Azure Active Directory v2.0 endpoint](v2-app-types.md).</span></span>

<span data-ttu-id="4980f-113">You can also contribute to the samples on GitHub.</span><span class="sxs-lookup"><span data-stu-id="4980f-113">You can also contribute to the samples on GitHub.</span></span> <span data-ttu-id="4980f-114">To learn how, see [Microsoft Azure Active Directory samples and documentation](https://github.com/Azure-Samples?page=3&query=active-directory).</span><span class="sxs-lookup"><span data-stu-id="4980f-114">To learn how, see [Microsoft Azure Active Directory samples and documentation](https://github.com/Azure-Samples?page=3&query=active-directory).</span></span>

## <a name="desktop-and-mobile-public-client-apps"></a><span data-ttu-id="4980f-115">Desktop and mobile public client apps</span><span class="sxs-lookup"><span data-stu-id="4980f-115">Desktop and mobile public client apps</span></span>

<span data-ttu-id="4980f-116">The following samples show public client applications (desktop/mobile applications) that access the Microsoft Graph or a Web API in the name of a user.</span><span class="sxs-lookup"><span data-stu-id="4980f-116">The following samples show public client applications (desktop/mobile applications) that access the Microsoft Graph or a Web API in the name of a user.</span></span>

<span data-ttu-id="4980f-117">Client application</span><span class="sxs-lookup"><span data-stu-id="4980f-117">Client application</span></span> | <span data-ttu-id="4980f-118">Platform</span><span class="sxs-lookup"><span data-stu-id="4980f-118">Platform</span></span> | <span data-ttu-id="4980f-119">Flow/Grant</span><span class="sxs-lookup"><span data-stu-id="4980f-119">Flow/Grant</span></span> | <span data-ttu-id="4980f-120">Calls Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4980f-120">Calls Microsoft Graph</span></span> | <span data-ttu-id="4980f-121">Calls an ASP.NET Core 2.0 Web API</span><span class="sxs-lookup"><span data-stu-id="4980f-121">Calls an ASP.NET Core 2.0 Web API</span></span>
------------------ | -------- | ---------- | -------------------- | -------------------------
<span data-ttu-id="4980f-122">Desktop (WPF)</span><span class="sxs-lookup"><span data-stu-id="4980f-122">Desktop (WPF)</span></span>      | <span data-ttu-id="4980f-123">.NET/C#</span><span class="sxs-lookup"><span data-stu-id="4980f-123">.NET/C#</span></span>  | <span data-ttu-id="4980f-124">Interactive</span><span class="sxs-lookup"><span data-stu-id="4980f-124">Interactive</span></span> | [<span data-ttu-id="4980f-125">dotnet-desktop-msgraph-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-125">dotnet-desktop-msgraph-v2</span></span>](http://github.com/azure-samples/active-directory-dotnet-desktop-msgraph-v2) <p/> [<span data-ttu-id="4980f-126">dotnet-admin-restricted-scopes-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-126">dotnet-admin-restricted-scopes-v2</span></span>](https://github.com/azure-samples/active-directory-dotnet-admin-restricted-scopes-v2) | [<span data-ttu-id="4980f-127">dotnet-native-aspnetcore-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-127">dotnet-native-aspnetcore-v2</span></span>](https://GitHub.com/azure-samples/active-directory-dotnet-native-aspnetcore-v2)
<span data-ttu-id="4980f-128">Mobile (UWP)</span><span class="sxs-lookup"><span data-stu-id="4980f-128">Mobile (UWP)</span></span>   | <span data-ttu-id="4980f-129">.NET/C# (UWP)</span><span class="sxs-lookup"><span data-stu-id="4980f-129">.NET/C# (UWP)</span></span> | <span data-ttu-id="4980f-130">Interactive</span><span class="sxs-lookup"><span data-stu-id="4980f-130">Interactive</span></span> | [<span data-ttu-id="4980f-131">dotnet-native-uwp-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-131">dotnet-native-uwp-v2</span></span>](https://github.com/azure-samples/active-directory-dotnet-native-uwp-v2) |
<span data-ttu-id="4980f-132">Mobile (Android, iOS, UWP)</span><span class="sxs-lookup"><span data-stu-id="4980f-132">Mobile (Android, iOS, UWP)</span></span>   | <span data-ttu-id="4980f-133">.NET/C# (Xamarin)</span><span class="sxs-lookup"><span data-stu-id="4980f-133">.NET/C# (Xamarin)</span></span> | <span data-ttu-id="4980f-134">Interactive</span><span class="sxs-lookup"><span data-stu-id="4980f-134">Interactive</span></span> | [<span data-ttu-id="4980f-135">xamarin-native-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-135">xamarin-native-v2</span></span>](https://Github.com/azure-samples/active-directory-xamarin-native-v2) |
<span data-ttu-id="4980f-136">Mobile (iOS)</span><span class="sxs-lookup"><span data-stu-id="4980f-136">Mobile (iOS)</span></span>       | <span data-ttu-id="4980f-137">iOS / Objective C or swift</span><span class="sxs-lookup"><span data-stu-id="4980f-137">iOS / Objective C or swift</span></span> | <span data-ttu-id="4980f-138">Interactive</span><span class="sxs-lookup"><span data-stu-id="4980f-138">Interactive</span></span> | [<span data-ttu-id="4980f-139">ios-swift-native-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-139">ios-swift-native-v2</span></span>](https://github.com/azure-samples/active-directory-ios-swift-native-v2) <p/> [<span data-ttu-id="4980f-140">ios-native-nxoauth2-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-140">ios-native-nxoauth2-v2</span></span>](https://github.com/azure-samples/active-directory-ios-native-nxoauth2-v2) |
<span data-ttu-id="4980f-141">Mobile (Android)</span><span class="sxs-lookup"><span data-stu-id="4980f-141">Mobile (Android)</span></span>   | <span data-ttu-id="4980f-142">Android / Java</span><span class="sxs-lookup"><span data-stu-id="4980f-142">Android / Java</span></span> | <span data-ttu-id="4980f-143">Interactive</span><span class="sxs-lookup"><span data-stu-id="4980f-143">Interactive</span></span> |   [<span data-ttu-id="4980f-144">android-native-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-144">android-native-v2</span></span>](https://github.com/azure-samples/active-directory-android-native-v2 ) |

## <a name="web-applications"></a><span data-ttu-id="4980f-145">Web applications</span><span class="sxs-lookup"><span data-stu-id="4980f-145">Web applications</span></span>

<span data-ttu-id="4980f-146">The following samples illustrate web applications that sign in users, call Microsoft Graph, or call a web API with the user's identity.</span><span class="sxs-lookup"><span data-stu-id="4980f-146">The following samples illustrate web applications that sign in users, call Microsoft Graph, or call a web API with the user's identity.</span></span>

 <span data-ttu-id="4980f-147">Platform</span><span class="sxs-lookup"><span data-stu-id="4980f-147">Platform</span></span> | <span data-ttu-id="4980f-148">Only signs in users</span><span class="sxs-lookup"><span data-stu-id="4980f-148">Only signs in users</span></span> | <span data-ttu-id="4980f-149">Signs in users and calls Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4980f-149">Signs in users and calls Microsoft Graph</span></span> 
 -------- | ------------------- | --------------------------------- 
<span data-ttu-id="4980f-150">ASP.NET 4.x</span><span class="sxs-lookup"><span data-stu-id="4980f-150">ASP.NET 4.x</span></span> | [<span data-ttu-id="4980f-151">appmodelv2-webapp-openIDConnect-dotNet</span><span class="sxs-lookup"><span data-stu-id="4980f-151">appmodelv2-webapp-openIDConnect-dotNet</span></span>](https://GitHub.com/AzureAdQuickstarts/AppModelv2-WebApp-OpenIDConnect-DotNet) <p/> [<span data-ttu-id="4980f-152">dotnet-webapp-openidconnect-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-152">dotnet-webapp-openidconnect-v2</span></span>](https://GitHub.com/azure-samples/active-directory-dotnet-webapp-openidconnect-v2)  |              [<span data-ttu-id="4980f-153">aspnet-connect-rest-sample</span><span class="sxs-lookup"><span data-stu-id="4980f-153">aspnet-connect-rest-sample</span></span>](https://github.com/microsoftgraph/aspnet-connect-rest-sample)   
<span data-ttu-id="4980f-154">ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="4980f-154">ASP.NET Core 2.0</span></span> | [<span data-ttu-id="4980f-155">aspnetcore-webapp-openidconnect-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-155">aspnetcore-webapp-openidconnect-v2</span></span>](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2) |              [<span data-ttu-id="4980f-156">aspnetcore-connect-sample</span><span class="sxs-lookup"><span data-stu-id="4980f-156">aspnetcore-connect-sample</span></span>](https://github.com/microsoftgraph/aspnetcore-connect-sample)   
<span data-ttu-id="4980f-157">Node.js</span><span class="sxs-lookup"><span data-stu-id="4980f-157">Node.js</span></span>      |                   | [<span data-ttu-id="4980f-158">AppModelv2-WebApp-OpenIDConnect-nodejs</span><span class="sxs-lookup"><span data-stu-id="4980f-158">AppModelv2-WebApp-OpenIDConnect-nodejs</span></span>](https://github.com/azureadquickstarts/appmodelv2-webapp-openidconnect-nodejs)     
<span data-ttu-id="4980f-159">Ruby</span><span class="sxs-lookup"><span data-stu-id="4980f-159">Ruby</span></span>      |                   | [<span data-ttu-id="4980f-160">ruby-connect-rest-sample</span><span class="sxs-lookup"><span data-stu-id="4980f-160">ruby-connect-rest-sample</span></span>](https://github.com/microsoftgraph/ruby-connect-rest-sample)     

## <a name="daemon-applications"></a><span data-ttu-id="4980f-161">Daemon applications</span><span class="sxs-lookup"><span data-stu-id="4980f-161">Daemon applications</span></span>

<span data-ttu-id="4980f-162">The following samples show desktop or web applications that access the Microsoft Graph or a web API with the application identity (no user).</span><span class="sxs-lookup"><span data-stu-id="4980f-162">The following samples show desktop or web applications that access the Microsoft Graph or a web API with the application identity (no user).</span></span>

<span data-ttu-id="4980f-163">Client application</span><span class="sxs-lookup"><span data-stu-id="4980f-163">Client application</span></span> | <span data-ttu-id="4980f-164">Platform</span><span class="sxs-lookup"><span data-stu-id="4980f-164">Platform</span></span> | <span data-ttu-id="4980f-165">Flow/Grant</span><span class="sxs-lookup"><span data-stu-id="4980f-165">Flow/Grant</span></span> | <span data-ttu-id="4980f-166">Calls Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4980f-166">Calls Microsoft Graph</span></span> 
------------------ | -------- | ---------- | -------------------- 
<span data-ttu-id="4980f-167">Web app</span><span class="sxs-lookup"><span data-stu-id="4980f-167">Web app</span></span> | <span data-ttu-id="4980f-168">.NET/C#</span><span class="sxs-lookup"><span data-stu-id="4980f-168">.NET/C#</span></span>  | <span data-ttu-id="4980f-169">Client Credentials</span><span class="sxs-lookup"><span data-stu-id="4980f-169">Client Credentials</span></span> | [<span data-ttu-id="4980f-170">dotnet-daemon-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-170">dotnet-daemon-v2</span></span>](https://github.com/azure-samples/active-directory-dotnet-daemon-v2) 

## <a name="single-page-applications-spa"></a><span data-ttu-id="4980f-171">Single page applications (SPA)</span><span class="sxs-lookup"><span data-stu-id="4980f-171">Single page applications (SPA)</span></span>

<span data-ttu-id="4980f-172">This sample shows how to write a single page application secured with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4980f-172">This sample shows how to write a single page application secured with Azure AD.</span></span>

 <span data-ttu-id="4980f-173">Platform</span><span class="sxs-lookup"><span data-stu-id="4980f-173">Platform</span></span> |  <span data-ttu-id="4980f-174">Calls Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4980f-174">Calls Microsoft Graph</span></span> 
 -------- |  --------------------- 
<span data-ttu-id="4980f-175">JavaScript (msal.js)</span><span class="sxs-lookup"><span data-stu-id="4980f-175">JavaScript (msal.js)</span></span>  | [<span data-ttu-id="4980f-176">javascript-graphapi-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-176">javascript-graphapi-v2</span></span>](https://github.com/azure-samples/active-directory-javascript-graphapi-v2) 
<span data-ttu-id="4980f-177">JavaScript (msal.js + AngularJS)</span><span class="sxs-lookup"><span data-stu-id="4980f-177">JavaScript (msal.js + AngularJS)</span></span> | [<span data-ttu-id="4980f-178">angular-connect-rest-sample</span><span class="sxs-lookup"><span data-stu-id="4980f-178">angular-connect-rest-sample</span></span>](https://github.com/microsoftgraph/angular-connect-rest-sample) 
<span data-ttu-id="4980f-179">JavaScript (Hello.JS)</span><span class="sxs-lookup"><span data-stu-id="4980f-179">JavaScript (Hello.JS)</span></span>  | [<span data-ttu-id="4980f-180">javascript-graphapi-web-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-180">javascript-graphapi-web-v2</span></span>](https://github.com/azure-samples/active-directory-javascript-graphapi-web-v2) 
<span data-ttu-id="4980f-181">JavaScript (hello.js + Angular 4)</span><span class="sxs-lookup"><span data-stu-id="4980f-181">JavaScript (hello.js + Angular 4)</span></span> | [<span data-ttu-id="4980f-182">angular4-connect-sample</span><span class="sxs-lookup"><span data-stu-id="4980f-182">angular4-connect-sample</span></span>](https://github.com/microsoftgraph/angular4-connect-sample) 

## <a name="web-apis"></a><span data-ttu-id="4980f-183">Web APIs</span><span class="sxs-lookup"><span data-stu-id="4980f-183">Web APIs</span></span>

### <a name="web-api-protected-by-azure-ad"></a><span data-ttu-id="4980f-184">Web API protected by Azure AD</span><span class="sxs-lookup"><span data-stu-id="4980f-184">Web API protected by Azure AD</span></span>

<span data-ttu-id="4980f-185">The following sample shows how to protect a web API with the Azure AD V2 endpoint.</span><span class="sxs-lookup"><span data-stu-id="4980f-185">The following sample shows how to protect a web API with the Azure AD V2 endpoint.</span></span>

<span data-ttu-id="4980f-186">Platform</span><span class="sxs-lookup"><span data-stu-id="4980f-186">Platform</span></span> | <span data-ttu-id="4980f-187">Sample</span><span class="sxs-lookup"><span data-stu-id="4980f-187">Sample</span></span> | <span data-ttu-id="4980f-188">Description</span><span class="sxs-lookup"><span data-stu-id="4980f-188">Description</span></span>
 -------- | ------------------- | ---------------------
<span data-ttu-id="4980f-189">Node.js</span><span class="sxs-lookup"><span data-stu-id="4980f-189">Node.js</span></span> | [<span data-ttu-id="4980f-190">dotnet-native-aspnetcore-v2</span><span class="sxs-lookup"><span data-stu-id="4980f-190">dotnet-native-aspnetcore-v2</span></span>](https://GitHub.com/azure-samples/active-directory-dotnet-native-aspnetcore-v2) | <span data-ttu-id="4980f-191">Calls an ASP.NET Core Web API from a WPF application using Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="4980f-191">Calls an ASP.NET Core Web API from a WPF application using Azure AD V2.</span></span>

### <a name="web-api-calling-microsoft-graph-or-another-web-api"></a><span data-ttu-id="4980f-192">Web API calling Microsoft Graph or another Web API</span><span class="sxs-lookup"><span data-stu-id="4980f-192">Web API calling Microsoft Graph or another Web API</span></span>

<span data-ttu-id="4980f-193">This sample is not yet available.</span><span class="sxs-lookup"><span data-stu-id="4980f-193">This sample is not yet available.</span></span>

## <a name="other-microsoft-graph-samples"></a><span data-ttu-id="4980f-194">Other Microsoft Graph samples</span><span class="sxs-lookup"><span data-stu-id="4980f-194">Other Microsoft Graph samples</span></span>

<span data-ttu-id="4980f-195">To learn about [samples](https://github.com/microsoftgraph/msgraph-community-samples/tree/master/samples#aspnet) and tutorials that demonstrate different usage patterns for the Microsoft Graph API, including authentication with Azure AD, see [Microsoft Graph Community samples & tutorials](https://github.com/microsoftgraph/msgraph-community-samples).</span><span class="sxs-lookup"><span data-stu-id="4980f-195">To learn about [samples](https://github.com/microsoftgraph/msgraph-community-samples/tree/master/samples#aspnet) and tutorials that demonstrate different usage patterns for the Microsoft Graph API, including authentication with Azure AD, see [Microsoft Graph Community samples & tutorials](https://github.com/microsoftgraph/msgraph-community-samples).</span></span>

## <a name="see-also"></a><span data-ttu-id="4980f-196">See also</span><span class="sxs-lookup"><span data-stu-id="4980f-196">See also</span></span>

[<span data-ttu-id="4980f-197">Azure Active Directory developer's guide</span><span class="sxs-lookup"><span data-stu-id="4980f-197">Azure Active Directory developer's guide</span></span>](azure-ad-developers-guide.md)

[<span data-ttu-id="4980f-198">Azure AD Graph API conceptual and reference</span><span class="sxs-lookup"><span data-stu-id="4980f-198">Azure AD Graph API conceptual and reference</span></span>](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[<span data-ttu-id="4980f-199">Azure AD Graph API Helper Library</span><span class="sxs-lookup"><span data-stu-id="4980f-199">Azure AD Graph API Helper Library</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
