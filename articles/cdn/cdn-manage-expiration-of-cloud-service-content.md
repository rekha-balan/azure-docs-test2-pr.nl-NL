---
title: Manage expiration of web content in Azure CDN | Microsoft Docs
description: Learn how to manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN.
services: cdn
documentationcenter: .NET
author: dksimpson
manager: akucer
editor: ''
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2018
ms.author: mazha
ms.openlocfilehash: fc74d7fdd082cf497b7cabf30d96509ebe8b6b68
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800870"
---
# <a name="manage-expiration-of-web-content-in-azure-cdn"></a><span data-ttu-id="caa21-103">Manage expiration of web content in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="caa21-103">Manage expiration of web content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [Azure web content](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure Blob storage](cdn-manage-expiration-of-blob-content.md)
> 

<span data-ttu-id="caa21-106">Files from publicly accessible origin web servers can be cached in Azure Content Delivery Network (CDN) until their time-to-live (TTL) elapses.</span><span class="sxs-lookup"><span data-stu-id="caa21-106">Files from publicly accessible origin web servers can be cached in Azure Content Delivery Network (CDN) until their time-to-live (TTL) elapses.</span></span> <span data-ttu-id="caa21-107">The TTL is determined by the `Cache-Control` header in the HTTP response from the origin server.</span><span class="sxs-lookup"><span data-stu-id="caa21-107">The TTL is determined by the `Cache-Control` header in the HTTP response from the origin server.</span></span> <span data-ttu-id="caa21-108">This article describes how to set `Cache-Control` headers for the Web Apps feature of Microsoft Azure App Service, Azure Cloud Services, ASP.NET applications, and Internet Information Services (IIS) sites, all of which are configured similarly.</span><span class="sxs-lookup"><span data-stu-id="caa21-108">This article describes how to set `Cache-Control` headers for the Web Apps feature of Microsoft Azure App Service, Azure Cloud Services, ASP.NET applications, and Internet Information Services (IIS) sites, all of which are configured similarly.</span></span> <span data-ttu-id="caa21-109">You can set the `Cache-Control` header either by using configuration files or programmatically.</span><span class="sxs-lookup"><span data-stu-id="caa21-109">You can set the `Cache-Control` header either by using configuration files or programmatically.</span></span> 

<span data-ttu-id="caa21-110">You can also control cache settings from the Azure portal by setting [CDN caching rules](cdn-caching-rules.md).</span><span class="sxs-lookup"><span data-stu-id="caa21-110">You can also control cache settings from the Azure portal by setting [CDN caching rules](cdn-caching-rules.md).</span></span> <span data-ttu-id="caa21-111">If you create one or more caching rules and set their caching behavior to **Override** or **Bypass cache**, the origin-provided caching settings discussed in this article are ignored.</span><span class="sxs-lookup"><span data-stu-id="caa21-111">If you create one or more caching rules and set their caching behavior to **Override** or **Bypass cache**, the origin-provided caching settings discussed in this article are ignored.</span></span> <span data-ttu-id="caa21-112">For information about general caching concepts, see [How caching works](cdn-how-caching-works.md).</span><span class="sxs-lookup"><span data-stu-id="caa21-112">For information about general caching concepts, see [How caching works](cdn-how-caching-works.md).</span></span>

> [!TIP]
> You can choose to set no TTL on a file. In this case, Azure CDN automatically applies a default TTL of seven days, unless you've set up caching rules in the Azure portal. This default TTL applies only to general web delivery optimizations. For large file optimizations, the default TTL is one day, and for media streaming optimizations, the default TTL is one year.
> 
> For more information about how Azure CDN works to speed up access to files and other resources, see [Overview of the Azure Content Delivery Network](cdn-overview.md).
> 

## <a name="setting-cache-control-headers-by-using-cdn-caching-rules"></a><span data-ttu-id="caa21-118">Setting Cache-Control headers by using CDN caching rules</span><span class="sxs-lookup"><span data-stu-id="caa21-118">Setting Cache-Control headers by using CDN caching rules</span></span>
<span data-ttu-id="caa21-119">The preferred method for setting a web server's `Cache-Control` header is to use caching rules in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="caa21-119">The preferred method for setting a web server's `Cache-Control` header is to use caching rules in the Azure portal.</span></span> <span data-ttu-id="caa21-120">For more information about CDN caching rules, see [Control Azure CDN caching behavior with caching rules](cdn-caching-rules.md).</span><span class="sxs-lookup"><span data-stu-id="caa21-120">For more information about CDN caching rules, see [Control Azure CDN caching behavior with caching rules](cdn-caching-rules.md).</span></span>

> [!NOTE] 
> Caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles. For **Azure CDN Premium from Verizon** profiles, you must use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.

<span data-ttu-id="caa21-123">**To navigate to the CDN caching rules page**:</span><span class="sxs-lookup"><span data-stu-id="caa21-123">**To navigate to the CDN caching rules page**:</span></span>

1. <span data-ttu-id="caa21-124">In the Azure portal, select a CDN profile, then select the endpoint for the web server.</span><span class="sxs-lookup"><span data-stu-id="caa21-124">In the Azure portal, select a CDN profile, then select the endpoint for the web server.</span></span>

1. <span data-ttu-id="caa21-125">In the left pane under Settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="caa21-125">In the left pane under Settings, select **Caching rules**.</span></span>

   ![CDN caching rules button](./media/cdn-manage-expiration-of-cloud-service-content/cdn-caching-rules-btn.png)

   <span data-ttu-id="caa21-127">The **Caching rules** page appears.</span><span class="sxs-lookup"><span data-stu-id="caa21-127">The **Caching rules** page appears.</span></span>

   ![CDN caching page](./media/cdn-manage-expiration-of-cloud-service-content/cdn-caching-page.png)


<span data-ttu-id="caa21-129">**To set a web server's Cache-Control headers by using global caching rules:**</span><span class="sxs-lookup"><span data-stu-id="caa21-129">**To set a web server's Cache-Control headers by using global caching rules:**</span></span>

1. <span data-ttu-id="caa21-130">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings** and set **Caching behavior** to **Override**.</span><span class="sxs-lookup"><span data-stu-id="caa21-130">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings** and set **Caching behavior** to **Override**.</span></span>
      
1. <span data-ttu-id="caa21-131">For **Cache expiration duration**, enter 3600 in the **Seconds** box or 1 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="caa21-131">For **Cache expiration duration**, enter 3600 in the **Seconds** box or 1 in the **Hours** box.</span></span> 

   ![CDN global caching rules example](./media/cdn-manage-expiration-of-cloud-service-content/cdn-global-caching-rules-example.png)

   <span data-ttu-id="caa21-133">This global caching rule sets a cache duration of one hour and affects all requests to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="caa21-133">This global caching rule sets a cache duration of one hour and affects all requests to the endpoint.</span></span> <span data-ttu-id="caa21-134">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server specified by the endpoint.</span><span class="sxs-lookup"><span data-stu-id="caa21-134">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server specified by the endpoint.</span></span>   

1. <span data-ttu-id="caa21-135">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="caa21-135">Select **Save**.</span></span>

<span data-ttu-id="caa21-136">**To set a web server file's Cache-Control headers by using custom caching rules:**</span><span class="sxs-lookup"><span data-stu-id="caa21-136">**To set a web server file's Cache-Control headers by using custom caching rules:**</span></span>

1. <span data-ttu-id="caa21-137">Under **Custom caching rules**, create two match conditions:</span><span class="sxs-lookup"><span data-stu-id="caa21-137">Under **Custom caching rules**, create two match conditions:</span></span>

     <span data-ttu-id="caa21-138">a.</span><span class="sxs-lookup"><span data-stu-id="caa21-138">a.</span></span> <span data-ttu-id="caa21-139">For the first match condition, set **Match condition** to **Path** and enter `/webfolder1/*` for **Match value**.</span><span class="sxs-lookup"><span data-stu-id="caa21-139">For the first match condition, set **Match condition** to **Path** and enter `/webfolder1/*` for **Match value**.</span></span> <span data-ttu-id="caa21-140">Set **Caching behavior** to **Override** and enter 4 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="caa21-140">Set **Caching behavior** to **Override** and enter 4 in the **Hours** box.</span></span>

     <span data-ttu-id="caa21-141">b.</span><span class="sxs-lookup"><span data-stu-id="caa21-141">b.</span></span> <span data-ttu-id="caa21-142">For the second match condition, set **Match condition** to **Path** and enter `/webfolder1/file1.txt` for **Match value**.</span><span class="sxs-lookup"><span data-stu-id="caa21-142">For the second match condition, set **Match condition** to **Path** and enter `/webfolder1/file1.txt` for **Match value**.</span></span> <span data-ttu-id="caa21-143">Set **Caching behavior** to **Override** and enter 2 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="caa21-143">Set **Caching behavior** to **Override** and enter 2 in the **Hours** box.</span></span>

    ![CDN custom caching rules example](./media/cdn-manage-expiration-of-cloud-service-content/cdn-custom-caching-rules-example.png)

    <span data-ttu-id="caa21-145">The first custom caching rule sets a cache duration of four hours for any files in the `/webfolder1` folder on the origin server specified by your endpoint.</span><span class="sxs-lookup"><span data-stu-id="caa21-145">The first custom caching rule sets a cache duration of four hours for any files in the `/webfolder1` folder on the origin server specified by your endpoint.</span></span> <span data-ttu-id="caa21-146">The second rule overrides the first rule for the `file1.txt` file only and sets a cache duration of two hours for it.</span><span class="sxs-lookup"><span data-stu-id="caa21-146">The second rule overrides the first rule for the `file1.txt` file only and sets a cache duration of two hours for it.</span></span>

1. <span data-ttu-id="caa21-147">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="caa21-147">Select **Save**.</span></span>


## <a name="setting-cache-control-headers-by-using-configuration-files"></a><span data-ttu-id="caa21-148">Setting Cache-Control headers by using configuration files</span><span class="sxs-lookup"><span data-stu-id="caa21-148">Setting Cache-Control headers by using configuration files</span></span>
<span data-ttu-id="caa21-149">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **Web.config** configuration files for your web application.</span><span class="sxs-lookup"><span data-stu-id="caa21-149">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **Web.config** configuration files for your web application.</span></span> <span data-ttu-id="caa21-150">To set the `Cache-Control` header for your content, use the `<system.webServer>/<staticContent>/<clientCache>` element in either file.</span><span class="sxs-lookup"><span data-stu-id="caa21-150">To set the `Cache-Control` header for your content, use the `<system.webServer>/<staticContent>/<clientCache>` element in either file.</span></span>

### <a name="using-applicationhostconfig-files"></a><span data-ttu-id="caa21-151">Using ApplicationHost.config files</span><span class="sxs-lookup"><span data-stu-id="caa21-151">Using ApplicationHost.config files</span></span>
<span data-ttu-id="caa21-152">The **ApplicationHost.config** file is the root file of the IIS configuration system.</span><span class="sxs-lookup"><span data-stu-id="caa21-152">The **ApplicationHost.config** file is the root file of the IIS configuration system.</span></span> <span data-ttu-id="caa21-153">The configuration settings in an **ApplicationHost.config** file affect all applications on the site, but are overridden by the settings of any **Web.config** files that exist for a web application.</span><span class="sxs-lookup"><span data-stu-id="caa21-153">The configuration settings in an **ApplicationHost.config** file affect all applications on the site, but are overridden by the settings of any **Web.config** files that exist for a web application.</span></span>

### <a name="using-webconfig-files"></a><span data-ttu-id="caa21-154">Using Web.config files</span><span class="sxs-lookup"><span data-stu-id="caa21-154">Using Web.config files</span></span>
<span data-ttu-id="caa21-155">With a **Web.config** file, you can customize the way your entire web application or a specific directory on your web application behaves.</span><span class="sxs-lookup"><span data-stu-id="caa21-155">With a **Web.config** file, you can customize the way your entire web application or a specific directory on your web application behaves.</span></span> <span data-ttu-id="caa21-156">Typically, you have at least one **Web.config** file in the root folder of your web application.</span><span class="sxs-lookup"><span data-stu-id="caa21-156">Typically, you have at least one **Web.config** file in the root folder of your web application.</span></span> <span data-ttu-id="caa21-157">For each **Web.config** file in a specific folder, the configuration settings affect everything in that folder and its subfolders, unless they are overridden at the subfolder level by another **Web.config** file.</span><span class="sxs-lookup"><span data-stu-id="caa21-157">For each **Web.config** file in a specific folder, the configuration settings affect everything in that folder and its subfolders, unless they are overridden at the subfolder level by another **Web.config** file.</span></span> 

<span data-ttu-id="caa21-158">For example, you can set a `<clientCache>` element in a **Web.config** file in the root folder of your web application to cache all static content on your web application for three days.</span><span class="sxs-lookup"><span data-stu-id="caa21-158">For example, you can set a `<clientCache>` element in a **Web.config** file in the root folder of your web application to cache all static content on your web application for three days.</span></span> <span data-ttu-id="caa21-159">You can also add a **Web.config** file in a subfolder with more variable content (for example, `\frequent`) and set its `<clientCache>` element to cache the subfolder's content for six hours.</span><span class="sxs-lookup"><span data-stu-id="caa21-159">You can also add a **Web.config** file in a subfolder with more variable content (for example, `\frequent`) and set its `<clientCache>` element to cache the subfolder's content for six hours.</span></span> <span data-ttu-id="caa21-160">The net result is that content on the entire web site is cached for three days, except for any content in the `\frequent` directory, which is cached for only six hours.</span><span class="sxs-lookup"><span data-stu-id="caa21-160">The net result is that content on the entire web site is cached for three days, except for any content in the `\frequent` directory, which is cached for only six hours.</span></span>  

<span data-ttu-id="caa21-161">The following XML configuration file example shows how to set the `<clientCache>` element to specify a maximum age of three days:</span><span class="sxs-lookup"><span data-stu-id="caa21-161">The following XML configuration file example shows how to set the `<clientCache>` element to specify a maximum age of three days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="caa21-162">To use the **cacheControlMaxAge** attribute, you must set the value of the **cacheControlMode** attribute to `UseMaxAge`.</span><span class="sxs-lookup"><span data-stu-id="caa21-162">To use the **cacheControlMaxAge** attribute, you must set the value of the **cacheControlMode** attribute to `UseMaxAge`.</span></span> <span data-ttu-id="caa21-163">This setting caused the HTTP header and directive, `Cache-Control: max-age=<nnn>`, to be added to the response.</span><span class="sxs-lookup"><span data-stu-id="caa21-163">This setting caused the HTTP header and directive, `Cache-Control: max-age=<nnn>`, to be added to the response.</span></span> <span data-ttu-id="caa21-164">The format of the timespan value for the **cacheControlMaxAge** attribute is `<days>.<hours>:<min>:<sec>`.</span><span class="sxs-lookup"><span data-stu-id="caa21-164">The format of the timespan value for the **cacheControlMaxAge** attribute is `<days>.<hours>:<min>:<sec>`.</span></span> <span data-ttu-id="caa21-165">Its value is converted to seconds and is used as the value of the `Cache-Control` `max-age` directive.</span><span class="sxs-lookup"><span data-stu-id="caa21-165">Its value is converted to seconds and is used as the value of the `Cache-Control` `max-age` directive.</span></span> <span data-ttu-id="caa21-166">For more information about the `<clientCache>` element, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="caa21-166">For more information about the `<clientCache>` element, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-programmatically"></a><span data-ttu-id="caa21-167">Setting Cache-Control headers programmatically</span><span class="sxs-lookup"><span data-stu-id="caa21-167">Setting Cache-Control headers programmatically</span></span>
<span data-ttu-id="caa21-168">For ASP.NET applications, you control the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property of the .NET API.</span><span class="sxs-lookup"><span data-stu-id="caa21-168">For ASP.NET applications, you control the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property of the .NET API.</span></span> <span data-ttu-id="caa21-169">For information about the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="caa21-169">For information about the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="caa21-170">To programmatically cache application content in ASP.NET, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="caa21-170">To programmatically cache application content in ASP.NET, follow these steps:</span></span>
   1. <span data-ttu-id="caa21-171">Verify that the content is marked as cacheable by setting `HttpCacheability` to `Public`.</span><span class="sxs-lookup"><span data-stu-id="caa21-171">Verify that the content is marked as cacheable by setting `HttpCacheability` to `Public`.</span></span> 
   1. <span data-ttu-id="caa21-172">Set a cache validator by calling one of the following `HttpCachePolicy` methods:</span><span class="sxs-lookup"><span data-stu-id="caa21-172">Set a cache validator by calling one of the following `HttpCachePolicy` methods:</span></span>
      - <span data-ttu-id="caa21-173">Call `SetLastModified` to set a timestamp value for the `Last-Modified` header.</span><span class="sxs-lookup"><span data-stu-id="caa21-173">Call `SetLastModified` to set a timestamp value for the `Last-Modified` header.</span></span>
      - <span data-ttu-id="caa21-174">Call `SetETag` to set a value for the `ETag` header.</span><span class="sxs-lookup"><span data-stu-id="caa21-174">Call `SetETag` to set a value for the `ETag` header.</span></span>
   1. <span data-ttu-id="caa21-175">Optionally, specify a cache expiration time by calling `SetExpires` to set a value for the `Expires` header.</span><span class="sxs-lookup"><span data-stu-id="caa21-175">Optionally, specify a cache expiration time by calling `SetExpires` to set a value for the `Expires` header.</span></span> <span data-ttu-id="caa21-176">Otherwise, the default cache heuristics described previously in this document apply.</span><span class="sxs-lookup"><span data-stu-id="caa21-176">Otherwise, the default cache heuristics described previously in this document apply.</span></span>

<span data-ttu-id="caa21-177">For example, to cache content for one hour, add the following C# code:</span><span class="sxs-lookup"><span data-stu-id="caa21-177">For example, to cache content for one hour, add the following C# code:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="caa21-178">Testing the Cache-Control header</span><span class="sxs-lookup"><span data-stu-id="caa21-178">Testing the Cache-Control header</span></span>
<span data-ttu-id="caa21-179">You can easily verify the TTL settings of your web content.</span><span class="sxs-lookup"><span data-stu-id="caa21-179">You can easily verify the TTL settings of your web content.</span></span> <span data-ttu-id="caa21-180">With your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your web content includes the `Cache-Control` response header.</span><span class="sxs-lookup"><span data-stu-id="caa21-180">With your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your web content includes the `Cache-Control` response header.</span></span> <span data-ttu-id="caa21-181">You can also use a tool such as **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span><span class="sxs-lookup"><span data-stu-id="caa21-181">You can also use a tool such as **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caa21-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="caa21-182">Next Steps</span></span>
* [<span data-ttu-id="caa21-183">Read details about the **clientCache** element</span><span class="sxs-lookup"><span data-stu-id="caa21-183">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="caa21-184">Read the documentation for the **HttpResponse.Cache** Property</span><span class="sxs-lookup"><span data-stu-id="caa21-184">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [<span data-ttu-id="caa21-185">Read the documentation for the **HttpCachePolicy Class**</span><span class="sxs-lookup"><span data-stu-id="caa21-185">Read the documentation for the **HttpCachePolicy Class**</span></span>](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)  
* [<span data-ttu-id="caa21-186">Learn about caching concepts</span><span class="sxs-lookup"><span data-stu-id="caa21-186">Learn about caching concepts</span></span>](cdn-how-caching-works.md)
