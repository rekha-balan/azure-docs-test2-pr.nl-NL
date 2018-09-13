---
title: IP addresses in Azure Functions
description: Learn how to find inbound and outbound IP addresses for function apps, and what causes them to change.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: glenga
ms.openlocfilehash: 0fcda59add346d60f37273625fbbcf41faab0e15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857648"
---
# <a name="ip-addresses-in-azure-functions"></a><span data-ttu-id="08317-103">IP addresses in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="08317-103">IP addresses in Azure Functions</span></span>

<span data-ttu-id="08317-104">This article explains the following topics related to IP addresses of function apps:</span><span class="sxs-lookup"><span data-stu-id="08317-104">This article explains the following topics related to IP addresses of function apps:</span></span>

* <span data-ttu-id="08317-105">How to find the IP addresses currently in use by a function app.</span><span class="sxs-lookup"><span data-stu-id="08317-105">How to find the IP addresses currently in use by a function app.</span></span>
* <span data-ttu-id="08317-106">What causes a function app's IP addresses to be changed.</span><span class="sxs-lookup"><span data-stu-id="08317-106">What causes a function app's IP addresses to be changed.</span></span>
* <span data-ttu-id="08317-107">How to restrict the IP addresses that can access a function app.</span><span class="sxs-lookup"><span data-stu-id="08317-107">How to restrict the IP addresses that can access a function app.</span></span>
* <span data-ttu-id="08317-108">How to get dedicated IP addresses for a function app.</span><span class="sxs-lookup"><span data-stu-id="08317-108">How to get dedicated IP addresses for a function app.</span></span>

<span data-ttu-id="08317-109">IP addresses are associated with function apps, not with individual functions.</span><span class="sxs-lookup"><span data-stu-id="08317-109">IP addresses are associated with function apps, not with individual functions.</span></span> <span data-ttu-id="08317-110">Incoming HTTP requests can't use the inbound IP address to call individual functions; they must use the default domain name (functionappname.azurewebsites.net) or a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="08317-110">Incoming HTTP requests can't use the inbound IP address to call individual functions; they must use the default domain name (functionappname.azurewebsites.net) or a custom domain name.</span></span>

## <a name="function-app-inbound-ip-address"></a><span data-ttu-id="08317-111">Function app inbound IP address</span><span class="sxs-lookup"><span data-stu-id="08317-111">Function app inbound IP address</span></span>

<span data-ttu-id="08317-112">Each function app has a single inbound IP address.</span><span class="sxs-lookup"><span data-stu-id="08317-112">Each function app has a single inbound IP address.</span></span> <span data-ttu-id="08317-113">To find that IP address:</span><span class="sxs-lookup"><span data-stu-id="08317-113">To find that IP address:</span></span>

1. <span data-ttu-id="08317-114">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08317-114">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="08317-115">Navigate to the function app.</span><span class="sxs-lookup"><span data-stu-id="08317-115">Navigate to the function app.</span></span>
3. <span data-ttu-id="08317-116">Select **Platform features**.</span><span class="sxs-lookup"><span data-stu-id="08317-116">Select **Platform features**.</span></span>
4. <span data-ttu-id="08317-117">Select **Properties**, and the inbound IP address appears under **Virtual IP address**.</span><span class="sxs-lookup"><span data-stu-id="08317-117">Select **Properties**, and the inbound IP address appears under **Virtual IP address**.</span></span>

## <a name="find-outbound-ip-addresses"></a><span data-ttu-id="08317-118">Function app outbound IP addresses</span><span class="sxs-lookup"><span data-stu-id="08317-118">Function app outbound IP addresses</span></span>

<span data-ttu-id="08317-119">Each function app has a set of available outbound IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08317-119">Each function app has a set of available outbound IP addresses.</span></span> <span data-ttu-id="08317-120">Any outbound connection from a function, such as to a back-end database, uses one of the available outbound IP addresses as the origin IP address.</span><span class="sxs-lookup"><span data-stu-id="08317-120">Any outbound connection from a function, such as to a back-end database, uses one of the available outbound IP addresses as the origin IP address.</span></span> <span data-ttu-id="08317-121">You can't know beforehand which IP address a given connection will use.</span><span class="sxs-lookup"><span data-stu-id="08317-121">You can't know beforehand which IP address a given connection will use.</span></span> <span data-ttu-id="08317-122">For this reason, your back-end service must open its firewall to all of the function app's outbound IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08317-122">For this reason, your back-end service must open its firewall to all of the function app's outbound IP addresses.</span></span>

<span data-ttu-id="08317-123">To find the outbound IP addresses available to a function app:</span><span class="sxs-lookup"><span data-stu-id="08317-123">To find the outbound IP addresses available to a function app:</span></span>

1. <span data-ttu-id="08317-124">Sign in to the [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08317-124">Sign in to the [Azure Resource Explorer](https://resources.azure.com).</span></span>
2. <span data-ttu-id="08317-125">Select **subscriptions > {your subscription} > providers > Microsoft.Web > sites**.</span><span class="sxs-lookup"><span data-stu-id="08317-125">Select **subscriptions > {your subscription} > providers > Microsoft.Web > sites**.</span></span>
3. <span data-ttu-id="08317-126">In the JSON panel, find the site with an `id` property that ends in the name of your function app.</span><span class="sxs-lookup"><span data-stu-id="08317-126">In the JSON panel, find the site with an `id` property that ends in the name of your function app.</span></span>
4. <span data-ttu-id="08317-127">See `outboundIpAddresses` and `possibleOutboundIpAddresses`.</span><span class="sxs-lookup"><span data-stu-id="08317-127">See `outboundIpAddresses` and `possibleOutboundIpAddresses`.</span></span> 

<span data-ttu-id="08317-128">The set of `outboundIpAddresses` is currently available to the function app.</span><span class="sxs-lookup"><span data-stu-id="08317-128">The set of `outboundIpAddresses` is currently available to the function app.</span></span> <span data-ttu-id="08317-129">The set of `possibleOutboundIpAddresses` includes IP addresses that will be available only if the function app [scales to other pricing tiers](#outbound-ip-address-changes).</span><span class="sxs-lookup"><span data-stu-id="08317-129">The set of `possibleOutboundIpAddresses` includes IP addresses that will be available only if the function app [scales to other pricing tiers](#outbound-ip-address-changes).</span></span>

<span data-ttu-id="08317-130">An alternative way to find the available outbound IP addresses is by using the [Cloud Shell](../cloud-shell/quickstart.md):</span><span class="sxs-lookup"><span data-stu-id="08317-130">An alternative way to find the available outbound IP addresses is by using the [Cloud Shell](../cloud-shell/quickstart.md):</span></span>

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query outboundIpAddresses --output tsv
az webapp show --resource-group <group_name> --name <app_name> --query possibleOutboundIpAddresses --output tsv
```

## <a name="data-center-outbound-ip-addresses"></a><span data-ttu-id="08317-131">Data center outbound IP addresses</span><span class="sxs-lookup"><span data-stu-id="08317-131">Data center outbound IP addresses</span></span>

<span data-ttu-id="08317-132">If you need to whitelist the outbound IP addresses used by your function apps, another option is to whitelist the function apps' data center (Azure region).</span><span class="sxs-lookup"><span data-stu-id="08317-132">If you need to whitelist the outbound IP addresses used by your function apps, another option is to whitelist the function apps' data center (Azure region).</span></span> <span data-ttu-id="08317-133">You can [download an XML file that lists IP addresses for all Azure data centers](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="08317-133">You can [download an XML file that lists IP addresses for all Azure data centers](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span></span> <span data-ttu-id="08317-134">Then find the XML element that applies to the region that your function app runs in.</span><span class="sxs-lookup"><span data-stu-id="08317-134">Then find the XML element that applies to the region that your function app runs in.</span></span>

<span data-ttu-id="08317-135">For example, this is what the Western Europe XML element might look like:</span><span class="sxs-lookup"><span data-stu-id="08317-135">For example, this is what the Western Europe XML element might look like:</span></span>

```
  <Region Name="europewest">
    <IpRange Subnet="13.69.0.0/17" />
    <IpRange Subnet="13.73.128.0/18" />
    <!-- Some IP addresses not shown here -->
    <IpRange Subnet="213.199.180.192/27" />
    <IpRange Subnet="213.199.183.0/24" />
  </Region>
```

 <span data-ttu-id="08317-136">For information about when this file is updated and when the IP addresses change, expand the **Details** section of the [Download Center page](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="08317-136">For information about when this file is updated and when the IP addresses change, expand the **Details** section of the [Download Center page](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span></span>

## <a name="inbound-ip-address-changes"></a><span data-ttu-id="08317-137">Inbound IP address changes</span><span class="sxs-lookup"><span data-stu-id="08317-137">Inbound IP address changes</span></span>

 <span data-ttu-id="08317-138">The inbound IP address **might** change when you:</span><span class="sxs-lookup"><span data-stu-id="08317-138">The inbound IP address **might** change when you:</span></span>

- <span data-ttu-id="08317-139">Delete a function app and recreate it in a different resource group.</span><span class="sxs-lookup"><span data-stu-id="08317-139">Delete a function app and recreate it in a different resource group.</span></span>
- <span data-ttu-id="08317-140">Delete the last function app in a resource group and region combination, and re-create it.</span><span class="sxs-lookup"><span data-stu-id="08317-140">Delete the last function app in a resource group and region combination, and re-create it.</span></span>
- <span data-ttu-id="08317-141">Delete an SSL binding, such as during [certificate renewal](../app-service/app-service-web-tutorial-custom-ssl.md#renew-certificates)).</span><span class="sxs-lookup"><span data-stu-id="08317-141">Delete an SSL binding, such as during [certificate renewal](../app-service/app-service-web-tutorial-custom-ssl.md#renew-certificates)).</span></span>

<span data-ttu-id="08317-142">The inbound IP address might also change when you haven't taken any actions such as the ones listed.</span><span class="sxs-lookup"><span data-stu-id="08317-142">The inbound IP address might also change when you haven't taken any actions such as the ones listed.</span></span>

## <a name="outbound-ip-address-changes"></a><span data-ttu-id="08317-143">Outbound IP address changes</span><span class="sxs-lookup"><span data-stu-id="08317-143">Outbound IP address changes</span></span>

<span data-ttu-id="08317-144">The set of available outbound IP addresses for a function app might change when you:</span><span class="sxs-lookup"><span data-stu-id="08317-144">The set of available outbound IP addresses for a function app might change when you:</span></span>

* <span data-ttu-id="08317-145">Take any action that can change the inbound IP address.</span><span class="sxs-lookup"><span data-stu-id="08317-145">Take any action that can change the inbound IP address.</span></span>
* <span data-ttu-id="08317-146">Change your App Service plan pricing tier.</span><span class="sxs-lookup"><span data-stu-id="08317-146">Change your App Service plan pricing tier.</span></span> <span data-ttu-id="08317-147">The list of all possible outbound IP addresses your app can use, for all pricing tiers, is in the `possibleOutboundIPAddresses` property.</span><span class="sxs-lookup"><span data-stu-id="08317-147">The list of all possible outbound IP addresses your app can use, for all pricing tiers, is in the `possibleOutboundIPAddresses` property.</span></span> <span data-ttu-id="08317-148">See [Find outbound IPs](#find-outbound-ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="08317-148">See [Find outbound IPs](#find-outbound-ip-addresses).</span></span>

<span data-ttu-id="08317-149">The inbound IP address might also change when you haven't taken any actions such as the ones listed.</span><span class="sxs-lookup"><span data-stu-id="08317-149">The inbound IP address might also change when you haven't taken any actions such as the ones listed.</span></span>

<span data-ttu-id="08317-150">To deliberately force an outbound IP address change:</span><span class="sxs-lookup"><span data-stu-id="08317-150">To deliberately force an outbound IP address change:</span></span>

1. <span data-ttu-id="08317-151">Scale your App Service plan up or down between Standard and Premium v2 pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="08317-151">Scale your App Service plan up or down between Standard and Premium v2 pricing tiers.</span></span>
2. <span data-ttu-id="08317-152">Wait 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="08317-152">Wait 10 minutes.</span></span>
3. <span data-ttu-id="08317-153">Scale back to where you started.</span><span class="sxs-lookup"><span data-stu-id="08317-153">Scale back to where you started.</span></span>

## <a name="ip-address-restrictions"></a><span data-ttu-id="08317-154">IP address restrictions</span><span class="sxs-lookup"><span data-stu-id="08317-154">IP address restrictions</span></span>

<span data-ttu-id="08317-155">You can configure a list of IP addresses that you want to allow or deny access to a function app.</span><span class="sxs-lookup"><span data-stu-id="08317-155">You can configure a list of IP addresses that you want to allow or deny access to a function app.</span></span> <span data-ttu-id="08317-156">For more information, see [Azure App Service Static IP Restrictions](../app-service/app-service-ip-restrictions.md).</span><span class="sxs-lookup"><span data-stu-id="08317-156">For more information, see [Azure App Service Static IP Restrictions](../app-service/app-service-ip-restrictions.md).</span></span>

## <a name="dedicated-ip-addresses"></a><span data-ttu-id="08317-157">Dedicated IP addresses</span><span class="sxs-lookup"><span data-stu-id="08317-157">Dedicated IP addresses</span></span>

<span data-ttu-id="08317-158">If you need static, dedicated IP addresses, we recommend [App Service Environments](../app-service/environment/intro.md) (the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/) of App Service plans).</span><span class="sxs-lookup"><span data-stu-id="08317-158">If you need static, dedicated IP addresses, we recommend [App Service Environments](../app-service/environment/intro.md) (the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/) of App Service plans).</span></span> <span data-ttu-id="08317-159">For more information, see [App Service Environment IP addresses](../app-service/environment/network-info.md#ase-ip-addresses) and [How to control inbound traffic to an App Service Environment](../app-service/environment/app-service-app-service-environment-control-inbound-traffic.md).</span><span class="sxs-lookup"><span data-stu-id="08317-159">For more information, see [App Service Environment IP addresses](../app-service/environment/network-info.md#ase-ip-addresses) and [How to control inbound traffic to an App Service Environment](../app-service/environment/app-service-app-service-environment-control-inbound-traffic.md).</span></span>

<span data-ttu-id="08317-160">To find out if your function app runs in an App Service Environment:</span><span class="sxs-lookup"><span data-stu-id="08317-160">To find out if your function app runs in an App Service Environment:</span></span>

1. <span data-ttu-id="08317-161">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08317-161">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="08317-162">Navigate to the function app.</span><span class="sxs-lookup"><span data-stu-id="08317-162">Navigate to the function app.</span></span>
3. <span data-ttu-id="08317-163">Select the **Overview** tab.</span><span class="sxs-lookup"><span data-stu-id="08317-163">Select the **Overview** tab.</span></span>
4. <span data-ttu-id="08317-164">The App Service plan tier appears under **App Service plan/pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="08317-164">The App Service plan tier appears under **App Service plan/pricing tier**.</span></span> <span data-ttu-id="08317-165">The App Service Environment pricing tier is **Isolated**.</span><span class="sxs-lookup"><span data-stu-id="08317-165">The App Service Environment pricing tier is **Isolated**.</span></span>
 
<span data-ttu-id="08317-166">As an alternative, you can use the [Cloud Shell](../cloud-shell/quickstart.md):</span><span class="sxs-lookup"><span data-stu-id="08317-166">As an alternative, you can use the [Cloud Shell](../cloud-shell/quickstart.md):</span></span>

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query sku --output tsv
```

<span data-ttu-id="08317-167">The App Service Environment `sku` is `Isolated`.</span><span class="sxs-lookup"><span data-stu-id="08317-167">The App Service Environment `sku` is `Isolated`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08317-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="08317-168">Next steps</span></span>

<span data-ttu-id="08317-169">A common cause of IP changes is function app scale changes.</span><span class="sxs-lookup"><span data-stu-id="08317-169">A common cause of IP changes is function app scale changes.</span></span> <span data-ttu-id="08317-170">[Learn more about function app scaling](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="08317-170">[Learn more about function app scaling](functions-scale.md).</span></span>
