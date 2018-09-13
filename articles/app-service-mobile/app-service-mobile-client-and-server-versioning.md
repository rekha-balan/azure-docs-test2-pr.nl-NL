---
title: Client and server SDK versioning in Mobile Apps and Mobile Services | Microsoft Docs
description: List of client SDKs and compatibility with server SDK versions for Mobile Services and Azure Mobile Apps
services: app-service\mobile
documentationcenter: ''
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: d74137dc3c994cb05e02c4f866043eabf134fcdd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553832"
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="b6dbe-103">Client and server versioning in Mobile Apps and Mobile Services</span><span class="sxs-lookup"><span data-stu-id="b6dbe-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="b6dbe-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="b6dbe-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="b6dbe-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="b6dbe-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="b6dbe-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="b6dbe-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="b6dbe-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="b6dbe-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="b6dbe-111">Header specification</span><span class="sxs-lookup"><span data-stu-id="b6dbe-111">Header specification</span></span>
<span data-ttu-id="b6dbe-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="b6dbe-113">The value is a version string in the form **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="b6dbe-114">For example:</span><span class="sxs-lookup"><span data-stu-id="b6dbe-114">For example:</span></span>

<span data-ttu-id="b6dbe-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="b6dbe-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="b6dbe-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="b6dbe-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="b6dbe-118">Opting out of version checking</span><span class="sxs-lookup"><span data-stu-id="b6dbe-118">Opting out of version checking</span></span>
<span data-ttu-id="b6dbe-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="b6dbe-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b6dbe-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="b6dbe-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
> 
> 

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="b6dbe-123">Summary of compatibility for all versions</span><span class="sxs-lookup"><span data-stu-id="b6dbe-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="b6dbe-124">The chart below shows the compatibility between all client and server types.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="b6dbe-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="b6dbe-126">**Mobile Services** Node.js or .NET</span><span class="sxs-lookup"><span data-stu-id="b6dbe-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="b6dbe-127">**Mobile Apps** Node.js or .NET</span><span class="sxs-lookup"><span data-stu-id="b6dbe-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-128">[Mobile Services clients]</span><span class="sxs-lookup"><span data-stu-id="b6dbe-128">[Mobile Services clients]</span></span> |<span data-ttu-id="b6dbe-129">Ok</span><span class="sxs-lookup"><span data-stu-id="b6dbe-129">Ok</span></span> |<span data-ttu-id="b6dbe-130">Error\*</span><span class="sxs-lookup"><span data-stu-id="b6dbe-130">Error\*</span></span> |
| <span data-ttu-id="b6dbe-131">[Mobile Apps clients]</span><span class="sxs-lookup"><span data-stu-id="b6dbe-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="b6dbe-132">Error\*</span><span class="sxs-lookup"><span data-stu-id="b6dbe-132">Error\*</span></span> |<span data-ttu-id="b6dbe-133">Ok</span><span class="sxs-lookup"><span data-stu-id="b6dbe-133">Ok</span></span> |

<span data-ttu-id="b6dbe-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a><span data-ttu-id="b6dbe-135">Mobile Services client and server</span><span class="sxs-lookup"><span data-stu-id="b6dbe-135">Mobile Services client and server</span></span>
<span data-ttu-id="b6dbe-136">The client SDKs in the table below are compatible with **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="b6dbe-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="b6dbe-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span><span class="sxs-lookup"><span data-stu-id="b6dbe-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <a name="MobileServicesClients"></a> <span data-ttu-id="b6dbe-139">Mobile *Services* client SDKs</span><span class="sxs-lookup"><span data-stu-id="b6dbe-139">Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="b6dbe-140">Client platform</span><span class="sxs-lookup"><span data-stu-id="b6dbe-140">Client platform</span></span> | <span data-ttu-id="b6dbe-141">Version</span><span class="sxs-lookup"><span data-stu-id="b6dbe-141">Version</span></span> | <span data-ttu-id="b6dbe-142">Version header value</span><span class="sxs-lookup"><span data-stu-id="b6dbe-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-143">Managed client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="b6dbe-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="b6dbe-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="b6dbe-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="b6dbe-145">n/a</span><span class="sxs-lookup"><span data-stu-id="b6dbe-145">n/a</span></span> |
| <span data-ttu-id="b6dbe-146">iOS</span><span class="sxs-lookup"><span data-stu-id="b6dbe-146">iOS</span></span> |[<span data-ttu-id="b6dbe-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="b6dbe-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="b6dbe-148">n/a</span><span class="sxs-lookup"><span data-stu-id="b6dbe-148">n/a</span></span> |
| <span data-ttu-id="b6dbe-149">Android</span><span class="sxs-lookup"><span data-stu-id="b6dbe-149">Android</span></span> |[<span data-ttu-id="b6dbe-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="b6dbe-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="b6dbe-151">n/a</span><span class="sxs-lookup"><span data-stu-id="b6dbe-151">n/a</span></span> |
| <span data-ttu-id="b6dbe-152">HTML</span><span class="sxs-lookup"><span data-stu-id="b6dbe-152">HTML</span></span> |[<span data-ttu-id="b6dbe-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="b6dbe-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="b6dbe-154">n/a</span><span class="sxs-lookup"><span data-stu-id="b6dbe-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="b6dbe-155">Mobile *Services* server SDKs</span><span class="sxs-lookup"><span data-stu-id="b6dbe-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="b6dbe-156">Server platform</span><span class="sxs-lookup"><span data-stu-id="b6dbe-156">Server platform</span></span> | <span data-ttu-id="b6dbe-157">Version</span><span class="sxs-lookup"><span data-stu-id="b6dbe-157">Version</span></span> | <span data-ttu-id="b6dbe-158">Accepted version header</span><span class="sxs-lookup"><span data-stu-id="b6dbe-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-159">.NET</span><span class="sxs-lookup"><span data-stu-id="b6dbe-159">.NET</span></span> |[<span data-ttu-id="b6dbe-160">WindowsAzure.MobileServices.Backend.\* Version 1.0.x</span><span class="sxs-lookup"><span data-stu-id="b6dbe-160">WindowsAzure.MobileServices.Backend.\* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="b6dbe-161">\*\*No version header \*\*</span><span class="sxs-lookup"><span data-stu-id="b6dbe-161">\*\*No version header \*\*</span></span> |
| <span data-ttu-id="b6dbe-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6dbe-162">Node.js</span></span> |<span data-ttu-id="b6dbe-163">(coming soon)</span><span class="sxs-lookup"><span data-stu-id="b6dbe-163">(coming soon)</span></span> |<span data-ttu-id="b6dbe-164">**No version header**</span><span class="sxs-lookup"><span data-stu-id="b6dbe-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="b6dbe-165">Behavior of Mobile Services backends</span><span class="sxs-lookup"><span data-stu-id="b6dbe-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="b6dbe-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="b6dbe-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="b6dbe-167">Value of MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="b6dbe-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="b6dbe-168">Response</span><span class="sxs-lookup"><span data-stu-id="b6dbe-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-169">Not specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-169">Not specified</span></span> |<span data-ttu-id="b6dbe-170">Any</span><span class="sxs-lookup"><span data-stu-id="b6dbe-170">Any</span></span> |<span data-ttu-id="b6dbe-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b6dbe-171">200 - OK</span></span> |
| <span data-ttu-id="b6dbe-172">Any value</span><span class="sxs-lookup"><span data-stu-id="b6dbe-172">Any value</span></span> |<span data-ttu-id="b6dbe-173">True</span><span class="sxs-lookup"><span data-stu-id="b6dbe-173">True</span></span> |<span data-ttu-id="b6dbe-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b6dbe-174">200 - OK</span></span> |
| <span data-ttu-id="b6dbe-175">Any value</span><span class="sxs-lookup"><span data-stu-id="b6dbe-175">Any value</span></span> |<span data-ttu-id="b6dbe-176">False/Not Specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-176">False/Not Specified</span></span> |<span data-ttu-id="b6dbe-177">400 - Bad Request</span><span class="sxs-lookup"><span data-stu-id="b6dbe-177">400 - Bad Request</span></span> |

## <a name="2.0.0"></a><span data-ttu-id="b6dbe-178">Azure Mobile Apps client and server</span><span class="sxs-lookup"><span data-stu-id="b6dbe-178">Azure Mobile Apps client and server</span></span>
### <a name="MobileAppsClients"></a> <span data-ttu-id="b6dbe-179">Mobile *Apps* client SDKs</span><span class="sxs-lookup"><span data-stu-id="b6dbe-179">Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="b6dbe-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="b6dbe-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="b6dbe-181">Client platform</span><span class="sxs-lookup"><span data-stu-id="b6dbe-181">Client platform</span></span> | <span data-ttu-id="b6dbe-182">Version</span><span class="sxs-lookup"><span data-stu-id="b6dbe-182">Version</span></span> | <span data-ttu-id="b6dbe-183">Version header value</span><span class="sxs-lookup"><span data-stu-id="b6dbe-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-184">Managed client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="b6dbe-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="b6dbe-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="b6dbe-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-186">2.0.0</span></span> |
| <span data-ttu-id="b6dbe-187">iOS</span><span class="sxs-lookup"><span data-stu-id="b6dbe-187">iOS</span></span> |[<span data-ttu-id="b6dbe-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="b6dbe-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-189">2.0.0</span></span> |
| <span data-ttu-id="b6dbe-190">Android</span><span class="sxs-lookup"><span data-stu-id="b6dbe-190">Android</span></span> |[<span data-ttu-id="b6dbe-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="b6dbe-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="b6dbe-193">Mobile *Apps* server SDKs</span><span class="sxs-lookup"><span data-stu-id="b6dbe-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="b6dbe-194">Version checking is included in following server SDK versions:</span><span class="sxs-lookup"><span data-stu-id="b6dbe-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="b6dbe-195">Server platform</span><span class="sxs-lookup"><span data-stu-id="b6dbe-195">Server platform</span></span> | <span data-ttu-id="b6dbe-196">SDK</span><span class="sxs-lookup"><span data-stu-id="b6dbe-196">SDK</span></span> | <span data-ttu-id="b6dbe-197">Accepted version header</span><span class="sxs-lookup"><span data-stu-id="b6dbe-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-198">.NET</span><span class="sxs-lookup"><span data-stu-id="b6dbe-198">.NET</span></span> |[<span data-ttu-id="b6dbe-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="b6dbe-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="b6dbe-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-200">2.0.0</span></span> |
| <span data-ttu-id="b6dbe-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6dbe-201">Node.js</span></span> |[<span data-ttu-id="b6dbe-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="b6dbe-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="b6dbe-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="b6dbe-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="b6dbe-204">Behavior of Mobile Apps backends</span><span class="sxs-lookup"><span data-stu-id="b6dbe-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="b6dbe-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="b6dbe-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="b6dbe-206">Value of MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="b6dbe-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="b6dbe-207">Response</span><span class="sxs-lookup"><span data-stu-id="b6dbe-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6dbe-208">x.y.z or Null</span><span class="sxs-lookup"><span data-stu-id="b6dbe-208">x.y.z or Null</span></span> |<span data-ttu-id="b6dbe-209">True</span><span class="sxs-lookup"><span data-stu-id="b6dbe-209">True</span></span> |<span data-ttu-id="b6dbe-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b6dbe-210">200 - OK</span></span> |
| <span data-ttu-id="b6dbe-211">Null</span><span class="sxs-lookup"><span data-stu-id="b6dbe-211">Null</span></span> |<span data-ttu-id="b6dbe-212">False/Not Specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-212">False/Not Specified</span></span> |<span data-ttu-id="b6dbe-213">400 - Bad Request</span><span class="sxs-lookup"><span data-stu-id="b6dbe-213">400 - Bad Request</span></span> |
| <span data-ttu-id="b6dbe-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="b6dbe-214">1.x.y</span></span> |<span data-ttu-id="b6dbe-215">False/Not Specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-215">False/Not Specified</span></span> |<span data-ttu-id="b6dbe-216">400 - Bad Request</span><span class="sxs-lookup"><span data-stu-id="b6dbe-216">400 - Bad Request</span></span> |
| <span data-ttu-id="b6dbe-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="b6dbe-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="b6dbe-218">False/Not Specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-218">False/Not Specified</span></span> |<span data-ttu-id="b6dbe-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="b6dbe-219">200 - OK</span></span> |
| <span data-ttu-id="b6dbe-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="b6dbe-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="b6dbe-221">False/Not Specified</span><span class="sxs-lookup"><span data-stu-id="b6dbe-221">False/Not Specified</span></span> |<span data-ttu-id="b6dbe-222">400 - Bad Request</span><span class="sxs-lookup"><span data-stu-id="b6dbe-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6dbe-223">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b6dbe-223">Next Steps</span></span>
* <span data-ttu-id="b6dbe-224">[Migrate a Mobile Service to Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="b6dbe-224">[Migrate a Mobile Service to Azure App Service]</span></span>

[Mobile Services clients]: #MobileServicesClients
[Mobile Apps clients]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md

