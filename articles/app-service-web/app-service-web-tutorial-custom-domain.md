---
title: Map a custom DNS name to an Azure web app | Microsoft Docs
description: Learn add a custom DNS domain name (i.e. vanity domain) to web app, mobile app backend, or API app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/29/2017
ms.author: cephalin
ms.openlocfilehash: 2a2671c7de3365d40e9ef7a2075514a6d8232baa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552947"
---
# <a name="map-a-custom-dns-name-to-an-azure-web-app"></a><span data-ttu-id="3b599-103">Map a custom DNS name to an Azure web app</span><span class="sxs-lookup"><span data-stu-id="3b599-103">Map a custom DNS name to an Azure web app</span></span>

<span data-ttu-id="3b599-104">This tutorial shows you how to map a custom DNS name (i.e. vanity domain) to your web app, mobile app backend, or API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3b599-104">This tutorial shows you how to map a custom DNS name (i.e. vanity domain) to your web app, mobile app backend, or API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="3b599-106">This tutorial follows the example scenario of mapping two DNS names to an app in App Service:</span><span class="sxs-lookup"><span data-stu-id="3b599-106">This tutorial follows the example scenario of mapping two DNS names to an app in App Service:</span></span>

- <span data-ttu-id="3b599-107">`contoso.com` - a root domain.</span><span class="sxs-lookup"><span data-stu-id="3b599-107">`contoso.com` - a root domain.</span></span> <span data-ttu-id="3b599-108">You will use an [A record](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) to map it to Azure.</span><span class="sxs-lookup"><span data-stu-id="3b599-108">You will use an [A record](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) to map it to Azure.</span></span> 
- <span data-ttu-id="3b599-109">`www.contoso.com` - a subdomain of `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3b599-109">`www.contoso.com` - a subdomain of `contoso.com`.</span></span> <span data-ttu-id="3b599-110">You can use either an [A record](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) or a [CNAME record](https://en.wikipedia.org/wiki/CNAME_record).</span><span class="sxs-lookup"><span data-stu-id="3b599-110">You can use either an [A record](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) or a [CNAME record](https://en.wikipedia.org/wiki/CNAME_record).</span></span>

<span data-ttu-id="3b599-111">The tutorial also shows you how to map a [wildcard DNS](https://en.wikipedia.org/wiki/Wildcard_DNS_record) to App Service (e.g. `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3b599-111">The tutorial also shows you how to map a [wildcard DNS](https://en.wikipedia.org/wiki/Wildcard_DNS_record) to App Service (e.g. `*.contoso.com`).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3b599-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3b599-112">Before you begin</span></span>

<span data-ttu-id="3b599-113">Since this tutorial shows you how to map a DNS name to Azure App Service, you must have administrative access to the DNS configuration page for your respective domain provider (e.g. GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="3b599-113">Since this tutorial shows you how to map a DNS name to Azure App Service, you must have administrative access to the DNS configuration page for your respective domain provider (e.g. GoDaddy).</span></span> <span data-ttu-id="3b599-114">For example, to add a mapping for `contoso.com` and `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3b599-114">For example, to add a mapping for `contoso.com` and `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="3b599-115">If you haven't registered a domain with a domain provider yet, you can always just [buy a domain directly from Azure and map it to your app](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="3b599-115">If you haven't registered a domain with a domain provider yet, you can always just [buy a domain directly from Azure and map it to your app](custom-dns-web-site-buydomains-web-app.md).</span></span>

## <a name="step-1---prepare-your-app"></a><span data-ttu-id="3b599-116">Step 1 - Prepare your app</span><span class="sxs-lookup"><span data-stu-id="3b599-116">Step 1 - Prepare your app</span></span>
<span data-ttu-id="3b599-117">To map a custom DNS name, your[App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Shared** tier or above.</span><span class="sxs-lookup"><span data-stu-id="3b599-117">To map a custom DNS name, your[App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Shared** tier or above.</span></span> <span data-ttu-id="3b599-118">In this step, you make sure that your Azure app is in the supported pricing tier.</span><span class="sxs-lookup"><span data-stu-id="3b599-118">In this step, you make sure that your Azure app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="3b599-119">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="3b599-119">Log in to Azure</span></span>

<span data-ttu-id="3b599-120">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3b599-120">Open the Azure portal.</span></span> 

<span data-ttu-id="3b599-121">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="3b599-121">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

### <a name="navigate-to-your-app"></a><span data-ttu-id="3b599-122">Navigate to your app</span><span class="sxs-lookup"><span data-stu-id="3b599-122">Navigate to your app</span></span>
<span data-ttu-id="3b599-123">From the left menu, click **App Service**, then click the name of your Azure app.</span><span class="sxs-lookup"><span data-stu-id="3b599-123">From the left menu, click **App Service**, then click the name of your Azure app.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="3b599-125">You have landed in your app's _blade_ (a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="3b599-125">You have landed in your app's _blade_ (a portal page that opens horizontally).</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="3b599-126">Check the pricing tier</span><span class="sxs-lookup"><span data-stu-id="3b599-126">Check the pricing tier</span></span>
<span data-ttu-id="3b599-127">In the **Overview** page, which opens by default, check to make sure that your app is not in the **Free** tier.</span><span class="sxs-lookup"><span data-stu-id="3b599-127">In the **Overview** page, which opens by default, check to make sure that your app is not in the **Free** tier.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="3b599-129">Custom DNS is not supported in the **Free** tier.</span><span class="sxs-lookup"><span data-stu-id="3b599-129">Custom DNS is not supported in the **Free** tier.</span></span> <span data-ttu-id="3b599-130">If you need to scale up, follow the next section.</span><span class="sxs-lookup"><span data-stu-id="3b599-130">If you need to scale up, follow the next section.</span></span> <span data-ttu-id="3b599-131">Otherwise, skip to [Step 2]().</span><span class="sxs-lookup"><span data-stu-id="3b599-131">Otherwise, skip to [Step 2]().</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="3b599-132">Scale up your App Service plan</span><span class="sxs-lookup"><span data-stu-id="3b599-132">Scale up your App Service plan</span></span>

<span data-ttu-id="3b599-133">To scale up your plan, click **Scale up (App Service plan)** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="3b599-133">To scale up your plan, click **Scale up (App Service plan)** in the left pane.</span></span>

<span data-ttu-id="3b599-134">Select the tier you want to scale to.</span><span class="sxs-lookup"><span data-stu-id="3b599-134">Select the tier you want to scale to.</span></span> <span data-ttu-id="3b599-135">For example, select **Shared**.</span><span class="sxs-lookup"><span data-stu-id="3b599-135">For example, select **Shared**.</span></span> <span data-ttu-id="3b599-136">When ready, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="3b599-136">When ready, click **Select**.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="3b599-138">When you see the notification below, the scale operation is complete.</span><span class="sxs-lookup"><span data-stu-id="3b599-138">When you see the notification below, the scale operation is complete.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="info"></a>

## <a name="step-2---get-mapping-information"></a><span data-ttu-id="3b599-140">Step 2 - Get mapping information</span><span class="sxs-lookup"><span data-stu-id="3b599-140">Step 2 - Get mapping information</span></span>

<span data-ttu-id="3b599-141">In this step, you obtain the information that you will need to create the DNS record(s) later.</span><span class="sxs-lookup"><span data-stu-id="3b599-141">In this step, you obtain the information that you will need to create the DNS record(s) later.</span></span> 

### <a name="open-the-custom-domain-ui"></a><span data-ttu-id="3b599-142">Open the custom domain UI</span><span class="sxs-lookup"><span data-stu-id="3b599-142">Open the custom domain UI</span></span>

<span data-ttu-id="3b599-143">In your app's blade, click **Custom domains** in the menu.</span><span class="sxs-lookup"><span data-stu-id="3b599-143">In your app's blade, click **Custom domains** in the menu.</span></span> 

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

### <a name="copy-the-mapping-information"></a><span data-ttu-id="3b599-145">Copy the mapping information</span><span class="sxs-lookup"><span data-stu-id="3b599-145">Copy the mapping information</span></span>

<span data-ttu-id="3b599-146">In th **Custom domains** page, copy the app's **IP address** and its default hostname under **Hostnames assigned to site**.</span><span class="sxs-lookup"><span data-stu-id="3b599-146">In th **Custom domains** page, copy the app's **IP address** and its default hostname under **Hostnames assigned to site**.</span></span>

<span data-ttu-id="3b599-147">You will need the IP address later for the A record mapping, and the default hostname for the CNAME record mapping.</span><span class="sxs-lookup"><span data-stu-id="3b599-147">You will need the IP address later for the A record mapping, and the default hostname for the CNAME record mapping.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/mapping-information.png)

## <a name="step-3---add-dns-records"></a><span data-ttu-id="3b599-149">Step 3 - Add DNS records</span><span class="sxs-lookup"><span data-stu-id="3b599-149">Step 3 - Add DNS records</span></span> 

<span data-ttu-id="3b599-150">In this step, you add the DNS records you need to map your custom DNS to your app.</span><span class="sxs-lookup"><span data-stu-id="3b599-150">In this step, you add the DNS records you need to map your custom DNS to your app.</span></span> <span data-ttu-id="3b599-151">You perform this step with your own domain provider.</span><span class="sxs-lookup"><span data-stu-id="3b599-151">You perform this step with your own domain provider.</span></span>

### <a name="access-dns-records-with-domain-provider"></a><span data-ttu-id="3b599-152">Access DNS records with domain provider</span><span class="sxs-lookup"><span data-stu-id="3b599-152">Access DNS records with domain provider</span></span>

<span data-ttu-id="3b599-153">First, log in to the website of your domain provider.</span><span class="sxs-lookup"><span data-stu-id="3b599-153">First, log in to the website of your domain provider.</span></span>

<span data-ttu-id="3b599-154">Then, you need to find the page for managing DNS records.</span><span class="sxs-lookup"><span data-stu-id="3b599-154">Then, you need to find the page for managing DNS records.</span></span> <span data-ttu-id="3b599-155">Every domain provider has its own DNS records interface, so you should consult your provider's documentation.</span><span class="sxs-lookup"><span data-stu-id="3b599-155">Every domain provider has its own DNS records interface, so you should consult your provider's documentation.</span></span> <span data-ttu-id="3b599-156">In general, you should look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="3b599-156">In general, you should look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="3b599-157">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span><span class="sxs-lookup"><span data-stu-id="3b599-157">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span> 

<span data-ttu-id="3b599-158">Then, look for a link that lets you manage DNS records.</span><span class="sxs-lookup"><span data-stu-id="3b599-158">Then, look for a link that lets you manage DNS records.</span></span> <span data-ttu-id="3b599-159">This link might be named **Zone file**, **DNS Records**, or **Advanced configuration**.</span><span class="sxs-lookup"><span data-stu-id="3b599-159">This link might be named **Zone file**, **DNS Records**, or **Advanced configuration**.</span></span>

<span data-ttu-id="3b599-160">The following screenshot is an example of what your DNS records page may look like:</span><span class="sxs-lookup"><span data-stu-id="3b599-160">The following screenshot is an example of what your DNS records page may look like:</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/example-record-ui.png)

<span data-ttu-id="3b599-162">In the example screenshot, you click **Add** to create a record.</span><span class="sxs-lookup"><span data-stu-id="3b599-162">In the example screenshot, you click **Add** to create a record.</span></span> <span data-ttu-id="3b599-163">Some providers have different links to add different record types.</span><span class="sxs-lookup"><span data-stu-id="3b599-163">Some providers have different links to add different record types.</span></span> <span data-ttu-id="3b599-164">Again, consult your provider's documentation.</span><span class="sxs-lookup"><span data-stu-id="3b599-164">Again, consult your provider's documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="3b599-165">For certain providers, such as GoDaddy, changes to DNS records don't become effective until you click a separate **Save Changes** link after you create them.</span><span class="sxs-lookup"><span data-stu-id="3b599-165">For certain providers, such as GoDaddy, changes to DNS records don't become effective until you click a separate **Save Changes** link after you create them.</span></span> 
>
>

<a name="a"></a>

### <a name="create-an-a-record"></a><span data-ttu-id="3b599-166">Create an A record</span><span class="sxs-lookup"><span data-stu-id="3b599-166">Create an A record</span></span>

<span data-ttu-id="3b599-167">In the tutorial example, you want to add an A record for the root domain, `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3b599-167">In the tutorial example, you want to add an A record for the root domain, `contoso.com`.</span></span> 

<span data-ttu-id="3b599-168">To map an A record to your app, App Service actually requires _two_ DNS records:</span><span class="sxs-lookup"><span data-stu-id="3b599-168">To map an A record to your app, App Service actually requires _two_ DNS records:</span></span>

- <span data-ttu-id="3b599-169">An **A** record to map to your app's IP address.</span><span class="sxs-lookup"><span data-stu-id="3b599-169">An **A** record to map to your app's IP address.</span></span>
- <span data-ttu-id="3b599-170">A **TXT** record to map to your app's default hostname.</span><span class="sxs-lookup"><span data-stu-id="3b599-170">A **TXT** record to map to your app's default hostname.</span></span> <span data-ttu-id="3b599-171">This record lets App Service verify that you own the custom domain you want to map.</span><span class="sxs-lookup"><span data-stu-id="3b599-171">This record lets App Service verify that you own the custom domain you want to map.</span></span>

<span data-ttu-id="3b599-172">The following table shows you how you would configure an A record mapping for the supported domain types (`@` typically represents the root domain).</span><span class="sxs-lookup"><span data-stu-id="3b599-172">The following table shows you how you would configure an A record mapping for the supported domain types (`@` typically represents the root domain).</span></span> 

<table cellspacing="0" border="1">
  <tr>
    <th><span data-ttu-id="3b599-173">Domain type</span><span class="sxs-lookup"><span data-stu-id="3b599-173">Domain type</span></span></th>
    <th><span data-ttu-id="3b599-174">Record type</span><span class="sxs-lookup"><span data-stu-id="3b599-174">Record type</span></span></th>
    <th><span data-ttu-id="3b599-175">Host</span><span class="sxs-lookup"><span data-stu-id="3b599-175">Host</span></span></th>
    <th><span data-ttu-id="3b599-176">Value</span><span class="sxs-lookup"><span data-stu-id="3b599-176">Value</span></span></th>
  </tr>
  <tr>
    <td rowspan="2" align="left"><span data-ttu-id="3b599-177">Root domain</span><span class="sxs-lookup"><span data-stu-id="3b599-177">Root domain</span></span><br><span data-ttu-id="3b599-178">(e.g. <code>contoso.com</code>)</span><span class="sxs-lookup"><span data-stu-id="3b599-178">(e.g. <code>contoso.com</code>)</span></span></td>
    <td><span data-ttu-id="3b599-179">A</span><span class="sxs-lookup"><span data-stu-id="3b599-179">A</span></span></td>
    <td>@</td>
    <td><span data-ttu-id="3b599-180">IP address from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-180">IP address from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b599-181">TXT</span><span class="sxs-lookup"><span data-stu-id="3b599-181">TXT</span></span></td>
    <td>@</td>
    <td><span data-ttu-id="3b599-182">Default hostname from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-182">Default hostname from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td rowspan="2" align="left"><span data-ttu-id="3b599-183">Subdomain</span><span class="sxs-lookup"><span data-stu-id="3b599-183">Subdomain</span></span><br><span data-ttu-id="3b599-184">(e.g. <code>www.contoso.com</code>)</span><span class="sxs-lookup"><span data-stu-id="3b599-184">(e.g. <code>www.contoso.com</code>)</span></span></td>
    <td><span data-ttu-id="3b599-185">A</span><span class="sxs-lookup"><span data-stu-id="3b599-185">A</span></span></td>
    <td><span data-ttu-id="3b599-186">www</span><span class="sxs-lookup"><span data-stu-id="3b599-186">www</span></span></td>
    <td><span data-ttu-id="3b599-187">IP address from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-187">IP address from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b599-188">TXT</span><span class="sxs-lookup"><span data-stu-id="3b599-188">TXT</span></span></td>
    <td><span data-ttu-id="3b599-189">www</span><span class="sxs-lookup"><span data-stu-id="3b599-189">www</span></span></td>
    <td><span data-ttu-id="3b599-190">Default hostname from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-190">Default hostname from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td rowspan="2" align="left"><span data-ttu-id="3b599-191">Wildcard domain</span><span class="sxs-lookup"><span data-stu-id="3b599-191">Wildcard domain</span></span><br><span data-ttu-id="3b599-192">(e.g. <code>\*.contoso.com</code>)</span><span class="sxs-lookup"><span data-stu-id="3b599-192">(e.g. <code>\*.contoso.com</code>)</span></span></td>
    <td><span data-ttu-id="3b599-193">A</span><span class="sxs-lookup"><span data-stu-id="3b599-193">A</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="3b599-194">IP address from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-194">IP address from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b599-195">TXT</span><span class="sxs-lookup"><span data-stu-id="3b599-195">TXT</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="3b599-196">Default hostname from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-196">Default hostname from <a href="#info">Step 2</a></span></span></td>
  </tr>
</table>

<span data-ttu-id="3b599-197">For the `contoso.com` domain example, your DNS records page show look like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="3b599-197">For the `contoso.com` domain example, your DNS records page show look like the following screenshot:</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="cname"></a>

### <a name="create-a-cname-record"></a><span data-ttu-id="3b599-199">Create a CNAME record</span><span class="sxs-lookup"><span data-stu-id="3b599-199">Create a CNAME record</span></span>
<span data-ttu-id="3b599-200">In the tutorial example, you want to add a CNAME record for the root domain, `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3b599-200">In the tutorial example, you want to add a CNAME record for the root domain, `contoso.com`.</span></span> 

<span data-ttu-id="3b599-201">Unlike [mapping an A record](#a), mapping a CNAME record to your app doesn't require any additional record.</span><span class="sxs-lookup"><span data-stu-id="3b599-201">Unlike [mapping an A record](#a), mapping a CNAME record to your app doesn't require any additional record.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b599-202">It is recommended that you use a CNAME mapping.</span><span class="sxs-lookup"><span data-stu-id="3b599-202">It is recommended that you use a CNAME mapping.</span></span> <span data-ttu-id="3b599-203">If you delete and recreate your app, or change from a dedicated hosting tier back to the **Shared** tier, your app's virtual IP address may change.</span><span class="sxs-lookup"><span data-stu-id="3b599-203">If you delete and recreate your app, or change from a dedicated hosting tier back to the **Shared** tier, your app's virtual IP address may change.</span></span> <span data-ttu-id="3b599-204">A CNAME mapping is valid through such a change, whereas an A mapping is potentially invalidated by a new IP address.</span><span class="sxs-lookup"><span data-stu-id="3b599-204">A CNAME mapping is valid through such a change, whereas an A mapping is potentially invalidated by a new IP address.</span></span> 
>
> <span data-ttu-id="3b599-205">However, do _not_ create a CNAME record for your root domain (i.e. the "root record").</span><span class="sxs-lookup"><span data-stu-id="3b599-205">However, do _not_ create a CNAME record for your root domain (i.e. the "root record").</span></span> <span data-ttu-id="3b599-206">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span><span class="sxs-lookup"><span data-stu-id="3b599-206">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span></span>
> <span data-ttu-id="3b599-207">To map a root domain to your Azure app, use an [A record](#a) instead.</span><span class="sxs-lookup"><span data-stu-id="3b599-207">To map a root domain to your Azure app, use an [A record](#a) instead.</span></span>
> 
> 

<span data-ttu-id="3b599-208">The following table shows you how you would configure a CNAME record mapping for the supported domain types.</span><span class="sxs-lookup"><span data-stu-id="3b599-208">The following table shows you how you would configure a CNAME record mapping for the supported domain types.</span></span>

<span data-ttu-id="3b599-209">Configure your CNAME record as follows.</span><span class="sxs-lookup"><span data-stu-id="3b599-209">Configure your CNAME record as follows.</span></span>

<table cellspacing="0" border="1">
  <tr>
    <th><span data-ttu-id="3b599-210">Domain type</span><span class="sxs-lookup"><span data-stu-id="3b599-210">Domain type</span></span></th>
    <th><span data-ttu-id="3b599-211">CNAME Host</span><span class="sxs-lookup"><span data-stu-id="3b599-211">CNAME Host</span></span></th>
    <th><span data-ttu-id="3b599-212">CNAME Value</span><span class="sxs-lookup"><span data-stu-id="3b599-212">CNAME Value</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="3b599-213">Subdomain</span><span class="sxs-lookup"><span data-stu-id="3b599-213">Subdomain</span></span><br><span data-ttu-id="3b599-214">(e.g. <code>www.contoso.com</code>)</span><span class="sxs-lookup"><span data-stu-id="3b599-214">(e.g. <code>www.contoso.com</code>)</span></span></td>
    <td><span data-ttu-id="3b599-215">www</span><span class="sxs-lookup"><span data-stu-id="3b599-215">www</span></span></td>
    <td><span data-ttu-id="3b599-216">Default hostname from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-216">Default hostname from <a href="#info">Step 2</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b599-217">Wildcard domain</span><span class="sxs-lookup"><span data-stu-id="3b599-217">Wildcard domain</span></span><br><span data-ttu-id="3b599-218">(e.g. <code>\*.contoso.com</code>)</span><span class="sxs-lookup"><span data-stu-id="3b599-218">(e.g. <code>\*.contoso.com</code>)</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="3b599-219">Default hostname from <a href="#info">Step 2</a></span><span class="sxs-lookup"><span data-stu-id="3b599-219">Default hostname from <a href="#info">Step 2</a></span></span></td>
  </tr>
</table>

<span data-ttu-id="3b599-220">For the `www.contoso.com` domain example, your DNS records page show look like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="3b599-220">For the `www.contoso.com` domain example, your DNS records page show look like the following screenshot:</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/cname-record.png)

<a name="enable"></a>

## <a name="step-4---enable-the-custom-dns-in-your-app"></a><span data-ttu-id="3b599-222">Step 4 - Enable the custom DNS in your app</span><span class="sxs-lookup"><span data-stu-id="3b599-222">Step 4 - Enable the custom DNS in your app</span></span>

<span data-ttu-id="3b599-223">You are now ready to add your configured DNS names (e.g. `contoso.com` and `www.contoso.com`) to your app.</span><span class="sxs-lookup"><span data-stu-id="3b599-223">You are now ready to add your configured DNS names (e.g. `contoso.com` and `www.contoso.com`) to your app.</span></span>

<span data-ttu-id="3b599-224">Back in your app's **Custom domains** page in the Azure portal (see [Step 1](#info)), you need to add the fully-qualified domain name (FQDN) of your custom domain to the list.</span><span class="sxs-lookup"><span data-stu-id="3b599-224">Back in your app's **Custom domains** page in the Azure portal (see [Step 1](#info)), you need to add the fully-qualified domain name (FQDN) of your custom domain to the list.</span></span>

### <a name="add-the-a-hostname-to-your-app"></a><span data-ttu-id="3b599-225">Add the A hostname to your app</span><span class="sxs-lookup"><span data-stu-id="3b599-225">Add the A hostname to your app</span></span>

<span data-ttu-id="3b599-226">Click the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="3b599-226">Click the **+** icon next to **Add hostname**.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="3b599-228">Type the FQDN for which you configured the A record earlier (e.g. `contoso.com`), then click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="3b599-228">Type the FQDN for which you configured the A record earlier (e.g. `contoso.com`), then click **Validate**.</span></span>

<span data-ttu-id="3b599-229">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3b599-229">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/verification-error.png)

<span data-ttu-id="3b599-231">Otherwise, the **Add hostname** button is activated.</span><span class="sxs-lookup"><span data-stu-id="3b599-231">Otherwise, the **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3b599-232">Make sure that **Hostname record type** is set to **A record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="3b599-232">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="3b599-233">Click **Add hostname** to add the DNS name to your app.</span><span class="sxs-lookup"><span data-stu-id="3b599-233">Click **Add hostname** to add the DNS name to your app.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="3b599-235">It might take some time for the new hostname to be reflected in your app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="3b599-235">It might take some time for the new hostname to be reflected in your app's **Custom domains** page.</span></span> <span data-ttu-id="3b599-236">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="3b599-236">Try refreshing the browser to update the data.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/a-record-added.png)

<a name="add-cname"></a>
### <a name="add-the-cname-hostname-to-your-app"></a><span data-ttu-id="3b599-238">Add the CNAME hostname to your app</span><span class="sxs-lookup"><span data-stu-id="3b599-238">Add the CNAME hostname to your app</span></span>

<span data-ttu-id="3b599-239">Click the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="3b599-239">Click the **+** icon next to **Add hostname**.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="3b599-241">Type the FQDN for which you configured the CNAME record earlier (e.g. `www.contoso.com`), then click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="3b599-241">Type the FQDN for which you configured the CNAME record earlier (e.g. `www.contoso.com`), then click **Validate**.</span></span>

<span data-ttu-id="3b599-242">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3b599-242">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<span data-ttu-id="3b599-244">Otherwise, the **Add hostname** button is activated.</span><span class="sxs-lookup"><span data-stu-id="3b599-244">Otherwise, the **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3b599-245">Make sure that **Hostname record type** is set to **A record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="3b599-245">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="3b599-246">Click **Add hostname** to add the DNS name to your app.</span><span class="sxs-lookup"><span data-stu-id="3b599-246">Click **Add hostname** to add the DNS name to your app.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="3b599-248">It might take some time for the new hostname to be reflected in your app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="3b599-248">It might take some time for the new hostname to be reflected in your app's **Custom domains** page.</span></span> <span data-ttu-id="3b599-249">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="3b599-249">Try refreshing the browser to update the data.</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/cname-record-added.png)

### <a name="step-5---test-in-browser"></a><span data-ttu-id="3b599-251">Step 5 - Test in browser</span><span class="sxs-lookup"><span data-stu-id="3b599-251">Step 5 - Test in browser</span></span>

<span data-ttu-id="3b599-252">In your browser, browse to the DNS name(s) that you configured earlier (`contoso.com` and `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3b599-252">In your browser, browse to the DNS name(s) that you configured earlier (`contoso.com` and `www.contoso.com`).</span></span>

![Portal navigation to Azure app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="more-resources"></a><span data-ttu-id="3b599-254">More resources</span><span class="sxs-lookup"><span data-stu-id="3b599-254">More resources</span></span>

[<span data-ttu-id="3b599-255">Buy and Configure a custom domain name in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3b599-255">Buy and Configure a custom domain name in Azure App Service</span></span>](custom-dns-web-site-buydomains-web-app.md)



















