---
title: Set up failover across multiple Azure CDN endpoints with Azure Traffic Manager | Microsoft Docs
description: Learn about how to set up Azure Traffic Manager with Azure CDN endpoints.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: v-deasim
ms.custom: ''
ms.openlocfilehash: b52cad1f32cc3d16cf70bb81640dcb1d9f8614bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856643"
---
# <a name="set-up-failover-across-multiple-azure-cdn-endpoints-with-azure-traffic-manager"></a><span data-ttu-id="0c544-103">Set up failover across multiple Azure CDN endpoints with Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0c544-103">Set up failover across multiple Azure CDN endpoints with Azure Traffic Manager</span></span>

<span data-ttu-id="0c544-104">When you configure Azure Content Delivery Network (CDN), you can select the optimal provider and pricing tier for your needs.</span><span class="sxs-lookup"><span data-stu-id="0c544-104">When you configure Azure Content Delivery Network (CDN), you can select the optimal provider and pricing tier for your needs.</span></span> <span data-ttu-id="0c544-105">Azure CDN, with its globally distributed infrastructure, by default creates local and geographic redundancy and global load balancing to improve service availability and performance.</span><span class="sxs-lookup"><span data-stu-id="0c544-105">Azure CDN, with its globally distributed infrastructure, by default creates local and geographic redundancy and global load balancing to improve service availability and performance.</span></span> <span data-ttu-id="0c544-106">If a location is not available to serve content, requests are automatically routed to another location and the optimal POP (based on such factors as request location and  server load) is used to serve each client request.</span><span class="sxs-lookup"><span data-stu-id="0c544-106">If a location is not available to serve content, requests are automatically routed to another location and the optimal POP (based on such factors as request location and  server load) is used to serve each client request.</span></span> 
 
<span data-ttu-id="0c544-107">If you have multiple CDN profiles, you can further improve availability and performance with Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0c544-107">If you have multiple CDN profiles, you can further improve availability and performance with Azure Traffic Manager.</span></span> <span data-ttu-id="0c544-108">You can use Azure Traffic Manager with Azure CDN to load balance among multiple CDN endpoints for failover, geo-load balancing, and other scenarios.</span><span class="sxs-lookup"><span data-stu-id="0c544-108">You can use Azure Traffic Manager with Azure CDN to load balance among multiple CDN endpoints for failover, geo-load balancing, and other scenarios.</span></span> <span data-ttu-id="0c544-109">In a typical failover scenario, all client requests are first directed to the primary CDN profile; if the profile is not available, requests are then passed to the secondary CDN profile until your primary CDN profile is back online.</span><span class="sxs-lookup"><span data-stu-id="0c544-109">In a typical failover scenario, all client requests are first directed to the primary CDN profile; if the profile is not available, requests are then passed to the secondary CDN profile until your primary CDN profile is back online.</span></span> <span data-ttu-id="0c544-110">Using Azure Traffic Manager in this way ensures your web application is always available.</span><span class="sxs-lookup"><span data-stu-id="0c544-110">Using Azure Traffic Manager in this way ensures your web application is always available.</span></span> 

<span data-ttu-id="0c544-111">This article provides guidance and an example of how to set up failover with **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span><span class="sxs-lookup"><span data-stu-id="0c544-111">This article provides guidance and an example of how to set up failover with **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>

## <a name="set-up-azure-cdn"></a><span data-ttu-id="0c544-112">Set up Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0c544-112">Set up Azure CDN</span></span> 
<span data-ttu-id="0c544-113">Create two or more Azure CDN profiles and endpoints with different providers.</span><span class="sxs-lookup"><span data-stu-id="0c544-113">Create two or more Azure CDN profiles and endpoints with different providers.</span></span>

1. <span data-ttu-id="0c544-114">Create an **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profile by following the steps in [Create a new CDN profile](cdn-create-new-endpoint.md#create-a-new-cdn-profile).</span><span class="sxs-lookup"><span data-stu-id="0c544-114">Create an **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profile by following the steps in [Create a new CDN profile](cdn-create-new-endpoint.md#create-a-new-cdn-profile).</span></span>
 
   ![CDN multiple profiles](./media/cdn-traffic-manager/cdn-multiple-profiles.png)

2. <span data-ttu-id="0c544-116">In each of the new profiles, create at least one endpoint by following the steps in [Create a new CDN endpoint](cdn-create-new-endpoint.md#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0c544-116">In each of the new profiles, create at least one endpoint by following the steps in [Create a new CDN endpoint](cdn-create-new-endpoint.md#create-a-new-cdn-endpoint).</span></span>

## <a name="set-up-azure-traffic-manager"></a><span data-ttu-id="0c544-117">Set up Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0c544-117">Set up Azure Traffic Manager</span></span>
<span data-ttu-id="0c544-118">Create an Azure Traffic Manager profile and set up load balancing across your CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="0c544-118">Create an Azure Traffic Manager profile and set up load balancing across your CDN endpoints.</span></span> 

1. <span data-ttu-id="0c544-119">Create an Azure Traffic Manager profile by following the steps in [Create a Traffic Manager profile](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-create-profile#create-a-traffic-manager-profile-1).</span><span class="sxs-lookup"><span data-stu-id="0c544-119">Create an Azure Traffic Manager profile by following the steps in [Create a Traffic Manager profile](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-create-profile#create-a-traffic-manager-profile-1).</span></span> 

    <span data-ttu-id="0c544-120">For **Routing method**, select **Priority**.</span><span class="sxs-lookup"><span data-stu-id="0c544-120">For **Routing method**, select **Priority**.</span></span>

2. <span data-ttu-id="0c544-121">Add your CDN endpoints in your Traffic Manager profile by following the steps in [Add Traffic Manager endpoints](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-create-profile#add-traffic-manager-endpoints)</span><span class="sxs-lookup"><span data-stu-id="0c544-121">Add your CDN endpoints in your Traffic Manager profile by following the steps in [Add Traffic Manager endpoints](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-create-profile#add-traffic-manager-endpoints)</span></span>

    <span data-ttu-id="0c544-122">For **Type**, select **External endpoints**.</span><span class="sxs-lookup"><span data-stu-id="0c544-122">For **Type**, select **External endpoints**.</span></span> <span data-ttu-id="0c544-123">For **Priority**, enter a number.</span><span class="sxs-lookup"><span data-stu-id="0c544-123">For **Priority**, enter a number.</span></span>

    <span data-ttu-id="0c544-124">For example, create *cdndemo101akamai.azureedge.net* with a priority of *1* and *cdndemo101verizon.azureedge.net* with a priority of *2*.</span><span class="sxs-lookup"><span data-stu-id="0c544-124">For example, create *cdndemo101akamai.azureedge.net* with a priority of *1* and *cdndemo101verizon.azureedge.net* with a priority of *2*.</span></span>

   ![CDN traffic manager endpoints](./media/cdn-traffic-manager/cdn-traffic-manager-endpoints.png)


## <a name="set-up-custom-domain-on-azure-cdn-and-azure-traffic-manager"></a><span data-ttu-id="0c544-126">Set up custom domain on Azure CDN and Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0c544-126">Set up custom domain on Azure CDN and Azure Traffic Manager</span></span>
<span data-ttu-id="0c544-127">After you set up your CDN and Traffic Manager profiles, follow these steps to add DNS mapping and register custom domain to the CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="0c544-127">After you set up your CDN and Traffic Manager profiles, follow these steps to add DNS mapping and register custom domain to the CDN endpoints.</span></span> <span data-ttu-id="0c544-128">For this example, the custom domain name is *cdndemo101.dustydogpetcare.online*.</span><span class="sxs-lookup"><span data-stu-id="0c544-128">For this example, the custom domain name is *cdndemo101.dustydogpetcare.online*.</span></span>

1. <span data-ttu-id="0c544-129">Go to the web site for the domain provider of your custom domain, such as GoDaddy, and create two DNS CNAME entries.</span><span class="sxs-lookup"><span data-stu-id="0c544-129">Go to the web site for the domain provider of your custom domain, such as GoDaddy, and create two DNS CNAME entries.</span></span> 

    <span data-ttu-id="0c544-130">a.</span><span class="sxs-lookup"><span data-stu-id="0c544-130">a.</span></span> <span data-ttu-id="0c544-131">For the first CNAME entry, map your custom domain, with the cdnverify subdomain, to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c544-131">For the first CNAME entry, map your custom domain, with the cdnverify subdomain, to your CDN endpoint.</span></span> <span data-ttu-id="0c544-132">This entry is a required step to register the custom domain to the CDN endpoint that you added to Traffic Manager in step 2.</span><span class="sxs-lookup"><span data-stu-id="0c544-132">This entry is a required step to register the custom domain to the CDN endpoint that you added to Traffic Manager in step 2.</span></span>

      <span data-ttu-id="0c544-133">For example:</span><span class="sxs-lookup"><span data-stu-id="0c544-133">For example:</span></span> 

      `cdnverify.cdndemo101.dustydogpetcare.online  CNAME  cdnverify.cdndemo101akamai.azureedge.net`  

    <span data-ttu-id="0c544-134">b.</span><span class="sxs-lookup"><span data-stu-id="0c544-134">b.</span></span> <span data-ttu-id="0c544-135">For the second CNAME entry, map your custom domain, without the cdnverify subdomain, to your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c544-135">For the second CNAME entry, map your custom domain, without the cdnverify subdomain, to your CDN endpoint.</span></span> <span data-ttu-id="0c544-136">This entry maps the custom domain to Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0c544-136">This entry maps the custom domain to Traffic Manager.</span></span> 

      <span data-ttu-id="0c544-137">For example:</span><span class="sxs-lookup"><span data-stu-id="0c544-137">For example:</span></span> 
      
      `cdndemo101.dustydogpetcare.online  CNAME  cdndemo101.trafficmanager.net`   

    > [!NOTE]
    > <span data-ttu-id="0c544-138">If your domain is currently live and cannot be interrupted, do this step last.</span><span class="sxs-lookup"><span data-stu-id="0c544-138">If your domain is currently live and cannot be interrupted, do this step last.</span></span> <span data-ttu-id="0c544-139">Verify that the CDN endpoints and traffic manager domains are live before you update your custom domain DNS to Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0c544-139">Verify that the CDN endpoints and traffic manager domains are live before you update your custom domain DNS to Traffic Manager.</span></span>
    >


2.  <span data-ttu-id="0c544-140">From your Azure CDN profile, select the first CDN endpoint (Akamai).</span><span class="sxs-lookup"><span data-stu-id="0c544-140">From your Azure CDN profile, select the first CDN endpoint (Akamai).</span></span> <span data-ttu-id="0c544-141">Select **Add custom domain** and input *cdndemo101akamai.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="0c544-141">Select **Add custom domain** and input *cdndemo101akamai.azureedge.net*.</span></span> <span data-ttu-id="0c544-142">Verify that the checkmark to validate the custom domain is green.</span><span class="sxs-lookup"><span data-stu-id="0c544-142">Verify that the checkmark to validate the custom domain is green.</span></span> 

    <span data-ttu-id="0c544-143">Azure CDN uses the *cdnverify* subdomain to validate the DNS mapping to complete this registration process.</span><span class="sxs-lookup"><span data-stu-id="0c544-143">Azure CDN uses the *cdnverify* subdomain to validate the DNS mapping to complete this registration process.</span></span> <span data-ttu-id="0c544-144">For more information, see [Create a CNAME DNS record](cdn-map-content-to-custom-domain.md#create-a-cname-dns-record).</span><span class="sxs-lookup"><span data-stu-id="0c544-144">For more information, see [Create a CNAME DNS record](cdn-map-content-to-custom-domain.md#create-a-cname-dns-record).</span></span> <span data-ttu-id="0c544-145">This step enables Azure CDN to recognize the custom domain so that it can respond to its requests.</span><span class="sxs-lookup"><span data-stu-id="0c544-145">This step enables Azure CDN to recognize the custom domain so that it can respond to its requests.</span></span>

3.  <span data-ttu-id="0c544-146">Return to the web site for the domain provider of your custom domain and update the first DNS mapping you created in so that the custom domain is mapped to your second CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c544-146">Return to the web site for the domain provider of your custom domain and update the first DNS mapping you created in so that the custom domain is mapped to your second CDN endpoint.</span></span>
                             
    <span data-ttu-id="0c544-147">For example:</span><span class="sxs-lookup"><span data-stu-id="0c544-147">For example:</span></span> 

    `cdnverify.cdndemo101.dustydogpetcare.online  CNAME  cdnverify.cdndemo101verizon.azureedge.net`  

4. <span data-ttu-id="0c544-148">From your Azure CDN profile, select the second CDN endpoint (Verizon) and repeat step 2.</span><span class="sxs-lookup"><span data-stu-id="0c544-148">From your Azure CDN profile, select the second CDN endpoint (Verizon) and repeat step 2.</span></span> <span data-ttu-id="0c544-149">Select **Add custom domain**, and input *cdndemo101akamai.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="0c544-149">Select **Add custom domain**, and input *cdndemo101akamai.azureedge.net*.</span></span>
 
<span data-ttu-id="0c544-150">After you complete these steps, your multi-CDN service with failover capabilities is set up with Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0c544-150">After you complete these steps, your multi-CDN service with failover capabilities is set up with Azure Traffic Manager.</span></span> <span data-ttu-id="0c544-151">You'll be able to access the test URLs from your custom domain.</span><span class="sxs-lookup"><span data-stu-id="0c544-151">You'll be able to access the test URLs from your custom domain.</span></span> <span data-ttu-id="0c544-152">To test the functionality, disable the primary CDN endpoint and verify that the request is correctly moved over to the secondary CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c544-152">To test the functionality, disable the primary CDN endpoint and verify that the request is correctly moved over to the secondary CDN endpoint.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c544-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c544-153">Next steps</span></span>
<span data-ttu-id="0c544-154">You can also set up other routing methods, such as geographic, to balance the load among different CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="0c544-154">You can also set up other routing methods, such as geographic, to balance the load among different CDN endpoints.</span></span> <span data-ttu-id="0c544-155">For more information, see [Configure the geographic traffic routing method using Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-configure-geographic-routing-method).</span><span class="sxs-lookup"><span data-stu-id="0c544-155">For more information, see [Configure the geographic traffic routing method using Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-configure-geographic-routing-method).</span></span>



