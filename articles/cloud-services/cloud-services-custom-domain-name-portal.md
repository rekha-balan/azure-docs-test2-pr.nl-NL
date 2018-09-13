---
title: Configure a custom domain name in Cloud Services | Microsoft Docs
description: Learn how to expose your Azure application or data to the internet on a custom domain by configuring DNS settings.  These examples use the Azure portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: d156d34dfd47f37bc415fafa5f2b908828ee8de0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554951"
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="b3885-104">Configuring a custom domain name for an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="b3885-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-custom-domain-name-portal.md)
> * [Azure classic portal](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="b3885-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b3885-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="b3885-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b3885-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="b3885-109">Azure also assigns a virtual IP address.</span><span class="sxs-lookup"><span data-stu-id="b3885-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="b3885-110">However, you can also expose your application on your own domain name, such as **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b3885-110">However, you can also expose your application on your own domain name, such as **contoso.com**.</span></span> <span data-ttu-id="b3885-111">This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span><span class="sxs-lookup"><span data-stu-id="b3885-111">This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="b3885-112">Do you already understand what CNAME and A records are?</span><span class="sxs-lookup"><span data-stu-id="b3885-112">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="b3885-113">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="b3885-113">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> The procedures in this task apply to Azure Cloud Services. For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md). For storage accounts, see [this](../storage/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!  It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="b3885-119">Understand CNAME and A records</span><span class="sxs-lookup"><span data-stu-id="b3885-119">Understand CNAME and A records</span></span>
<span data-ttu-id="b3885-120">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span><span class="sxs-lookup"><span data-stu-id="b3885-120">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="b3885-121">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span><span class="sxs-lookup"><span data-stu-id="b3885-121">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="b3885-122">CNAME or Alias record</span><span class="sxs-lookup"><span data-stu-id="b3885-122">CNAME or Alias record</span></span>
<span data-ttu-id="b3885-123">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span><span class="sxs-lookup"><span data-stu-id="b3885-123">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="b3885-124">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span><span class="sxs-lookup"><span data-stu-id="b3885-124">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="b3885-125">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="b3885-125">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="b3885-126">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span><span class="sxs-lookup"><span data-stu-id="b3885-126">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.
> 
> 

### <a name="a-record"></a><span data-ttu-id="b3885-129">A record</span><span class="sxs-lookup"><span data-stu-id="b3885-129">A record</span></span>
<span data-ttu-id="b3885-130">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span><span class="sxs-lookup"><span data-stu-id="b3885-130">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="b3885-131">In the case of an Azure Cloud Service, the virtual IP of the service.</span><span class="sxs-lookup"><span data-stu-id="b3885-131">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="b3885-132">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="b3885-132">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service. The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.
> 
> Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment. For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="b3885-137">Add a CNAME record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="b3885-137">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="b3885-138">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span><span class="sxs-lookup"><span data-stu-id="b3885-138">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="b3885-139">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span><span class="sxs-lookup"><span data-stu-id="b3885-139">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="b3885-140">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="b3885-140">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="b3885-141">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span><span class="sxs-lookup"><span data-stu-id="b3885-141">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![quick glance section showing the site URL][csurl]
     
       <span data-ttu-id="b3885-143">**OR**</span><span class="sxs-lookup"><span data-stu-id="b3885-143">**OR**</span></span>
   * <span data-ttu-id="b3885-144">Install and configure [Azure Powershell](/powershell/azureps-cmdlets-docs), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="b3885-144">Install and configure [Azure Powershell](/powershell/azureps-cmdlets-docs), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="b3885-145">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span><span class="sxs-lookup"><span data-stu-id="b3885-145">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="b3885-146">Log on to your DNS registrar's website and go to the page for managing DNS.</span><span class="sxs-lookup"><span data-stu-id="b3885-146">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="b3885-147">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="b3885-147">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="b3885-148">Now find where you can select or enter CNAME's.</span><span class="sxs-lookup"><span data-stu-id="b3885-148">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="b3885-149">You may have to select the record type from a drop down, or go to an advanced settings page.</span><span class="sxs-lookup"><span data-stu-id="b3885-149">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="b3885-150">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span><span class="sxs-lookup"><span data-stu-id="b3885-150">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="b3885-151">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="b3885-151">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**.</span></span> <span data-ttu-id="b3885-152">If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span><span class="sxs-lookup"><span data-stu-id="b3885-152">If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="b3885-153">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span><span class="sxs-lookup"><span data-stu-id="b3885-153">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="b3885-154">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span><span class="sxs-lookup"><span data-stu-id="b3885-154">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="b3885-155">Alias/Host name/Subdomain</span><span class="sxs-lookup"><span data-stu-id="b3885-155">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="b3885-156">Canonical domain</span><span class="sxs-lookup"><span data-stu-id="b3885-156">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="b3885-157">www</span><span class="sxs-lookup"><span data-stu-id="b3885-157">www</span></span> |<span data-ttu-id="b3885-158">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b3885-158">contoso.cloudapp.net</span></span> |

> [!NOTE]
> A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.
> 
> The example above only applies to traffic at the **www** subdomain. Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain. If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="b3885-163">Add an A record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="b3885-163">Add an A record for your custom domain</span></span>
<span data-ttu-id="b3885-164">To create an A record, you must first find the virtual IP address of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="b3885-164">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="b3885-165">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span><span class="sxs-lookup"><span data-stu-id="b3885-165">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="b3885-166">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span><span class="sxs-lookup"><span data-stu-id="b3885-166">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="b3885-167">Use one of the following methods to get the IP address of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="b3885-167">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="b3885-168">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span><span class="sxs-lookup"><span data-stu-id="b3885-168">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![quick glance section showing the VIP][vip]
     
       <span data-ttu-id="b3885-170">**OR**</span><span class="sxs-lookup"><span data-stu-id="b3885-170">**OR**</span></span>
   * <span data-ttu-id="b3885-171">Install and configure [Azure Powershell](/powershell/azureps-cmdlets-docs), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="b3885-171">Install and configure [Azure Powershell](/powershell/azureps-cmdlets-docs), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="b3885-172">Save the IP address, as you will need it when creating an A record.</span><span class="sxs-lookup"><span data-stu-id="b3885-172">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="b3885-173">Log on to your DNS registrar's website and go to the page for managing DNS.</span><span class="sxs-lookup"><span data-stu-id="b3885-173">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="b3885-174">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="b3885-174">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="b3885-175">Now find where you can select or enter A record's.</span><span class="sxs-lookup"><span data-stu-id="b3885-175">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="b3885-176">You may have to select the record type from a drop down, or go to an advanced settings page.</span><span class="sxs-lookup"><span data-stu-id="b3885-176">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="b3885-177">Select or enter the domain or subdomain that will use this A record.</span><span class="sxs-lookup"><span data-stu-id="b3885-177">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="b3885-178">For example, select **www** if you want to create an alias for **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="b3885-178">For example, select **www** if you want to create an alias for **www.customdomain.com**.</span></span> <span data-ttu-id="b3885-179">If you want to create a wildcard entry for all subdomains, enter '\*\*\*\*\*'.</span><span class="sxs-lookup"><span data-stu-id="b3885-179">If you want to create a wildcard entry for all subdomains, enter '\*\*\*\*\*'.</span></span> <span data-ttu-id="b3885-180">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="b3885-180">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="b3885-181">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span><span class="sxs-lookup"><span data-stu-id="b3885-181">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="b3885-182">Enter the IP address of your cloud service in the provided field.</span><span class="sxs-lookup"><span data-stu-id="b3885-182">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="b3885-183">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="b3885-183">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="b3885-184">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span><span class="sxs-lookup"><span data-stu-id="b3885-184">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="b3885-185">Host name/Subdomain</span><span class="sxs-lookup"><span data-stu-id="b3885-185">Host name/Subdomain</span></span> | <span data-ttu-id="b3885-186">IP address</span><span class="sxs-lookup"><span data-stu-id="b3885-186">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="b3885-187">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="b3885-187">137.135.70.239</span></span> |

<span data-ttu-id="b3885-188">This example demonstrates creating an A record for the root domain.</span><span class="sxs-lookup"><span data-stu-id="b3885-188">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="b3885-189">If you wish to create a wildcard entry to cover all subdomains, you would enter '\*\*\*\*\*' as the subdomain.</span><span class="sxs-lookup"><span data-stu-id="b3885-189">If you wish to create a wildcard entry to cover all subdomains, you would enter '\*\*\*\*\*' as the subdomain.</span></span>

> [!WARNING]
> IP addresses in Azure are dynamic by default. You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b3885-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="b3885-192">Next steps</span></span>
* [<span data-ttu-id="b3885-193">How to Manage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b3885-193">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="b3885-194">How to Map CDN Content to a Custom Domain</span><span class="sxs-lookup"><span data-stu-id="b3885-194">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="b3885-195">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3885-195">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="b3885-196">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3885-196">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="b3885-197">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3885-197">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure portal]: https://portal.azure.com
[vip]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-custom-domain-name-portal/csurl.png


