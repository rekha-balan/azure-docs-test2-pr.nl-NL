---
title: Create an application gateway with a virtual machine scale set - Azure CLI | Microsoft Docs
description: Learn how to create an application gateway with a virtual machine scale set using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.openlocfilehash: 3efd07f5e44863e6e2e16db96953826200cb138b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857493"
---
# <a name="create-an-application-gateway-with-a-virtual-machine-scale-set-using-the-azure-cli"></a><span data-ttu-id="3af5e-103">Create an application gateway with a virtual machine scale set using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3af5e-103">Create an application gateway with a virtual machine scale set using the Azure CLI</span></span>

<span data-ttu-id="3af5e-104">You can use the Azure CLI to create an [application gateway](application-gateway-introduction.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span><span class="sxs-lookup"><span data-stu-id="3af5e-104">You can use the Azure CLI to create an [application gateway](application-gateway-introduction.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span></span> <span data-ttu-id="3af5e-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="3af5e-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span></span>

<span data-ttu-id="3af5e-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="3af5e-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3af5e-107">Set up the network</span><span class="sxs-lookup"><span data-stu-id="3af5e-107">Set up the network</span></span>
> * <span data-ttu-id="3af5e-108">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3af5e-108">Create an application gateway</span></span>
> * <span data-ttu-id="3af5e-109">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="3af5e-109">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="3af5e-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3af5e-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3af5e-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="3af5e-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3af5e-112">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="3af5e-112">To find the version, run `az --version`.</span></span> <span data-ttu-id="3af5e-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3af5e-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="3af5e-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="3af5e-114">Create a resource group</span></span>

<span data-ttu-id="3af5e-115">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="3af5e-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="3af5e-116">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="3af5e-116">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span></span> 

<span data-ttu-id="3af5e-117">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="3af5e-117">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="3af5e-118">Create network resources</span><span class="sxs-lookup"><span data-stu-id="3af5e-118">Create network resources</span></span> 

<span data-ttu-id="3af5e-119">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="3af5e-119">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="3af5e-120">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="3af5e-120">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="3af5e-121">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="3af5e-121">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="3af5e-122">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3af5e-122">Create an application gateway</span></span>

<span data-ttu-id="3af5e-123">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="3af5e-123">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="3af5e-124">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="3af5e-124">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="3af5e-125">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="3af5e-125">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span></span> 

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

 <span data-ttu-id="3af5e-126">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="3af5e-126">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="3af5e-127">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="3af5e-127">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="3af5e-128">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="3af5e-128">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="3af5e-129">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="3af5e-129">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="3af5e-130">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="3af5e-130">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="3af5e-131">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="3af5e-131">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="3af5e-132">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="3af5e-132">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="3af5e-133">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="3af5e-133">Create a virtual machine scale set</span></span>

<span data-ttu-id="3af5e-134">In this example, you create a virtual machine scale set that provides servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="3af5e-134">In this example, you create a virtual machine scale set that provides servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="3af5e-135">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="3af5e-135">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span></span> <span data-ttu-id="3af5e-136">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="3af5e-136">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="3af5e-137">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="3af5e-137">Install NGINX</span></span>

```azurecli-interactive
az vmss extension set \
  --publisher Microsoft.Azure.Extensions \
  --version 2.0 \
  --name CustomScript \
  --resource-group myResourceGroupAG \
  --vmss-name myvmss \
  --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"], "commandToExecute": "./install_nginx.sh" }'
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="3af5e-138">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="3af5e-138">Test the application gateway</span></span>

<span data-ttu-id="3af5e-139">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="3af5e-139">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="3af5e-140">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="3af5e-140">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Test base URL in application gateway](./media/tutorial-create-vmss-cli/tutorial-nginxtest.png)

## <a name="next-steps"></a><span data-ttu-id="3af5e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="3af5e-142">Next steps</span></span>

<span data-ttu-id="3af5e-143">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="3af5e-143">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3af5e-144">Set up the network</span><span class="sxs-lookup"><span data-stu-id="3af5e-144">Set up the network</span></span>
> * <span data-ttu-id="3af5e-145">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3af5e-145">Create an application gateway</span></span>
> * <span data-ttu-id="3af5e-146">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="3af5e-146">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="3af5e-147">To learn more about application gateways and their associated resources, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="3af5e-147">To learn more about application gateways and their associated resources, continue to the how-to articles.</span></span>
