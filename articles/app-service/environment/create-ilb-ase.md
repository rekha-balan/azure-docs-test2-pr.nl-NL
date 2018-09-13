---
title: Create and use an internal load balancer with an Azure App Service Environment
description: Details on how to create and use an internet-isolated Azure App Service Environment
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/12/2018
ms.author: ccompy
ms.custom: mvc
ms.openlocfilehash: e9d1f77a85d4b5cfb5bb7d3cb80380be3c79315d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869126"
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="edd86-103">Create and use an internal load balancer with an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="edd86-103">Create and use an internal load balancer with an App Service Environment</span></span> #

 <span data-ttu-id="edd86-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span><span class="sxs-lookup"><span data-stu-id="edd86-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="edd86-105">There are two ways to deploy an App Service Environment (ASE):</span><span class="sxs-lookup"><span data-stu-id="edd86-105">There are two ways to deploy an App Service Environment (ASE):</span></span> 

- <span data-ttu-id="edd86-106">With a VIP on an external IP address, often called an External ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="edd86-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="edd86-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="edd86-108">This article shows you how to create an ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="edd86-109">For an overview on the ASE, see [Introduction to App Service Environments][Intro].</span><span class="sxs-lookup"><span data-stu-id="edd86-109">For an overview on the ASE, see [Introduction to App Service Environments][Intro].</span></span> <span data-ttu-id="edd86-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="edd86-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="edd86-111">Overview</span><span class="sxs-lookup"><span data-stu-id="edd86-111">Overview</span></span> ##

<span data-ttu-id="edd86-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span><span class="sxs-lookup"><span data-stu-id="edd86-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="edd86-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span><span class="sxs-lookup"><span data-stu-id="edd86-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="edd86-114">When you deploy your ASE with an ILB, you must provide:</span><span class="sxs-lookup"><span data-stu-id="edd86-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="edd86-115">Your own domain that you use when you create your apps.</span><span class="sxs-lookup"><span data-stu-id="edd86-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="edd86-116">The certificate used for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="edd86-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="edd86-117">DNS management for your domain.</span><span class="sxs-lookup"><span data-stu-id="edd86-117">DNS management for your domain.</span></span>

<span data-ttu-id="edd86-118">In return, you can do things such as:</span><span class="sxs-lookup"><span data-stu-id="edd86-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="edd86-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span><span class="sxs-lookup"><span data-stu-id="edd86-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="edd86-120">Host apps in the cloud that aren't listed in public DNS servers.</span><span class="sxs-lookup"><span data-stu-id="edd86-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="edd86-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span><span class="sxs-lookup"><span data-stu-id="edd86-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="edd86-122">Disabled functionality</span><span class="sxs-lookup"><span data-stu-id="edd86-122">Disabled functionality</span></span> ###

<span data-ttu-id="edd86-123">There are some things that you can't do when you use an ILB ASE:</span><span class="sxs-lookup"><span data-stu-id="edd86-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="edd86-124">Use IP-based SSL.</span><span class="sxs-lookup"><span data-stu-id="edd86-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="edd86-125">Assign IP addresses to specific apps.</span><span class="sxs-lookup"><span data-stu-id="edd86-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="edd86-126">Buy and use a certificate with an app through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edd86-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="edd86-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span><span class="sxs-lookup"><span data-stu-id="edd86-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="edd86-128">You can't obtain them through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edd86-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="edd86-129">Create an ILB ASE</span><span class="sxs-lookup"><span data-stu-id="edd86-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="edd86-130">To create an ILB ASE:</span><span class="sxs-lookup"><span data-stu-id="edd86-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="edd86-131">In the Azure portal, select **Create a resource** > **Web** > **App Service Environment**.</span><span class="sxs-lookup"><span data-stu-id="edd86-131">In the Azure portal, select **Create a resource** > **Web** > **App Service Environment**.</span></span>

1. <span data-ttu-id="edd86-132">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="edd86-132">Select your subscription.</span></span>

1. <span data-ttu-id="edd86-133">Select or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="edd86-133">Select or create a resource group.</span></span>

1. <span data-ttu-id="edd86-134">Select or create a VNet.</span><span class="sxs-lookup"><span data-stu-id="edd86-134">Select or create a VNet.</span></span>

1. <span data-ttu-id="edd86-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="edd86-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="edd86-137">We recommend a size of `/24`, which has 256 addresses and can handle a maximum-sized ASE and any scaling needs.</span><span class="sxs-lookup"><span data-stu-id="edd86-137">We recommend a size of `/24`, which has 256 addresses and can handle a maximum-sized ASE and any scaling needs.</span></span> 

1. <span data-ttu-id="edd86-138">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span><span class="sxs-lookup"><span data-stu-id="edd86-138">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="edd86-139">Set the **VIP Type** to **Internal**.</span><span class="sxs-lookup"><span data-stu-id="edd86-139">Set the **VIP Type** to **Internal**.</span></span>

1. <span data-ttu-id="edd86-140">Enter a domain name.</span><span class="sxs-lookup"><span data-stu-id="edd86-140">Enter a domain name.</span></span> <span data-ttu-id="edd86-141">This domain is the one used for apps created in this ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-141">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="edd86-142">There are some restrictions.</span><span class="sxs-lookup"><span data-stu-id="edd86-142">There are some restrictions.</span></span> <span data-ttu-id="edd86-143">It can't be:</span><span class="sxs-lookup"><span data-stu-id="edd86-143">It can't be:</span></span>

    * <span data-ttu-id="edd86-144">net</span><span class="sxs-lookup"><span data-stu-id="edd86-144">net</span></span>   

    * <span data-ttu-id="edd86-145">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="edd86-145">azurewebsites.net</span></span>

    * <span data-ttu-id="edd86-146">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="edd86-146">p.azurewebsites.net</span></span>

    * <span data-ttu-id="edd86-147">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="edd86-147">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="edd86-148">There is a feature called custom domain names that allows you to map an existing DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="edd86-148">There is a feature called custom domain names that allows you to map an existing DNS name to your web app.</span></span> <span data-ttu-id="edd86-149">You can read more about that feature in the [Map an existing DNS name to your web app][customdomain] document.</span><span class="sxs-lookup"><span data-stu-id="edd86-149">You can read more about that feature in the [Map an existing DNS name to your web app][customdomain] document.</span></span> <span data-ttu-id="edd86-150">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span><span class="sxs-lookup"><span data-stu-id="edd86-150">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="edd86-151">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span><span class="sxs-lookup"><span data-stu-id="edd86-151">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="edd86-152">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="edd86-152">www.contoso.com</span></span>

    * <span data-ttu-id="edd86-153">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="edd86-153">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="edd86-154">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="edd86-154">abcd.contoso.com</span></span>

   <span data-ttu-id="edd86-155">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span><span class="sxs-lookup"><span data-stu-id="edd86-155">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="edd86-156">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="edd86-156">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

1. <span data-ttu-id="edd86-157">Select **OK**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="edd86-157">Select **OK**, and then select **Create**.</span></span>

    ![ASE creation][1]

<span data-ttu-id="edd86-159">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span><span class="sxs-lookup"><span data-stu-id="edd86-159">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="edd86-160">You can use it to select an External VIP or an Internal VIP.</span><span class="sxs-lookup"><span data-stu-id="edd86-160">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="edd86-161">The default is **External**.</span><span class="sxs-lookup"><span data-stu-id="edd86-161">The default is **External**.</span></span> <span data-ttu-id="edd86-162">If you select **External**, your ASE uses an internet-accessible VIP.</span><span class="sxs-lookup"><span data-stu-id="edd86-162">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="edd86-163">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span><span class="sxs-lookup"><span data-stu-id="edd86-163">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="edd86-164">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span><span class="sxs-lookup"><span data-stu-id="edd86-164">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="edd86-165">Instead, you need to provide the domain of the ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-165">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="edd86-166">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-166">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="edd86-167">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-167">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="edd86-168">You specify the domain explicitly.</span><span class="sxs-lookup"><span data-stu-id="edd86-168">You specify the domain explicitly.</span></span> <span data-ttu-id="edd86-169">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="edd86-169">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="edd86-170">Create an app in an ILB ASE</span><span class="sxs-lookup"><span data-stu-id="edd86-170">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="edd86-171">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span><span class="sxs-lookup"><span data-stu-id="edd86-171">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="edd86-172">In the Azure portal, select **Create a resource** > **Web + Mobile** > **Web App**.</span><span class="sxs-lookup"><span data-stu-id="edd86-172">In the Azure portal, select **Create a resource** > **Web + Mobile** > **Web App**.</span></span>

1. <span data-ttu-id="edd86-173">Enter the name of the app.</span><span class="sxs-lookup"><span data-stu-id="edd86-173">Enter the name of the app.</span></span>

1. <span data-ttu-id="edd86-174">Select the subscription.</span><span class="sxs-lookup"><span data-stu-id="edd86-174">Select the subscription.</span></span>

1. <span data-ttu-id="edd86-175">Select or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="edd86-175">Select or create a resource group.</span></span>

1. <span data-ttu-id="edd86-176">Select your OS.</span><span class="sxs-lookup"><span data-stu-id="edd86-176">Select your OS.</span></span> 

    * <span data-ttu-id="edd86-177">If you want to create a Linux app using a custom Docker container, you can just bring your own container using the instructions [here][linuxapp].</span><span class="sxs-lookup"><span data-stu-id="edd86-177">If you want to create a Linux app using a custom Docker container, you can just bring your own container using the instructions [here][linuxapp].</span></span> 

1. <span data-ttu-id="edd86-178">Select or create an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="edd86-178">Select or create an App Service plan.</span></span> <span data-ttu-id="edd86-179">If you want to create a new App Service plan, select your ASE as the location.</span><span class="sxs-lookup"><span data-stu-id="edd86-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="edd86-180">Select the worker pool where you want your App Service plan to be created.</span><span class="sxs-lookup"><span data-stu-id="edd86-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="edd86-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span><span class="sxs-lookup"><span data-stu-id="edd86-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="edd86-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

1. <span data-ttu-id="edd86-183">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="edd86-183">Select **Create**.</span></span> <span data-ttu-id="edd86-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span><span class="sxs-lookup"><span data-stu-id="edd86-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![App Service plan creation][2]

    <span data-ttu-id="edd86-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="edd86-187">Post-ILB ASE creation validation</span><span class="sxs-lookup"><span data-stu-id="edd86-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="edd86-188">An ILB ASE is slightly different than the non-ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="edd86-189">As already noted, you need to manage your own DNS.</span><span class="sxs-lookup"><span data-stu-id="edd86-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="edd86-190">You also have to provide your own certificate for HTTPS connections.</span><span class="sxs-lookup"><span data-stu-id="edd86-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="edd86-191">After you create your ASE, the domain name shows the domain you specified.</span><span class="sxs-lookup"><span data-stu-id="edd86-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="edd86-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span><span class="sxs-lookup"><span data-stu-id="edd86-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="edd86-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span><span class="sxs-lookup"><span data-stu-id="edd86-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="edd86-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span><span class="sxs-lookup"><span data-stu-id="edd86-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="edd86-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span><span class="sxs-lookup"><span data-stu-id="edd86-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="edd86-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span><span class="sxs-lookup"><span data-stu-id="edd86-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ASE domain name][3]

<span data-ttu-id="edd86-198">Your ILB ASE needs a valid SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="edd86-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="edd86-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="edd86-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="edd86-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span><span class="sxs-lookup"><span data-stu-id="edd86-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="edd86-201">**Subject**: This attribute must be set to \*.your-root-domain-here.</span><span class="sxs-lookup"><span data-stu-id="edd86-201">**Subject**: This attribute must be set to \*.your-root-domain-here.</span></span>
* <span data-ttu-id="edd86-202">**Subject Alternative Name**: This attribute must include both \**.your-root-domain-here* and \**.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="edd86-202">**Subject Alternative Name**: This attribute must include both \**.your-root-domain-here* and \**.scm.your-root-domain-here*.</span></span> <span data-ttu-id="edd86-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="edd86-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="edd86-204">Convert/save the SSL certificate as a .pfx file.</span><span class="sxs-lookup"><span data-stu-id="edd86-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="edd86-205">The .pfx file must include all intermediate and root certificates.</span><span class="sxs-lookup"><span data-stu-id="edd86-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="edd86-206">Secure it with a password.</span><span class="sxs-lookup"><span data-stu-id="edd86-206">Secure it with a password.</span></span>

<span data-ttu-id="edd86-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span><span class="sxs-lookup"><span data-stu-id="edd86-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="edd86-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="edd86-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="edd86-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span><span class="sxs-lookup"><span data-stu-id="edd86-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="edd86-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span><span class="sxs-lookup"><span data-stu-id="edd86-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Set ILB certificate][4]

<span data-ttu-id="edd86-212">To upload your own certificates and test access:</span><span class="sxs-lookup"><span data-stu-id="edd86-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="edd86-213">After the ASE is created, go to the ASE UI.</span><span class="sxs-lookup"><span data-stu-id="edd86-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="edd86-214">Select **ASE** > **Settings** > **ILB Certificate**.</span><span class="sxs-lookup"><span data-stu-id="edd86-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

1. <span data-ttu-id="edd86-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span><span class="sxs-lookup"><span data-stu-id="edd86-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="edd86-216">This step takes some time to process.</span><span class="sxs-lookup"><span data-stu-id="edd86-216">This step takes some time to process.</span></span> <span data-ttu-id="edd86-217">A message appears stating that an upload operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="edd86-217">A message appears stating that an upload operation is in progress.</span></span>

1. <span data-ttu-id="edd86-218">Get the ILB address for your ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="edd86-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span><span class="sxs-lookup"><span data-stu-id="edd86-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

1. <span data-ttu-id="edd86-220">Create a web app in your ASE after the ASE is created.</span><span class="sxs-lookup"><span data-stu-id="edd86-220">Create a web app in your ASE after the ASE is created.</span></span>

1. <span data-ttu-id="edd86-221">Create a VM if you don't have one in that VNet.</span><span class="sxs-lookup"><span data-stu-id="edd86-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edd86-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span><span class="sxs-lookup"><span data-stu-id="edd86-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >

1. <span data-ttu-id="edd86-223">Set the DNS for your ASE domain.</span><span class="sxs-lookup"><span data-stu-id="edd86-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="edd86-224">You can use a wildcard with your domain in your DNS.</span><span class="sxs-lookup"><span data-stu-id="edd86-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="edd86-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span><span class="sxs-lookup"><span data-stu-id="edd86-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="edd86-226">a.</span><span class="sxs-lookup"><span data-stu-id="edd86-226">a.</span></span> <span data-ttu-id="edd86-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="edd86-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_.</span></span> <span data-ttu-id="edd86-228">You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span><span class="sxs-lookup"><span data-stu-id="edd86-228">You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="edd86-229">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="edd86-229">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="edd86-230">b.</span><span class="sxs-lookup"><span data-stu-id="edd86-230">b.</span></span> <span data-ttu-id="edd86-231">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="edd86-231">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

1. <span data-ttu-id="edd86-232">Use a browser on that VM and go to http://mytestapp.ilbase.com.</span><span class="sxs-lookup"><span data-stu-id="edd86-232">Use a browser on that VM and go to http://mytestapp.ilbase.com.</span></span> <span data-ttu-id="edd86-233">(Or go to whatever your web app name is with your domain.)</span><span class="sxs-lookup"><span data-stu-id="edd86-233">(Or go to whatever your web app name is with your domain.)</span></span>

1. <span data-ttu-id="edd86-234">Use a browser on that VM and go to https://mytestapp.ilbase.com.</span><span class="sxs-lookup"><span data-stu-id="edd86-234">Use a browser on that VM and go to https://mytestapp.ilbase.com.</span></span> <span data-ttu-id="edd86-235">If you use a self-signed certificate, accept the lack of security.</span><span class="sxs-lookup"><span data-stu-id="edd86-235">If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="edd86-236">The IP address for your ILB is listed under **IP addresses**.</span><span class="sxs-lookup"><span data-stu-id="edd86-236">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="edd86-237">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span><span class="sxs-lookup"><span data-stu-id="edd86-237">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![ILB IP address][5]

## <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="edd86-239">Web jobs, Functions and the ILB ASE</span><span class="sxs-lookup"><span data-stu-id="edd86-239">Web jobs, Functions and the ILB ASE</span></span> ##

<span data-ttu-id="edd86-240">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span><span class="sxs-lookup"><span data-stu-id="edd86-240">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="edd86-241">This means your browser must either be on a host that is either in or connected to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="edd86-241">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="edd86-242">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span><span class="sxs-lookup"><span data-stu-id="edd86-242">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="edd86-243">Please try again later."</span><span class="sxs-lookup"><span data-stu-id="edd86-243">Please try again later."</span></span> <span data-ttu-id="edd86-244">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span><span class="sxs-lookup"><span data-stu-id="edd86-244">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="edd86-245">Web jobs has a similar problem.</span><span class="sxs-lookup"><span data-stu-id="edd86-245">Web jobs has a similar problem.</span></span> <span data-ttu-id="edd86-246">To avoid this problem you can do one of the following:</span><span class="sxs-lookup"><span data-stu-id="edd86-246">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="edd86-247">Add the certificate to your trusted certificate store.</span><span class="sxs-lookup"><span data-stu-id="edd86-247">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="edd86-248">This unblocks Edge and Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="edd86-248">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="edd86-249">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span><span class="sxs-lookup"><span data-stu-id="edd86-249">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="edd86-250">Use a commercial certificate that is in your browser chain of trust.</span><span class="sxs-lookup"><span data-stu-id="edd86-250">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="edd86-251">This is the best option.</span><span class="sxs-lookup"><span data-stu-id="edd86-251">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="edd86-252">DNS configuration</span><span class="sxs-lookup"><span data-stu-id="edd86-252">DNS configuration</span></span> ##

<span data-ttu-id="edd86-253">When you use an External VIP, the DNS is managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="edd86-253">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="edd86-254">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span><span class="sxs-lookup"><span data-stu-id="edd86-254">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="edd86-255">In an ILB ASE, you must manage your own DNS.</span><span class="sxs-lookup"><span data-stu-id="edd86-255">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="edd86-256">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span><span class="sxs-lookup"><span data-stu-id="edd86-256">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="edd86-257">\*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="edd86-257">\*.contoso.net</span></span>
- <span data-ttu-id="edd86-258">\*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="edd86-258">\*.scm.contoso.net</span></span>

<span data-ttu-id="edd86-259">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span><span class="sxs-lookup"><span data-stu-id="edd86-259">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="edd86-260">This method is challenging because you need to add each new app name into your DNS when you create it.</span><span class="sxs-lookup"><span data-stu-id="edd86-260">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="edd86-261">For this reason, we recommend that you use a dedicated domain.</span><span class="sxs-lookup"><span data-stu-id="edd86-261">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="edd86-262">Publish with an ILB ASE</span><span class="sxs-lookup"><span data-stu-id="edd86-262">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="edd86-263">For every app that's created, there are two endpoints.</span><span class="sxs-lookup"><span data-stu-id="edd86-263">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="edd86-264">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span><span class="sxs-lookup"><span data-stu-id="edd86-264">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="edd86-265">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edd86-265">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="edd86-266">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span><span class="sxs-lookup"><span data-stu-id="edd86-266">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="edd86-267">For more information, see [Kudu console for Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="edd86-267">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="edd86-268">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span><span class="sxs-lookup"><span data-stu-id="edd86-268">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="edd86-269">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span><span class="sxs-lookup"><span data-stu-id="edd86-269">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="edd86-270">Internet-based CI systems, such as GitHub and Azure DevOps, will still work with an ILB ASE if the build agent is internet accessible and on the same network as ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-270">Internet-based CI systems, such as GitHub and Azure DevOps, will still work with an ILB ASE if the build agent is internet accessible and on the same network as ILB ASE.</span></span> <span data-ttu-id="edd86-271">So in case of Azure DevOps, if the build agent is created on the same VNET as ILB ASE (different subnet is fine), it will be able to pull code from Azure DevOps git and deploy to ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-271">So in case of Azure DevOps, if the build agent is created on the same VNET as ILB ASE (different subnet is fine), it will be able to pull code from Azure DevOps git and deploy to ILB ASE.</span></span> <span data-ttu-id="edd86-272">If you don't want to create your own build agent, you need to use a CI system that uses a pull model, such as Dropbox.</span><span class="sxs-lookup"><span data-stu-id="edd86-272">If you don't want to create your own build agent, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="edd86-273">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span><span class="sxs-lookup"><span data-stu-id="edd86-273">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="edd86-274">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span><span class="sxs-lookup"><span data-stu-id="edd86-274">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="edd86-275">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span><span class="sxs-lookup"><span data-stu-id="edd86-275">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="edd86-276">Couple an ILB ASE with a WAF device</span><span class="sxs-lookup"><span data-stu-id="edd86-276">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="edd86-277">Azure App Service provides many security measures that protect the system.</span><span class="sxs-lookup"><span data-stu-id="edd86-277">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="edd86-278">They also help to determine whether an app was hacked.</span><span class="sxs-lookup"><span data-stu-id="edd86-278">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="edd86-279">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="edd86-279">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="edd86-280">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span><span class="sxs-lookup"><span data-stu-id="edd86-280">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="edd86-281">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="edd86-281">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="edd86-282">This article shows how to use a Barracuda virtual appliance with your ASE.</span><span class="sxs-lookup"><span data-stu-id="edd86-282">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="edd86-283">Another option is to use Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="edd86-283">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="edd86-284">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span><span class="sxs-lookup"><span data-stu-id="edd86-284">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="edd86-285">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span><span class="sxs-lookup"><span data-stu-id="edd86-285">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="edd86-286">Get started</span><span class="sxs-lookup"><span data-stu-id="edd86-286">Get started</span></span> ##

* <span data-ttu-id="edd86-287">To get started with ASEs, see [Introduction to App Service environments][Intro].</span><span class="sxs-lookup"><span data-stu-id="edd86-287">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/security-overview.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[customdomain]: ../app-service-web-tutorial-custom-domain.md
[linuxapp]: ../containers/app-service-linux-intro.md
