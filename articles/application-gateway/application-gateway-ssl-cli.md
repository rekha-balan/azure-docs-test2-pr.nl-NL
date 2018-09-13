---
title: Create an application gateway with SSL termination - Azure CLI | Microsoft Docs
description: Learn how to create an application gateway and add a certificate for SSL termination using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.openlocfilehash: 435223012ac637db9cda7af8e596fdcf88a76b76
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870099"
---
# <a name="create-an-application-gateway-with-ssl-termination-using-the-azure-cli"></a><span data-ttu-id="f2a2e-103">Create an application gateway with SSL termination using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f2a2e-103">Create an application gateway with SSL termination using the Azure CLI</span></span>

<span data-ttu-id="f2a2e-104">You can use the Azure CLI to create an [application gateway](application-gateway-introduction.md) with a certificate for [SSL termination](application-gateway-backend-ssl.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-104">You can use the Azure CLI to create an [application gateway](application-gateway-introduction.md) with a certificate for [SSL termination](application-gateway-backend-ssl.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span></span> <span data-ttu-id="f2a2e-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span></span>

<span data-ttu-id="f2a2e-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f2a2e-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2a2e-107">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f2a2e-107">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f2a2e-108">Set up a network</span><span class="sxs-lookup"><span data-stu-id="f2a2e-108">Set up a network</span></span>
> * <span data-ttu-id="f2a2e-109">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f2a2e-109">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f2a2e-110">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="f2a2e-110">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="f2a2e-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f2a2e-112">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-112">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f2a2e-113">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="f2a2e-114">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-114">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f2a2e-115">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f2a2e-115">Create a self-signed certificate</span></span>

<span data-ttu-id="f2a2e-116">For production use, you should import a valid certificate signed by trusted provider.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-116">For production use, you should import a valid certificate signed by trusted provider.</span></span> <span data-ttu-id="f2a2e-117">For this tutorial, you create a self-signed certificate and pfx file using the openssl command.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-117">For this tutorial, you create a self-signed certificate and pfx file using the openssl command.</span></span>

```azurecli-interactive
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out appgwcert.crt
```

<span data-ttu-id="f2a2e-118">Enter values that make sense for your certificate.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-118">Enter values that make sense for your certificate.</span></span> <span data-ttu-id="f2a2e-119">You can accept the default values.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-119">You can accept the default values.</span></span>

```azurecli-interactive
openssl pkcs12 -export -out appgwcert.pfx -inkey privateKey.key -in appgwcert.crt
```

<span data-ttu-id="f2a2e-120">Enter the password for the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-120">Enter the password for the certificate.</span></span> <span data-ttu-id="f2a2e-121">In this example, *Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="f2a2e-121">In this example, *Azure123456!*</span></span> <span data-ttu-id="f2a2e-122">is being used.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-122">is being used.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f2a2e-123">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f2a2e-123">Create a resource group</span></span>

<span data-ttu-id="f2a2e-124">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-124">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f2a2e-125">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-125">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="f2a2e-126">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-126">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="f2a2e-127">Create network resources</span><span class="sxs-lookup"><span data-stu-id="f2a2e-127">Create network resources</span></span>

<span data-ttu-id="f2a2e-128">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-128">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="f2a2e-129">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-129">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="f2a2e-130">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-130">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway"></a><span data-ttu-id="f2a2e-131">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="f2a2e-131">Create the application gateway</span></span>

<span data-ttu-id="f2a2e-132">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-132">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway.</span></span> <span data-ttu-id="f2a2e-133">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-133">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> 

<span data-ttu-id="f2a2e-134">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-134">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> <span data-ttu-id="f2a2e-135">In this example, you associate the certificate that you created and its password when you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-135">In this example, you associate the certificate that you created and its password when you create the application gateway.</span></span> 

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
  --frontend-port 443 \
  --http-settings-port 80 \
  --http-settings-protocol Http \
  --public-ip-address myAGPublicIPAddress \
  --cert-file appgwcert.pfx \
  --cert-password "Azure123456!"

```

 <span data-ttu-id="f2a2e-136">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-136">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="f2a2e-137">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="f2a2e-137">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="f2a2e-138">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-138">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="f2a2e-139">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-139">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="f2a2e-140">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-140">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="f2a2e-141">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-141">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="f2a2e-142">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-142">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="f2a2e-143">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f2a2e-143">Create a virtual machine scale set</span></span>

<span data-ttu-id="f2a2e-144">In this example, you create a virtual machine scale set that provides servers for the default backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-144">In this example, you create a virtual machine scale set that provides servers for the default backend pool in the application gateway.</span></span> <span data-ttu-id="f2a2e-145">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-145">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span></span> <span data-ttu-id="f2a2e-146">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-146">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="f2a2e-147">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="f2a2e-147">Install NGINX</span></span>

```azurecli-interactive
az vmss extension set \
  --publisher Microsoft.Azure.Extensions \
  --version 2.0 \
  --name CustomScript \
  --resource-group myResourceGroupAG \
  --vmss-name myvmss \
  --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],
  "commandToExecute": "./install_nginx.sh" }'
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="f2a2e-148">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="f2a2e-148">Test the application gateway</span></span>

<span data-ttu-id="f2a2e-149">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="f2a2e-149">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="f2a2e-150">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-150">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Secure warning](./media/application-gateway-ssl-cli/application-gateway-secure.png)

<span data-ttu-id="f2a2e-152">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-152">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span></span> <span data-ttu-id="f2a2e-153">Your secured NGINX site is then displayed as in the following example:</span><span class="sxs-lookup"><span data-stu-id="f2a2e-153">Your secured NGINX site is then displayed as in the following example:</span></span>

![Test base URL in application gateway](./media/application-gateway-ssl-cli/application-gateway-nginx.png)

## <a name="next-steps"></a><span data-ttu-id="f2a2e-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2a2e-155">Next steps</span></span>

<span data-ttu-id="f2a2e-156">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f2a2e-156">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2a2e-157">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f2a2e-157">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f2a2e-158">Set up a network</span><span class="sxs-lookup"><span data-stu-id="f2a2e-158">Set up a network</span></span>
> * <span data-ttu-id="f2a2e-159">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f2a2e-159">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f2a2e-160">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="f2a2e-160">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="f2a2e-161">To learn more about application gateways and their associated resources, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="f2a2e-161">To learn more about application gateways and their associated resources, continue to the how-to articles.</span></span>
