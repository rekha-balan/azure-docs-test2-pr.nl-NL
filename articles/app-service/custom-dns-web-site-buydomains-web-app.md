---
title: Buy a custom domain name for Azure Web Apps
description: Learn how to buy a custom domain name with a web app in Azure App Service.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/24/2017
ms.author: cephalin
ms.openlocfilehash: 48e0e68794e83739835d97aa8a2b26516c660357
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864337"
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="ca2ac-103">Buy a custom domain name for Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="ca2ac-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="ca2ac-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="ca2ac-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="ca2ac-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="ca2ac-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="ca2ac-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="ca2ac-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca2ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca2ac-110">Prerequisites</span></span>

<span data-ttu-id="ca2ac-111">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="ca2ac-111">To complete this tutorial:</span></span>

* <span data-ttu-id="ca2ac-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="ca2ac-113">[Remove the spending limit on your subscription](../billing/billing-spending-limit.md#remove).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-113">[Remove the spending limit on your subscription](../billing/billing-spending-limit.md#remove).</span></span> <span data-ttu-id="ca2ac-114">You cannot buy App Service domains with free subscription credits.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-114">You cannot buy App Service domains with free subscription credits.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="ca2ac-115">Prepare the app</span><span class="sxs-lookup"><span data-stu-id="ca2ac-115">Prepare the app</span></span>

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

<span data-ttu-id="ca2ac-116">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-116">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="ca2ac-117">In this step, you make sure that the web app is in the supported pricing tier.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-117">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="ca2ac-118">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="ca2ac-118">Sign in to Azure</span></span>

<span data-ttu-id="ca2ac-119">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-119">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="ca2ac-120">Navigate to the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ca2ac-120">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="ca2ac-121">From the left menu, select **App Services**, and then select the name of the app.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-121">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="ca2ac-123">You see the management page of the App Service app.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-123">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="ca2ac-124">Check the pricing tier</span><span class="sxs-lookup"><span data-stu-id="ca2ac-124">Check the pricing tier</span></span>

<span data-ttu-id="ca2ac-125">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-125">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Scale-up menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="ca2ac-127">The app's current tier is highlighted by a blue border.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-127">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="ca2ac-128">Check to make sure that the app is not in the **F1** tier.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-128">Check to make sure that the app is not in the **F1** tier.</span></span> <span data-ttu-id="ca2ac-129">Custom DNS is not supported in the **F1** tier.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-129">Custom DNS is not supported in the **F1** tier.</span></span> 

![Check pricing tier](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="ca2ac-131">If the App Service plan is not in the **F1** tier, close the **Scale up** page and skip to [Buy the domain](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-131">If the App Service plan is not in the **F1** tier, close the **Scale up** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="ca2ac-132">Scale up the App Service plan</span><span class="sxs-lookup"><span data-stu-id="ca2ac-132">Scale up the App Service plan</span></span>

<span data-ttu-id="ca2ac-133">Select any of the non-free tiers (**D1**, **B1**, **B2**, **B3**, or any tier in the **Production** category).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-133">Select any of the non-free tiers (**D1**, **B1**, **B2**, **B3**, or any tier in the **Production** category).</span></span> <span data-ttu-id="ca2ac-134">For additional options, click **See additional options**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-134">For additional options, click **See additional options**.</span></span>

<span data-ttu-id="ca2ac-135">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-135">Click **Apply**.</span></span>

![Check pricing tier](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="ca2ac-137">When you see the following notification, the scale operation is complete.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-137">When you see the following notification, the scale operation is complete.</span></span>

![Scale operation confirmation](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="ca2ac-139">Buy the domain</span><span class="sxs-lookup"><span data-stu-id="ca2ac-139">Buy the domain</span></span>

### <a name="pricing-information"></a><span data-ttu-id="ca2ac-140">Pricing Information</span><span class="sxs-lookup"><span data-stu-id="ca2ac-140">Pricing Information</span></span>
<span data-ttu-id="ca2ac-141">For pricing information on Azure App Service Domains, please visit the [App Service Pricing page](https://azure.microsoft.com/pricing/details/app-service/windows/) and scroll down to App Service Domain.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-141">For pricing information on Azure App Service Domains, please visit the [App Service Pricing page](https://azure.microsoft.com/pricing/details/app-service/windows/) and scroll down to App Service Domain.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="ca2ac-142">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="ca2ac-142">Sign in to Azure</span></span>
<span data-ttu-id="ca2ac-143">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-143">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="ca2ac-144">Launch Buy domains</span><span class="sxs-lookup"><span data-stu-id="ca2ac-144">Launch Buy domains</span></span>
<span data-ttu-id="ca2ac-145">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span><span class="sxs-lookup"><span data-stu-id="ca2ac-145">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ca2ac-146">In the **Custom domains** page, click **Buy Domain**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-146">In the **Custom domains** page, click **Buy Domain**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

> [!NOTE]
> <span data-ttu-id="ca2ac-147">If you cannot see the **App Service Domains** section, you need to remove the spending limit on your Azure account (see [Prerequisites](#prerequisites)).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-147">If you cannot see the **App Service Domains** section, you need to remove the spending limit on your Azure account (see [Prerequisites](#prerequisites)).</span></span>
>
>

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="ca2ac-148">Configure the domain purchase</span><span class="sxs-lookup"><span data-stu-id="ca2ac-148">Configure the domain purchase</span></span>

<span data-ttu-id="ca2ac-149">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-149">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="ca2ac-150">The suggested available domains are shown just below the text box.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-150">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="ca2ac-151">Select one or more domains you want to buy.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-151">Select one or more domains you want to buy.</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

> [!NOTE]
> <span data-ttu-id="ca2ac-152">The following [top-level domains](https://wikipedia.org/wiki/Top-level_domain) are supported by App Service domains: _com_, _net_, _co.uk_, _org_, _nl_, _in_, _biz_, _org.uk_, and _co.in_.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-152">The following [top-level domains](https://wikipedia.org/wiki/Top-level_domain) are supported by App Service domains: _com_, _net_, _co.uk_, _org_, _nl_, _in_, _biz_, _org.uk_, and _co.in_.</span></span>
>
>

<span data-ttu-id="ca2ac-153">Click the **Contact Information** and fill out the domain's contact information form.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-153">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="ca2ac-154">When finished, click **OK** to return to the App Service Domain page.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-154">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="ca2ac-155">It is important that you fill out all required fields with as much accuracy as possible.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-155">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="ca2ac-156">Incorrect data for contact information can result in failure to purchase domains.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-156">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="ca2ac-157">Next, select the desired options for your domain.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-157">Next, select the desired options for your domain.</span></span> <span data-ttu-id="ca2ac-158">See the following table for explanations:</span><span class="sxs-lookup"><span data-stu-id="ca2ac-158">See the following table for explanations:</span></span>

| <span data-ttu-id="ca2ac-159">Setting</span><span class="sxs-lookup"><span data-stu-id="ca2ac-159">Setting</span></span> | <span data-ttu-id="ca2ac-160">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="ca2ac-160">Suggested Value</span></span> | <span data-ttu-id="ca2ac-161">Description</span><span class="sxs-lookup"><span data-stu-id="ca2ac-161">Description</span></span> |
|-|-|-|
|<span data-ttu-id="ca2ac-162">Privacy protection</span><span class="sxs-lookup"><span data-stu-id="ca2ac-162">Privacy protection</span></span> | <span data-ttu-id="ca2ac-163">Enable</span><span class="sxs-lookup"><span data-stu-id="ca2ac-163">Enable</span></span> | <span data-ttu-id="ca2ac-164">Opt in to "Privacy protection", which is included in the purchase price _for free_.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-164">Opt in to "Privacy protection", which is included in the purchase price _for free_.</span></span> <span data-ttu-id="ca2ac-165">Some top-level domains are managed by registrars that do not support privacy protection, and they are listed on the **Privacy protection** page.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-165">Some top-level domains are managed by registrars that do not support privacy protection, and they are listed on the **Privacy protection** page.</span></span> |
| <span data-ttu-id="ca2ac-166">Assign default hostnames</span><span class="sxs-lookup"><span data-stu-id="ca2ac-166">Assign default hostnames</span></span> | <span data-ttu-id="ca2ac-167">**www** and **@**</span><span class="sxs-lookup"><span data-stu-id="ca2ac-167">**www** and **@**</span></span> | <span data-ttu-id="ca2ac-168">Select the desired hostname bindings, if desired.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-168">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="ca2ac-169">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-169">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="ca2ac-170">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-170">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="ca2ac-171">You can make changes to the hostname assignments after the domain purchase completes.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-171">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="ca2ac-172">Accept terms and purchase</span><span class="sxs-lookup"><span data-stu-id="ca2ac-172">Accept terms and purchase</span></span>

<span data-ttu-id="ca2ac-173">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-173">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="ca2ac-174">App Service Domains use Azure DNS to host the domains.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-174">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="ca2ac-175">In addition to the domain registration fee, usage charges for Azure DNS apply.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-175">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="ca2ac-176">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-176">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="ca2ac-177">Back in the **App Service Domain** page, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-177">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="ca2ac-178">While the operation is in progress, you see the following notifications:</span><span class="sxs-lookup"><span data-stu-id="ca2ac-178">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="ca2ac-179">Test the hostnames</span><span class="sxs-lookup"><span data-stu-id="ca2ac-179">Test the hostnames</span></span>

<span data-ttu-id="ca2ac-180">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-180">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="ca2ac-181">You also see the selected hostnames in the **Custom domains** page, in the **Custom Hostnames** section.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-181">You also see the selected hostnames in the **Custom domains** page, in the **Custom Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="ca2ac-182">To test the hostnames, navigate to the listed hostnames in the browser.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-182">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="ca2ac-183">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-183">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="ca2ac-184">Assign hostnames to web app</span><span class="sxs-lookup"><span data-stu-id="ca2ac-184">Assign hostnames to web app</span></span>

<span data-ttu-id="ca2ac-185">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-185">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="ca2ac-186">You can also assign hostnames in the App Service Domain to any other web app.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-186">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="ca2ac-187">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-187">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="ca2ac-188">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-188">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="ca2ac-189">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-189">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="ca2ac-190">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-190">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="ca2ac-191">Same subscription: Use the following steps.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-191">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="ca2ac-192">Launch add hostname</span><span class="sxs-lookup"><span data-stu-id="ca2ac-192">Launch add hostname</span></span>
<span data-ttu-id="ca2ac-193">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-193">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ca2ac-194">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-194">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="ca2ac-195">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-195">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="ca2ac-196">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-196">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="ca2ac-197">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-197">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="ca2ac-198">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-198">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="ca2ac-199">Configure hostname</span><span class="sxs-lookup"><span data-stu-id="ca2ac-199">Configure hostname</span></span>
<span data-ttu-id="ca2ac-200">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-200">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="ca2ac-201">For example:</span><span class="sxs-lookup"><span data-stu-id="ca2ac-201">For example:</span></span>

- <span data-ttu-id="ca2ac-202">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ca2ac-202">kontoso.net</span></span>
- <span data-ttu-id="ca2ac-203">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ca2ac-203">www.kontoso.net</span></span>
- <span data-ttu-id="ca2ac-204">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ca2ac-204">abc.kontoso.net</span></span>

<span data-ttu-id="ca2ac-205">When finished, select **Validate**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-205">When finished, select **Validate**.</span></span> <span data-ttu-id="ca2ac-206">The hostname record type is automatically selected for you.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-206">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="ca2ac-207">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-207">Select **Add hostname**.</span></span>

<span data-ttu-id="ca2ac-208">When the operation is complete, you see a success notification for the assigned hostname.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-208">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="ca2ac-209">Close add hostname</span><span class="sxs-lookup"><span data-stu-id="ca2ac-209">Close add hostname</span></span>
<span data-ttu-id="ca2ac-210">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-210">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="ca2ac-211">When finished, close the **Add hostname** page.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-211">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="ca2ac-212">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-212">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="ca2ac-213">Test the hostnames</span><span class="sxs-lookup"><span data-stu-id="ca2ac-213">Test the hostnames</span></span>

<span data-ttu-id="ca2ac-214">Navigate to the listed hostnames in the browser.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-214">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="ca2ac-215">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-215">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

## <a name="renew-the-domain"></a><span data-ttu-id="ca2ac-216">Renew the domain</span><span class="sxs-lookup"><span data-stu-id="ca2ac-216">Renew the domain</span></span>

<span data-ttu-id="ca2ac-217">The App Service domain you bought is valid for one year from the time of purchase.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-217">The App Service domain you bought is valid for one year from the time of purchase.</span></span> <span data-ttu-id="ca2ac-218">By default, the domain is configured to renew automatically by charging your payment method for the next year.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-218">By default, the domain is configured to renew automatically by charging your payment method for the next year.</span></span> <span data-ttu-id="ca2ac-219">If you want to turn off automatic renewal, or if you want to manually renew your domain, follow the steps here.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-219">If you want to turn off automatic renewal, or if you want to manually renew your domain, follow the steps here.</span></span>

<span data-ttu-id="ca2ac-220">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-220">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ca2ac-221">In the **App Service Domains** section, select the domain you want to configure.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-221">In the **App Service Domains** section, select the domain you want to configure.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

<span data-ttu-id="ca2ac-222">From the left navigation of the domain, select **Domain renewal**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-222">From the left navigation of the domain, select **Domain renewal**.</span></span> <span data-ttu-id="ca2ac-223">To stop renewing your domain automatically, select **Off**, and then **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-223">To stop renewing your domain automatically, select **Off**, and then **Save**.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-autorenew.png)

<span data-ttu-id="ca2ac-224">To manually renew your domain, select **Renew domain**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-224">To manually renew your domain, select **Renew domain**.</span></span> <span data-ttu-id="ca2ac-225">However, this button is not active until 90 days before the domain's expiration.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-225">However, this button is not active until 90 days before the domain's expiration.</span></span>

<a name="custom"></a>

## <a name="manage-custom-dns-records"></a><span data-ttu-id="ca2ac-226">Manage custom DNS records</span><span class="sxs-lookup"><span data-stu-id="ca2ac-226">Manage custom DNS records</span></span>

<span data-ttu-id="ca2ac-227">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-227">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="ca2ac-228">You can add, remove, and update DNS records, just like for an externally purchased domain.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-228">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ca2ac-229">Open App Service Domain</span><span class="sxs-lookup"><span data-stu-id="ca2ac-229">Open App Service Domain</span></span>

<span data-ttu-id="ca2ac-230">In the Azure portal, from the left menu, select **All services** > **App Service Domains**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-230">In the Azure portal, from the left menu, select **All services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ca2ac-231">Select the domain to manage.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-231">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="ca2ac-232">Access DNS zone</span><span class="sxs-lookup"><span data-stu-id="ca2ac-232">Access DNS zone</span></span>

<span data-ttu-id="ca2ac-233">In the domain's left menu, select **DNS zone**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-233">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="ca2ac-234">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-234">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="ca2ac-235">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-235">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="ca2ac-236">Cancel purchase (delete domain)</span><span class="sxs-lookup"><span data-stu-id="ca2ac-236">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="ca2ac-237">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-237">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="ca2ac-238">After five days, you can delete the App Service Domain, but cannot receive a refund.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-238">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ca2ac-239">Open App Service Domain</span><span class="sxs-lookup"><span data-stu-id="ca2ac-239">Open App Service Domain</span></span>

<span data-ttu-id="ca2ac-240">In the Azure portal, from the left menu, select **All services** > **App Service Domains**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-240">In the Azure portal, from the left menu, select **All services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ca2ac-241">Select the domain to you want to cancel or delete.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-241">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="ca2ac-242">Delete hostname bindings</span><span class="sxs-lookup"><span data-stu-id="ca2ac-242">Delete hostname bindings</span></span>

<span data-ttu-id="ca2ac-243">In the domain's left menu, select **Hostname bindings**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-243">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="ca2ac-244">The hostname bindings from all Azure services are listed here.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-244">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="ca2ac-245">You cannot delete the App Service Domain until all hostname bindings are deleted.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-245">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="ca2ac-246">Delete each hostname binding by selecting **...** > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-246">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="ca2ac-247">After all the bindings are deleted, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-247">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="ca2ac-248">Cancel or delete</span><span class="sxs-lookup"><span data-stu-id="ca2ac-248">Cancel or delete</span></span>

<span data-ttu-id="ca2ac-249">In the domain's left menu, select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-249">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="ca2ac-250">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-250">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="ca2ac-251">Otherwise, you see a **Delete** button instead.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-251">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="ca2ac-252">To delete the domain without a refund, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-252">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="ca2ac-253">To confirm the operation, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-253">To confirm the operation, select **Yes**.</span></span>

<span data-ttu-id="ca2ac-254">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-254">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 

## <a name="direct-default-url-to-a-custom-directory"></a><span data-ttu-id="ca2ac-255">Direct default URL to a custom directory</span><span class="sxs-lookup"><span data-stu-id="ca2ac-255">Direct default URL to a custom directory</span></span>

<span data-ttu-id="ca2ac-256">By default, App Service directs web requests to the root directory of your app code.</span><span class="sxs-lookup"><span data-stu-id="ca2ac-256">By default, App Service directs web requests to the root directory of your app code.</span></span> <span data-ttu-id="ca2ac-257">To direct them to a subdirectory, such as `public`, see [Direct default URL to a custom directory](app-service-web-tutorial-custom-domain.md#virtualdir).</span><span class="sxs-lookup"><span data-stu-id="ca2ac-257">To direct them to a subdirectory, such as `public`, see [Direct default URL to a custom directory](app-service-web-tutorial-custom-domain.md#virtualdir).</span></span>

## <a name="more-resources"></a><span data-ttu-id="ca2ac-258">More resources</span><span class="sxs-lookup"><span data-stu-id="ca2ac-258">More resources</span></span>

[<span data-ttu-id="ca2ac-259">FAQ : App Service Domain (preview) and Custom Domains</span><span class="sxs-lookup"><span data-stu-id="ca2ac-259">FAQ : App Service Domain (preview) and Custom Domains</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/08/08/faq-app-service-domain-preview-and-custom-domains/)
