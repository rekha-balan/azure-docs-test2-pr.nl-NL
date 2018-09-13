---
title: Use an Azure App Service environment
description: How to create, publish, and scale apps in an Azure App Service environment
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 80abe29c80898b691aa6e5e47bf068a9e69e50e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867465"
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="b9cd6-103">Use an App Service environment</span><span class="sxs-lookup"><span data-stu-id="b9cd6-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="b9cd6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b9cd6-104">Overview</span></span> ##

<span data-ttu-id="b9cd6-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="b9cd6-106">It consists of:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-106">It consists of:</span></span>

- <span data-ttu-id="b9cd6-107">**Front ends**: The front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span><span class="sxs-lookup"><span data-stu-id="b9cd6-107">**Front ends**: The front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="b9cd6-108">**Workers**: The workers are the resources that host your apps.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-108">**Workers**: The workers are the resources that host your apps.</span></span>
- <span data-ttu-id="b9cd6-109">**Database**: The database holds information that defines the environment.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-109">**Database**: The database holds information that defines the environment.</span></span>
- <span data-ttu-id="b9cd6-110">**Storage**: The storage is used to host the customer-published apps.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-110">**Storage**: The storage is used to host the customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="b9cd6-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="b9cd6-112">In ASEv1, you must manage the resources before you can use them.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-112">In ASEv1, you must manage the resources before you can use them.</span></span> <span data-ttu-id="b9cd6-113">To learn how to configure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-113">To learn how to configure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="b9cd6-114">The rest of this article focuses on ASEv2.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-114">The rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="b9cd6-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="b9cd6-116">The deployment with an external VIP is commonly called an External ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-116">The deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="b9cd6-117">The internal version is called the ILB ASE because it uses an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="b9cd6-117">The internal version is called the ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="b9cd6-118">To learn more about the ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-118">To learn more about the ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="b9cd6-119">Create a web app in an ASE</span><span class="sxs-lookup"><span data-stu-id="b9cd6-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="b9cd6-120">To create a web app in an ASE, you use the same process as when you create it normally, but with a few small differences.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-120">To create a web app in an ASE, you use the same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="b9cd6-121">When you create a new App Service plan:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="b9cd6-122">Instead of choosing a geographic location in which to deploy your app, you choose an ASE as your location.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-122">Instead of choosing a geographic location in which to deploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="b9cd6-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="b9cd6-124">If you don't have an ASE, you can create one by following the instructions in [Create an App Service environment][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-124">If you don't have an ASE, you can create one by following the instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="b9cd6-125">To create a web app in an ASE:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-125">To create a web app in an ASE:</span></span>

1. <span data-ttu-id="b9cd6-126">Select **Create a resource** > **Web + Mobile** > **Web App**.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-126">Select **Create a resource** > **Web + Mobile** > **Web App**.</span></span>

1. <span data-ttu-id="b9cd6-127">Enter a name for the web app.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-127">Enter a name for the web app.</span></span> <span data-ttu-id="b9cd6-128">If you already selected an App Service plan in an ASE, the domain name for the app reflects the domain name of the ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-128">If you already selected an App Service plan in an ASE, the domain name for the app reflects the domain name of the ASE.</span></span>

    ![Web app name selection][1]

1. <span data-ttu-id="b9cd6-130">Select a subscription.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-130">Select a subscription.</span></span>

1. <span data-ttu-id="b9cd6-131">Enter a name for a new resource group, or select **Use existing** and select one from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-131">Enter a name for a new resource group, or select **Use existing** and select one from the drop-down list.</span></span>

1. <span data-ttu-id="b9cd6-132">Select your OS.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-132">Select your OS.</span></span> 

    * <span data-ttu-id="b9cd6-133">Hosting a Linux app in an ASE is a new preview feature, so we suggest that you do not add Linux apps into an ASE that is currently running production workloads.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-133">Hosting a Linux app in an ASE is a new preview feature, so we suggest that you do not add Linux apps into an ASE that is currently running production workloads.</span></span> 
    * <span data-ttu-id="b9cd6-134">Adding a Linux app into an ASE means that the ASE will also be in preview mode.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-134">Adding a Linux app into an ASE means that the ASE will also be in preview mode.</span></span> 

1. <span data-ttu-id="b9cd6-135">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-135">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="b9cd6-136">a.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-136">a.</span></span> <span data-ttu-id="b9cd6-137">Select **Create New**.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-137">Select **Create New**.</span></span>

    <span data-ttu-id="b9cd6-138">b.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-138">b.</span></span> <span data-ttu-id="b9cd6-139">Enter the name for your App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-139">Enter the name for your App Service plan.</span></span>

    <span data-ttu-id="b9cd6-140">c.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-140">c.</span></span> <span data-ttu-id="b9cd6-141">Select your ASE in the **Location** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-141">Select your ASE in the **Location** drop-down list.</span></span> <span data-ttu-id="b9cd6-142">Hosting a Linux app in an ASE is only enabled in 6 regions, at the moment: **West US, East US, West Europe, North Europe, Australia East, Southeast Asia.**</span><span class="sxs-lookup"><span data-stu-id="b9cd6-142">Hosting a Linux app in an ASE is only enabled in 6 regions, at the moment: **West US, East US, West Europe, North Europe, Australia East, Southeast Asia.**</span></span> 

    <span data-ttu-id="b9cd6-143">d.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-143">d.</span></span> <span data-ttu-id="b9cd6-144">Select an **Isolated** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-144">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="b9cd6-145">Select **Select**.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-145">Select **Select**.</span></span>

    <span data-ttu-id="b9cd6-146">e.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-146">e.</span></span> <span data-ttu-id="b9cd6-147">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-147">Select **OK**.</span></span>
    
    ![Isolated pricing tiers][2]

    > [!NOTE]
    > <span data-ttu-id="b9cd6-149">Linux web apps and Windows web apps cannot be in the same App Service Plan, but can be in the same App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-149">Linux web apps and Windows web apps cannot be in the same App Service Plan, but can be in the same App Service Environment.</span></span> 
    >

1. <span data-ttu-id="b9cd6-150">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-150">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="b9cd6-151">How scale works</span><span class="sxs-lookup"><span data-stu-id="b9cd6-151">How scale works</span></span> ##

<span data-ttu-id="b9cd6-152">Every App Service app runs in an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-152">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="b9cd6-153">The container model is environments hold App Service plans, and App Service plans hold apps.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-153">The container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="b9cd6-154">When you scale an app, you scale the App Service plan and thus scale all the apps in the same plan.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-154">When you scale an app, you scale the App Service plan and thus scale all the apps in the same plan.</span></span>

<span data-ttu-id="b9cd6-155">In ASEv2, when you scale an App Service plan, the needed infrastructure is automatically added.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-155">In ASEv2, when you scale an App Service plan, the needed infrastructure is automatically added.</span></span> <span data-ttu-id="b9cd6-156">There is a time delay to scale operations while the infrastructure is added.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-156">There is a time delay to scale operations while the infrastructure is added.</span></span> <span data-ttu-id="b9cd6-157">In ASEv1, the needed infrastructure must be added before you can create or scale out your App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-157">In ASEv1, the needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="b9cd6-158">In the multitenant App Service, scaling is usually immediate because a pool of resources is readily available to support it.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-158">In the multitenant App Service, scaling is usually immediate because a pool of resources is readily available to support it.</span></span> <span data-ttu-id="b9cd6-159">In an ASE, there is no such buffer, and resources are allocated upon need.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-159">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="b9cd6-160">In an ASE, you can scale up to 100 instances.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-160">In an ASE, you can scale up to 100 instances.</span></span> <span data-ttu-id="b9cd6-161">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-161">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="b9cd6-162">IP addresses</span><span class="sxs-lookup"><span data-stu-id="b9cd6-162">IP addresses</span></span> ##

<span data-ttu-id="b9cd6-163">App Service has the ability to allocate a dedicated IP address to an app.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-163">App Service has the ability to allocate a dedicated IP address to an app.</span></span> <span data-ttu-id="b9cd6-164">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate to Azure web apps][ConfigureSSL].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-164">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate to Azure web apps][ConfigureSSL].</span></span> <span data-ttu-id="b9cd6-165">However, in an ASE, there is a notable exception.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-165">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="b9cd6-166">You can't add additional IP addresses to be used for an IP-based SSL in an ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-166">You can't add additional IP addresses to be used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="b9cd6-167">In ASEv1, you need to allocate the IP addresses as resources before you can use them.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-167">In ASEv1, you need to allocate the IP addresses as resources before you can use them.</span></span> <span data-ttu-id="b9cd6-168">In ASEv2, you use them from your app just as you do in the multitenant App Service.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-168">In ASEv2, you use them from your app just as you do in the multitenant App Service.</span></span> <span data-ttu-id="b9cd6-169">There is always one spare address in ASEv2 up to 30 IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-169">There is always one spare address in ASEv2 up to 30 IP addresses.</span></span> <span data-ttu-id="b9cd6-170">Each time you use one, another is added so that an address is always readily available for use.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-170">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="b9cd6-171">A time delay is required to allocate another IP address, which prevents adding IP addresses in quick succession.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-171">A time delay is required to allocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="b9cd6-172">Front-end scaling</span><span class="sxs-lookup"><span data-stu-id="b9cd6-172">Front-end scaling</span></span> ##

<span data-ttu-id="b9cd6-173">In ASEv2, when you scale out your App Service plans, workers are automatically added to support them.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-173">In ASEv2, when you scale out your App Service plans, workers are automatically added to support them.</span></span> <span data-ttu-id="b9cd6-174">Every ASE is created with two front ends.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-174">Every ASE is created with two front ends.</span></span> <span data-ttu-id="b9cd6-175">In addition, the front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-175">In addition, the front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="b9cd6-176">For example, if you have 15 instances, then you have three front ends.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-176">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="b9cd6-177">If you scale to 30 instances, then you have four front ends, and so on.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-177">If you scale to 30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="b9cd6-178">This number of front ends should be more than enough for most scenarios.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-178">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="b9cd6-179">However, you can scale out at a faster rate.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-179">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="b9cd6-180">You can change the ratio to as low as one front end for every five instances.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-180">You can change the ratio to as low as one front end for every five instances.</span></span> <span data-ttu-id="b9cd6-181">There is a charge for changing the ratio.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-181">There is a charge for changing the ratio.</span></span> <span data-ttu-id="b9cd6-182">For more information, see [Azure App Service pricing][Pricing].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-182">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="b9cd6-183">Front-end resources are the HTTP/HTTPS endpoint for the ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-183">Front-end resources are the HTTP/HTTPS endpoint for the ASE.</span></span> <span data-ttu-id="b9cd6-184">With the default front-end configuration, memory usage per front end is consistently around 60 percent.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-184">With the default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="b9cd6-185">Customer workloads don't run on a front end.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-185">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="b9cd6-186">The key factor for a front end with respect to scale is the CPU, which is driven primarily by HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-186">The key factor for a front end with respect to scale is the CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="b9cd6-187">App access</span><span class="sxs-lookup"><span data-stu-id="b9cd6-187">App access</span></span> ##

<span data-ttu-id="b9cd6-188">In an External ASE, the domain that's used when you create apps is different from the multitenant App Service.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-188">In an External ASE, the domain that's used when you create apps is different from the multitenant App Service.</span></span> <span data-ttu-id="b9cd6-189">It includes the name of the ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-189">It includes the name of the ASE.</span></span> <span data-ttu-id="b9cd6-190">For more information on how to create an External ASE, see [Create an App Service environment][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-190">For more information on how to create an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="b9cd6-191">The domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-191">The domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="b9cd6-192">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at the following URLs:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-192">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at the following URLs:</span></span>

- <span data-ttu-id="b9cd6-193">contoso.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b9cd6-193">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="b9cd6-194">contoso.scm.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b9cd6-194">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="b9cd6-195">The URL contoso.scm.external-ase.p.azurewebsites.net is used to access the Kudu console or for publishing your app by using web deploy.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-195">The URL contoso.scm.external-ase.p.azurewebsites.net is used to access the Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="b9cd6-196">For information on the Kudu console, see [Kudu console for Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-196">For information on the Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="b9cd6-197">The Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-197">The Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="b9cd6-198">In an ILB ASE, you determine the domain at deployment time.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-198">In an ILB ASE, you determine the domain at deployment time.</span></span> <span data-ttu-id="b9cd6-199">For more information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-199">For more information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="b9cd6-200">If you specify the domain name _ilb-ase.info_, the apps in that ASE use that domain during app creation.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-200">If you specify the domain name _ilb-ase.info_, the apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="b9cd6-201">For the app named _contoso_, the URLs are:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-201">For the app named _contoso_, the URLs are:</span></span>

- <span data-ttu-id="b9cd6-202">contoso.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="b9cd6-202">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="b9cd6-203">contoso.scm.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="b9cd6-203">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="b9cd6-204">Publishing</span><span class="sxs-lookup"><span data-stu-id="b9cd6-204">Publishing</span></span> ##

<span data-ttu-id="b9cd6-205">As with the multitenant App Service, in an ASE you can publish with:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-205">As with the multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="b9cd6-206">Web deployment.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-206">Web deployment.</span></span>
- <span data-ttu-id="b9cd6-207">FTP.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-207">FTP.</span></span>
- <span data-ttu-id="b9cd6-208">Continuous integration.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-208">Continuous integration.</span></span>
- <span data-ttu-id="b9cd6-209">Drag and drop in the Kudu console.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-209">Drag and drop in the Kudu console.</span></span>
- <span data-ttu-id="b9cd6-210">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-210">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="b9cd6-211">With an External ASE, these publishing options all behave the same.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-211">With an External ASE, these publishing options all behave the same.</span></span> <span data-ttu-id="b9cd6-212">For more information, see [Deployment in Azure App Service][AppDeploy].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-212">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="b9cd6-213">The major difference with publishing is with respect to an ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-213">The major difference with publishing is with respect to an ILB ASE.</span></span> <span data-ttu-id="b9cd6-214">With an ILB ASE, the publishing endpoints are all available only through the ILB.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-214">With an ILB ASE, the publishing endpoints are all available only through the ILB.</span></span> <span data-ttu-id="b9cd6-215">The ILB is on a private IP in the ASE subnet in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-215">The ILB is on a private IP in the ASE subnet in the virtual network.</span></span> <span data-ttu-id="b9cd6-216">If you don’t have network access to the ILB, you can't publish any apps on that ASE.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-216">If you don’t have network access to the ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="b9cd6-217">As noted in [Create and use an ILB ASE][MakeILBASE], you need to configure DNS for the apps in the system.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-217">As noted in [Create and use an ILB ASE][MakeILBASE], you need to configure DNS for the apps in the system.</span></span> <span data-ttu-id="b9cd6-218">That includes the SCM endpoint.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-218">That includes the SCM endpoint.</span></span> <span data-ttu-id="b9cd6-219">If they're not defined properly, you can't publish.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-219">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="b9cd6-220">Your IDEs also need to have network access to the ILB in order to publish directly to it.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-220">Your IDEs also need to have network access to the ILB in order to publish directly to it.</span></span>

<span data-ttu-id="b9cd6-221">Internet-based CI systems, such as GitHub and Azure DevOps, don't work with an ILB ASE because the publishing endpoint is not Internet accessible.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-221">Internet-based CI systems, such as GitHub and Azure DevOps, don't work with an ILB ASE because the publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="b9cd6-222">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-222">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="b9cd6-223">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-223">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="b9cd6-224">You can see it in the app's publishing profile and in the app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span><span class="sxs-lookup"><span data-stu-id="b9cd6-224">You can see it in the app's publishing profile and in the app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="b9cd6-225">Pricing</span><span class="sxs-lookup"><span data-stu-id="b9cd6-225">Pricing</span></span> ##

<span data-ttu-id="b9cd6-226">The pricing SKU called **Isolated** was created for use only with ASEv2.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-226">The pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="b9cd6-227">All App Service plans that are hosted in ASEv2 are in the Isolated pricing SKU.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-227">All App Service plans that are hosted in ASEv2 are in the Isolated pricing SKU.</span></span> <span data-ttu-id="b9cd6-228">Isolated App Service plan rates can vary per region.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-228">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="b9cd6-229">In addition to the price for your App Service plans, there is a flat rate for ASE itself.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-229">In addition to the price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="b9cd6-230">The flat rate doesn't change with the size of your ASE and pays for the ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-230">The flat rate doesn't change with the size of your ASE and pays for the ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="b9cd6-231">If the default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust the ratio at which front-ends are added or the size of the front-ends.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-231">If the default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust the ratio at which front-ends are added or the size of the front-ends.</span></span>  <span data-ttu-id="b9cd6-232">When you adjust the ratio or size, you pay for the front-end cores that would not be added by default.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-232">When you adjust the ratio or size, you pay for the front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="b9cd6-233">For example, if you adjust the scale ratio to 10, a front end is added for every 10 instances in your App Service plans.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-233">For example, if you adjust the scale ratio to 10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="b9cd6-234">The flat fee covers a scale rate of one front end for every 15 instances.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-234">The flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="b9cd6-235">With a scale ratio of 10, you pay a fee for the third front end that's added for the 10 App Service plan instances.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-235">With a scale ratio of 10, you pay a fee for the third front end that's added for the 10 App Service plan instances.</span></span> <span data-ttu-id="b9cd6-236">You don't need to pay for it when you reach 15 instances because it was added automatically.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-236">You don't need to pay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="b9cd6-237">If you adjusted the size of the front-ends to 2 cores but do not adjust the ratio then you pay for the extra cores.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-237">If you adjusted the size of the front-ends to 2 cores but do not adjust the ratio then you pay for the extra cores.</span></span>  <span data-ttu-id="b9cd6-238">An ASE is created with 2 front-ends, so even below the automatic scaling threshold you would pay for 2 extra cores if you increased the size to 2 core front-ends.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-238">An ASE is created with 2 front-ends, so even below the automatic scaling threshold you would pay for 2 extra cores if you increased the size to 2 core front-ends.</span></span>

<span data-ttu-id="b9cd6-239">For more information, see [Azure App Service pricing][Pricing].</span><span class="sxs-lookup"><span data-stu-id="b9cd6-239">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="b9cd6-240">Delete an ASE</span><span class="sxs-lookup"><span data-stu-id="b9cd6-240">Delete an ASE</span></span> ##

<span data-ttu-id="b9cd6-241">To delete an ASE:</span><span class="sxs-lookup"><span data-stu-id="b9cd6-241">To delete an ASE:</span></span> 

1. <span data-ttu-id="b9cd6-242">Use **Delete** at the top of the **App Service Environment** blade.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-242">Use **Delete** at the top of the **App Service Environment** blade.</span></span> 

1. <span data-ttu-id="b9cd6-243">Enter the name of your ASE to confirm that you want to delete it.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-243">Enter the name of your ASE to confirm that you want to delete it.</span></span> <span data-ttu-id="b9cd6-244">When you delete an ASE, you delete all of the content within it as well.</span><span class="sxs-lookup"><span data-stu-id="b9cd6-244">When you delete an ASE, you delete all of the content within it as well.</span></span> 

    ![ASE deletion][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../app-service-deploy-local-git.md
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
