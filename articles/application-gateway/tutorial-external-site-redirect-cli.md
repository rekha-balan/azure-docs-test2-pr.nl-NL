---
title: Create an application gateway with external traffic redirection - Azure CLI | Microsoft Docs
description: Learn how to create an application gateway that redirects internal web traffic to the appropriate pool using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/24/2018
ms.author: victorh
ms.openlocfilehash: 06568c6822ec806792f442a0b53db958f2395b3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869202"
---
# <a name="create-an-application-gateway-with-external-redirection-using-the-azure-cli"></a><span data-ttu-id="05989-103">Create an application gateway with external redirection using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05989-103">Create an application gateway with external redirection using the Azure CLI</span></span>

<span data-ttu-id="05989-104">You can use the Azure CLI to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05989-104">You can use the Azure CLI to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="05989-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span><span class="sxs-lookup"><span data-stu-id="05989-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span></span>

<span data-ttu-id="05989-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="05989-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05989-107">Set up the network</span><span class="sxs-lookup"><span data-stu-id="05989-107">Set up the network</span></span>
> * <span data-ttu-id="05989-108">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="05989-108">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="05989-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="05989-109">Create an application gateway</span></span>

<span data-ttu-id="05989-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="05989-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05989-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="05989-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="05989-112">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="05989-112">To find the version, run `az --version`.</span></span> <span data-ttu-id="05989-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="05989-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="05989-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="05989-114">Create a resource group</span></span>

<span data-ttu-id="05989-115">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="05989-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="05989-116">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="05989-116">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="05989-117">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="05989-117">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="05989-118">Create network resources</span><span class="sxs-lookup"><span data-stu-id="05989-118">Create network resources</span></span> 

<span data-ttu-id="05989-119">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="05989-119">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="05989-120">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="05989-120">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span> <span data-ttu-id="05989-121">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="05989-121">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

```azurecli-interactive
az network vnet create \
  --name myVNet \
  --resource-group myResourceGroupAG \
  --location eastus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name myAGSubnet \
  --subnet-prefix 10.0.1.0/24
az network public-ip create \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="05989-122">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="05989-122">Create an application gateway</span></span>

<span data-ttu-id="05989-123">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="05989-123">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="05989-124">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="05989-124">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="05989-125">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="05989-125">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span></span> 

```azurecli-interactive
az network application-gateway create \
  --name myAppGateway \
  --location eastus \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --subnet myAGsubnet \
  --capacity 2 \
  --sku Standard_Medium \
  --http-settings-cookie-based-affinity Disabled \
  --frontend-port 8080 \
  --http-settings-port 80 \
  --http-settings-protocol Http \
  --public-ip-address myAGPublicIPAddress
```

<span data-ttu-id="05989-126">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="05989-126">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="05989-127">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="05989-127">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="05989-128">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="05989-128">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="05989-129">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="05989-129">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="05989-130">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="05989-130">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="05989-131">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="05989-131">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="05989-132">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="05989-132">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

### <a name="add-the-redirection-configuration"></a><span data-ttu-id="05989-133">Add the redirection configuration</span><span class="sxs-lookup"><span data-stu-id="05989-133">Add the redirection configuration</span></span>

<span data-ttu-id="05989-134">Add the redirection configuration that sends traffic from the application gateway to *bing.com* using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span><span class="sxs-lookup"><span data-stu-id="05989-134">Add the redirection configuration that sends traffic from the application gateway to *bing.com* using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span></span>

```azurecli-interactive
az network application-gateway redirect-config create \
  --name myredirect \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --type Temporary \
  --target-url "http://bing.com"
```

### <a name="add-a-listener-and-routing-rule"></a><span data-ttu-id="05989-135">Add a listener and routing rule</span><span class="sxs-lookup"><span data-stu-id="05989-135">Add a listener and routing rule</span></span>

<span data-ttu-id="05989-136">A listener is required to enable the application gateway to appropriately route traffic.</span><span class="sxs-lookup"><span data-stu-id="05989-136">A listener is required to enable the application gateway to appropriately route traffic.</span></span> <span data-ttu-id="05989-137">Create the listener using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create) with the frontend port created with [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span><span class="sxs-lookup"><span data-stu-id="05989-137">Create the listener using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create) with the frontend port created with [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span></span> <span data-ttu-id="05989-138">A rule is required for the listener to know where to send incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="05989-138">A rule is required for the listener to know where to send incoming traffic.</span></span> <span data-ttu-id="05989-139">Create a basic rule named *redirectRule* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create) with the redirection configuration.</span><span class="sxs-lookup"><span data-stu-id="05989-139">Create a basic rule named *redirectRule* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create) with the redirection configuration.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create \
  --port 80 \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name redirectPort
az network application-gateway http-listener create \
  --name redirectListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port redirectPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name redirectRule \
  --resource-group myResourceGroupAG \
  --http-listener redirectListener \
  --rule-type Basic \
  --redirect-config myredirect
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="05989-140">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="05989-140">Test the application gateway</span></span>

<span data-ttu-id="05989-141">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="05989-141">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="05989-142">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="05989-142">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

<span data-ttu-id="05989-143">You should see *bing.com* appear in your browser.</span><span class="sxs-lookup"><span data-stu-id="05989-143">You should see *bing.com* appear in your browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05989-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="05989-144">Next steps</span></span>

<span data-ttu-id="05989-145">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="05989-145">In this tutorial, you learned how to:</span></span>

> * <span data-ttu-id="05989-146">Set up the network</span><span class="sxs-lookup"><span data-stu-id="05989-146">Set up the network</span></span>
> * <span data-ttu-id="05989-147">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="05989-147">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="05989-148">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="05989-148">Create an application gateway</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05989-149">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="05989-149">Learn more about what you can do with application gateway</span></span>](./application-gateway-introduction.md)