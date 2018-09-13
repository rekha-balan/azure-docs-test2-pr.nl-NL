---
title: Create an Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs
description: Learn how to create an Application Gateway by using the Azure CLI 2.0 in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: cbe0720beca1fd12b172c90b617e0eee46e18391
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662269"
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="f226d-103">Create an application gateway by using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f226d-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

<span data-ttu-id="f226d-110">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="f226d-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f226d-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="f226d-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="f226d-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span><span class="sxs-lookup"><span data-stu-id="f226d-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f226d-113">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="f226d-113">CLI versions to complete the task</span></span>

<span data-ttu-id="f226d-114">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="f226d-114">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="f226d-115">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="f226d-115">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="f226d-116">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="f226d-116">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="f226d-117">Prerequisite: Install the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f226d-117">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="f226d-118">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f226d-118">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> If you don't have an Azure account, you need one. Go sign up for a [free trial here](../active-directory/sign-up-organization.md).

## <a name="scenario"></a><span data-ttu-id="f226d-121">Scenario</span><span class="sxs-lookup"><span data-stu-id="f226d-121">Scenario</span></span>

<span data-ttu-id="f226d-122">In this scenario, you learn how to create an application gateway using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f226d-122">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="f226d-123">This scenario will:</span><span class="sxs-lookup"><span data-stu-id="f226d-123">This scenario will:</span></span>

* <span data-ttu-id="f226d-124">Create a medium application gateway with two instances.</span><span class="sxs-lookup"><span data-stu-id="f226d-124">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="f226d-125">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="f226d-125">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="f226d-126">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="f226d-126">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="f226d-127">Configure a certificate for SSL offload.</span><span class="sxs-lookup"><span data-stu-id="f226d-127">Configure a certificate for SSL offload.</span></span>

![Scenario example][scenario]

> [!NOTE]
> Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.

## <a name="before-you-begin"></a><span data-ttu-id="f226d-130">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f226d-130">Before you begin</span></span>

<span data-ttu-id="f226d-131">Azure Application Gateway requires its own subnet.</span><span class="sxs-lookup"><span data-stu-id="f226d-131">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="f226d-132">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="f226d-132">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="f226d-133">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span><span class="sxs-lookup"><span data-stu-id="f226d-133">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="f226d-134">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f226d-134">Log in to Azure</span></span>

<span data-ttu-id="f226d-135">Open the **Microsoft Azure Command Prompt**, and log in.</span><span class="sxs-lookup"><span data-stu-id="f226d-135">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

>[NOTE] You can also use `az login` without the switch for device login that will require entering a code at aka.ms/devicelogin.

<span data-ttu-id="f226d-137">Once you type the preceding example, a code is provided.</span><span class="sxs-lookup"><span data-stu-id="f226d-137">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="f226d-138">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span><span class="sxs-lookup"><span data-stu-id="f226d-138">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd showing device login][1]

<span data-ttu-id="f226d-140">In the browser, enter the code you received.</span><span class="sxs-lookup"><span data-stu-id="f226d-140">In the browser, enter the code you received.</span></span> <span data-ttu-id="f226d-141">You are redirected to a sign-in page.</span><span class="sxs-lookup"><span data-stu-id="f226d-141">You are redirected to a sign-in page.</span></span>

![browser to enter code][2]

<span data-ttu-id="f226d-143">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span><span class="sxs-lookup"><span data-stu-id="f226d-143">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![successfully signed in][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="f226d-145">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="f226d-145">Create the resource group</span></span>

<span data-ttu-id="f226d-146">Before creating the application gateway, a resource group is created to contain the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f226d-146">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="f226d-147">The following shows the command.</span><span class="sxs-lookup"><span data-stu-id="f226d-147">The following shows the command.</span></span>

```azurecli
az resource group create --name myresourcegroup --location "West US"
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="f226d-148">Create a virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="f226d-148">Create a virtual network and subnet</span></span>

<span data-ttu-id="f226d-149">Once the resource group is created, a virtual network is created for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f226d-149">Once the resource group is created, a virtual network is created for the Application Gateway.</span></span>  <span data-ttu-id="f226d-150">In the following example, the address space was as 10.0.0.0/16 is defined for the virtual network and 10.0.0.0/28 is used for the subnet as seen in the preceding scenario notes.</span><span class="sxs-lookup"><span data-stu-id="f226d-150">In the following example, the address space was as 10.0.0.0/16 is defined for the virtual network and 10.0.0.0/28 is used for the subnet as seen in the preceding scenario notes.</span></span>

```azurecli
az network vnet create \
--name AdatumAppGatewayVNET \
--address-prefix 10.0.0.0/16 \
--subnet-name Appgatewaysubnet \
--subnet-prefix 10.0.0.0/28 \
--resource-group AdatumAppGateway \
--location eastus
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="f226d-151">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="f226d-151">Create the application gateway</span></span>

<span data-ttu-id="f226d-152">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span><span class="sxs-lookup"><span data-stu-id="f226d-152">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="f226d-153">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span><span class="sxs-lookup"><span data-stu-id="f226d-153">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="f226d-154">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span><span class="sxs-lookup"><span data-stu-id="f226d-154">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli
az network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group AdatumAppGatewayRG \
--vnet-name AdatumAppGatewayVNET \
--vnet-address-prefix 10.0.0.0/16 \
--subnet Appgatewaysubnet \
--subnet-address-prefix 10.0.0.0/28 \
--servers 10.0.0.4 10.0.0.5 \
--cert-file /mnt/c/Users/username/Desktop/application-gateway/fabrikam.pfx \
--cert-password P@ssw0rd \
--capacity 2 \
--sku-tier Standard \
--sku-name Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 443 \
--routing-rule-type Basic \
--http-settings-port 80

```

> [!NOTE]
> For a list of parameters that can be provided during creation run the following command: **az network application-gateway create --help**.

<span data-ttu-id="f226d-156">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span><span class="sxs-lookup"><span data-stu-id="f226d-156">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="f226d-157">It also configures SSL offload.</span><span class="sxs-lookup"><span data-stu-id="f226d-157">It also configures SSL offload.</span></span> <span data-ttu-id="f226d-158">You can modify these settings to suit your deployment once the provisioning is successful.</span><span class="sxs-lookup"><span data-stu-id="f226d-158">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="f226d-159">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span><span class="sxs-lookup"><span data-stu-id="f226d-159">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f226d-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="f226d-160">Next steps</span></span>

<span data-ttu-id="f226d-161">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f226d-161">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="f226d-162">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="f226d-162">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/scenario.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-cli/figure3.png




