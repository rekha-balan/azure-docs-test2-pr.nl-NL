---
title: Tutorial - Add a custom domain to your Azure CDN endpoint | Microsoft Docs
description: In this tutorial, you map Azure CDN endpoint content to a custom domain.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/11/2018
ms.author: v-deasim
ms.custom: mvc
ms.openlocfilehash: 30dbe6590cc1d70dfc026330a09645c86be24288
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790626"
---
# <a name="tutorial-add-a-custom-domain-to-your-azure-cdn-endpoint"></a><span data-ttu-id="49885-103">Tutorial: Add a custom domain to your Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="49885-103">Tutorial: Add a custom domain to your Azure CDN endpoint</span></span>
<span data-ttu-id="49885-104">This tutorial shows how to add a custom domain to an Azure Content Delivery Network (CDN) endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-104">This tutorial shows how to add a custom domain to an Azure Content Delivery Network (CDN) endpoint.</span></span> <span data-ttu-id="49885-105">When you use a CDN endpoint to deliver content, a custom domain is necessary if you would like your own domain name to be visible in your CDN URL.</span><span class="sxs-lookup"><span data-stu-id="49885-105">When you use a CDN endpoint to deliver content, a custom domain is necessary if you would like your own domain name to be visible in your CDN URL.</span></span> <span data-ttu-id="49885-106">Having a visible domain name can be convenient for your customers and useful for branding purposes.</span><span class="sxs-lookup"><span data-stu-id="49885-106">Having a visible domain name can be convenient for your customers and useful for branding purposes.</span></span> 

<span data-ttu-id="49885-107">After you create a CDN endpoint in your profile, the endpoint name, which is a subdomain of azureedge.net, is included in the URL for delivering CDN content by default (for example, https:\//contoso.azureedge.net/photo.png).</span><span class="sxs-lookup"><span data-stu-id="49885-107">After you create a CDN endpoint in your profile, the endpoint name, which is a subdomain of azureedge.net, is included in the URL for delivering CDN content by default (for example, https:\//contoso.azureedge.net/photo.png).</span></span> <span data-ttu-id="49885-108">For your convenience, Azure CDN provides the option of associating a custom domain with a CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-108">For your convenience, Azure CDN provides the option of associating a custom domain with a CDN endpoint.</span></span> <span data-ttu-id="49885-109">With this option, you deliver your content with a custom domain in your URL instead of an endpoint name (for example, https:\//www.contoso.com/photo.png).</span><span class="sxs-lookup"><span data-stu-id="49885-109">With this option, you deliver your content with a custom domain in your URL instead of an endpoint name (for example, https:\//www.contoso.com/photo.png).</span></span> 

<span data-ttu-id="49885-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="49885-110">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> - <span data-ttu-id="49885-111">Create a CNAME DNS record.</span><span class="sxs-lookup"><span data-stu-id="49885-111">Create a CNAME DNS record.</span></span>
> - <span data-ttu-id="49885-112">Associate the custom domain with your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-112">Associate the custom domain with your CDN endpoint.</span></span>
> - <span data-ttu-id="49885-113">Verify the custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-113">Verify the custom domain.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="49885-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49885-114">Prerequisites</span></span>

<span data-ttu-id="49885-115">Before you can complete the steps in this tutorial, you must first create a CDN profile and at least one CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-115">Before you can complete the steps in this tutorial, you must first create a CDN profile and at least one CDN endpoint.</span></span> <span data-ttu-id="49885-116">For more information, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="49885-116">For more information, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span></span>

<span data-ttu-id="49885-117">If you do not already have a custom domain, you must first purchase one with a domain provider.</span><span class="sxs-lookup"><span data-stu-id="49885-117">If you do not already have a custom domain, you must first purchase one with a domain provider.</span></span> <span data-ttu-id="49885-118">For example, see [Buy a custom domain name](https://docs.microsoft.com/azure/app-service/custom-dns-web-site-buydomains-web-app).</span><span class="sxs-lookup"><span data-stu-id="49885-118">For example, see [Buy a custom domain name](https://docs.microsoft.com/azure/app-service/custom-dns-web-site-buydomains-web-app).</span></span>

<span data-ttu-id="49885-119">If you are using Azure to host your [DNS domains](https://docs.microsoft.com/azure/dns/dns-overview), you must delegate the domain provider's domain name system (DNS) to an Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="49885-119">If you are using Azure to host your [DNS domains](https://docs.microsoft.com/azure/dns/dns-overview), you must delegate the domain provider's domain name system (DNS) to an Azure DNS.</span></span> <span data-ttu-id="49885-120">For more information, see [Delegate a domain to Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns).</span><span class="sxs-lookup"><span data-stu-id="49885-120">For more information, see [Delegate a domain to Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns).</span></span> <span data-ttu-id="49885-121">Otherwise, if you are using a domain provider to handle your DNS domain, proceed to [Create a CNAME DNS record](#create-a-cname-dns-record).</span><span class="sxs-lookup"><span data-stu-id="49885-121">Otherwise, if you are using a domain provider to handle your DNS domain, proceed to [Create a CNAME DNS record](#create-a-cname-dns-record).</span></span>


## <a name="create-a-cname-dns-record"></a><span data-ttu-id="49885-122">Create a CNAME DNS record</span><span class="sxs-lookup"><span data-stu-id="49885-122">Create a CNAME DNS record</span></span>

<span data-ttu-id="49885-123">Before you can use a custom domain with an Azure CDN endpoint, you must first create a canonical name (CNAME) record with your domain provider to point to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-123">Before you can use a custom domain with an Azure CDN endpoint, you must first create a canonical name (CNAME) record with your domain provider to point to your CDN endpoint.</span></span> <span data-ttu-id="49885-124">A CNAME record is a type of DNS record that maps a source domain name to a destination domain name.</span><span class="sxs-lookup"><span data-stu-id="49885-124">A CNAME record is a type of DNS record that maps a source domain name to a destination domain name.</span></span> <span data-ttu-id="49885-125">For Azure CDN, the source domain name is your custom domain name and the destination domain name is your CDN endpoint hostname.</span><span class="sxs-lookup"><span data-stu-id="49885-125">For Azure CDN, the source domain name is your custom domain name and the destination domain name is your CDN endpoint hostname.</span></span> <span data-ttu-id="49885-126">After Azure CDN verifies the CNAME record that you create, traffic addressed to the source custom domain (such as www.contoso.com) is routed to the specified destination CDN endpoint hostname (such as contoso.azureedge.net).</span><span class="sxs-lookup"><span data-stu-id="49885-126">After Azure CDN verifies the CNAME record that you create, traffic addressed to the source custom domain (such as www.contoso.com) is routed to the specified destination CDN endpoint hostname (such as contoso.azureedge.net).</span></span> 

<span data-ttu-id="49885-127">A custom domain and its subdomain can be associated with only a single endpoint at a time.</span><span class="sxs-lookup"><span data-stu-id="49885-127">A custom domain and its subdomain can be associated with only a single endpoint at a time.</span></span> <span data-ttu-id="49885-128">However, you can use different subdomains from the same custom domain for different Azure service endpoints by using multiple CNAME records.</span><span class="sxs-lookup"><span data-stu-id="49885-128">However, you can use different subdomains from the same custom domain for different Azure service endpoints by using multiple CNAME records.</span></span> <span data-ttu-id="49885-129">You can also map a custom domain with different subdomains to the same CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-129">You can also map a custom domain with different subdomains to the same CDN endpoint.</span></span>


## <a name="map-the-temporary-cdnverify-subdomain"></a><span data-ttu-id="49885-130">Map the temporary cdnverify subdomain</span><span class="sxs-lookup"><span data-stu-id="49885-130">Map the temporary cdnverify subdomain</span></span>

<span data-ttu-id="49885-131">When you map an existing domain that is in production, there are special considerations.</span><span class="sxs-lookup"><span data-stu-id="49885-131">When you map an existing domain that is in production, there are special considerations.</span></span> <span data-ttu-id="49885-132">While you are registering your custom domain in the Azure portal, a brief period of downtime for the domain can occur.</span><span class="sxs-lookup"><span data-stu-id="49885-132">While you are registering your custom domain in the Azure portal, a brief period of downtime for the domain can occur.</span></span> <span data-ttu-id="49885-133">To avoid interruption of web traffic, first map your custom domain to your CDN endpoint hostname with the Azure cdnverify subdomain to create a temporary CNAME mapping.</span><span class="sxs-lookup"><span data-stu-id="49885-133">To avoid interruption of web traffic, first map your custom domain to your CDN endpoint hostname with the Azure cdnverify subdomain to create a temporary CNAME mapping.</span></span> <span data-ttu-id="49885-134">With this method, users can access your domain without interruption while the DNS mapping occurs.</span><span class="sxs-lookup"><span data-stu-id="49885-134">With this method, users can access your domain without interruption while the DNS mapping occurs.</span></span> 

<span data-ttu-id="49885-135">Otherwise, if you are using your custom domain for the first time and no production traffic is running on it, you can directly map your custom domain to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-135">Otherwise, if you are using your custom domain for the first time and no production traffic is running on it, you can directly map your custom domain to your CDN endpoint.</span></span> <span data-ttu-id="49885-136">Proceed to [Map the permanent custom domain](#map-the-permanent-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="49885-136">Proceed to [Map the permanent custom domain](#map-the-permanent-custom-domain).</span></span>

<span data-ttu-id="49885-137">To create a CNAME record with the cdnverify subdomain:</span><span class="sxs-lookup"><span data-stu-id="49885-137">To create a CNAME record with the cdnverify subdomain:</span></span>

1. <span data-ttu-id="49885-138">Sign in to the web site of the domain provider for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-138">Sign in to the web site of the domain provider for your custom domain.</span></span>

2. <span data-ttu-id="49885-139">Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name server management**.</span><span class="sxs-lookup"><span data-stu-id="49885-139">Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name server management**.</span></span> 

3. <span data-ttu-id="49885-140">Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names may vary):</span><span class="sxs-lookup"><span data-stu-id="49885-140">Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names may vary):</span></span>

    | <span data-ttu-id="49885-141">Source</span><span class="sxs-lookup"><span data-stu-id="49885-141">Source</span></span>                    | <span data-ttu-id="49885-142">Type</span><span class="sxs-lookup"><span data-stu-id="49885-142">Type</span></span>  | <span data-ttu-id="49885-143">Destination</span><span class="sxs-lookup"><span data-stu-id="49885-143">Destination</span></span>                     |
    |---------------------------|-------|---------------------------------|
    | <span data-ttu-id="49885-144">cdnverify.www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="49885-144">cdnverify.www.contoso.com</span></span> | <span data-ttu-id="49885-145">CNAME</span><span class="sxs-lookup"><span data-stu-id="49885-145">CNAME</span></span> | <span data-ttu-id="49885-146">cdnverify.contoso.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="49885-146">cdnverify.contoso.azureedge.net</span></span> |

    - <span data-ttu-id="49885-147">Source: Enter your custom domain name, including the cdnverify subdomain, in the following format: cdnverify._&lt;custom domain name&gt;.</span><span class="sxs-lookup"><span data-stu-id="49885-147">Source: Enter your custom domain name, including the cdnverify subdomain, in the following format: cdnverify._&lt;custom domain name&gt;.</span></span> <span data-ttu-id="49885-148">For example, cdnverify.www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="49885-148">For example, cdnverify.www.contoso.com.</span></span>

    - <span data-ttu-id="49885-149">Type: Enter *CNAME*.</span><span class="sxs-lookup"><span data-stu-id="49885-149">Type: Enter *CNAME*.</span></span>

    - <span data-ttu-id="49885-150">Destination: Enter your CDN endpoint hostname, including the cdnverify subdomain, in the following format: cdnverify._&lt;endpoint name&gt;_.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-150">Destination: Enter your CDN endpoint hostname, including the cdnverify subdomain, in the following format: cdnverify._&lt;endpoint name&gt;_.azureedge.net.</span></span> <span data-ttu-id="49885-151">For example, cdnverify.contoso.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-151">For example, cdnverify.contoso.azureedge.net.</span></span>

4. <span data-ttu-id="49885-152">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="49885-152">Save your changes.</span></span>

<span data-ttu-id="49885-153">For example, the procedure for the GoDaddy domain registrar is as follows:</span><span class="sxs-lookup"><span data-stu-id="49885-153">For example, the procedure for the GoDaddy domain registrar is as follows:</span></span>

1. <span data-ttu-id="49885-154">Sign in and select the custom domain you want to use.</span><span class="sxs-lookup"><span data-stu-id="49885-154">Sign in and select the custom domain you want to use.</span></span>

2. <span data-ttu-id="49885-155">In the Domains section, select **Manage All**, then select **DNS** | **Manage Zones**.</span><span class="sxs-lookup"><span data-stu-id="49885-155">In the Domains section, select **Manage All**, then select **DNS** | **Manage Zones**.</span></span>

3. <span data-ttu-id="49885-156">For **Domain Name**, enter your custom domain, then select **Search**.</span><span class="sxs-lookup"><span data-stu-id="49885-156">For **Domain Name**, enter your custom domain, then select **Search**.</span></span>

4. <span data-ttu-id="49885-157">From the **DNS Management** page, select **Add**, then select **CNAME** in the **Type** list.</span><span class="sxs-lookup"><span data-stu-id="49885-157">From the **DNS Management** page, select **Add**, then select **CNAME** in the **Type** list.</span></span>

5. <span data-ttu-id="49885-158">Complete the following fields of the CNAME entry:</span><span class="sxs-lookup"><span data-stu-id="49885-158">Complete the following fields of the CNAME entry:</span></span>

    ![CNAME entry](./media/cdn-map-content-to-custom-domain/cdn-cdnverify-cname-entry.png)

    - <span data-ttu-id="49885-160">Type: Leave *CNAME* selected.</span><span class="sxs-lookup"><span data-stu-id="49885-160">Type: Leave *CNAME* selected.</span></span>

    - <span data-ttu-id="49885-161">Host: Enter the subdomain of your custom domain to use, including the cdnverify subdomain name.</span><span class="sxs-lookup"><span data-stu-id="49885-161">Host: Enter the subdomain of your custom domain to use, including the cdnverify subdomain name.</span></span> <span data-ttu-id="49885-162">For example, cdnverify.www.</span><span class="sxs-lookup"><span data-stu-id="49885-162">For example, cdnverify.www.</span></span>

    - <span data-ttu-id="49885-163">Points to: Enter the host name of your CDN endpoint, including the cdnverify subdomain name.</span><span class="sxs-lookup"><span data-stu-id="49885-163">Points to: Enter the host name of your CDN endpoint, including the cdnverify subdomain name.</span></span> <span data-ttu-id="49885-164">For example, cdnverify.contoso.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-164">For example, cdnverify.contoso.azureedge.net.</span></span> 

    - <span data-ttu-id="49885-165">TTL: Leave *1 Hour* selected.</span><span class="sxs-lookup"><span data-stu-id="49885-165">TTL: Leave *1 Hour* selected.</span></span>

6. <span data-ttu-id="49885-166">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="49885-166">Select **Save**.</span></span>
 
    <span data-ttu-id="49885-167">The CNAME entry is added to the DNS records table.</span><span class="sxs-lookup"><span data-stu-id="49885-167">The CNAME entry is added to the DNS records table.</span></span>

    ![DNS records table](./media/cdn-map-content-to-custom-domain/cdn-cdnverify-dns-table.png)


## <a name="associate-the-custom-domain-with-your-cdn-endpoint"></a><span data-ttu-id="49885-169">Associate the custom domain with your CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="49885-169">Associate the custom domain with your CDN endpoint</span></span>

<span data-ttu-id="49885-170">After you've registered your custom domain, you can then add it to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-170">After you've registered your custom domain, you can then add it to your CDN endpoint.</span></span> 

1. <span data-ttu-id="49885-171">Sign in to the [Azure portal](https://portal.azure.com/) and browse to the CDN profile containing the endpoint that you want to map to a custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-171">Sign in to the [Azure portal](https://portal.azure.com/) and browse to the CDN profile containing the endpoint that you want to map to a custom domain.</span></span>
    
2. <span data-ttu-id="49885-172">On the **CDN profile** page, select the CDN endpoint to associate with the custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-172">On the **CDN profile** page, select the CDN endpoint to associate with the custom domain.</span></span>

   <span data-ttu-id="49885-173">The **Endpoint** page opens.</span><span class="sxs-lookup"><span data-stu-id="49885-173">The **Endpoint** page opens.</span></span>
    
3. <span data-ttu-id="49885-174">Select **Custom domain**.</span><span class="sxs-lookup"><span data-stu-id="49885-174">Select **Custom domain**.</span></span> 

   ![CDN custom domain button](./media/cdn-map-content-to-custom-domain/cdn-custom-domain-button.png)

   <span data-ttu-id="49885-176">The **Add a custom domain** page opens.</span><span class="sxs-lookup"><span data-stu-id="49885-176">The **Add a custom domain** page opens.</span></span>

4. <span data-ttu-id="49885-177">For **Endpoint hostname**, the endpoint host name to use as the destination domain of your CNAME record is prefilled and is derived from your CDN endpoint URL: *&lt;endpoint hostname&gt;*.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-177">For **Endpoint hostname**, the endpoint host name to use as the destination domain of your CNAME record is prefilled and is derived from your CDN endpoint URL: *&lt;endpoint hostname&gt;*.azureedge.net.</span></span> <span data-ttu-id="49885-178">It cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="49885-178">It cannot be changed.</span></span>

5. <span data-ttu-id="49885-179">For **Custom hostname**, enter your custom domain, including the subdomain, to use as the source domain of your CNAME record.</span><span class="sxs-lookup"><span data-stu-id="49885-179">For **Custom hostname**, enter your custom domain, including the subdomain, to use as the source domain of your CNAME record.</span></span> <span data-ttu-id="49885-180">For example, www.contoso.com or cdn.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="49885-180">For example, www.contoso.com or cdn.contoso.com.</span></span> <span data-ttu-id="49885-181">Do not use the cdnverify subdomain name.</span><span class="sxs-lookup"><span data-stu-id="49885-181">Do not use the cdnverify subdomain name.</span></span>

   ![CDN custom domain dialog](./media/cdn-map-content-to-custom-domain/cdn-add-custom-domain.png)

6. <span data-ttu-id="49885-183">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="49885-183">Select **Add**.</span></span>

   <span data-ttu-id="49885-184">Azure verifies that the CNAME record exists for the custom domain name you entered.</span><span class="sxs-lookup"><span data-stu-id="49885-184">Azure verifies that the CNAME record exists for the custom domain name you entered.</span></span> <span data-ttu-id="49885-185">If the CNAME is correct, your custom domain will be validated.</span><span class="sxs-lookup"><span data-stu-id="49885-185">If the CNAME is correct, your custom domain will be validated.</span></span> 

   <span data-ttu-id="49885-186">It can take some time for the new custom domain settings to propagate to all CDN edge nodes:</span><span class="sxs-lookup"><span data-stu-id="49885-186">It can take some time for the new custom domain settings to propagate to all CDN edge nodes:</span></span> 
    - <span data-ttu-id="49885-187">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="49885-187">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span></span> 
    - <span data-ttu-id="49885-188">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span><span class="sxs-lookup"><span data-stu-id="49885-188">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span></span> 
    - <span data-ttu-id="49885-189">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="49885-189">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes in 10 minutes.</span></span>   


## <a name="verify-the-custom-domain"></a><span data-ttu-id="49885-190">Verify the custom domain</span><span class="sxs-lookup"><span data-stu-id="49885-190">Verify the custom domain</span></span>

<span data-ttu-id="49885-191">After you have completed the registration of your custom domain, verify that the custom domain references your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-191">After you have completed the registration of your custom domain, verify that the custom domain references your CDN endpoint.</span></span>
 
1. <span data-ttu-id="49885-192">Ensure that you have public content that is cached at the endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-192">Ensure that you have public content that is cached at the endpoint.</span></span> <span data-ttu-id="49885-193">For example, if your CDN endpoint is associated with a storage account, Azure CDN will cache the content in a public container.</span><span class="sxs-lookup"><span data-stu-id="49885-193">For example, if your CDN endpoint is associated with a storage account, Azure CDN will cache the content in a public container.</span></span> <span data-ttu-id="49885-194">To test the custom domain, verify that your container is set to allow public access and contains at least one file.</span><span class="sxs-lookup"><span data-stu-id="49885-194">To test the custom domain, verify that your container is set to allow public access and contains at least one file.</span></span>

2. <span data-ttu-id="49885-195">In your browser, navigate to the address of the file by using the custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-195">In your browser, navigate to the address of the file by using the custom domain.</span></span> <span data-ttu-id="49885-196">For example, if your custom domain is cdn.contoso.com, the URL to the cached file should be similar to the following URL: http:\//cdn.contoso.com/my-public-container/my-file.jpg.</span><span class="sxs-lookup"><span data-stu-id="49885-196">For example, if your custom domain is cdn.contoso.com, the URL to the cached file should be similar to the following URL: http:\//cdn.contoso.com/my-public-container/my-file.jpg.</span></span> <span data-ttu-id="49885-197">Verify that the result is that same as when you access the CDN endpoint directly at *&lt;endpoint hostname&gt;*.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-197">Verify that the result is that same as when you access the CDN endpoint directly at *&lt;endpoint hostname&gt;*.azureedge.net.</span></span>


## <a name="map-the-permanent-custom-domain"></a><span data-ttu-id="49885-198">Map the permanent custom domain</span><span class="sxs-lookup"><span data-stu-id="49885-198">Map the permanent custom domain</span></span>

<span data-ttu-id="49885-199">If you have verified that the cdnverify subdomain has been successfully mapped to your endpoint (or if you are using a new custom domain  that is not in production), you can then map the custom domain directly to your CDN endpoint hostname.</span><span class="sxs-lookup"><span data-stu-id="49885-199">If you have verified that the cdnverify subdomain has been successfully mapped to your endpoint (or if you are using a new custom domain  that is not in production), you can then map the custom domain directly to your CDN endpoint hostname.</span></span>

<span data-ttu-id="49885-200">To create a CNAME record for your custom domain:</span><span class="sxs-lookup"><span data-stu-id="49885-200">To create a CNAME record for your custom domain:</span></span>

1. <span data-ttu-id="49885-201">Sign in to the web site of the domain provider for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-201">Sign in to the web site of the domain provider for your custom domain.</span></span>

2. <span data-ttu-id="49885-202">Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="49885-202">Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> 

3. <span data-ttu-id="49885-203">Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names may vary):</span><span class="sxs-lookup"><span data-stu-id="49885-203">Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names may vary):</span></span>

    | <span data-ttu-id="49885-204">Source</span><span class="sxs-lookup"><span data-stu-id="49885-204">Source</span></span>          | <span data-ttu-id="49885-205">Type</span><span class="sxs-lookup"><span data-stu-id="49885-205">Type</span></span>  | <span data-ttu-id="49885-206">Destination</span><span class="sxs-lookup"><span data-stu-id="49885-206">Destination</span></span>           |
    |-----------------|-------|-----------------------|
    | <span data-ttu-id="49885-207">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="49885-207">www.contoso.com</span></span> | <span data-ttu-id="49885-208">CNAME</span><span class="sxs-lookup"><span data-stu-id="49885-208">CNAME</span></span> | <span data-ttu-id="49885-209">contoso.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="49885-209">contoso.azureedge.net</span></span> |

    - <span data-ttu-id="49885-210">Source: Enter your custom domain name (for example, www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="49885-210">Source: Enter your custom domain name (for example, www.contoso.com).</span></span>

    - <span data-ttu-id="49885-211">Type: Enter *CNAME*.</span><span class="sxs-lookup"><span data-stu-id="49885-211">Type: Enter *CNAME*.</span></span>

    - <span data-ttu-id="49885-212">Destination: Enter your CDN endpoint hostname.</span><span class="sxs-lookup"><span data-stu-id="49885-212">Destination: Enter your CDN endpoint hostname.</span></span> <span data-ttu-id="49885-213">It must be in the following format:_&lt;endpoint name&gt;_.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-213">It must be in the following format:_&lt;endpoint name&gt;_.azureedge.net.</span></span> <span data-ttu-id="49885-214">For example, contoso.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-214">For example, contoso.azureedge.net.</span></span>

4. <span data-ttu-id="49885-215">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="49885-215">Save your changes.</span></span>

5. <span data-ttu-id="49885-216">If you're previously created a temporary cdnverify subdomain CNAME record, delete it.</span><span class="sxs-lookup"><span data-stu-id="49885-216">If you're previously created a temporary cdnverify subdomain CNAME record, delete it.</span></span> 

6. <span data-ttu-id="49885-217">If you are using this custom domain in production for the first time, follow the steps for [Associate the custom domain with your CDN endpoint](#associate-the-custom-domain-with-your-cdn-endpoint) and [Verify the custom domain](#verify-the-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="49885-217">If you are using this custom domain in production for the first time, follow the steps for [Associate the custom domain with your CDN endpoint](#associate-the-custom-domain-with-your-cdn-endpoint) and [Verify the custom domain](#verify-the-custom-domain).</span></span>

<span data-ttu-id="49885-218">For example, the procedure for the GoDaddy domain registrar is as follows:</span><span class="sxs-lookup"><span data-stu-id="49885-218">For example, the procedure for the GoDaddy domain registrar is as follows:</span></span>

1. <span data-ttu-id="49885-219">Sign in and select the custom domain you want to use.</span><span class="sxs-lookup"><span data-stu-id="49885-219">Sign in and select the custom domain you want to use.</span></span>

2. <span data-ttu-id="49885-220">In the Domains section, select **Manage All**, then select **DNS** | **Manage Zones**.</span><span class="sxs-lookup"><span data-stu-id="49885-220">In the Domains section, select **Manage All**, then select **DNS** | **Manage Zones**.</span></span>

3. <span data-ttu-id="49885-221">For **Domain Name**, enter your custom domain, then select **Search**.</span><span class="sxs-lookup"><span data-stu-id="49885-221">For **Domain Name**, enter your custom domain, then select **Search**.</span></span>

4. <span data-ttu-id="49885-222">From the **DNS Management** page, select **Add**, then select **CNAME** in the **Type** list.</span><span class="sxs-lookup"><span data-stu-id="49885-222">From the **DNS Management** page, select **Add**, then select **CNAME** in the **Type** list.</span></span>

5. <span data-ttu-id="49885-223">Complete the fields of the CNAME entry:</span><span class="sxs-lookup"><span data-stu-id="49885-223">Complete the fields of the CNAME entry:</span></span>

    ![CNAME entry](./media/cdn-map-content-to-custom-domain/cdn-cname-entry.png)

    - <span data-ttu-id="49885-225">Type: Leave *CNAME* selected.</span><span class="sxs-lookup"><span data-stu-id="49885-225">Type: Leave *CNAME* selected.</span></span>

    - <span data-ttu-id="49885-226">Host: Enter the subdomain of your custom domain to use.</span><span class="sxs-lookup"><span data-stu-id="49885-226">Host: Enter the subdomain of your custom domain to use.</span></span> <span data-ttu-id="49885-227">For example, www or cdn.</span><span class="sxs-lookup"><span data-stu-id="49885-227">For example, www or cdn.</span></span>

    - <span data-ttu-id="49885-228">Points to: Enter the host name of your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-228">Points to: Enter the host name of your CDN endpoint.</span></span> <span data-ttu-id="49885-229">For example, contoso.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="49885-229">For example, contoso.azureedge.net.</span></span> 

    - <span data-ttu-id="49885-230">TTL: Leave *1 Hour* selected.</span><span class="sxs-lookup"><span data-stu-id="49885-230">TTL: Leave *1 Hour* selected.</span></span>

6. <span data-ttu-id="49885-231">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="49885-231">Select **Save**.</span></span>
 
    <span data-ttu-id="49885-232">The CNAME entry is added to the DNS records table.</span><span class="sxs-lookup"><span data-stu-id="49885-232">The CNAME entry is added to the DNS records table.</span></span>

    ![DNS records table](./media/cdn-map-content-to-custom-domain/cdn-dns-table.png)

7. <span data-ttu-id="49885-234">If you have a cdnverify CNAME record, select the pencil icon next to it, then select the trash can icon.</span><span class="sxs-lookup"><span data-stu-id="49885-234">If you have a cdnverify CNAME record, select the pencil icon next to it, then select the trash can icon.</span></span>

8. <span data-ttu-id="49885-235">Select **Delete** to delete the CNAME record.</span><span class="sxs-lookup"><span data-stu-id="49885-235">Select **Delete** to delete the CNAME record.</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="49885-236">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="49885-236">Clean up resources</span></span>

<span data-ttu-id="49885-237">In the preceding steps, you added a custom domain to a CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-237">In the preceding steps, you added a custom domain to a CDN endpoint.</span></span> <span data-ttu-id="49885-238">If you no longer want to associate your endpoint with a custom domain, you can remove the custom domain by performing these steps:</span><span class="sxs-lookup"><span data-stu-id="49885-238">If you no longer want to associate your endpoint with a custom domain, you can remove the custom domain by performing these steps:</span></span>
 
1. <span data-ttu-id="49885-239">In your CDN profile, select the endpoint with the custom domain that you want to remove.</span><span class="sxs-lookup"><span data-stu-id="49885-239">In your CDN profile, select the endpoint with the custom domain that you want to remove.</span></span>

2. <span data-ttu-id="49885-240">From the **Endpoint** page, under Custom domains, right-click the custom domain that you want to remove, then select **Delete** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="49885-240">From the **Endpoint** page, under Custom domains, right-click the custom domain that you want to remove, then select **Delete** from the context menu.</span></span>  

   <span data-ttu-id="49885-241">The custom domain is disassociated from your endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-241">The custom domain is disassociated from your endpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="49885-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="49885-242">Next steps</span></span>

<span data-ttu-id="49885-243">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="49885-243">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="49885-244">Create a CNAME DNS record.</span><span class="sxs-lookup"><span data-stu-id="49885-244">Create a CNAME DNS record.</span></span>
> - <span data-ttu-id="49885-245">Associate the custom domain with your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="49885-245">Associate the custom domain with your CDN endpoint.</span></span>
> - <span data-ttu-id="49885-246">Verify the custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-246">Verify the custom domain.</span></span>

<span data-ttu-id="49885-247">Advance to the next tutorial to learn how to configure HTTPS on an Azure CDN custom domain.</span><span class="sxs-lookup"><span data-stu-id="49885-247">Advance to the next tutorial to learn how to configure HTTPS on an Azure CDN custom domain.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49885-248">Tutorial: Configure HTTPS on an Azure CDN custom domain</span><span class="sxs-lookup"><span data-stu-id="49885-248">Tutorial: Configure HTTPS on an Azure CDN custom domain</span></span>](cdn-custom-ssl.md)


