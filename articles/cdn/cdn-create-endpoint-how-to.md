---
title: Create an Azure CDN endpoint | Microsoft Docs
description: This article shows how to create a new Azure Content Delivery Network (CDN) endpoint, including advanced settings.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: v-deasim
ms.custom: mvc
ms.openlocfilehash: 16a939c69d9ed9be597306765f316ffe32db6665
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968650"
---
# <a name="create-an-azure-cdn-endpoint"></a><span data-ttu-id="c440c-103">Create an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="c440c-103">Create an Azure CDN endpoint</span></span>
<span data-ttu-id="c440c-104">This article describes all the settings for creating an [Azure Content Delivery Network (CDN)](cdn-overview.md) endpoint in an existing CDN profile.</span><span class="sxs-lookup"><span data-stu-id="c440c-104">This article describes all the settings for creating an [Azure Content Delivery Network (CDN)](cdn-overview.md) endpoint in an existing CDN profile.</span></span> <span data-ttu-id="c440c-105">After you've created a profile and an endpoint, you can start delivering content to your customers.</span><span class="sxs-lookup"><span data-stu-id="c440c-105">After you've created a profile and an endpoint, you can start delivering content to your customers.</span></span> <span data-ttu-id="c440c-106">For a quickstart on creating a profile and endpoint, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="c440c-106">For a quickstart on creating a profile and endpoint, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c440c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c440c-107">Prerequisites</span></span>
<span data-ttu-id="c440c-108">Before you can create a CDN endpoint, you must have created at least one CDN profile, which can contain one or more CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="c440c-108">Before you can create a CDN endpoint, you must have created at least one CDN profile, which can contain one or more CDN endpoints.</span></span> <span data-ttu-id="c440c-109">To organize your CDN endpoints by internet domain, web application, or some other criteria, you can use multiple profiles.</span><span class="sxs-lookup"><span data-stu-id="c440c-109">To organize your CDN endpoints by internet domain, web application, or some other criteria, you can use multiple profiles.</span></span> <span data-ttu-id="c440c-110">Because CDN pricing is applied at the CDN profile level, you must create multiple CDN profiles if you want to use a mix of Azure CDN pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="c440c-110">Because CDN pricing is applied at the CDN profile level, you must create multiple CDN profiles if you want to use a mix of Azure CDN pricing tiers.</span></span> <span data-ttu-id="c440c-111">To create a CDN profile, see [Create a new CDN profile](cdn-create-new-endpoint.md#create-a-new-cdn-profile).</span><span class="sxs-lookup"><span data-stu-id="c440c-111">To create a CDN profile, see [Create a new CDN profile](cdn-create-new-endpoint.md#create-a-new-cdn-profile).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="c440c-112">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c440c-112">Log in to the Azure portal</span></span>
<span data-ttu-id="c440c-113">Log in to the [Azure portal](https://portal.azure.com) with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="c440c-113">Log in to the [Azure portal](https://portal.azure.com) with your Azure account.</span></span>

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="c440c-114">Create a new CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="c440c-114">Create a new CDN endpoint</span></span>

1. <span data-ttu-id="c440c-115">In the [Azure portal](https://portal.azure.com), navigate to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="c440c-115">In the [Azure portal](https://portal.azure.com), navigate to your CDN profile.</span></span> <span data-ttu-id="c440c-116">You may have pinned it to the dashboard in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c440c-116">You may have pinned it to the dashboard in the previous step.</span></span> <span data-ttu-id="c440c-117">If not, you can find it by selecting **All services**, then selecting **CDN profiles**.</span><span class="sxs-lookup"><span data-stu-id="c440c-117">If not, you can find it by selecting **All services**, then selecting **CDN profiles**.</span></span> <span data-ttu-id="c440c-118">In the **CDN profiles** pane, select the profile to which you plan to add your endpoint.</span><span class="sxs-lookup"><span data-stu-id="c440c-118">In the **CDN profiles** pane, select the profile to which you plan to add your endpoint.</span></span> 
   
    <span data-ttu-id="c440c-119">The CDN profile pane appears.</span><span class="sxs-lookup"><span data-stu-id="c440c-119">The CDN profile pane appears.</span></span>

2. <span data-ttu-id="c440c-120">Select **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="c440c-120">Select **Endpoint**.</span></span>
   
    ![CDN select endpoint](./media/cdn-create-endpoint-how-to/cdn-select-endpoint.png)
   
    <span data-ttu-id="c440c-122">The **Add an endpoint** page appears.</span><span class="sxs-lookup"><span data-stu-id="c440c-122">The **Add an endpoint** page appears.</span></span>
   
    ![Add endpoint page](./media/cdn-create-endpoint-how-to/cdn-add-endpoint-page.png)

3. <span data-ttu-id="c440c-124">For **Name**, enter a unique name for the new CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="c440c-124">For **Name**, enter a unique name for the new CDN endpoint.</span></span> <span data-ttu-id="c440c-125">This name is used to access your cached resources at the domain _<endpointname>_.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="c440c-125">This name is used to access your cached resources at the domain _<endpointname>_.azureedge.net.</span></span>

4. <span data-ttu-id="c440c-126">For **Origin type**, choose one of the following origin types:</span><span class="sxs-lookup"><span data-stu-id="c440c-126">For **Origin type**, choose one of the following origin types:</span></span> 
   - <span data-ttu-id="c440c-127">**Storage** for Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c440c-127">**Storage** for Azure Storage</span></span>
   - <span data-ttu-id="c440c-128">**Cloud service** for Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="c440c-128">**Cloud service** for Azure Cloud Services</span></span>
   - <span data-ttu-id="c440c-129">**Web App** for Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="c440c-129">**Web App** for Azure Web Apps</span></span>
   - <span data-ttu-id="c440c-130">**Custom origin** for any other publicly accessible origin web server (hosted in Azure or elsewhere)</span><span class="sxs-lookup"><span data-stu-id="c440c-130">**Custom origin** for any other publicly accessible origin web server (hosted in Azure or elsewhere)</span></span>

5. <span data-ttu-id="c440c-131">For **Origin hostname**, select or enter your origin server domain.</span><span class="sxs-lookup"><span data-stu-id="c440c-131">For **Origin hostname**, select or enter your origin server domain.</span></span> <span data-ttu-id="c440c-132">The drop-down lists all available origin servers of the type you specified in step 4.</span><span class="sxs-lookup"><span data-stu-id="c440c-132">The drop-down lists all available origin servers of the type you specified in step 4.</span></span> <span data-ttu-id="c440c-133">If you selected **Custom origin** as your origin type, enter the domain of your custom origin server.</span><span class="sxs-lookup"><span data-stu-id="c440c-133">If you selected **Custom origin** as your origin type, enter the domain of your custom origin server.</span></span>
    
6. <span data-ttu-id="c440c-134">For **Origin path**, enter the path to the resources that you want to cache.</span><span class="sxs-lookup"><span data-stu-id="c440c-134">For **Origin path**, enter the path to the resources that you want to cache.</span></span> <span data-ttu-id="c440c-135">To allow caching of any resource at the domain you specified in step 5, leave this setting blank.</span><span class="sxs-lookup"><span data-stu-id="c440c-135">To allow caching of any resource at the domain you specified in step 5, leave this setting blank.</span></span>
    
7. <span data-ttu-id="c440c-136">For **Origin host header**, enter the host header you want Azure CDN to send with each request, or leave the default.</span><span class="sxs-lookup"><span data-stu-id="c440c-136">For **Origin host header**, enter the host header you want Azure CDN to send with each request, or leave the default.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c440c-137">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span><span class="sxs-lookup"><span data-stu-id="c440c-137">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="c440c-138">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span><span class="sxs-lookup"><span data-stu-id="c440c-138">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
    
8. <span data-ttu-id="c440c-139">For **Protocol** and **Origin port**, specify the protocols and ports to use to access your resources at the origin server.</span><span class="sxs-lookup"><span data-stu-id="c440c-139">For **Protocol** and **Origin port**, specify the protocols and ports to use to access your resources at the origin server.</span></span> <span data-ttu-id="c440c-140">At least one protocol (HTTP or HTTPS) must be selected.</span><span class="sxs-lookup"><span data-stu-id="c440c-140">At least one protocol (HTTP or HTTPS) must be selected.</span></span> <span data-ttu-id="c440c-141">Use the CDN-provided domain (_<endpointname>_.azureedge.net) to access HTTPS content.</span><span class="sxs-lookup"><span data-stu-id="c440c-141">Use the CDN-provided domain (_<endpointname>_.azureedge.net) to access HTTPS content.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c440c-142">The **Origin port** value determines only the port the endpoint uses to retrieve information from the origin server.</span><span class="sxs-lookup"><span data-stu-id="c440c-142">The **Origin port** value determines only the port the endpoint uses to retrieve information from the origin server.</span></span> <span data-ttu-id="c440c-143">The endpoint itself is available only to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port** value.</span><span class="sxs-lookup"><span data-stu-id="c440c-143">The endpoint itself is available only to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port** value.</span></span>  
   > 
   > <span data-ttu-id="c440c-144">Endpoints in **Azure CDN from Akamai** profiles do not allow the full TCP port range for origin ports.</span><span class="sxs-lookup"><span data-stu-id="c440c-144">Endpoints in **Azure CDN from Akamai** profiles do not allow the full TCP port range for origin ports.</span></span> <span data-ttu-id="c440c-145">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="c440c-145">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="c440c-146">HTTPS support for Azure CDN custom domains is not supported on **Azure CDN from Akamai** products.</span><span class="sxs-lookup"><span data-stu-id="c440c-146">HTTPS support for Azure CDN custom domains is not supported on **Azure CDN from Akamai** products.</span></span> <span data-ttu-id="c440c-147">For more information, see [Configure HTTPS on an Azure CDN custom domain](cdn-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="c440c-147">For more information, see [Configure HTTPS on an Azure CDN custom domain](cdn-custom-ssl.md).</span></span>
    
9. <span data-ttu-id="c440c-148">For **Optimized for**, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span><span class="sxs-lookup"><span data-stu-id="c440c-148">For **Optimized for**, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span></span> <span data-ttu-id="c440c-149">For more information, see [Optimize Azure CDN for the type of content delivery](cdn-optimization-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c440c-149">For more information, see [Optimize Azure CDN for the type of content delivery](cdn-optimization-overview.md).</span></span>

    <span data-ttu-id="c440c-150">The following optimization type settings are supported, according to profile type:</span><span class="sxs-lookup"><span data-stu-id="c440c-150">The following optimization type settings are supported, according to profile type:</span></span>
    - <span data-ttu-id="c440c-151">**Azure CDN Standard from Microsoft** profiles:</span><span class="sxs-lookup"><span data-stu-id="c440c-151">**Azure CDN Standard from Microsoft** profiles:</span></span>
       - [<span data-ttu-id="c440c-152">**General web delivery**</span><span class="sxs-lookup"><span data-stu-id="c440c-152">**General web delivery**</span></span>](cdn-optimization-overview.md#general-web-delivery)

    - <span data-ttu-id="c440c-153">**Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles:</span><span class="sxs-lookup"><span data-stu-id="c440c-153">**Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles:</span></span>
       - [<span data-ttu-id="c440c-154">**General web delivery**</span><span class="sxs-lookup"><span data-stu-id="c440c-154">**General web delivery**</span></span>](cdn-optimization-overview.md#general-web-delivery)
       - [<span data-ttu-id="c440c-155">**Dynamic site acceleration**</span><span class="sxs-lookup"><span data-stu-id="c440c-155">**Dynamic site acceleration**</span></span>](cdn-optimization-overview.md#dynamic-site-acceleration)

    - <span data-ttu-id="c440c-156">**Azure CDN Standard from Akamai** profiles:</span><span class="sxs-lookup"><span data-stu-id="c440c-156">**Azure CDN Standard from Akamai** profiles:</span></span>
       - [<span data-ttu-id="c440c-157">**General web delivery**</span><span class="sxs-lookup"><span data-stu-id="c440c-157">**General web delivery**</span></span>](cdn-optimization-overview.md#general-web-delivery)
       - [<span data-ttu-id="c440c-158">**General media streaming**</span><span class="sxs-lookup"><span data-stu-id="c440c-158">**General media streaming**</span></span>](cdn-optimization-overview.md#general-media-streaming)
       - [<span data-ttu-id="c440c-159">**Video on demand media streaming**</span><span class="sxs-lookup"><span data-stu-id="c440c-159">**Video on demand media streaming**</span></span>](cdn-optimization-overview.md#video-on-demand-media-streaming)
       - [<span data-ttu-id="c440c-160">**Large file download**</span><span class="sxs-lookup"><span data-stu-id="c440c-160">**Large file download**</span></span>](cdn-optimization-overview.md#large-file-download)
       - [<span data-ttu-id="c440c-161">**Dynamic site acceleration**</span><span class="sxs-lookup"><span data-stu-id="c440c-161">**Dynamic site acceleration**</span></span>](cdn-optimization-overview.md#dynamic-site-acceleration)

10. <span data-ttu-id="c440c-162">Select **Add** to create the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="c440c-162">Select **Add** to create the new endpoint.</span></span>
   
    <span data-ttu-id="c440c-163">After the endpoint is created, it appears in the list of endpoints for the profile.</span><span class="sxs-lookup"><span data-stu-id="c440c-163">After the endpoint is created, it appears in the list of endpoints for the profile.</span></span>
    
    ![CDN endpoint](./media/cdn-create-new-endpoint/cdn-endpoint-success.png)
    
    <span data-ttu-id="c440c-165">Because it takes time for the registration to propagate, the endpoint isn't immediately available for use:</span><span class="sxs-lookup"><span data-stu-id="c440c-165">Because it takes time for the registration to propagate, the endpoint isn't immediately available for use:</span></span> 
    - <span data-ttu-id="c440c-166">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="c440c-166">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span></span> 
    - <span data-ttu-id="c440c-167">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span><span class="sxs-lookup"><span data-stu-id="c440c-167">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span></span> 
    - <span data-ttu-id="c440c-168">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes within 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="c440c-168">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes within 90 minutes.</span></span> 
   
    <span data-ttu-id="c440c-169">If you attempt to use the CDN domain name before the endpoint configuration has propagated to the point-of-presence (POP) servers, you might receive an HTTP 404 response status.</span><span class="sxs-lookup"><span data-stu-id="c440c-169">If you attempt to use the CDN domain name before the endpoint configuration has propagated to the point-of-presence (POP) servers, you might receive an HTTP 404 response status.</span></span> <span data-ttu-id="c440c-170">If it's been several hours since you created your endpoint and you're still receiving a 404 response status, see [Troubleshooting Azure CDN endpoints that return a 404 status code](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="c440c-170">If it's been several hours since you created your endpoint and you're still receiving a 404 response status, see [Troubleshooting Azure CDN endpoints that return a 404 status code](cdn-troubleshoot-endpoint.md).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="c440c-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c440c-171">Clean up resources</span></span>
<span data-ttu-id="c440c-172">To delete an endpoint when it is no longer needed, select it and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="c440c-172">To delete an endpoint when it is no longer needed, select it and then select **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c440c-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="c440c-173">Next steps</span></span>
<span data-ttu-id="c440c-174">To learn about custom domains, continue to the tutorial for adding a custom domain to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="c440c-174">To learn about custom domains, continue to the tutorial for adding a custom domain to your CDN endpoint.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c440c-175">Add a custom domain</span><span class="sxs-lookup"><span data-stu-id="c440c-175">Add a custom domain</span></span>](cdn-map-content-to-custom-domain.md)


