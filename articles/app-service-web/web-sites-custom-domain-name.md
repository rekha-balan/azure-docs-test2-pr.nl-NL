---
title: Map a custom domain name to an Azure app
description: Learn how to map a custom domain name (vanity domain) to your app in Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 48644a39-107c-45fb-9cd3-c741974ff590
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: cephalin
ms.openlocfilehash: 3851dfbb6bc28260572339637013dde228f15bff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555455"
---
# <a name="map-a-custom-domain-name-to-an-azure-app"></a><span data-ttu-id="b4837-103">Map a custom domain name to an Azure app</span><span class="sxs-lookup"><span data-stu-id="b4837-103">Map a custom domain name to an Azure app</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

<span data-ttu-id="b4837-104">This article shows you how to manually map a custom domain name to your web app, mobile app backend, or API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b4837-104">This article shows you how to manually map a custom domain name to your web app, mobile app backend, or API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="b4837-105">You can always just [buy a custom domain name directly from Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4837-105">You can always just [buy a custom domain name directly from Azure](custom-dns-web-site-buydomains-web-app.md).</span></span>
>
>

<span data-ttu-id="b4837-106">There are three main steps to map the custom domain to your app:</span><span class="sxs-lookup"><span data-stu-id="b4837-106">There are three main steps to map the custom domain to your app:</span></span>

1. <span data-ttu-id="b4837-107">[*(A record only)* Get app's IP address](#vip).</span><span class="sxs-lookup"><span data-stu-id="b4837-107">[*(A record only)* Get app's IP address](#vip).</span></span>
2. <span data-ttu-id="b4837-108">[Create the DNS records that map your domain to your app](#createdns).</span><span class="sxs-lookup"><span data-stu-id="b4837-108">[Create the DNS records that map your domain to your app](#createdns).</span></span> 
   * <span data-ttu-id="b4837-109">**Where**: your domain registrar's own management tool (e.g. Azure DNS, GoDaddy, etc.).</span><span class="sxs-lookup"><span data-stu-id="b4837-109">**Where**: your domain registrar's own management tool (e.g. Azure DNS, GoDaddy, etc.).</span></span>
   * <span data-ttu-id="b4837-110">**Why**: so your domain registrar knows to resolves the desired custom domain to your Azure app.</span><span class="sxs-lookup"><span data-stu-id="b4837-110">**Why**: so your domain registrar knows to resolves the desired custom domain to your Azure app.</span></span>
3. <span data-ttu-id="b4837-111">[Enable the custom domain name for your Azure app](#enable).</span><span class="sxs-lookup"><span data-stu-id="b4837-111">[Enable the custom domain name for your Azure app](#enable).</span></span>
   * <span data-ttu-id="b4837-112">**Where**: the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4837-112">**Where**: the [Azure portal](https://portal.azure.com).</span></span>
   * <span data-ttu-id="b4837-113">**Why**: so your app knows to respond to requests made to the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="b4837-113">**Why**: so your app knows to respond to requests made to the custom domain name.</span></span>
4. <span data-ttu-id="b4837-114">[Verify DNS propagation](#verify).</span><span class="sxs-lookup"><span data-stu-id="b4837-114">[Verify DNS propagation](#verify).</span></span>

## <a name="types-of-domains-you-can-map"></a><span data-ttu-id="b4837-115">Types of domains you can map</span><span class="sxs-lookup"><span data-stu-id="b4837-115">Types of domains you can map</span></span>
<span data-ttu-id="b4837-116">Azure App Service lets you map the following categories of custom domains to your app.</span><span class="sxs-lookup"><span data-stu-id="b4837-116">Azure App Service lets you map the following categories of custom domains to your app.</span></span>

* <span data-ttu-id="b4837-117">**Root domain** - the domain name that you reserved with the domain registrar (represented by the `@` host record, typically).</span><span class="sxs-lookup"><span data-stu-id="b4837-117">**Root domain** - the domain name that you reserved with the domain registrar (represented by the `@` host record, typically).</span></span> 
  <span data-ttu-id="b4837-118">For example, **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b4837-118">For example, **contoso.com**.</span></span>
* <span data-ttu-id="b4837-119">**Subdomain** - any domain that's under your root domain.</span><span class="sxs-lookup"><span data-stu-id="b4837-119">**Subdomain** - any domain that's under your root domain.</span></span> <span data-ttu-id="b4837-120">For example, **www.contoso.com** (represented by the `www` host record).</span><span class="sxs-lookup"><span data-stu-id="b4837-120">For example, **www.contoso.com** (represented by the `www` host record).</span></span>  <span data-ttu-id="b4837-121">You can map different subdomains of the same root domain to different apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4837-121">You can map different subdomains of the same root domain to different apps in Azure.</span></span>
* <span data-ttu-id="b4837-122">**Wildcard domain** - [any subdomain whose leftmost DNS label is `*`](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (e.g. host records `*` and `*.blogs`).</span><span class="sxs-lookup"><span data-stu-id="b4837-122">**Wildcard domain** - [any subdomain whose leftmost DNS label is `*`](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (e.g. host records `*` and `*.blogs`).</span></span> <span data-ttu-id="b4837-123">For example, **\*.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b4837-123">For example, **\*.contoso.com**.</span></span>

## <a name="types-of-dns-records-you-can-use"></a><span data-ttu-id="b4837-124">Types of DNS records you can use</span><span class="sxs-lookup"><span data-stu-id="b4837-124">Types of DNS records you can use</span></span>
<span data-ttu-id="b4837-125">Depending on your need, you can use two different types of standard DNS records to map your custom domain:</span><span class="sxs-lookup"><span data-stu-id="b4837-125">Depending on your need, you can use two different types of standard DNS records to map your custom domain:</span></span> 

* <span data-ttu-id="b4837-126">[A](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) - maps your custom domain name to the Azure app's virtual IP address directly.</span><span class="sxs-lookup"><span data-stu-id="b4837-126">[A](https://en.wikipedia.org/wiki/List_of_DNS_record_types#A) - maps your custom domain name to the Azure app's virtual IP address directly.</span></span> 
* <span data-ttu-id="b4837-127">[CNAME](https://en.wikipedia.org/wiki/CNAME_record) - maps your custom domain name to your app's Azure domain name, **&lt;*appname*>.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="b4837-127">[CNAME](https://en.wikipedia.org/wiki/CNAME_record) - maps your custom domain name to your app's Azure domain name, **&lt;*appname*>.azurewebsites.net**.</span></span> 

<span data-ttu-id="b4837-128">The advantage of CNAME is that it persists across IP address changes.</span><span class="sxs-lookup"><span data-stu-id="b4837-128">The advantage of CNAME is that it persists across IP address changes.</span></span> <span data-ttu-id="b4837-129">If you delete and recreate your app, or change from a higher pricing tier back to the **Shared** tier, your app's virtual IP address may change.</span><span class="sxs-lookup"><span data-stu-id="b4837-129">If you delete and recreate your app, or change from a higher pricing tier back to the **Shared** tier, your app's virtual IP address may change.</span></span> <span data-ttu-id="b4837-130">Through such a change, a CNAME record is still valid, whereas an A record requires an update.</span><span class="sxs-lookup"><span data-stu-id="b4837-130">Through such a change, a CNAME record is still valid, whereas an A record requires an update.</span></span> 

<span data-ttu-id="b4837-131">The tutorial shows you steps for using the A record and also for using the CNAME record.</span><span class="sxs-lookup"><span data-stu-id="b4837-131">The tutorial shows you steps for using the A record and also for using the CNAME record.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4837-132">Do not create a CNAME record for your root domain (i.e. the "root record").</span><span class="sxs-lookup"><span data-stu-id="b4837-132">Do not create a CNAME record for your root domain (i.e. the "root record").</span></span> <span data-ttu-id="b4837-133">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span><span class="sxs-lookup"><span data-stu-id="b4837-133">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span></span>
> <span data-ttu-id="b4837-134">To map a root domain to your Azure app, use an A record instead.</span><span class="sxs-lookup"><span data-stu-id="b4837-134">To map a root domain to your Azure app, use an A record instead.</span></span>
> 
> 

<a name="vip"></a>

## <a name="step-1-a-record-only-get-apps-ip-address"></a><span data-ttu-id="b4837-135">Step 1.</span><span class="sxs-lookup"><span data-stu-id="b4837-135">Step 1.</span></span> <span data-ttu-id="b4837-136">*(A record only)* Get app's IP address</span><span class="sxs-lookup"><span data-stu-id="b4837-136">*(A record only)* Get app's IP address</span></span>
<span data-ttu-id="b4837-137">To map a custom domain name using an A record, you need your Azure app's IP address.</span><span class="sxs-lookup"><span data-stu-id="b4837-137">To map a custom domain name using an A record, you need your Azure app's IP address.</span></span> <span data-ttu-id="b4837-138">If you will map using a CNAME record instead, skip this step and move onto the next section.</span><span class="sxs-lookup"><span data-stu-id="b4837-138">If you will map using a CNAME record instead, skip this step and move onto the next section.</span></span>

1. <span data-ttu-id="b4837-139">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4837-139">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b4837-140">Click **App Services** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="b4837-140">Click **App Services** on the left menu.</span></span>
3. <span data-ttu-id="b4837-141">Click your app, then click **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="b4837-141">Click your app, then click **Custom domains**.</span></span>
4. <span data-ttu-id="b4837-142">Take note of the IP address above Hostnames section..</span><span class="sxs-lookup"><span data-stu-id="b4837-142">Take note of the IP address above Hostnames section..</span></span>
   
   ![Map custom domain name with A record: Get IP address for your Azure App Service app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-custom-domain-name/virtual-ip-address.png)
5. <span data-ttu-id="b4837-144">Keep this portal blade open.</span><span class="sxs-lookup"><span data-stu-id="b4837-144">Keep this portal blade open.</span></span> <span data-ttu-id="b4837-145">You will come back to it once you create the DNS records.</span><span class="sxs-lookup"><span data-stu-id="b4837-145">You will come back to it once you create the DNS records.</span></span>

<a name="createdns"></a>

## <a name="step-2-create-the-dns-records"></a><span data-ttu-id="b4837-146">Step 2.</span><span class="sxs-lookup"><span data-stu-id="b4837-146">Step 2.</span></span> <span data-ttu-id="b4837-147">Create the DNS record(s)</span><span class="sxs-lookup"><span data-stu-id="b4837-147">Create the DNS record(s)</span></span>
<span data-ttu-id="b4837-148">Log in to your domain registrar and use their tool to add an A record or CNAME record.</span><span class="sxs-lookup"><span data-stu-id="b4837-148">Log in to your domain registrar and use their tool to add an A record or CNAME record.</span></span> <span data-ttu-id="b4837-149">Every registrar’s UI is slightly different, so you should consult your provider's documentation.</span><span class="sxs-lookup"><span data-stu-id="b4837-149">Every registrar’s UI is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="b4837-150">However, here are some general guidelines.</span><span class="sxs-lookup"><span data-stu-id="b4837-150">However, here are some general guidelines.</span></span>

1. <span data-ttu-id="b4837-151">Find the page for managing DNS records.</span><span class="sxs-lookup"><span data-stu-id="b4837-151">Find the page for managing DNS records.</span></span> <span data-ttu-id="b4837-152">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="b4837-152">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="b4837-153">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span><span class="sxs-lookup"><span data-stu-id="b4837-153">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="b4837-154">Look for a link that lets you add or edit DNS records.</span><span class="sxs-lookup"><span data-stu-id="b4837-154">Look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="b4837-155">This might be a **Zone file** or **DNS Records** link, or an **Advanced** configuration link.</span><span class="sxs-lookup"><span data-stu-id="b4837-155">This might be a **Zone file** or **DNS Records** link, or an **Advanced** configuration link.</span></span>
3. <span data-ttu-id="b4837-156">Create the record and save your changes.</span><span class="sxs-lookup"><span data-stu-id="b4837-156">Create the record and save your changes.</span></span>
   * <span data-ttu-id="b4837-157">[Instructions for an A record are here](#a).</span><span class="sxs-lookup"><span data-stu-id="b4837-157">[Instructions for an A record are here](#a).</span></span>
   * <span data-ttu-id="b4837-158">[Instructions for a CNAME record are here](#cname).</span><span class="sxs-lookup"><span data-stu-id="b4837-158">[Instructions for a CNAME record are here](#cname).</span></span>

<a name="a"></a>

### <a name="create-an-a-record"></a><span data-ttu-id="b4837-159">Create an A record</span><span class="sxs-lookup"><span data-stu-id="b4837-159">Create an A record</span></span>
<span data-ttu-id="b4837-160">To use an A record to map to your Azure app's IP address, you actually need to create both an A record and a TXT record.</span><span class="sxs-lookup"><span data-stu-id="b4837-160">To use an A record to map to your Azure app's IP address, you actually need to create both an A record and a TXT record.</span></span> <span data-ttu-id="b4837-161">The A record is for the DNS resolution itself, and the TXT record is for Azure to verify that you own the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="b4837-161">The A record is for the DNS resolution itself, and the TXT record is for Azure to verify that you own the custom domain name.</span></span> 

<span data-ttu-id="b4837-162">Configure your A record as follows (@ typically represents the root domain):</span><span class="sxs-lookup"><span data-stu-id="b4837-162">Configure your A record as follows (@ typically represents the root domain):</span></span>

<table cellspacing="0" border="1">
  <tr>
    <th><span data-ttu-id="b4837-163">FQDN example</span><span class="sxs-lookup"><span data-stu-id="b4837-163">FQDN example</span></span></th>
    <th><span data-ttu-id="b4837-164">A Host</span><span class="sxs-lookup"><span data-stu-id="b4837-164">A Host</span></span></th>
    <th><span data-ttu-id="b4837-165">A Value</span><span class="sxs-lookup"><span data-stu-id="b4837-165">A Value</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-166">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="b4837-166">contoso.com (root)</span></span></td>
    <td>@</td>
    <td><span data-ttu-id="b4837-167">IP address from <a href="#vip">Step 1</a></span><span class="sxs-lookup"><span data-stu-id="b4837-167">IP address from <a href="#vip">Step 1</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-168">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="b4837-168">www.contoso.com (sub)</span></span></td>
    <td><span data-ttu-id="b4837-169">www</span><span class="sxs-lookup"><span data-stu-id="b4837-169">www</span></span></td>
    <td><span data-ttu-id="b4837-170">IP address from <a href="#vip">Step 1</a></span><span class="sxs-lookup"><span data-stu-id="b4837-170">IP address from <a href="#vip">Step 1</a></span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-171">\*.contoso.com (wildcard)</span><span class="sxs-lookup"><span data-stu-id="b4837-171">\*.contoso.com (wildcard)</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="b4837-172">IP address from <a href="#vip">Step 1</a></span><span class="sxs-lookup"><span data-stu-id="b4837-172">IP address from <a href="#vip">Step 1</a></span></span></td>
  </tr>
</table>

<span data-ttu-id="b4837-173">Your additional TXT record takes on the convention that maps from &lt;*subdomain*>.&lt;*rootdomain*> to &lt;*appname*>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b4837-173">Your additional TXT record takes on the convention that maps from &lt;*subdomain*>.&lt;*rootdomain*> to &lt;*appname*>.azurewebsites.net.</span></span> <span data-ttu-id="b4837-174">Configure your TXT record as follows:</span><span class="sxs-lookup"><span data-stu-id="b4837-174">Configure your TXT record as follows:</span></span>

<table cellspacing="0" border="1">
  <tr>
    <th><span data-ttu-id="b4837-175">FQDN example</span><span class="sxs-lookup"><span data-stu-id="b4837-175">FQDN example</span></span></th>
    <th><span data-ttu-id="b4837-176">TXT Host</span><span class="sxs-lookup"><span data-stu-id="b4837-176">TXT Host</span></span></th>
    <th><span data-ttu-id="b4837-177">TXT Value</span><span class="sxs-lookup"><span data-stu-id="b4837-177">TXT Value</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-178">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="b4837-178">contoso.com (root)</span></span></td>
    <td>@</td>
    <td><span data-ttu-id="b4837-179">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b4837-179">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-180">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="b4837-180">www.contoso.com (sub)</span></span></td>
    <td><span data-ttu-id="b4837-181">www</span><span class="sxs-lookup"><span data-stu-id="b4837-181">www</span></span></td>
    <td><span data-ttu-id="b4837-182">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b4837-182">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-183">\*.contoso.com (wildcard)</span><span class="sxs-lookup"><span data-stu-id="b4837-183">\*.contoso.com (wildcard)</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="b4837-184">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b4837-184">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
  </tr>
</table>

<a name="cname"></a>

### <a name="create-a-cname-record"></a><span data-ttu-id="b4837-185">Create a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4837-185">Create a CNAME record</span></span>
<span data-ttu-id="b4837-186">If you use a CNAME record to map to your Azure app's default domain name, you don't need an additional TXT record like you do with an A record.</span><span class="sxs-lookup"><span data-stu-id="b4837-186">If you use a CNAME record to map to your Azure app's default domain name, you don't need an additional TXT record like you do with an A record.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b4837-187">Do not create a CNAME record for your root domain (i.e. the "root record").</span><span class="sxs-lookup"><span data-stu-id="b4837-187">Do not create a CNAME record for your root domain (i.e. the "root record").</span></span> <span data-ttu-id="b4837-188">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span><span class="sxs-lookup"><span data-stu-id="b4837-188">For more information, see [Why can't a CNAME record be used at the root domain](http://serverfault.com/questions/613829/why-cant-a-cname-record-be-used-at-the-apex-aka-root-of-a-domain).</span></span>
> <span data-ttu-id="b4837-189">To map a root domain to your Azure app, use an [A record](#a) instead.</span><span class="sxs-lookup"><span data-stu-id="b4837-189">To map a root domain to your Azure app, use an [A record](#a) instead.</span></span>
> 
> 

<span data-ttu-id="b4837-190">Configure your CNAME record as follows (@ typically represents the root domain):</span><span class="sxs-lookup"><span data-stu-id="b4837-190">Configure your CNAME record as follows (@ typically represents the root domain):</span></span>

<table cellspacing="0" border="1">
  <tr>
    <th><span data-ttu-id="b4837-191">FQDN example</span><span class="sxs-lookup"><span data-stu-id="b4837-191">FQDN example</span></span></th>
    <th><span data-ttu-id="b4837-192">CNAME Host</span><span class="sxs-lookup"><span data-stu-id="b4837-192">CNAME Host</span></span></th>
    <th><span data-ttu-id="b4837-193">CNAME Value</span><span class="sxs-lookup"><span data-stu-id="b4837-193">CNAME Value</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-194">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="b4837-194">www.contoso.com (sub)</span></span></td>
    <td><span data-ttu-id="b4837-195">www</span><span class="sxs-lookup"><span data-stu-id="b4837-195">www</span></span></td>
    <td><span data-ttu-id="b4837-196">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b4837-196">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b4837-197">\*.contoso.com (wildcard)</span><span class="sxs-lookup"><span data-stu-id="b4837-197">\*.contoso.com (wildcard)</span></span></td>
    <td>\*</td>
    <td><span data-ttu-id="b4837-198">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b4837-198">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
  </tr>
</table>

<a name="enable"></a>

## <a name="step-3-enable-the-custom-domain-name-for-your-app"></a><span data-ttu-id="b4837-199">Step 3.</span><span class="sxs-lookup"><span data-stu-id="b4837-199">Step 3.</span></span> <span data-ttu-id="b4837-200">Enable the custom domain name for your app</span><span class="sxs-lookup"><span data-stu-id="b4837-200">Enable the custom domain name for your app</span></span>
<span data-ttu-id="b4837-201">Back in the **Custom Domains** blade in the Azure portal (see [Step 1](#vip)), you need to add the fully-qualified domain name (FQDN) of your custom domain to the list.</span><span class="sxs-lookup"><span data-stu-id="b4837-201">Back in the **Custom Domains** blade in the Azure portal (see [Step 1](#vip)), you need to add the fully-qualified domain name (FQDN) of your custom domain to the list.</span></span>

1. <span data-ttu-id="b4837-202">If you haven't done so, log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4837-202">If you haven't done so, log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b4837-203">In the Azure portal, click **App Services** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="b4837-203">In the Azure portal, click **App Services** on the left menu.</span></span>
3. <span data-ttu-id="b4837-204">Click your app, then click **Custom domains** > **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4837-204">Click your app, then click **Custom domains** > **Add hostname**.</span></span>
4. <span data-ttu-id="b4837-205">Add the FQDN of your custom domain to the list (e.g. **www.contoso.com**).</span><span class="sxs-lookup"><span data-stu-id="b4837-205">Add the FQDN of your custom domain to the list (e.g. **www.contoso.com**).</span></span>
   
   ![Map a custom domain name to an Azure app: add to list of domain names](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-custom-domain-name/add-custom-domain.png)
   
   > [!NOTE]
   > <span data-ttu-id="b4837-207">Azure will attempt to verify the domain name that you use here.</span><span class="sxs-lookup"><span data-stu-id="b4837-207">Azure will attempt to verify the domain name that you use here.</span></span> <span data-ttu-id="b4837-208">Be sure that it is the same domain name for which you created a DNS record in [Step 2](#createdns).</span><span class="sxs-lookup"><span data-stu-id="b4837-208">Be sure that it is the same domain name for which you created a DNS record in [Step 2](#createdns).</span></span> 
   > 
   > 
5. <span data-ttu-id="b4837-209">Click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="b4837-209">Click **Validate**.</span></span>
6. <span data-ttu-id="b4837-210">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span><span class="sxs-lookup"><span data-stu-id="b4837-210">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="b4837-211">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span><span class="sxs-lookup"><span data-stu-id="b4837-211">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span></span>    
7. <span data-ttu-id="b4837-212">Upon successful validation **Add hostname** button will become active and you will be able to the assign hostname.</span><span class="sxs-lookup"><span data-stu-id="b4837-212">Upon successful validation **Add hostname** button will become active and you will be able to the assign hostname.</span></span> 
8. <span data-ttu-id="b4837-213">Once Azure finishes configuring your new custom domain name, navigate to your custom domain name in a browser.</span><span class="sxs-lookup"><span data-stu-id="b4837-213">Once Azure finishes configuring your new custom domain name, navigate to your custom domain name in a browser.</span></span> <span data-ttu-id="b4837-214">The browser should open your Azure app, which means that your custom domain name is configured properly.</span><span class="sxs-lookup"><span data-stu-id="b4837-214">The browser should open your Azure app, which means that your custom domain name is configured properly.</span></span>

## <a name="migrate-an-active-domain-name"></a><span data-ttu-id="b4837-215">Migrate an active domain name</span><span class="sxs-lookup"><span data-stu-id="b4837-215">Migrate an active domain name</span></span>

<span data-ttu-id="b4837-216">If the domain name you want to map is already in use by an existing website, and you want to avoid downtime, see [Migrate an active custom domain to App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b4837-216">If the domain name you want to map is already in use by an existing website, and you want to avoid downtime, see [Migrate an active custom domain to App Service](app-service-custom-domain-name-migrate.md).</span></span>

<a name="verify"></a>

## <a name="verify-dns-propagation"></a><span data-ttu-id="b4837-217">Verify DNS propagation</span><span class="sxs-lookup"><span data-stu-id="b4837-217">Verify DNS propagation</span></span>
<span data-ttu-id="b4837-218">After you finish the configuration steps, it can take some time for the changes to propagate, depending on your DNS provider.</span><span class="sxs-lookup"><span data-stu-id="b4837-218">After you finish the configuration steps, it can take some time for the changes to propagate, depending on your DNS provider.</span></span> <span data-ttu-id="b4837-219">You can verify that the DNS propagation is working as expected by using [http://digwebinterface.com/](http://digwebinterface.com/).</span><span class="sxs-lookup"><span data-stu-id="b4837-219">You can verify that the DNS propagation is working as expected by using [http://digwebinterface.com/](http://digwebinterface.com/).</span></span> <span data-ttu-id="b4837-220">After you browse to the site, specify the hostnames in the textbox and click **Dig**.</span><span class="sxs-lookup"><span data-stu-id="b4837-220">After you browse to the site, specify the hostnames in the textbox and click **Dig**.</span></span> <span data-ttu-id="b4837-221">Verify the results to confirm if the recent changes have taken effect.</span><span class="sxs-lookup"><span data-stu-id="b4837-221">Verify the results to confirm if the recent changes have taken effect.</span></span>  

![Map a custom domain name to an Azure app: verify DNS propagation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-custom-domain-name/1-digwebinterface.png)

> [!NOTE]
> <span data-ttu-id="b4837-223">The propagation of the DNS entries can take up to 48 hours (sometimes longer).</span><span class="sxs-lookup"><span data-stu-id="b4837-223">The propagation of the DNS entries can take up to 48 hours (sometimes longer).</span></span> <span data-ttu-id="b4837-224">If you have configured everything correctly, you still need to wait for the propagation to succeed.</span><span class="sxs-lookup"><span data-stu-id="b4837-224">If you have configured everything correctly, you still need to wait for the propagation to succeed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b4837-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4837-225">Next steps</span></span>
<span data-ttu-id="b4837-226">Learn how to secure your custom domain name with HTTPS by [buying an SSL certificate in Azure](web-sites-purchase-ssl-web-site.md) or [using an SSL certificate from elsewhere](web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="b4837-226">Learn how to secure your custom domain name with HTTPS by [buying an SSL certificate in Azure](web-sites-purchase-ssl-web-site.md) or [using an SSL certificate from elsewhere](web-sites-configure-ssl-certificate.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b4837-227">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="b4837-227">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b4837-228">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="b4837-228">No credit cards required; no commitments.</span></span>
> 
> 

[<span data-ttu-id="b4837-229">Get started with Azure DNS</span><span class="sxs-lookup"><span data-stu-id="b4837-229">Get started with Azure DNS</span></span>](../dns/dns-getstarted-create-dnszone.md)  
[<span data-ttu-id="b4837-230">Create DNS records for a web app in a custom domain</span><span class="sxs-lookup"><span data-stu-id="b4837-230">Create DNS records for a web app in a custom domain</span></span>](../dns/dns-web-sites-custom-domain.md)  
[<span data-ttu-id="b4837-231">Delegate Domain to Azure DNS</span><span class="sxs-lookup"><span data-stu-id="b4837-231">Delegate Domain to Azure DNS</span></span>](../dns/dns-domain-delegation.md)

<!-- Images -->
[subdomain]: media/web-sites-custom-domain-name/azurewebsites-subdomain.png



