---
title: Application Gateway integration with Azure Security Center | Microsoft Docs
description: This page provides information on how Application Gateway is integrated into Azure Security Center.
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: ''
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: ''
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: victorh
ms.openlocfilehash: b3a4abf4d0f408cdb49020d831b50d943c3467dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856157"
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="93ea9-103">Overview of integration between Application Gateway and Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="93ea9-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="93ea9-104">Learn how Application Gateway and Security Center help protect your web application resources.</span><span class="sxs-lookup"><span data-stu-id="93ea9-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="93ea9-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect, and respond to threats to unprotected web applications in your environment.</span><span class="sxs-lookup"><span data-stu-id="93ea9-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect, and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="93ea9-106">Overview</span><span class="sxs-lookup"><span data-stu-id="93ea9-106">Overview</span></span>

<span data-ttu-id="93ea9-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="93ea9-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="93ea9-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span><span class="sxs-lookup"><span data-stu-id="93ea9-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="93ea9-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![integration with security center][1]

<span data-ttu-id="93ea9-111">Clicking any recommendations regarding web application firewall opens a new page showing the details of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="93ea9-111">Clicking any recommendations regarding web application firewall opens a new page showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="93ea9-112">Add a web application firewall to an existing resource</span><span class="sxs-lookup"><span data-stu-id="93ea9-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="93ea9-113">Navigate to **All services** > **Security + Identity** > **Security Center** and on **Security Center - Overview**, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-113">Navigate to **All services** > **Security + Identity** > **Security Center** and on **Security Center - Overview**, click **Applications**.</span></span> <span data-ttu-id="93ea9-114">On **Security Center - Applications**, the table contains a list of applications that Security Center detected in your subscription.</span><span class="sxs-lookup"><span data-stu-id="93ea9-114">On **Security Center - Applications**, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![web applications][3]

<span data-ttu-id="93ea9-116">By clicking on a web application with a critical issue, you get the **Application security health** page.</span><span class="sxs-lookup"><span data-stu-id="93ea9-116">By clicking on a web application with a critical issue, you get the **Application security health** page.</span></span> <span data-ttu-id="93ea9-117">In the image below, the web application that is not protected by a web application firewall.</span><span class="sxs-lookup"><span data-stu-id="93ea9-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![web resources not protected][2]

<span data-ttu-id="93ea9-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** page.</span><span class="sxs-lookup"><span data-stu-id="93ea9-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** page.</span></span>

<span data-ttu-id="93ea9-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on  **Create a new Web Application Firewall**, and click **Microsoft - Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on  **Create a new Web Application Firewall**, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="93ea9-121">This takes you through the steps to create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="93ea9-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="93ea9-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span><span class="sxs-lookup"><span data-stu-id="93ea9-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="93ea9-123">This does not add it as a backend pool member.</span><span class="sxs-lookup"><span data-stu-id="93ea9-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="93ea9-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span><span class="sxs-lookup"><span data-stu-id="93ea9-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![web application firewall add page][4]

<span data-ttu-id="93ea9-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member.</span><span class="sxs-lookup"><span data-stu-id="93ea9-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member.</span></span> <span data-ttu-id="93ea9-127">This must be done on the application gateway resource directly.</span><span class="sxs-lookup"><span data-stu-id="93ea9-127">This must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="93ea9-128">Add a resource to an existing web application firewall</span><span class="sxs-lookup"><span data-stu-id="93ea9-128">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="93ea9-129">Navigate to **All services** > **Security + Identity** > **Security Center** and on **Security Center - Overview**, click **Partner solutions**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-129">Navigate to **All services** > **Security + Identity** > **Security Center** and on **Security Center - Overview**, click **Partner solutions**.</span></span> <span data-ttu-id="93ea9-130">Existing Security Center aware application gateways show in the **Partner Solutions** page.</span><span class="sxs-lookup"><span data-stu-id="93ea9-130">Existing Security Center aware application gateways show in the **Partner Solutions** page.</span></span>

![partner solutions][7]

<span data-ttu-id="93ea9-132">Click **Link app** to open **Link Applications**, here you are given the options to select existing applications.</span><span class="sxs-lookup"><span data-stu-id="93ea9-132">Click **Link app** to open **Link Applications**, here you are given the options to select existing applications.</span></span> <span data-ttu-id="93ea9-133">Choose the applications to protect and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-133">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="93ea9-134">This does not add the web application to the backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="93ea9-134">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="93ea9-135">This sets the resources as a protected resource so Security Center can track it.</span><span class="sxs-lookup"><span data-stu-id="93ea9-135">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="93ea9-136">To add the resource as a backend pool member, this must be done on the application gateway, from the current page you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="93ea9-136">To add the resource as a backend pool member, this must be done on the application gateway, from the current page you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![partner solutions applications][6]

## <a name="finalize-configuration"></a><span data-ttu-id="93ea9-138">Finalize configuration</span><span class="sxs-lookup"><span data-stu-id="93ea9-138">Finalize configuration</span></span>

<span data-ttu-id="93ea9-139">Security Center tracks applications added to an application gateway as a protected resource.</span><span class="sxs-lookup"><span data-stu-id="93ea9-139">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="93ea9-140">It monitors the health of this resource and ensures that it is protected by an application gateway.</span><span class="sxs-lookup"><span data-stu-id="93ea9-140">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="93ea9-141">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="93ea9-141">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="93ea9-142">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span><span class="sxs-lookup"><span data-stu-id="93ea9-142">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![web application firewall add page][5]

## <a name="security-alerts"></a><span data-ttu-id="93ea9-144">Security Alerts</span><span class="sxs-lookup"><span data-stu-id="93ea9-144">Security Alerts</span></span>

<span data-ttu-id="93ea9-145">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span><span class="sxs-lookup"><span data-stu-id="93ea9-145">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="93ea9-146">Here you find WAF alerts for your application gateways.</span><span class="sxs-lookup"><span data-stu-id="93ea9-146">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="93ea9-147">Alerts are broken down by WAF rule.</span><span class="sxs-lookup"><span data-stu-id="93ea9-147">Alerts are broken down by WAF rule.</span></span>

![security alerts][8]

<span data-ttu-id="93ea9-149">Clicking an rule will provide a list of alerts for that specific WAF rule.</span><span class="sxs-lookup"><span data-stu-id="93ea9-149">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="93ea9-150">Each alert shows additional details on the finding.</span><span class="sxs-lookup"><span data-stu-id="93ea9-150">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="93ea9-151">The details provide a link to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="93ea9-151">The details provide a link to the application gateway.</span></span>
 
![alert details][9]

## <a name="next-steps"></a><span data-ttu-id="93ea9-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="93ea9-153">Next steps</span></span>

<span data-ttu-id="93ea9-154">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md).</span><span class="sxs-lookup"><span data-stu-id="93ea9-154">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md).</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png