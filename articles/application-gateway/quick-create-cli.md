---
title: Quickstart - Direct web traffic with Azure Application Gateway - Azure CLI | Microsoft Docs
description: Learn how use the Azure CLI to create an Azure Application Gateway that directs web traffic to virtual machines in a backend pool.
services: application-gateway
author: vhorne
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: quickstart
ms.workload: infrastructure-services
ms.date: 02/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 23ab97918d7def744f9ac3427faa3743b15124eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858097"
---
# <a name="quickstart-direct-web-traffic-with-azure-application-gateway---azure-cli"></a><span data-ttu-id="874a4-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="874a4-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure CLI</span></span>

<span data-ttu-id="874a4-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span><span class="sxs-lookup"><span data-stu-id="874a4-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span></span>

<span data-ttu-id="874a4-105">This quickstart shows you how to use the Azure CLI to quickly create the application gateway with two virtual machines in its backend pool.</span><span class="sxs-lookup"><span data-stu-id="874a4-105">This quickstart shows you how to use the Azure CLI to quickly create the application gateway with two virtual machines in its backend pool.</span></span> <span data-ttu-id="874a4-106">You then test it to make sure it's working correctly.</span><span class="sxs-lookup"><span data-stu-id="874a4-106">You then test it to make sure it's working correctly.</span></span>

<span data-ttu-id="874a4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="874a4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="874a4-108">If you choose to install and use the CLI locally, this quickstart requires that you run the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="874a4-108">If you choose to install and use the CLI locally, this quickstart requires that you run the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="874a4-109">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="874a4-109">To find the version, run `az --version`.</span></span> <span data-ttu-id="874a4-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="874a4-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="874a4-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="874a4-111">Create a resource group</span></span>

<span data-ttu-id="874a4-112">You need to always create resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="874a4-112">You need to always create resources in a resource group.</span></span> <span data-ttu-id="874a4-113">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-113">Create a resource group using [az group create](/cli/azure/group#az-group-create).</span></span> 

<span data-ttu-id="874a4-114">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="874a4-114">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="874a4-115">Create network resources</span><span class="sxs-lookup"><span data-stu-id="874a4-115">Create network resources</span></span> 

<span data-ttu-id="874a4-116">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span><span class="sxs-lookup"><span data-stu-id="874a4-116">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span></span> <span data-ttu-id="874a4-117">You can create a virtual network at the same time that you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="874a4-117">You can create a virtual network at the same time that you create the application gateway.</span></span> <span data-ttu-id="874a4-118">Two subnets are created in this example: one for the application gateway, and the other for the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="874a4-118">Two subnets are created in this example: one for the application gateway, and the other for the virtual machines.</span></span> 

<span data-ttu-id="874a4-119">Create the virtual network and subnet using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-119">Create the virtual network and subnet using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span></span> <span data-ttu-id="874a4-120">Create the public IP address using [az network public-ip create](/cli/azure/network/public-ip#az-public-ip-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-120">Create the public IP address using [az network public-ip create](/cli/azure/network/public-ip#az-public-ip-create).</span></span>

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
  --vnet-name myVNet   \
  --address-prefix 10.0.2.0/24
az network public-ip create \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress
```

## <a name="create-backend-servers"></a><span data-ttu-id="874a4-121">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="874a4-121">Create backend servers</span></span>

<span data-ttu-id="874a4-122">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="874a4-122">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span></span> 

### <a name="create-two-virtual-machines"></a><span data-ttu-id="874a4-123">Create two virtual machines</span><span class="sxs-lookup"><span data-stu-id="874a4-123">Create two virtual machines</span></span>

<span data-ttu-id="874a4-124">You also install NGINX on the virtual machines to verify that the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="874a4-124">You also install NGINX on the virtual machines to verify that the application gateway was successfully created.</span></span> <span data-ttu-id="874a4-125">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="874a4-125">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span></span> 

<span data-ttu-id="874a4-126">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span><span class="sxs-lookup"><span data-stu-id="874a4-126">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span></span> <span data-ttu-id="874a4-127">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="874a4-127">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="874a4-128">Create the network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-128">Create the network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create).</span></span> <span data-ttu-id="874a4-129">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-129">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span></span>

```azurecli-interactive
for i in `seq 1 2`; do
  az network nic create \
    --resource-group myResourceGroupAG \
    --name myNic$i \
    --vnet-name myVNet \
    --subnet myBackendSubnet
  az vm create \
    --resource-group myResourceGroupAG \
    --name myVM$i \
    --nics myNic$i \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
done
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="874a4-130">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="874a4-130">Create the application gateway</span></span>

<span data-ttu-id="874a4-131">Create an application gateway using [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create).</span><span class="sxs-lookup"><span data-stu-id="874a4-131">Create an application gateway using [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create).</span></span> <span data-ttu-id="874a4-132">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="874a4-132">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="874a4-133">The private IP addresses of the network interfaces are added as servers in the backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="874a4-133">The private IP addresses of the network interfaces are added as servers in the backend pool of the application gateway.</span></span>

```azurecli-interactive
address1=$(az network nic show --name myNic1 --resource-group myResourceGroupAG | grep "\"privateIpAddress\":" | grep -oE '[^ ]+$' | tr -d '",')
address2=$(az network nic show --name myNic2 --resource-group myResourceGroupAG | grep "\"privateIpAddress\":" | grep -oE '[^ ]+$' | tr -d '",')
az network application-gateway create \
  --name myAppGateway \
  --location eastus \
  --resource-group myResourceGroupAG \
  --capacity 2 \
  --sku Standard_Medium \
  --http-settings-cookie-based-affinity Enabled \
  --public-ip-address myAGPublicIPAddress \
  --vnet-name myVNet \
  --subnet myAGSubnet \
  --servers "$address1" "$address2"
```

<span data-ttu-id="874a4-134">It may take up to 30 minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="874a4-134">It may take up to 30 minutes for the application gateway to be created.</span></span> <span data-ttu-id="874a4-135">After the application gateway is created, you can see these features of it:</span><span class="sxs-lookup"><span data-stu-id="874a4-135">After the application gateway is created, you can see these features of it:</span></span>

- <span data-ttu-id="874a4-136">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="874a4-136">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="874a4-137">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="874a4-137">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="874a4-138">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="874a4-138">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="874a4-139">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="874a4-139">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="874a4-140">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="874a4-140">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="874a4-141">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="874a4-141">Test the application gateway</span></span>

<span data-ttu-id="874a4-142">Installing NGINX is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="874a4-142">Installing NGINX is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span></span> <span data-ttu-id="874a4-143">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="874a4-143">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> <span data-ttu-id="874a4-144">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="874a4-144">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
``` 

![Test application gateway](./media/quick-create-cli/application-gateway-nginxtest.png)

<span data-ttu-id="874a4-146">When you refresh the browser, you should see the name of the other VM appear.</span><span class="sxs-lookup"><span data-stu-id="874a4-146">When you refresh the browser, you should see the name of the other VM appear.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="874a4-147">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="874a4-147">Clean up resources</span></span>

<span data-ttu-id="874a4-148">First explore the resources that were created with the application gateway, and then when no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="874a4-148">First explore the resources that were created with the application gateway, and then when no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupAG
```
 
## <a name="next-steps"></a><span data-ttu-id="874a4-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="874a4-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="874a4-150">Manage web traffic with an application gateway using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="874a4-150">Manage web traffic with an application gateway using the Azure CLI</span></span>](./tutorial-manage-web-traffic-cli.md)

