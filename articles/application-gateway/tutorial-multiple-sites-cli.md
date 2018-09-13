---
title: Create an application gateway that hosts multiple web sites - Azure CLI
description: Learn how to create an application gateway that hosts multiple web sites using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 13f37f1b0efaa8169d272220362290bac9b3aac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856324"
---
# <a name="tutorial-create-an-application-gateway-that-hosts-multiple-web-sites-using-the-azure-cli"></a><span data-ttu-id="94ff9-103">Tutorial: Create an application gateway that hosts multiple web sites using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94ff9-103">Tutorial: Create an application gateway that hosts multiple web sites using the Azure CLI</span></span>

<span data-ttu-id="94ff9-104">You can use the Azure CLI to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="94ff9-104">You can use the Azure CLI to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="94ff9-105">In this tutorial, you define backend address pools using virtual machines scale sets.</span><span class="sxs-lookup"><span data-stu-id="94ff9-105">In this tutorial, you define backend address pools using virtual machines scale sets.</span></span> <span data-ttu-id="94ff9-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="94ff9-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span></span> <span data-ttu-id="94ff9-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="94ff9-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span></span>

<span data-ttu-id="94ff9-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="94ff9-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94ff9-109">Set up the network</span><span class="sxs-lookup"><span data-stu-id="94ff9-109">Set up the network</span></span>
> * <span data-ttu-id="94ff9-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="94ff9-110">Create an application gateway</span></span>
> * <span data-ttu-id="94ff9-111">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="94ff9-111">Create backend listeners</span></span>
> * <span data-ttu-id="94ff9-112">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="94ff9-112">Create routing rules</span></span>
> * <span data-ttu-id="94ff9-113">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="94ff9-113">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="94ff9-114">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="94ff9-114">Create a CNAME record in your domain</span></span>

![Multi-site routing example](./media/tutorial-multiple-sites-cli/scenario.png)


<span data-ttu-id="94ff9-116">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-multiple-sites-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="94ff9-116">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-multiple-sites-powershell.md).</span></span>

<span data-ttu-id="94ff9-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="94ff9-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94ff9-118">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="94ff9-118">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="94ff9-119">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="94ff9-119">To find the version, run `az --version`.</span></span> <span data-ttu-id="94ff9-120">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94ff9-120">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="94ff9-121">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="94ff9-121">Create a resource group</span></span>

<span data-ttu-id="94ff9-122">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="94ff9-122">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="94ff9-123">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-123">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="94ff9-124">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="94ff9-124">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="94ff9-125">Create network resources</span><span class="sxs-lookup"><span data-stu-id="94ff9-125">Create network resources</span></span> 

<span data-ttu-id="94ff9-126">Create the virtual network and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="94ff9-126">Create the virtual network and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="94ff9-127">You can then add the subnet that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-127">You can then add the subnet that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="94ff9-128">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-128">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway"></a><span data-ttu-id="94ff9-129">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="94ff9-129">Create the application gateway</span></span>

<span data-ttu-id="94ff9-130">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="94ff9-130">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway.</span></span> <span data-ttu-id="94ff9-131">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="94ff9-131">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="94ff9-132">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="94ff9-132">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> 

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

<span data-ttu-id="94ff9-133">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="94ff9-133">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="94ff9-134">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="94ff9-134">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="94ff9-135">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="94ff9-135">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="94ff9-136">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="94ff9-136">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="94ff9-137">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="94ff9-137">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="94ff9-138">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="94ff9-138">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="94ff9-139">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="94ff9-139">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

### <a name="add-the-backend-pools"></a><span data-ttu-id="94ff9-140">Add the backend pools</span><span class="sxs-lookup"><span data-stu-id="94ff9-140">Add the backend pools</span></span>

<span data-ttu-id="94ff9-141">Add the backend pools that are needed to contain the backend servers using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address_pool_create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-141">Add the backend pools that are needed to contain the backend servers using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address_pool_create).</span></span>

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

### <a name="add-backend-listeners"></a><span data-ttu-id="94ff9-142">Add backend listeners</span><span class="sxs-lookup"><span data-stu-id="94ff9-142">Add backend listeners</span></span>

<span data-ttu-id="94ff9-143">Add the backend listeners that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-143">Add the backend listeners that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span></span>

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

### <a name="add-routing-rules"></a><span data-ttu-id="94ff9-144">Add routing rules</span><span class="sxs-lookup"><span data-stu-id="94ff9-144">Add routing rules</span></span>

<span data-ttu-id="94ff9-145">Rules are processed in the order they are listed, and traffic is directed using the first rule that matches regardless of specificity.</span><span class="sxs-lookup"><span data-stu-id="94ff9-145">Rules are processed in the order they are listed, and traffic is directed using the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="94ff9-146">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span><span class="sxs-lookup"><span data-stu-id="94ff9-146">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 

<span data-ttu-id="94ff9-147">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span><span class="sxs-lookup"><span data-stu-id="94ff9-147">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span></span> <span data-ttu-id="94ff9-148">You can add the rule using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="94ff9-148">You can add the rule using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span></span>

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

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="94ff9-149">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="94ff9-149">Create virtual machine scale sets</span></span>

<span data-ttu-id="94ff9-150">In this example, you create three virtual machine scale sets that support the three backend pools in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="94ff9-150">In this example, you create three virtual machine scale sets that support the three backend pools in the application gateway.</span></span> <span data-ttu-id="94ff9-151">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="94ff9-151">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="94ff9-152">Each scale set contains two virtual machine instances on which you install IIS.</span><span class="sxs-lookup"><span data-stu-id="94ff9-152">Each scale set contains two virtual machine instances on which you install IIS.</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="94ff9-153">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="94ff9-153">Install NGINX</span></span>

```azurecli-interactive
for i in `seq 1 2`; do

  az vmss extension set \
    --publisher Microsoft.Azure.Extensions \
    --version 2.0 \
    --name CustomScript \
    --resource-group myResourceGroupAG \
    --vmss-name myvmss$i \
    --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],
  "commandToExecute": "./install_nginx.sh" }'

done
```

## <a name="create-a-cname-record-in-your-domain"></a><span data-ttu-id="94ff9-154">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="94ff9-154">Create a CNAME record in your domain</span></span>

<span data-ttu-id="94ff9-155">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="94ff9-155">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="94ff9-156">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="94ff9-156">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span></span> <span data-ttu-id="94ff9-157">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span><span class="sxs-lookup"><span data-stu-id="94ff9-157">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span></span> 

```azurecli-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [dnsSettings.fqdn] \
  --output tsv
```

<span data-ttu-id="94ff9-158">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="94ff9-158">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="94ff9-159">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="94ff9-159">Test the application gateway</span></span>

<span data-ttu-id="94ff9-160">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="94ff9-160">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="94ff9-161">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="94ff9-161">Such as, http://www.contoso.com.</span></span>

![Test contoso site in application gateway](./media/tutorial-multiple-sites-cli/application-gateway-nginxtest1.png)

<span data-ttu-id="94ff9-163">Change the address to your other domain and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="94ff9-163">Change the address to your other domain and you should see something like the following example:</span></span>

![Test fabrikam site in application gateway](./media/tutorial-multiple-sites-cli/application-gateway-nginxtest2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="94ff9-165">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="94ff9-165">Clean up resources</span></span>

<span data-ttu-id="94ff9-166">When no longer needed, remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="94ff9-166">When no longer needed, remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroupAG --location eastus
```

## <a name="next-steps"></a><span data-ttu-id="94ff9-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="94ff9-167">Next steps</span></span>

<span data-ttu-id="94ff9-168">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="94ff9-168">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94ff9-169">Set up the network</span><span class="sxs-lookup"><span data-stu-id="94ff9-169">Set up the network</span></span>
> * <span data-ttu-id="94ff9-170">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="94ff9-170">Create an application gateway</span></span>
> * <span data-ttu-id="94ff9-171">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="94ff9-171">Create backend listeners</span></span>
> * <span data-ttu-id="94ff9-172">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="94ff9-172">Create routing rules</span></span>
> * <span data-ttu-id="94ff9-173">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="94ff9-173">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="94ff9-174">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="94ff9-174">Create a CNAME record in your domain</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94ff9-175">Create an application gateway with URL path-based routing rules</span><span class="sxs-lookup"><span data-stu-id="94ff9-175">Create an application gateway with URL path-based routing rules</span></span>](./tutorial-url-route-cli.md)