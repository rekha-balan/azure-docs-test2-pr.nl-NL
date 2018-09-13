---
title: Create a custom probe - Azure Application Gateway - Azure Portal | Microsoft Docs
description: Learn how to create a custom probe for Application Gateway by using the portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: a0c264c46ad5e807584f5a2ef8bdf5e99109befb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551675"
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-the-portal"></a><span data-ttu-id="e8909-103">Create a custom probe for Application Gateway by using the portal</span><span class="sxs-lookup"><span data-stu-id="e8909-103">Create a custom probe for Application Gateway by using the portal</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

[!INCLUDE [azure-probe-intro-include](../../includes/application-gateway-create-probe-intro-include.md)]

## <a name="scenario"></a><span data-ttu-id="e8909-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="e8909-107">Scenario</span></span>

<span data-ttu-id="e8909-108">The following scenario goes through creating a custom health probe in an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="e8909-108">The following scenario goes through creating a custom health probe in an existing application gateway.</span></span>
<span data-ttu-id="e8909-109">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8909-109">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="createprobe"></a><span data-ttu-id="e8909-110">Create the probe</span><span class="sxs-lookup"><span data-stu-id="e8909-110">Create the probe</span></span>

<span data-ttu-id="e8909-111">Probes are configured in a two-step process through the portal.</span><span class="sxs-lookup"><span data-stu-id="e8909-111">Probes are configured in a two-step process through the portal.</span></span> <span data-ttu-id="e8909-112">The first step is to create the probe.</span><span class="sxs-lookup"><span data-stu-id="e8909-112">The first step is to create the probe.</span></span> <span data-ttu-id="e8909-113">Next you add the probe to the backend http settings of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e8909-113">Next you add the probe to the backend http settings of the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="e8909-114">Step 1</span><span class="sxs-lookup"><span data-stu-id="e8909-114">Step 1</span></span>

<span data-ttu-id="e8909-115">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="e8909-115">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span>

![Application Gateway overview][1]

### <a name="step-2"></a><span data-ttu-id="e8909-117">Step 2</span><span class="sxs-lookup"><span data-stu-id="e8909-117">Step 2</span></span>

<span data-ttu-id="e8909-118">Click **Probes** and click the **Add** button to add a probe.</span><span class="sxs-lookup"><span data-stu-id="e8909-118">Click **Probes** and click the **Add** button to add a probe.</span></span>

![Add Probe blade with information filled out][2]

### <a name="step-3"></a><span data-ttu-id="e8909-120">Step 3</span><span class="sxs-lookup"><span data-stu-id="e8909-120">Step 3</span></span>

<span data-ttu-id="e8909-121">Fill out the required information for the probe and when complete click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8909-121">Fill out the required information for the probe and when complete click **OK**.</span></span>

* <span data-ttu-id="e8909-122">**Name** - This value is a friendly name to the probe that is accessible in the portal.</span><span class="sxs-lookup"><span data-stu-id="e8909-122">**Name** - This value is a friendly name to the probe that is accessible in the portal.</span></span>
* <span data-ttu-id="e8909-123">**Host** - This value is the host name that is used for the probe.</span><span class="sxs-lookup"><span data-stu-id="e8909-123">**Host** - This value is the host name that is used for the probe.</span></span> <span data-ttu-id="e8909-124">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="e8909-124">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="e8909-125">This value is different from the VM host name.</span><span class="sxs-lookup"><span data-stu-id="e8909-125">This value is different from the VM host name.</span></span>
* <span data-ttu-id="e8909-126">**Path** - The remainder of the full url for the custom probe.</span><span class="sxs-lookup"><span data-stu-id="e8909-126">**Path** - The remainder of the full url for the custom probe.</span></span> <span data-ttu-id="e8909-127">A valid path starts with '/'</span><span class="sxs-lookup"><span data-stu-id="e8909-127">A valid path starts with '/'</span></span>
* <span data-ttu-id="e8909-128">**Interval (secs)** - How often the probe is run to check for health.</span><span class="sxs-lookup"><span data-stu-id="e8909-128">**Interval (secs)** - How often the probe is run to check for health.</span></span> <span data-ttu-id="e8909-129">It is not recommended to set the lower than 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="e8909-129">It is not recommended to set the lower than 30 seconds.</span></span>
* <span data-ttu-id="e8909-130">**Timeout (secs)** - The amount of time the probe waits before timing out. The timeout interval needs to be high enough that an http call can be made to ensure the backend health page is available.</span><span class="sxs-lookup"><span data-stu-id="e8909-130">**Timeout (secs)** - The amount of time the probe waits before timing out. The timeout interval needs to be high enough that an http call can be made to ensure the backend health page is available.</span></span>
* <span data-ttu-id="e8909-131">**Unhealthy threshold** - Number of failed attempts to be considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="e8909-131">**Unhealthy threshold** - Number of failed attempts to be considered unhealthy.</span></span> <span data-ttu-id="e8909-132">A threshold of 0 means that if a health check fails the back-end is determined unhealthy immediately.</span><span class="sxs-lookup"><span data-stu-id="e8909-132">A threshold of 0 means that if a health check fails the back-end is determined unhealthy immediately.</span></span>

> [!IMPORTANT]
> The host name is not the same as server name. This value is the name of the virtual host running on the application server. The probe is sent to http://(host name):(port from httpsetting)/urlPath

![probe configuration settings][3]

## <a name="add-probe-to-the-gateway"></a><span data-ttu-id="e8909-137">Add probe to the gateway</span><span class="sxs-lookup"><span data-stu-id="e8909-137">Add probe to the gateway</span></span>

<span data-ttu-id="e8909-138">Now that the probe has been created, it is time to add it to the gateway.</span><span class="sxs-lookup"><span data-stu-id="e8909-138">Now that the probe has been created, it is time to add it to the gateway.</span></span> <span data-ttu-id="e8909-139">Probe settings are set on the backend http settings of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e8909-139">Probe settings are set on the backend http settings of the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="e8909-140">Step 1</span><span class="sxs-lookup"><span data-stu-id="e8909-140">Step 1</span></span>

<span data-ttu-id="e8909-141">Click the **HTTP settings** of the application gateway, to bring up the configuration blade click the current backend http settings in the window.</span><span class="sxs-lookup"><span data-stu-id="e8909-141">Click the **HTTP settings** of the application gateway, to bring up the configuration blade click the current backend http settings in the window.</span></span>

![https settings window][4]

### <a name="step-2"></a><span data-ttu-id="e8909-143">Step 2</span><span class="sxs-lookup"><span data-stu-id="e8909-143">Step 2</span></span>

<span data-ttu-id="e8909-144">On the **appGatewayBackEndHttp** settings blade, click **Use custom probe** and choose the probe created in the [Create the probe](#createprobe) section.</span><span class="sxs-lookup"><span data-stu-id="e8909-144">On the **appGatewayBackEndHttp** settings blade, click **Use custom probe** and choose the probe created in the [Create the probe](#createprobe) section.</span></span>
<span data-ttu-id="e8909-145">When complete, click **OK** and the settings are applied.</span><span class="sxs-lookup"><span data-stu-id="e8909-145">When complete, click **OK** and the settings are applied.</span></span>

![appgatewaybackend settings blade][5]

<span data-ttu-id="e8909-147">The default probe checks the default access to the web application.</span><span class="sxs-lookup"><span data-stu-id="e8909-147">The default probe checks the default access to the web application.</span></span> <span data-ttu-id="e8909-148">Now that a custom probe has been created, the application gateway uses the custom path defined to monitor health for the backend selected.</span><span class="sxs-lookup"><span data-stu-id="e8909-148">Now that a custom probe has been created, the application gateway uses the custom path defined to monitor health for the backend selected.</span></span> <span data-ttu-id="e8909-149">Based on the criteria that was defined, the application gateway checks the file specified in the probe.</span><span class="sxs-lookup"><span data-stu-id="e8909-149">Based on the criteria that was defined, the application gateway checks the file specified in the probe.</span></span> <span data-ttu-id="e8909-150">If the call to host:Port/path does not return an Http 200 OK status response, the server is taken out of rotation, after the unhealthy threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="e8909-150">If the call to host:Port/path does not return an Http 200 OK status response, the server is taken out of rotation, after the unhealthy threshold is reached.</span></span> <span data-ttu-id="e8909-151">Probing continues on the unhealthy instance to determine when it becomes healthy again.</span><span class="sxs-lookup"><span data-stu-id="e8909-151">Probing continues on the unhealthy instance to determine when it becomes healthy again.</span></span> <span data-ttu-id="e8909-152">Once the instance is added back to healthy server pool, traffic begins flowing to it again and probing to the instance continues at user specified interval as normal.</span><span class="sxs-lookup"><span data-stu-id="e8909-152">Once the instance is added back to healthy server pool, traffic begins flowing to it again and probing to the instance continues at user specified interval as normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8909-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8909-153">Next steps</span></span>

<span data-ttu-id="e8909-154">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e8909-154">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-probe-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-probe-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-probe-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-probe-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-probe-portal/figure5.png





