---
title: Integrate an Azure cloud service with Azure CDN | Microsoft Docs
description: Learn how to deploy a cloud service that serves content from an integrated Azure CDN endpoint
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 4cf0ee56da9fd4758dca9fb3cc70284d95490c71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563569"
---
# <a name="intro"></a> <span data-ttu-id="547e0-103">Integrate a cloud service with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-103">Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="547e0-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span><span class="sxs-lookup"><span data-stu-id="547e0-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="547e0-105">This approach gives you the following advantages:</span><span class="sxs-lookup"><span data-stu-id="547e0-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="547e0-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span><span class="sxs-lookup"><span data-stu-id="547e0-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="547e0-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span><span class="sxs-lookup"><span data-stu-id="547e0-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="547e0-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span><span class="sxs-lookup"><span data-stu-id="547e0-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="547e0-109">Unified deployment workflow for your Web application and your CDN-served content</span><span class="sxs-lookup"><span data-stu-id="547e0-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="547e0-110">Integrate ASP.NET bundling and minification with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="547e0-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="547e0-111">What you will learn</span></span>
<span data-ttu-id="547e0-112">In this tutorial, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="547e0-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="547e0-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="547e0-114">Configure cache settings for static content in your cloud service</span><span class="sxs-lookup"><span data-stu-id="547e0-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="547e0-115">Serve content from controller actions through Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="547e0-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="547e0-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="547e0-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span><span class="sxs-lookup"><span data-stu-id="547e0-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="547e0-118">What you will build</span><span class="sxs-lookup"><span data-stu-id="547e0-118">What you will build</span></span>
<span data-ttu-id="547e0-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span><span class="sxs-lookup"><span data-stu-id="547e0-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="547e0-120">What you will need</span><span class="sxs-lookup"><span data-stu-id="547e0-120">What you will need</span></span>
<span data-ttu-id="547e0-121">This tutorial has the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="547e0-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="547e0-122">An active [Microsoft Azure account](/account/)</span><span class="sxs-lookup"><span data-stu-id="547e0-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="547e0-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="547e0-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="547e0-124">You need an Azure account to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="547e0-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="547e0-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span><span class="sxs-lookup"><span data-stu-id="547e0-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="547e0-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="547e0-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="547e0-127">Deploy a cloud service</span><span class="sxs-lookup"><span data-stu-id="547e0-127">Deploy a cloud service</span></span>
<span data-ttu-id="547e0-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="547e0-129">Follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="547e0-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="547e0-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="547e0-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="547e0-131">Give it a name and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="547e0-131">Give it a name and click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="547e0-132">Select **ASP.NET Web Role** and click the **>** button.</span><span class="sxs-lookup"><span data-stu-id="547e0-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="547e0-133">Click OK.</span><span class="sxs-lookup"><span data-stu-id="547e0-133">Click OK.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="547e0-134">Select **MVC** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="547e0-134">Select **MVC** and click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="547e0-135">Now, publish this Web role to an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="547e0-136">Right-click the cloud service project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="547e0-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="547e0-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span><span class="sxs-lookup"><span data-stu-id="547e0-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="547e0-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span><span class="sxs-lookup"><span data-stu-id="547e0-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="547e0-139">Once you're signed in, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="547e0-139">Once you're signed in, click **Next**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="547e0-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span><span class="sxs-lookup"><span data-stu-id="547e0-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="547e0-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span><span class="sxs-lookup"><span data-stu-id="547e0-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="547e0-142">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="547e0-142">Then, click **Create**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="547e0-143">In the publish settings page, verify the configuration and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="547e0-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="547e0-144">The publishing process for cloud services takes a long time.</span><span class="sxs-lookup"><span data-stu-id="547e0-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="547e0-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span><span class="sxs-lookup"><span data-stu-id="547e0-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="547e0-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="547e0-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="547e0-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="547e0-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="547e0-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="547e0-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="547e0-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="547e0-150">Create a new CDN profile</span><span class="sxs-lookup"><span data-stu-id="547e0-150">Create a new CDN profile</span></span>
<span data-ttu-id="547e0-151">A CDN profile is a collection of CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="547e0-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="547e0-152">Each profile contains one or more CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="547e0-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="547e0-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span><span class="sxs-lookup"><span data-stu-id="547e0-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="547e0-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="547e0-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="547e0-155">Create a new CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="547e0-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="547e0-156">**To create a new CDN endpoint for your storage account**</span><span class="sxs-lookup"><span data-stu-id="547e0-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="547e0-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="547e0-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="547e0-158">You may have pinned it to the dashboard in the previous step.</span><span class="sxs-lookup"><span data-stu-id="547e0-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="547e0-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span><span class="sxs-lookup"><span data-stu-id="547e0-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="547e0-160">The CDN profile blade appears.</span><span class="sxs-lookup"><span data-stu-id="547e0-160">The CDN profile blade appears.</span></span>
   
    ![CDN profile][cdn-profile-settings]
2. <span data-ttu-id="547e0-162">Click the **Add Endpoint** button.</span><span class="sxs-lookup"><span data-stu-id="547e0-162">Click the **Add Endpoint** button.</span></span>
   
    ![Add endpoint button][cdn-new-endpoint-button]
   
    <span data-ttu-id="547e0-164">The **Add an endpoint** blade appears.</span><span class="sxs-lookup"><span data-stu-id="547e0-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Add endpoint blade][cdn-add-endpoint]
3. <span data-ttu-id="547e0-166">Enter a **Name** for this CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="547e0-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="547e0-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="547e0-168">In the **Origin type** dropdown, select *Cloud service*.</span><span class="sxs-lookup"><span data-stu-id="547e0-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="547e0-169">In the **Origin hostname** dropdown, select your cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="547e0-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span><span class="sxs-lookup"><span data-stu-id="547e0-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="547e0-171">You must specify at least one protocol (HTTP or HTTPS).</span><span class="sxs-lookup"><span data-stu-id="547e0-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="547e0-172">Click the **Add** button to create the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="547e0-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span><span class="sxs-lookup"><span data-stu-id="547e0-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="547e0-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span><span class="sxs-lookup"><span data-stu-id="547e0-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN endpoint][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="547e0-176">The endpoint will not immediately be available for use.</span><span class="sxs-lookup"><span data-stu-id="547e0-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="547e0-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span><span class="sxs-lookup"><span data-stu-id="547e0-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="547e0-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="547e0-179">Test the CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="547e0-179">Test the CDN endpoint</span></span>
<span data-ttu-id="547e0-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>\*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="547e0-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>\*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="547e0-181">In my setup, this URL is:</span><span class="sxs-lookup"><span data-stu-id="547e0-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="547e0-182">Which corresponds to the following origin URL at the CDN endpoint:</span><span class="sxs-lookup"><span data-stu-id="547e0-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="547e0-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span><span class="sxs-lookup"><span data-stu-id="547e0-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="547e0-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="547e0-185">For example:</span><span class="sxs-lookup"><span data-stu-id="547e0-185">For example:</span></span>

* <span data-ttu-id="547e0-186">A .js file from the /Script path</span><span class="sxs-lookup"><span data-stu-id="547e0-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="547e0-187">Any content file from the /Content path</span><span class="sxs-lookup"><span data-stu-id="547e0-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="547e0-188">Any controller/action</span><span class="sxs-lookup"><span data-stu-id="547e0-188">Any controller/action</span></span>
* <span data-ttu-id="547e0-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span><span class="sxs-lookup"><span data-stu-id="547e0-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="547e0-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="547e0-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="547e0-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span><span class="sxs-lookup"><span data-stu-id="547e0-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="547e0-192">This does not mean, however, that it's always a good idea (or generally a good idea) to serve an entire cloud service through Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-192">This does not mean, however, that it's always a good idea (or generally a good idea) to serve an entire cloud service through Azure CDN.</span></span> <span data-ttu-id="547e0-193">Some of the caveats are:</span><span class="sxs-lookup"><span data-stu-id="547e0-193">Some of the caveats are:</span></span>

* <span data-ttu-id="547e0-194">This approach requires your entire site to be public, because Azure CDN cannot serve any private content at this time.</span><span class="sxs-lookup"><span data-stu-id="547e0-194">This approach requires your entire site to be public, because Azure CDN cannot serve any private content at this time.</span></span>
* <span data-ttu-id="547e0-195">If the CDN endpoint goes offline for any reason, whether scheduled maintenance or user error, your entire cloud service goes offline unless the customers can be redirected to the origin URL **http://*&lt;serviceName>*.cloudapp.net/**.</span><span class="sxs-lookup"><span data-stu-id="547e0-195">If the CDN endpoint goes offline for any reason, whether scheduled maintenance or user error, your entire cloud service goes offline unless the customers can be redirected to the origin URL **http://*&lt;serviceName>*.cloudapp.net/**.</span></span>
* <span data-ttu-id="547e0-196">Even with the custom Cache-Control settings (see [Configure caching options for static files in your cloud service](#caching)), a CDN endpoint does not improve the performance of highly-dynamic content.</span><span class="sxs-lookup"><span data-stu-id="547e0-196">Even with the custom Cache-Control settings (see [Configure caching options for static files in your cloud service](#caching)), a CDN endpoint does not improve the performance of highly-dynamic content.</span></span> <span data-ttu-id="547e0-197">If you tried to load the home page from your CDN endpoint as shown above, notice that it took at least 5 seconds to load the default home page the first time, which is a fairly simple page.</span><span class="sxs-lookup"><span data-stu-id="547e0-197">If you tried to load the home page from your CDN endpoint as shown above, notice that it took at least 5 seconds to load the default home page the first time, which is a fairly simple page.</span></span> <span data-ttu-id="547e0-198">Imagine what would happen to the client experience if this page contains dynamic content that must update every minute.</span><span class="sxs-lookup"><span data-stu-id="547e0-198">Imagine what would happen to the client experience if this page contains dynamic content that must update every minute.</span></span> <span data-ttu-id="547e0-199">Serving dynamic content from a CDN endpoint requires short cache expiration, which translates to frequent cache misses at the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-199">Serving dynamic content from a CDN endpoint requires short cache expiration, which translates to frequent cache misses at the CDN endpoint.</span></span> <span data-ttu-id="547e0-200">This hurts the performance of your cloud service and defeats the purpose of a CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-200">This hurts the performance of your cloud service and defeats the purpose of a CDN.</span></span>

<span data-ttu-id="547e0-201">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-201">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="547e0-202">To that end, you have already seen how to access individual content files from the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-202">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="547e0-203">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="547e0-203">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="547e0-204">Configure caching options for static files in your cloud service</span><span class="sxs-lookup"><span data-stu-id="547e0-204">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="547e0-205">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-205">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="547e0-206">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="547e0-206">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="547e0-207">The XML below configures the cache to expire in 3 days.</span><span class="sxs-lookup"><span data-stu-id="547e0-207">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="547e0-208">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span><span class="sxs-lookup"><span data-stu-id="547e0-208">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="547e0-209">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span><span class="sxs-lookup"><span data-stu-id="547e0-209">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="547e0-210">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span><span class="sxs-lookup"><span data-stu-id="547e0-210">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="547e0-211">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span><span class="sxs-lookup"><span data-stu-id="547e0-211">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="547e0-212">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="547e0-212">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="547e0-213">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span><span class="sxs-lookup"><span data-stu-id="547e0-213">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="547e0-214">Serve content from controller actions through Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-214">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="547e0-215">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-215">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="547e0-216">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="547e0-216">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="547e0-217">I will simply reproduce it here.</span><span class="sxs-lookup"><span data-stu-id="547e0-217">I will simply reproduce it here.</span></span>

<span data-ttu-id="547e0-218">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span><span class="sxs-lookup"><span data-stu-id="547e0-218">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="547e0-219">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span><span class="sxs-lookup"><span data-stu-id="547e0-219">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="547e0-220">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span><span class="sxs-lookup"><span data-stu-id="547e0-220">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="547e0-221">This is a good example of serving semi-dynamic content with Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-221">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="547e0-222">Follow the steps above to setup this controller action:</span><span class="sxs-lookup"><span data-stu-id="547e0-222">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="547e0-223">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span><span class="sxs-lookup"><span data-stu-id="547e0-223">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="547e0-224">Be sure to replace the highlighted portion with your CDN name.</span><span class="sxs-lookup"><span data-stu-id="547e0-224">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="547e0-225">Right-click in the default `Index()` action and select **Add View**.</span><span class="sxs-lookup"><span data-stu-id="547e0-225">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="547e0-226">Accept the settings below and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="547e0-226">Accept the settings below and click **Add**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="547e0-227">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span><span class="sxs-lookup"><span data-stu-id="547e0-227">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="547e0-228">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span><span class="sxs-lookup"><span data-stu-id="547e0-228">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="547e0-229">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span><span class="sxs-lookup"><span data-stu-id="547e0-229">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="547e0-230">When you click the link, you reach the following code:</span><span class="sxs-lookup"><span data-stu-id="547e0-230">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="547e0-231">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span><span class="sxs-lookup"><span data-stu-id="547e0-231">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="547e0-232">If it's running in the cloud service, then it will redirect to:</span><span class="sxs-lookup"><span data-stu-id="547e0-232">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="547e0-233">Which corresponds to the following origin URL at your CDN endpoint:</span><span class="sxs-lookup"><span data-stu-id="547e0-233">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="547e0-234">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span><span class="sxs-lookup"><span data-stu-id="547e0-234">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="547e0-235">The code below specify a cache expiration of 1 hour (3,600 seconds).</span><span class="sxs-lookup"><span data-stu-id="547e0-235">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="547e0-236">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span><span class="sxs-lookup"><span data-stu-id="547e0-236">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="547e0-237">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-237">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="547e0-238">Integrate ASP.NET bundling and minification with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-238">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="547e0-239">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span><span class="sxs-lookup"><span data-stu-id="547e0-239">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="547e0-240">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-240">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="547e0-241">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span><span class="sxs-lookup"><span data-stu-id="547e0-241">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="547e0-242">Great debug mode experience</span><span class="sxs-lookup"><span data-stu-id="547e0-242">Great debug mode experience</span></span>
* <span data-ttu-id="547e0-243">Streamlined deployment</span><span class="sxs-lookup"><span data-stu-id="547e0-243">Streamlined deployment</span></span>
* <span data-ttu-id="547e0-244">Immediate updates to clients for script/CSS version upgrades</span><span class="sxs-lookup"><span data-stu-id="547e0-244">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="547e0-245">Fallback mechanism when your CDN endpoint fails</span><span class="sxs-lookup"><span data-stu-id="547e0-245">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="547e0-246">Minimize code modification</span><span class="sxs-lookup"><span data-stu-id="547e0-246">Minimize code modification</span></span>

<span data-ttu-id="547e0-247">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span><span class="sxs-lookup"><span data-stu-id="547e0-247">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="547e0-248">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="547e0-248">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="547e0-249">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span><span class="sxs-lookup"><span data-stu-id="547e0-249">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="547e0-250">You should be able to find the following line of Razor code:</span><span class="sxs-lookup"><span data-stu-id="547e0-250">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="547e0-251">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span><span class="sxs-lookup"><span data-stu-id="547e0-251">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="547e0-252">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span><span class="sxs-lookup"><span data-stu-id="547e0-252">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="547e0-253">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span><span class="sxs-lookup"><span data-stu-id="547e0-253">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="547e0-254">It's a great feature to preserve with Azure CDN integration.</span><span class="sxs-lookup"><span data-stu-id="547e0-254">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="547e0-255">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="547e0-255">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="547e0-256">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="547e0-256">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="547e0-257">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span><span class="sxs-lookup"><span data-stu-id="547e0-257">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="547e0-258">To do this, replace the `RegisterBundles` method definition with the following code:</span><span class="sxs-lookup"><span data-stu-id="547e0-258">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="547e0-259">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-259">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="547e0-260">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span><span class="sxs-lookup"><span data-stu-id="547e0-260">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="547e0-261">For example, the first constructor in the code:</span><span class="sxs-lookup"><span data-stu-id="547e0-261">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="547e0-262">is the same as:</span><span class="sxs-lookup"><span data-stu-id="547e0-262">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="547e0-263">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span><span class="sxs-lookup"><span data-stu-id="547e0-263">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="547e0-264">However, note two important characteristics with this carefully crafted CDN URL:</span><span class="sxs-lookup"><span data-stu-id="547e0-264">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="547e0-265">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-265">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="547e0-266">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span><span class="sxs-lookup"><span data-stu-id="547e0-266">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="547e0-267">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="547e0-267">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="547e0-268">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span><span class="sxs-lookup"><span data-stu-id="547e0-268">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="547e0-269">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span><span class="sxs-lookup"><span data-stu-id="547e0-269">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="547e0-270">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span><span class="sxs-lookup"><span data-stu-id="547e0-270">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="547e0-271">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '\*'.</span><span class="sxs-lookup"><span data-stu-id="547e0-271">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '\*'.</span></span> <span data-ttu-id="547e0-272">For example:</span><span class="sxs-lookup"><span data-stu-id="547e0-272">For example:</span></span>
     
        <span data-ttu-id="547e0-273">[assembly: AssemblyVersion("1.0.0.\*")]</span><span class="sxs-lookup"><span data-stu-id="547e0-273">[assembly: AssemblyVersion("1.0.0.\*")]</span></span>
     
     <span data-ttu-id="547e0-274">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span><span class="sxs-lookup"><span data-stu-id="547e0-274">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="547e0-275">Republish the cloud service and access the home page.</span><span class="sxs-lookup"><span data-stu-id="547e0-275">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="547e0-276">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="547e0-276">View the HTML code for the page.</span></span> <span data-ttu-id="547e0-277">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="547e0-277">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="547e0-278">For example:</span><span class="sxs-lookup"><span data-stu-id="547e0-278">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="547e0-279">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span><span class="sxs-lookup"><span data-stu-id="547e0-279">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="547e0-280">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="547e0-280">View the HTML code for the page.</span></span> <span data-ttu-id="547e0-281">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="547e0-281">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="547e0-282">Fallback mechanism for CDN URLs</span><span class="sxs-lookup"><span data-stu-id="547e0-282">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="547e0-283">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="547e0-283">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="547e0-284">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span><span class="sxs-lookup"><span data-stu-id="547e0-284">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="547e0-285">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span><span class="sxs-lookup"><span data-stu-id="547e0-285">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="547e0-286">To use this property, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="547e0-286">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="547e0-287">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span><span class="sxs-lookup"><span data-stu-id="547e0-287">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="547e0-288">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span><span class="sxs-lookup"><span data-stu-id="547e0-288">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="547e0-289">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span><span class="sxs-lookup"><span data-stu-id="547e0-289">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="547e0-290">The expression needed to test each bundle differs according to the content.</span><span class="sxs-lookup"><span data-stu-id="547e0-290">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="547e0-291">For the default bundles above:</span><span class="sxs-lookup"><span data-stu-id="547e0-291">For the default bundles above:</span></span>
   
   * <span data-ttu-id="547e0-292">`window.jquery` is defined in jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="547e0-292">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="547e0-293">`$.validator` is defined in jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="547e0-293">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="547e0-294">`window.Modernizr` is defined in modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="547e0-294">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="547e0-295">`$.fn.modal` is defined in bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="547e0-295">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="547e0-296">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span><span class="sxs-lookup"><span data-stu-id="547e0-296">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="547e0-297">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span><span class="sxs-lookup"><span data-stu-id="547e0-297">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="547e0-298">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="547e0-298">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="547e0-299">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="547e0-299">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="547e0-300">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="547e0-300">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="547e0-301">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span><span class="sxs-lookup"><span data-stu-id="547e0-301">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="547e0-302">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span><span class="sxs-lookup"><span data-stu-id="547e0-302">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="547e0-303">Publish the cloud service again and access the home page.</span><span class="sxs-lookup"><span data-stu-id="547e0-303">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="547e0-304">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="547e0-304">View the HTML code for the page.</span></span> <span data-ttu-id="547e0-305">You should find injected scripts similar to the following:</span><span class="sxs-lookup"><span data-stu-id="547e0-305">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="547e0-306">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span><span class="sxs-lookup"><span data-stu-id="547e0-306">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="547e0-307">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span><span class="sxs-lookup"><span data-stu-id="547e0-307">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="547e0-308">More Information</span><span class="sxs-lookup"><span data-stu-id="547e0-308">More Information</span></span>
* [<span data-ttu-id="547e0-309">Overview of the Azure Content Delivery Network (CDN)</span><span class="sxs-lookup"><span data-stu-id="547e0-309">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="547e0-310">Using Azure CDN</span><span class="sxs-lookup"><span data-stu-id="547e0-310">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="547e0-311">ASP.NET Bundling and Minification</span><span class="sxs-lookup"><span data-stu-id="547e0-311">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png

















