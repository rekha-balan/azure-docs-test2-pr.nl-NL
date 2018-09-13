---
title: Tutorial - Manage web traffic - Azure CLI
description: Learn how to create an application gateway with a virtual machine scale set to manage web traffic using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 686036a1ebb52c34d79822cf9fd3cdcba0349fca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867431"
---
# <a name="tutorial-manage-web-traffic-with-an-application-gateway-using-the-azure-cli"></a><span data-ttu-id="0ac71-103">Tutorial: Manage web traffic with an application gateway using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ac71-103">Tutorial: Manage web traffic with an application gateway using the Azure CLI</span></span>

<span data-ttu-id="0ac71-104">Application gateway is used to manage and secure web traffic to servers that you maintain.</span><span class="sxs-lookup"><span data-stu-id="0ac71-104">Application gateway is used to manage and secure web traffic to servers that you maintain.</span></span> <span data-ttu-id="0ac71-105">You can use the Azure CLI to create an [application gateway](overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers to manage web traffic.</span><span class="sxs-lookup"><span data-stu-id="0ac71-105">You can use the Azure CLI to create an [application gateway](overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers to manage web traffic.</span></span> <span data-ttu-id="0ac71-106">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0ac71-106">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span></span>

<span data-ttu-id="0ac71-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="0ac71-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ac71-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="0ac71-108">Set up the network</span></span>
> * <span data-ttu-id="0ac71-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="0ac71-109">Create an application gateway</span></span>
> * <span data-ttu-id="0ac71-110">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="0ac71-110">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="0ac71-111">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-manage-web-traffic-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0ac71-111">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-manage-web-traffic-powershell.md).</span></span>

<span data-ttu-id="0ac71-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0ac71-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0ac71-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="0ac71-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0ac71-114">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="0ac71-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="0ac71-115">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ac71-115">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0ac71-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="0ac71-116">Create a resource group</span></span>

<span data-ttu-id="0ac71-117">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="0ac71-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0ac71-118">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="0ac71-118">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span></span> 

<span data-ttu-id="0ac71-119">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="0ac71-119">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="0ac71-120">Create network resources</span><span class="sxs-lookup"><span data-stu-id="0ac71-120">Create network resources</span></span> 

<span data-ttu-id="0ac71-121">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="0ac71-121">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="0ac71-122">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="0ac71-122">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="0ac71-123">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="0ac71-123">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

```azurecli-interactive
az network vnet create \
  --name myVNet \
  --resource-group myResourceGroupAG \
  --location eastus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name myAGSubnet \
  --subnet-prefix 10.0.1.0/24

az network vnet subnet create \
  --name myBackendSubnet \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --address-prefix 10.0.2.0/24

az network public-ip create \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="0ac71-124">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="0ac71-124">Create an application gateway</span></span>

<span data-ttu-id="0ac71-125">Use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="0ac71-125">Use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="0ac71-126">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="0ac71-126">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="0ac71-127">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="0ac71-127">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span></span> 

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
  --frontend-port 80 \
  --http-settings-port 80 \
  --http-settings-protocol Http \
  --public-ip-address myAGPublicIPAddress
```

 <span data-ttu-id="0ac71-128">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="0ac71-128">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="0ac71-129">After the application gateway is created, you will see these new features:</span><span class="sxs-lookup"><span data-stu-id="0ac71-129">After the application gateway is created, you will see these new features:</span></span>

- <span data-ttu-id="0ac71-130">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="0ac71-130">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="0ac71-131">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="0ac71-131">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="0ac71-132">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="0ac71-132">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="0ac71-133">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="0ac71-133">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="0ac71-134">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="0ac71-134">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="0ac71-135">Create a Virtual Machine Scale Set</span><span class="sxs-lookup"><span data-stu-id="0ac71-135">Create a Virtual Machine Scale Set</span></span>

<span data-ttu-id="0ac71-136">In this example, you create a virtual machine scale set that provides servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0ac71-136">In this example, you create a virtual machine scale set that provides servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="0ac71-137">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="0ac71-137">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span></span> <span data-ttu-id="0ac71-138">To create the scale set, use [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="0ac71-138">To create the scale set, use [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span>

```azurecli-interactive
az vmss create \
  --name myvmss \
  --resource-group myResourceGroupAG \
  --image UbuntuLTS \
  --admin-username azureuser \
  --admin-password Azure123456! \
  --instance-count 2 \
  --vnet-name myVNet \
  --subnet myBackendSubnet \
  --vm-sku Standard_DS2 \
  --upgrade-policy-mode Automatic \
  --app-gateway myAppGateway \
  --backend-pool-name appGatewayBackendPool
```

### <a name="install-nginx"></a><span data-ttu-id="0ac71-139">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="0ac71-139">Install NGINX</span></span>

<span data-ttu-id="0ac71-140">Now you can install NGINX on the virtual machine scale set so you can test HTTP connectivity to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="0ac71-140">Now you can install NGINX on the virtual machine scale set so you can test HTTP connectivity to the backend pool.</span></span>

```azurecli-interactive
az vmss extension set \
  --publisher Microsoft.Azure.Extensions \
  --version 2.0 \
  --name CustomScript \
  --resource-group myResourceGroupAG \
  --vmss-name myvmss \
  --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"], "commandToExecute": "./install_nginx.sh" }'
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="0ac71-141">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="0ac71-141">Test the application gateway</span></span>

<span data-ttu-id="0ac71-142">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="0ac71-142">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="0ac71-143">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="0ac71-143">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Test base URL in application gateway](./media/tutorial-manage-web-traffic-cli/tutorial-nginxtest.png)

## <a name="clean-up-resources"></a><span data-ttu-id="0ac71-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0ac71-145">Clean up resources</span></span>

<span data-ttu-id="0ac71-146">When no longer needed, remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="0ac71-146">When no longer needed, remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroupAG --location eastus
```

## <a name="next-steps"></a><span data-ttu-id="0ac71-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ac71-147">Next steps</span></span>

<span data-ttu-id="0ac71-148">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="0ac71-148">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ac71-149">Set up the network</span><span class="sxs-lookup"><span data-stu-id="0ac71-149">Set up the network</span></span>
> * <span data-ttu-id="0ac71-150">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="0ac71-150">Create an application gateway</span></span>
> * <span data-ttu-id="0ac71-151">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="0ac71-151">Create a virtual machine scale set with the default backend pool</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ac71-152">Restrict web traffic with a web application firewall</span><span class="sxs-lookup"><span data-stu-id="0ac71-152">Restrict web traffic with a web application firewall</span></span>](./tutorial-restrict-web-traffic-cli.md)
