---
title: Getting started with Azure CDN | Microsoft Docs
description: This topic shows how to enable the Azure Content Delivery Network (CDN). The tutorial walks through the creation of a new CDN profile and endpoint.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6aaa66d5cfbabb598d572b437d6e0477151a3ac0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562943"
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="f0c27-104">Getting started with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0c27-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="f0c27-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span><span class="sxs-lookup"><span data-stu-id="f0c27-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0c27-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0c27-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="f0c27-107">Create a new CDN profile</span><span class="sxs-lookup"><span data-stu-id="f0c27-107">Create a new CDN profile</span></span>
<span data-ttu-id="f0c27-108">A CDN profile is a collection of CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="f0c27-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="f0c27-109">Each profile contains one or more CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="f0c27-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="f0c27-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span><span class="sxs-lookup"><span data-stu-id="f0c27-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="f0c27-111">By default, a single Azure subscription is limited to eight CDN profiles.</span><span class="sxs-lookup"><span data-stu-id="f0c27-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="f0c27-112">Each CDN profile is limited to ten CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="f0c27-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="f0c27-113">CDN pricing is applied at the CDN profile level.</span><span class="sxs-lookup"><span data-stu-id="f0c27-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="f0c27-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span><span class="sxs-lookup"><span data-stu-id="f0c27-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="f0c27-115">Create a new CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="f0c27-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="f0c27-116">**To create a new CDN endpoint**</span><span class="sxs-lookup"><span data-stu-id="f0c27-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="f0c27-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="f0c27-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="f0c27-118">You may have pinned it to the dashboard in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f0c27-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="f0c27-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span><span class="sxs-lookup"><span data-stu-id="f0c27-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="f0c27-120">The CDN profile blade appears.</span><span class="sxs-lookup"><span data-stu-id="f0c27-120">The CDN profile blade appears.</span></span>
   
    ![CDN profile][cdn-profile-settings]
2. <span data-ttu-id="f0c27-122">Click the **Add Endpoint** button.</span><span class="sxs-lookup"><span data-stu-id="f0c27-122">Click the **Add Endpoint** button.</span></span>
   
    ![Add endpoint button][cdn-new-endpoint-button]
   
    <span data-ttu-id="f0c27-124">The **Add an endpoint** blade appears.</span><span class="sxs-lookup"><span data-stu-id="f0c27-124">The **Add an endpoint** blade appears.</span></span>
   
    ![Add endpoint blade][cdn-add-endpoint]
3. <span data-ttu-id="f0c27-126">Enter a **Name** for this CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="f0c27-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="f0c27-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="f0c27-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="f0c27-128">In the **Origin type** dropdown, select your origin type.</span><span class="sxs-lookup"><span data-stu-id="f0c27-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="f0c27-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span><span class="sxs-lookup"><span data-stu-id="f0c27-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![CDN origin type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="f0c27-131">In the **Origin hostname** dropdown, select or type your origin domain.</span><span class="sxs-lookup"><span data-stu-id="f0c27-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="f0c27-132">The dropdown will list all available origins of the type you specified in step 4.</span><span class="sxs-lookup"><span data-stu-id="f0c27-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="f0c27-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span><span class="sxs-lookup"><span data-stu-id="f0c27-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="f0c27-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span><span class="sxs-lookup"><span data-stu-id="f0c27-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="f0c27-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span><span class="sxs-lookup"><span data-stu-id="f0c27-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f0c27-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span><span class="sxs-lookup"><span data-stu-id="f0c27-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="f0c27-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span><span class="sxs-lookup"><span data-stu-id="f0c27-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="f0c27-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span><span class="sxs-lookup"><span data-stu-id="f0c27-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="f0c27-139">At least one protocol (HTTP or HTTPS) must be selected.</span><span class="sxs-lookup"><span data-stu-id="f0c27-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f0c27-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span><span class="sxs-lookup"><span data-stu-id="f0c27-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="f0c27-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span><span class="sxs-lookup"><span data-stu-id="f0c27-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="f0c27-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span><span class="sxs-lookup"><span data-stu-id="f0c27-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="f0c27-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0c27-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="f0c27-144">Accessing CDN content using HTTPS has the following constraints:</span><span class="sxs-lookup"><span data-stu-id="f0c27-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="f0c27-145">You must use the SSL certificate provided by the CDN.</span><span class="sxs-lookup"><span data-stu-id="f0c27-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="f0c27-146">Third party certificates are not supported.</span><span class="sxs-lookup"><span data-stu-id="f0c27-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="f0c27-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span><span class="sxs-lookup"><span data-stu-id="f0c27-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="f0c27-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span><span class="sxs-lookup"><span data-stu-id="f0c27-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="f0c27-149">Click the **Add** button to create the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="f0c27-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="f0c27-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span><span class="sxs-lookup"><span data-stu-id="f0c27-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="f0c27-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span><span class="sxs-lookup"><span data-stu-id="f0c27-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![CDN endpoint][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="f0c27-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span><span class="sxs-lookup"><span data-stu-id="f0c27-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="f0c27-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span><span class="sxs-lookup"><span data-stu-id="f0c27-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="f0c27-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span><span class="sxs-lookup"><span data-stu-id="f0c27-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="f0c27-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span><span class="sxs-lookup"><span data-stu-id="f0c27-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="f0c27-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f0c27-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="f0c27-158">See Also</span><span class="sxs-lookup"><span data-stu-id="f0c27-158">See Also</span></span>
* [<span data-ttu-id="f0c27-159">Controlling caching behavior of requests with query strings</span><span class="sxs-lookup"><span data-stu-id="f0c27-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="f0c27-160">How to Map CDN Content to a Custom Domain</span><span class="sxs-lookup"><span data-stu-id="f0c27-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="f0c27-161">Pre-load assets on an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="f0c27-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="f0c27-162">Purge an Azure CDN Endpoint</span><span class="sxs-lookup"><span data-stu-id="f0c27-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="f0c27-163">Troubleshooting CDN endpoints returning 404 statuses</span><span class="sxs-lookup"><span data-stu-id="f0c27-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-new-endpoint/cdn-endpoint-success.png





