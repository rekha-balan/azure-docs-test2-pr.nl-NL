---
title: Migrate an active DNS name to Azure App Service | Microsoft Docs
description: Learn how to migrate a custom DNS domain name that is already assigned to a live site to Azure App Service without any downtime.
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
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: a5d031622103183fa9aa7a3f3771a055fc16edb2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870778"
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="356ff-103">Migrate an active DNS name to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="356ff-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="356ff-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-web-overview.md) without any downtime.</span><span class="sxs-lookup"><span data-stu-id="356ff-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-web-overview.md) without any downtime.</span></span>

<span data-ttu-id="356ff-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span><span class="sxs-lookup"><span data-stu-id="356ff-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="356ff-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span><span class="sxs-lookup"><span data-stu-id="356ff-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="356ff-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="356ff-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="356ff-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="356ff-108">Prerequisites</span></span>

<span data-ttu-id="356ff-109">To complete this how-to:</span><span class="sxs-lookup"><span data-stu-id="356ff-109">To complete this how-to:</span></span>

- <span data-ttu-id="356ff-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="356ff-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="356ff-111">Bind the domain name preemptively</span><span class="sxs-lookup"><span data-stu-id="356ff-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="356ff-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span><span class="sxs-lookup"><span data-stu-id="356ff-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="356ff-113">Verify domain ownership</span><span class="sxs-lookup"><span data-stu-id="356ff-113">Verify domain ownership</span></span>
- <span data-ttu-id="356ff-114">Enable the domain name for your app</span><span class="sxs-lookup"><span data-stu-id="356ff-114">Enable the domain name for your app</span></span>

<span data-ttu-id="356ff-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span><span class="sxs-lookup"><span data-stu-id="356ff-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="356ff-116">Create domain verification record</span><span class="sxs-lookup"><span data-stu-id="356ff-116">Create domain verification record</span></span>

<span data-ttu-id="356ff-117">To verify domain ownership, Add a TXT record.</span><span class="sxs-lookup"><span data-stu-id="356ff-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="356ff-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="356ff-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="356ff-119">The TXT record you need depends on the DNS record you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="356ff-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="356ff-120">For examples, see the following table (`@` typically represents the root domain):</span><span class="sxs-lookup"><span data-stu-id="356ff-120">For examples, see the following table (`@` typically represents the root domain):</span></span>

| <span data-ttu-id="356ff-121">DNS record example</span><span class="sxs-lookup"><span data-stu-id="356ff-121">DNS record example</span></span> | <span data-ttu-id="356ff-122">TXT Host</span><span class="sxs-lookup"><span data-stu-id="356ff-122">TXT Host</span></span> | <span data-ttu-id="356ff-123">TXT Value</span><span class="sxs-lookup"><span data-stu-id="356ff-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="356ff-124">\@ (root)</span><span class="sxs-lookup"><span data-stu-id="356ff-124">\@ (root)</span></span> | <span data-ttu-id="356ff-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="356ff-125">_awverify_</span></span> | <span data-ttu-id="356ff-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="356ff-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="356ff-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="356ff-127">www (sub)</span></span> | <span data-ttu-id="356ff-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="356ff-128">_awverify.www_</span></span> | <span data-ttu-id="356ff-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="356ff-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="356ff-130">\* (wildcard)</span><span class="sxs-lookup"><span data-stu-id="356ff-130">\* (wildcard)</span></span> | <span data-ttu-id="356ff-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="356ff-131">_awverify.\*_</span></span> | <span data-ttu-id="356ff-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="356ff-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="356ff-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="356ff-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="356ff-134">App Service supports mappings from CNAME and A records.</span><span class="sxs-lookup"><span data-stu-id="356ff-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="356ff-135">Enable the domain for your app</span><span class="sxs-lookup"><span data-stu-id="356ff-135">Enable the domain for your app</span></span>

<span data-ttu-id="356ff-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="356ff-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Custom domain menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="356ff-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="356ff-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Add host name](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="356ff-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="356ff-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="356ff-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span><span class="sxs-lookup"><span data-stu-id="356ff-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="356ff-142">Select **Validate**.</span><span class="sxs-lookup"><span data-stu-id="356ff-142">Select **Validate**.</span></span>

<span data-ttu-id="356ff-143">The **Add hostname** button is activated.</span><span class="sxs-lookup"><span data-stu-id="356ff-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="356ff-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="356ff-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="356ff-145">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="356ff-145">Select **Add hostname**.</span></span>

![Add DNS name to the app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="356ff-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="356ff-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="356ff-148">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="356ff-148">Try refreshing the browser to update the data.</span></span>

![CNAME record added](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="356ff-150">Your custom DNS name is now enabled in your Azure app.</span><span class="sxs-lookup"><span data-stu-id="356ff-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="356ff-151">Remap the active DNS name</span><span class="sxs-lookup"><span data-stu-id="356ff-151">Remap the active DNS name</span></span>

<span data-ttu-id="356ff-152">The only thing left to do is remapping your active DNS record to point to App Service.</span><span class="sxs-lookup"><span data-stu-id="356ff-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="356ff-153">Right now, it still points to your old site.</span><span class="sxs-lookup"><span data-stu-id="356ff-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="356ff-154">Copy the app's IP address (A record only)</span><span class="sxs-lookup"><span data-stu-id="356ff-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="356ff-155">If you are remapping a CNAME record, skip this section.</span><span class="sxs-lookup"><span data-stu-id="356ff-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="356ff-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="356ff-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="356ff-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="356ff-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="356ff-158">In the **Custom domains** page, copy the app's IP address.</span><span class="sxs-lookup"><span data-stu-id="356ff-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="356ff-160">Update the DNS record</span><span class="sxs-lookup"><span data-stu-id="356ff-160">Update the DNS record</span></span>

<span data-ttu-id="356ff-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span><span class="sxs-lookup"><span data-stu-id="356ff-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="356ff-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span><span class="sxs-lookup"><span data-stu-id="356ff-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="356ff-163">FQDN example</span><span class="sxs-lookup"><span data-stu-id="356ff-163">FQDN example</span></span> | <span data-ttu-id="356ff-164">Record type</span><span class="sxs-lookup"><span data-stu-id="356ff-164">Record type</span></span> | <span data-ttu-id="356ff-165">Host</span><span class="sxs-lookup"><span data-stu-id="356ff-165">Host</span></span> | <span data-ttu-id="356ff-166">Value</span><span class="sxs-lookup"><span data-stu-id="356ff-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="356ff-167">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="356ff-167">contoso.com (root)</span></span> | <span data-ttu-id="356ff-168">A</span><span class="sxs-lookup"><span data-stu-id="356ff-168">A</span></span> | `@` | <span data-ttu-id="356ff-169">IP address from [Copy the app's IP address](#info)</span><span class="sxs-lookup"><span data-stu-id="356ff-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="356ff-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="356ff-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="356ff-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="356ff-171">CNAME</span></span> | `www` | <span data-ttu-id="356ff-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="356ff-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="356ff-173">\*.contoso.com (wildcard)</span><span class="sxs-lookup"><span data-stu-id="356ff-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="356ff-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="356ff-174">CNAME</span></span> | _\*_ | <span data-ttu-id="356ff-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="356ff-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="356ff-176">Save your settings.</span><span class="sxs-lookup"><span data-stu-id="356ff-176">Save your settings.</span></span>

<span data-ttu-id="356ff-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span><span class="sxs-lookup"><span data-stu-id="356ff-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="356ff-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="356ff-178">Next steps</span></span>

<span data-ttu-id="356ff-179">Learn how to bind a custom SSL certificate to App Service.</span><span class="sxs-lookup"><span data-stu-id="356ff-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="356ff-180">Bind an existing custom SSL certificate to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="356ff-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
