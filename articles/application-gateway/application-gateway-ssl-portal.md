---
title: Configure SSL offload - Azure Application Gateway - Azure Portal | Microsoft Docs
description: This page provides instructions to create an application gateway with SSL offload by using the portal
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 0aa7fbf6d08eb1f478fbbdfa20904209aa7e7051
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549281"
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="1173a-103">Configure an application gateway for SSL offload by using the portal</span><span class="sxs-lookup"><span data-stu-id="1173a-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)

<span data-ttu-id="1173a-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span><span class="sxs-lookup"><span data-stu-id="1173a-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="1173a-108">SSL offload also simplifies the front-end server setup and management of the web application.</span><span class="sxs-lookup"><span data-stu-id="1173a-108">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="1173a-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="1173a-109">Scenario</span></span>

<span data-ttu-id="1173a-110">The following scenario goes through configuring SSL offload on an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="1173a-110">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="1173a-111">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1173a-111">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1173a-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1173a-112">Before you begin</span></span>

<span data-ttu-id="1173a-113">To configure SSL offload with an application gateway, a certificate is required.</span><span class="sxs-lookup"><span data-stu-id="1173a-113">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="1173a-114">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span><span class="sxs-lookup"><span data-stu-id="1173a-114">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="1173a-115">The certificate needs to be in Personal Information Exchange (pfx) format.</span><span class="sxs-lookup"><span data-stu-id="1173a-115">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="1173a-116">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span><span class="sxs-lookup"><span data-stu-id="1173a-116">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="1173a-117">Add an HTTPS listener</span><span class="sxs-lookup"><span data-stu-id="1173a-117">Add an HTTPS listener</span></span>

<span data-ttu-id="1173a-118">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span><span class="sxs-lookup"><span data-stu-id="1173a-118">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="1173a-119">Step 1</span><span class="sxs-lookup"><span data-stu-id="1173a-119">Step 1</span></span>

<span data-ttu-id="1173a-120">Navigate to the Azure portal and select an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="1173a-120">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="1173a-121">Step 2</span><span class="sxs-lookup"><span data-stu-id="1173a-121">Step 2</span></span>

<span data-ttu-id="1173a-122">Click Listeners and click the Add button to add a listener.</span><span class="sxs-lookup"><span data-stu-id="1173a-122">Click Listeners and click the Add button to add a listener.</span></span>

![app gateway overview blade][1]

### <a name="step-3"></a><span data-ttu-id="1173a-124">Step 3</span><span class="sxs-lookup"><span data-stu-id="1173a-124">Step 3</span></span>

<span data-ttu-id="1173a-125">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span><span class="sxs-lookup"><span data-stu-id="1173a-125">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="1173a-126">**Name** - This value is a friendly name of the listener.</span><span class="sxs-lookup"><span data-stu-id="1173a-126">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="1173a-127">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span><span class="sxs-lookup"><span data-stu-id="1173a-127">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="1173a-128">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span><span class="sxs-lookup"><span data-stu-id="1173a-128">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="1173a-129">**Protocol** - A switch to determine if https or http is used for the front end.</span><span class="sxs-lookup"><span data-stu-id="1173a-129">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="1173a-130">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span><span class="sxs-lookup"><span data-stu-id="1173a-130">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![add listener blade][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="1173a-132">Create a rule and associate it to the listener</span><span class="sxs-lookup"><span data-stu-id="1173a-132">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="1173a-133">The listener has now been created.</span><span class="sxs-lookup"><span data-stu-id="1173a-133">The listener has now been created.</span></span> <span data-ttu-id="1173a-134">It is time to create a rule to handle the traffic from the listener.</span><span class="sxs-lookup"><span data-stu-id="1173a-134">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="1173a-135">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie based session affinity is used, protocol, port and health probes.</span><span class="sxs-lookup"><span data-stu-id="1173a-135">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie based session affinity is used, protocol, port and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="1173a-136">Step 1</span><span class="sxs-lookup"><span data-stu-id="1173a-136">Step 1</span></span>

<span data-ttu-id="1173a-137">Click the **Rules** of the application gateway, and then click Add.</span><span class="sxs-lookup"><span data-stu-id="1173a-137">Click the **Rules** of the application gateway, and then click Add.</span></span>

![app gateway rules blade][3]

### <a name="step-2"></a><span data-ttu-id="1173a-139">Step 2</span><span class="sxs-lookup"><span data-stu-id="1173a-139">Step 2</span></span>

<span data-ttu-id="1173a-140">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="1173a-140">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="1173a-141">Choose the appropriate backend pool and http setting and click **OK**</span><span class="sxs-lookup"><span data-stu-id="1173a-141">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![https settings window][4]

<span data-ttu-id="1173a-143">The settings are now saved to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1173a-143">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="1173a-144">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1173a-144">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="1173a-145">Once saved the application gateway handles the encryption and decryption of traffic.</span><span class="sxs-lookup"><span data-stu-id="1173a-145">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="1173a-146">All traffic between the application gateway and the backend web servers will be handled over http.</span><span class="sxs-lookup"><span data-stu-id="1173a-146">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="1173a-147">Any communication back to the client if initiated over https will be returned to the client encrypted.</span><span class="sxs-lookup"><span data-stu-id="1173a-147">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1173a-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="1173a-148">Next steps</span></span>

<span data-ttu-id="1173a-149">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1173a-149">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure4.png




