---
title: Migrate an active custom domain to Azure App Service | Microsoft Docs
description: Learn how to migrate a custom domain that is already assigned to a live site to your app in Azure App Service without any downtime.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: cephalin
ms.openlocfilehash: d6d506eef720488969c5b33fe4b94c02752c6b58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553766"
---
# <a name="migrate-an-active-custom-domain-to-azure-app-service"></a><span data-ttu-id="5f54b-103">Migrate an active custom domain to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5f54b-103">Migrate an active custom domain to Azure App Service</span></span>

<span data-ttu-id="5f54b-104">This article shows you how to migrate an active custom domain to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span><span class="sxs-lookup"><span data-stu-id="5f54b-104">This article shows you how to migrate an active custom domain to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="5f54b-105">When you migrate a live site and its domain name to App Service, that domain name is already serving live traffic, and you don't want any downtime in DNS resolution during the migration process.</span><span class="sxs-lookup"><span data-stu-id="5f54b-105">When you migrate a live site and its domain name to App Service, that domain name is already serving live traffic, and you don't want any downtime in DNS resolution during the migration process.</span></span> <span data-ttu-id="5f54b-106">In this case, you need to preemptively bind the domain name to your Azure app for domain verification.</span><span class="sxs-lookup"><span data-stu-id="5f54b-106">In this case, you need to preemptively bind the domain name to your Azure app for domain verification.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5f54b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5f54b-107">Prerequisites</span></span>

<span data-ttu-id="5f54b-108">This article assumes that you already know how to [manually map a custom domain to App Service](web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5f54b-108">This article assumes that you already know how to [manually map a custom domain to App Service](web-sites-custom-domain-name.md).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="5f54b-109">Bind the domain name preemptively</span><span class="sxs-lookup"><span data-stu-id="5f54b-109">Bind the domain name preemptively</span></span>

<span data-ttu-id="5f54b-110">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span><span class="sxs-lookup"><span data-stu-id="5f54b-110">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="5f54b-111">Verify domain ownership</span><span class="sxs-lookup"><span data-stu-id="5f54b-111">Verify domain ownership</span></span>
- <span data-ttu-id="5f54b-112">Enable the domain name for your app</span><span class="sxs-lookup"><span data-stu-id="5f54b-112">Enable the domain name for your app</span></span>

<span data-ttu-id="5f54b-113">When you finally change the DNS record to point to your App Service app, clients are redirected from your old site to your App Service app without any downtime in DNS resolution.</span><span class="sxs-lookup"><span data-stu-id="5f54b-113">When you finally change the DNS record to point to your App Service app, clients are redirected from your old site to your App Service app without any downtime in DNS resolution.</span></span>

<span data-ttu-id="5f54b-114">Follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5f54b-114">Follow the steps below:</span></span>

1. <span data-ttu-id="5f54b-115">First, create a verification TXT record with your DNS registry by following the steps at [Create the DNS record(s)](web-sites-custom-domain-name.md#createdns).</span><span class="sxs-lookup"><span data-stu-id="5f54b-115">First, create a verification TXT record with your DNS registry by following the steps at [Create the DNS record(s)](web-sites-custom-domain-name.md#createdns).</span></span>
<span data-ttu-id="5f54b-116">Your additional TXT record takes on the convention that maps from &lt;*subdomain*>.&lt;*rootdomain*> to &lt;*appname*>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="5f54b-116">Your additional TXT record takes on the convention that maps from &lt;*subdomain*>.&lt;*rootdomain*> to &lt;*appname*>.azurewebsites.net.</span></span>
<span data-ttu-id="5f54b-117">See the following table for examples:</span><span class="sxs-lookup"><span data-stu-id="5f54b-117">See the following table for examples:</span></span>  
 
    <table cellspacing="0" border="1">
    <tr>
    <th><span data-ttu-id="5f54b-118">FQDN example</span><span class="sxs-lookup"><span data-stu-id="5f54b-118">FQDN example</span></span></th>
    <th><span data-ttu-id="5f54b-119">TXT Host</span><span class="sxs-lookup"><span data-stu-id="5f54b-119">TXT Host</span></span></th>
    <th><span data-ttu-id="5f54b-120">TXT Value</span><span class="sxs-lookup"><span data-stu-id="5f54b-120">TXT Value</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="5f54b-121">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="5f54b-121">contoso.com (root)</span></span></td>
    <td><span data-ttu-id="5f54b-122">awverify.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5f54b-122">awverify.contoso.com</span></span></td>
    <td><span data-ttu-id="5f54b-123">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5f54b-123">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5f54b-124">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="5f54b-124">www.contoso.com (sub)</span></span></td>
    <td><span data-ttu-id="5f54b-125">awverify.www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5f54b-125">awverify.www.contoso.com</span></span></td>
    <td><span data-ttu-id="5f54b-126">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5f54b-126">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5f54b-127">\*.contoso.com (wildcard)</span><span class="sxs-lookup"><span data-stu-id="5f54b-127">\*.contoso.com (wildcard)</span></span></td>
    <td><span data-ttu-id="5f54b-128">awverify.\*.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5f54b-128">awverify.\*.contoso.com</span></span></td>
    <td><span data-ttu-id="5f54b-129">&lt;<i>appname</i>>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5f54b-129">&lt;<i>appname</i>>.azurewebsites.net</span></span></td>
    </tr>
    </table>

2. <span data-ttu-id="5f54b-130">Then, add your custom domain name to your Azure app by following the steps at [Enable the custom domain name for your app](web-sites-custom-domain-name.md#enable).</span><span class="sxs-lookup"><span data-stu-id="5f54b-130">Then, add your custom domain name to your Azure app by following the steps at [Enable the custom domain name for your app](web-sites-custom-domain-name.md#enable).</span></span>

    <span data-ttu-id="5f54b-131">Your custom domain is now enabled in your Azure app.</span><span class="sxs-lookup"><span data-stu-id="5f54b-131">Your custom domain is now enabled in your Azure app.</span></span> <span data-ttu-id="5f54b-132">The only thing left to do is to update the DNS record with your domain registrar.</span><span class="sxs-lookup"><span data-stu-id="5f54b-132">The only thing left to do is to update the DNS record with your domain registrar.</span></span>

3. <span data-ttu-id="5f54b-133">Finally, update your domain's DNS record to point to your Azure app as is shown in [Create the DNS record(s)](web-sites-custom-domain-name.md#createdns).</span><span class="sxs-lookup"><span data-stu-id="5f54b-133">Finally, update your domain's DNS record to point to your Azure app as is shown in [Create the DNS record(s)](web-sites-custom-domain-name.md#createdns).</span></span> 

    <span data-ttu-id="5f54b-134">User traffic should be redirected to your Azure app immediately after DNS propagation happens.</span><span class="sxs-lookup"><span data-stu-id="5f54b-134">User traffic should be redirected to your Azure app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f54b-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f54b-135">Next steps</span></span>
<span data-ttu-id="5f54b-136">Learn how to secure your custom domain name with HTTPS by [buying an SSL certificate in Azure](web-sites-purchase-ssl-web-site.md) or [using an SSL certificate from elsewhere](web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="5f54b-136">Learn how to secure your custom domain name with HTTPS by [buying an SSL certificate in Azure](web-sites-purchase-ssl-web-site.md) or [using an SSL certificate from elsewhere](web-sites-configure-ssl-certificate.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5f54b-137">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="5f54b-137">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5f54b-138">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="5f54b-138">No credit cards required; no commitments.</span></span>
> 
> 

[<span data-ttu-id="5f54b-139">Get started with Azure DNS</span><span class="sxs-lookup"><span data-stu-id="5f54b-139">Get started with Azure DNS</span></span>](../dns/dns-getstarted-create-dnszone.md)  
[<span data-ttu-id="5f54b-140">Create DNS records for a web app in a custom domain</span><span class="sxs-lookup"><span data-stu-id="5f54b-140">Create DNS records for a web app in a custom domain</span></span>](../dns/dns-web-sites-custom-domain.md)  
[<span data-ttu-id="5f54b-141">Delegate Domain to Azure DNS</span><span class="sxs-lookup"><span data-stu-id="5f54b-141">Delegate Domain to Azure DNS</span></span>](../dns/dns-domain-delegation.md)

