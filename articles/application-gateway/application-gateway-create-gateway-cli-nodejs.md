---
title: Create an Azure Application Gateway - Azure CLI 1.0  | Microsoft Docs
description: Learn how to create an Application Gateway by using the Azure CLI 1.0 in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: fad7fcf34fe6833eaa87340453485d0a412c3585
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550745"
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="77d10-103">Create an application gateway by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77d10-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="77d10-110">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="77d10-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="77d10-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="77d10-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="77d10-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span><span class="sxs-lookup"><span data-stu-id="77d10-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="77d10-113">Prerequisite: Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77d10-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="77d10-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="77d10-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> If you don't have an Azure account, you need one. Go sign up for a [free trial here](../active-directory/sign-up-organization.md).

## <a name="scenario"></a><span data-ttu-id="77d10-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="77d10-117">Scenario</span></span>

<span data-ttu-id="77d10-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="77d10-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="77d10-119">This scenario will:</span><span class="sxs-lookup"><span data-stu-id="77d10-119">This scenario will:</span></span>

* <span data-ttu-id="77d10-120">Create a medium application gateway with two instances.</span><span class="sxs-lookup"><span data-stu-id="77d10-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="77d10-121">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="77d10-121">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="77d10-122">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="77d10-122">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="77d10-123">Configure a certificate for SSL offload.</span><span class="sxs-lookup"><span data-stu-id="77d10-123">Configure a certificate for SSL offload.</span></span>

![Scenario example][scenario]

> [!NOTE]
> Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.

## <a name="before-you-begin"></a><span data-ttu-id="77d10-126">Before you begin</span><span class="sxs-lookup"><span data-stu-id="77d10-126">Before you begin</span></span>

<span data-ttu-id="77d10-127">Azure Application Gateway requires its own subnet.</span><span class="sxs-lookup"><span data-stu-id="77d10-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="77d10-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="77d10-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="77d10-129">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span><span class="sxs-lookup"><span data-stu-id="77d10-129">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="77d10-130">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="77d10-130">Log in to Azure</span></span>

<span data-ttu-id="77d10-131">Open the **Microsoft Azure Command Prompt**, and log in.</span><span class="sxs-lookup"><span data-stu-id="77d10-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
azure login
```

<span data-ttu-id="77d10-132">Once you type the preceding example, a code is provided.</span><span class="sxs-lookup"><span data-stu-id="77d10-132">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="77d10-133">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span><span class="sxs-lookup"><span data-stu-id="77d10-133">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd showing device login][1]

<span data-ttu-id="77d10-135">In the browser, enter the code you received.</span><span class="sxs-lookup"><span data-stu-id="77d10-135">In the browser, enter the code you received.</span></span> <span data-ttu-id="77d10-136">You are redirected to a sign-in page.</span><span class="sxs-lookup"><span data-stu-id="77d10-136">You are redirected to a sign-in page.</span></span>

![browser to enter code][2]

<span data-ttu-id="77d10-138">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span><span class="sxs-lookup"><span data-stu-id="77d10-138">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![successfully signed in][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="77d10-140">Switch to Resource Manager Mode</span><span class="sxs-lookup"><span data-stu-id="77d10-140">Switch to Resource Manager Mode</span></span>

```azurecli
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="77d10-141">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="77d10-141">Create the resource group</span></span>

<span data-ttu-id="77d10-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span><span class="sxs-lookup"><span data-stu-id="77d10-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="77d10-143">The following shows the command.</span><span class="sxs-lookup"><span data-stu-id="77d10-143">The following shows the command.</span></span>

```azurecli
azure group create -n AdatumAppGatewayRG -l eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="77d10-144">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="77d10-144">Create a virtual network</span></span>

<span data-ttu-id="77d10-145">Once the resource group is created, a virtual network is created for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="77d10-145">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="77d10-146">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span><span class="sxs-lookup"><span data-stu-id="77d10-146">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli
azure network vnet create -n AdatumAppGatewayVNET -a 10.0.0.0/16 -g AdatumAppGatewayRG -l eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="77d10-147">Create a subnet</span><span class="sxs-lookup"><span data-stu-id="77d10-147">Create a subnet</span></span>

<span data-ttu-id="77d10-148">After the virtual network is created, a subnet is added for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="77d10-148">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="77d10-149">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span><span class="sxs-lookup"><span data-stu-id="77d10-149">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli
azure network vnet subnet create -g AdatumAppGatewayRG -n Appgatewaysubnet -v AdatumAppGatewayVNET -a 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="77d10-150">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="77d10-150">Create the application gateway</span></span>

<span data-ttu-id="77d10-151">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span><span class="sxs-lookup"><span data-stu-id="77d10-151">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="77d10-152">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span><span class="sxs-lookup"><span data-stu-id="77d10-152">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="77d10-153">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span><span class="sxs-lookup"><span data-stu-id="77d10-153">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli
azure network application-gateway create -n AdatumAppGateway -l eastus -g AdatumAppGatewayRG -e AdatumAppGatewayVNET -m Appgatewaysubnet -r 134.170.185.46,134.170.188.221,134.170.185.50 -y c:\AdatumAppGateway\adatumcert.pfx -x P@ssw0rd -z 2 -a Standard_Medium -w Basic -j 443 -f Enabled -o 80 -i http -b https -u Standard
```

> [!NOTE]
> For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.

<span data-ttu-id="77d10-155">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span><span class="sxs-lookup"><span data-stu-id="77d10-155">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="77d10-156">It also configures SSL offload.</span><span class="sxs-lookup"><span data-stu-id="77d10-156">It also configures SSL offload.</span></span> <span data-ttu-id="77d10-157">You can modify these settings to suit your deployment once the provisioning is successful.</span><span class="sxs-lookup"><span data-stu-id="77d10-157">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="77d10-158">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span><span class="sxs-lookup"><span data-stu-id="77d10-158">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77d10-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="77d10-159">Next steps</span></span>

<span data-ttu-id="77d10-160">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="77d10-160">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="77d10-161">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="77d10-161">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/scenario.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure3.png




