---
title: Create an application gateway with multiple site hosting - Azure CLI | Microsoft Docs
description: Learn how to create an application gateway that hosts multiple sites using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.openlocfilehash: ff84c755cf9c871a27bf70e4c1a05aa63bc4f128
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865226"
---
# <a name="create-an-application-gateway-with-multiple-site-hosting-using-the-azure-cli"></a><span data-ttu-id="0a096-103">Create an application gateway with multiple site hosting using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a096-103">Create an application gateway with multiple site hosting using the Azure CLI</span></span>

<span data-ttu-id="0a096-104">You can use the Azure CLI to configure [hosting of multiple web sites](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a096-104">You can use the Azure CLI to configure [hosting of multiple web sites](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="0a096-105">In this tutorial, you create backend pools using virtual machines scale sets.</span><span class="sxs-lookup"><span data-stu-id="0a096-105">In this tutorial, you create backend pools using virtual machines scale sets.</span></span> <span data-ttu-id="0a096-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="0a096-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span></span> <span data-ttu-id="0a096-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="0a096-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span></span>

<span data-ttu-id="0a096-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="0a096-108">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a096-109">Set up the network</span><span class="sxs-lookup"><span data-stu-id="0a096-109">Set up the network</span></span>
> * <span data-ttu-id="0a096-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="0a096-110">Create an application gateway</span></span>
> * <span data-ttu-id="0a096-111">Create listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="0a096-111">Create listeners and routing rules</span></span>
> * <span data-ttu-id="0a096-112">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="0a096-112">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="0a096-113">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="0a096-113">Create a CNAME record in your domain</span></span>

![Multi-site routing example](./media/tutorial-multisite-cli/scenario.png)

<span data-ttu-id="0a096-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0a096-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a096-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="0a096-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0a096-117">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="0a096-117">To find the version, run `az --version`.</span></span> <span data-ttu-id="0a096-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0a096-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0a096-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="0a096-119">Create a resource group</span></span>

<span data-ttu-id="0a096-120">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="0a096-120">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0a096-121">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0a096-121">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="0a096-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="0a096-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="0a096-123">Create network resources</span><span class="sxs-lookup"><span data-stu-id="0a096-123">Create network resources</span></span> 

<span data-ttu-id="0a096-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="0a096-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="0a096-125">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="0a096-125">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="0a096-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="0a096-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway"></a><span data-ttu-id="0a096-127">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="0a096-127">Create the application gateway</span></span>

<span data-ttu-id="0a096-128">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="0a096-128">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="0a096-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="0a096-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="0a096-130">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="0a096-130">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> 

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

<span data-ttu-id="0a096-131">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="0a096-131">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="0a096-132">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="0a096-132">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="0a096-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="0a096-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="0a096-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="0a096-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="0a096-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="0a096-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="0a096-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="0a096-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="0a096-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="0a096-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

### <a name="add-the-backend-pools"></a><span data-ttu-id="0a096-138">Add the backend pools</span><span class="sxs-lookup"><span data-stu-id="0a096-138">Add the backend pools</span></span>

<span data-ttu-id="0a096-139">Add the backend pools named *contosoPool* and *fabrikamPool* that are needed to contain the backend servers using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address_pool_create).</span><span class="sxs-lookup"><span data-stu-id="0a096-139">Add the backend pools named *contosoPool* and *fabrikamPool* that are needed to contain the backend servers using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address_pool_create).</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name contosoPool
az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name fabrikamPool
```

### <a name="add-listeners"></a><span data-ttu-id="0a096-140">Add listeners</span><span class="sxs-lookup"><span data-stu-id="0a096-140">Add listeners</span></span>

<span data-ttu-id="0a096-141">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="0a096-141">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="0a096-142">In this tutorial, you create two listeners for your two domains.</span><span class="sxs-lookup"><span data-stu-id="0a096-142">In this tutorial, you create two listeners for your two domains.</span></span> <span data-ttu-id="0a096-143">In this example, listeners are created for the domains of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="0a096-143">In this example, listeners are created for the domains of *www.contoso.com* and *www.fabrikam.com*.</span></span> 

<span data-ttu-id="0a096-144">Add the listeners named *contosoListener* and *fabrikamListener* that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span><span class="sxs-lookup"><span data-stu-id="0a096-144">Add the listeners named *contosoListener* and *fabrikamListener* that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span></span>

```azurecli-interactive
az network application-gateway http-listener create \
  --name contosoListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.contoso.com
az network application-gateway http-listener create \
  --name fabrikamListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.fabrikam.com   
  ```

### <a name="add-routing-rules"></a><span data-ttu-id="0a096-145">Add routing rules</span><span class="sxs-lookup"><span data-stu-id="0a096-145">Add routing rules</span></span>

<span data-ttu-id="0a096-146">Rules are processed in the order in which they are created, and traffic is directed using the first rule that matches the URL sent to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0a096-146">Rules are processed in the order in which they are created, and traffic is directed using the first rule that matches the URL sent to the application gateway.</span></span> <span data-ttu-id="0a096-147">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span><span class="sxs-lookup"><span data-stu-id="0a096-147">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 

<span data-ttu-id="0a096-148">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0a096-148">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span></span> <span data-ttu-id="0a096-149">You can add the rule using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="0a096-149">You can add the rule using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span></span>

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name contosoRule \
  --resource-group myResourceGroupAG \
  --http-listener contosoListener \
  --rule-type Basic \
  --address-pool contosoPool
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name fabrikamRule \
  --resource-group myResourceGroupAG \
  --http-listener fabrikamListener \
  --rule-type Basic \
  --address-pool fabrikamPool
az network application-gateway rule delete \
  --gateway-name myAppGateway \
  --name rule1 \
  --resource-group myResourceGroupAG
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="0a096-150">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="0a096-150">Create virtual machine scale sets</span></span>

<span data-ttu-id="0a096-151">In this example, you create three virtual machine scale sets that support the three backend pools in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0a096-151">In this example, you create three virtual machine scale sets that support the three backend pools in the application gateway.</span></span> <span data-ttu-id="0a096-152">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="0a096-152">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="0a096-153">Each scale set contains two virtual machine instances on which you install NGINX.</span><span class="sxs-lookup"><span data-stu-id="0a096-153">Each scale set contains two virtual machine instances on which you install NGINX.</span></span>

```azurecli-interactive
for i in `seq 1 2`; do
  if [ $i -eq 1 ]
  then
    poolName="contosoPool"
  fi
  if [ $i -eq 2 ]
  then
    poolName="fabrikamPool"
  fi
  az vmss create \
    --name myvmss$i \
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
    --backend-pool-name $poolName
done
```

### <a name="install-nginx"></a><span data-ttu-id="0a096-154">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="0a096-154">Install NGINX</span></span>

```azurecli-interactive
for i in `seq 1 2`; do
  az vmss extension set \
    --publisher Microsoft.Azure.Extensions \
    --version 2.0 \
    --name CustomScript \
    --resource-group myResourceGroupAG \
    --vmss-name myvmss$i \
    --settings '{
  "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],
  "commandToExecute": "./install_nginx.sh" }'
done
```

## <a name="create-a-cname-record-in-your-domain"></a><span data-ttu-id="0a096-155">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="0a096-155">Create a CNAME record in your domain</span></span>

<span data-ttu-id="0a096-156">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="0a096-156">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="0a096-157">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="0a096-157">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span></span> <span data-ttu-id="0a096-158">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span><span class="sxs-lookup"><span data-stu-id="0a096-158">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span></span> 

```azurecli-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [dnsSettings.fqdn] \
  --output tsv
```

<span data-ttu-id="0a096-159">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="0a096-159">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="0a096-160">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="0a096-160">Test the application gateway</span></span>

<span data-ttu-id="0a096-161">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="0a096-161">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="0a096-162">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0a096-162">Such as, http://www.contoso.com.</span></span>

![Test contoso site in application gateway](./media/tutorial-multisite-cli/application-gateway-nginxtest1.png)

<span data-ttu-id="0a096-164">Change the address to your other domain and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="0a096-164">Change the address to your other domain and you should see something like the following example:</span></span>

![Test fabrikam site in application gateway](./media/tutorial-multisite-cli/application-gateway-nginxtest2.png)

## <a name="next-steps"></a><span data-ttu-id="0a096-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a096-166">Next steps</span></span>

<span data-ttu-id="0a096-167">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="0a096-167">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a096-168">Set up the network</span><span class="sxs-lookup"><span data-stu-id="0a096-168">Set up the network</span></span>
> * <span data-ttu-id="0a096-169">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="0a096-169">Create an application gateway</span></span>
> * <span data-ttu-id="0a096-170">Create listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="0a096-170">Create listeners and routing rules</span></span>
> * <span data-ttu-id="0a096-171">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="0a096-171">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="0a096-172">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="0a096-172">Create a CNAME record in your domain</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a096-173">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="0a096-173">Learn more about what you can do with application gateway</span></span>](application-gateway-introduction.md)