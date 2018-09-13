---
title: Create an application gateway with internal redirection - Azure CLI | Microsoft Docs
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
ms.date: 7/14/2018
ms.author: victorh
ms.openlocfilehash: 1fee9e511b251648adb412fe3e4ca01c20c7edc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869696"
---
# <a name="create-an-application-gateway-with-internal-redirection-using-the-azure-cli"></a><span data-ttu-id="9abcd-103">Create an application gateway with internal redirection using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9abcd-103">Create an application gateway with internal redirection using the Azure CLI</span></span>

<span data-ttu-id="9abcd-104">You can use the Azure CLI to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9abcd-104">You can use the Azure CLI to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="9abcd-105">In this tutorial, you create a backend pool using a virtual machines scale set.</span><span class="sxs-lookup"><span data-stu-id="9abcd-105">In this tutorial, you create a backend pool using a virtual machines scale set.</span></span> <span data-ttu-id="9abcd-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate pool.</span><span class="sxs-lookup"><span data-stu-id="9abcd-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate pool.</span></span> <span data-ttu-id="9abcd-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.contoso.org*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.contoso.org*.</span></span>

<span data-ttu-id="9abcd-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="9abcd-108">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9abcd-109">Set up the network</span><span class="sxs-lookup"><span data-stu-id="9abcd-109">Set up the network</span></span>
> * <span data-ttu-id="9abcd-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="9abcd-110">Create an application gateway</span></span>
> * <span data-ttu-id="9abcd-111">Add listeners and redirection rule</span><span class="sxs-lookup"><span data-stu-id="9abcd-111">Add listeners and redirection rule</span></span>
> * <span data-ttu-id="9abcd-112">Create a virtual machine scale set with the backend pool</span><span class="sxs-lookup"><span data-stu-id="9abcd-112">Create a virtual machine scale set with the backend pool</span></span>
> * <span data-ttu-id="9abcd-113">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="9abcd-113">Create a CNAME record in your domain</span></span>

<span data-ttu-id="9abcd-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9abcd-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9abcd-115">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="9abcd-115">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9abcd-116">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9abcd-116">To find the version, run `az --version`.</span></span> <span data-ttu-id="9abcd-117">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9abcd-117">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="9abcd-118">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="9abcd-118">Create a resource group</span></span>

<span data-ttu-id="9abcd-119">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="9abcd-119">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="9abcd-120">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-120">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="9abcd-121">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="9abcd-121">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="9abcd-122">Create network resources</span><span class="sxs-lookup"><span data-stu-id="9abcd-122">Create network resources</span></span> 

<span data-ttu-id="9abcd-123">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="9abcd-123">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="9abcd-124">You can then add the subnet named *myBackendSubnet* that's needed by the backend pool of servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-124">You can then add the subnet named *myBackendSubnet* that's needed by the backend pool of servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="9abcd-125">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-125">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway"></a><span data-ttu-id="9abcd-126">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="9abcd-126">Create the application gateway</span></span>

<span data-ttu-id="9abcd-127">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-127">You can use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="9abcd-128">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="9abcd-128">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="9abcd-129">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="9abcd-129">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> 

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

<span data-ttu-id="9abcd-130">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="9abcd-130">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="9abcd-131">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="9abcd-131">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="9abcd-132">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="9abcd-132">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="9abcd-133">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="9abcd-133">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="9abcd-134">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-134">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="9abcd-135">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-135">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="9abcd-136">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-136">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>


## <a name="add-listeners-and-rules"></a><span data-ttu-id="9abcd-137">Add listeners and rules</span><span class="sxs-lookup"><span data-stu-id="9abcd-137">Add listeners and rules</span></span> 

<span data-ttu-id="9abcd-138">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="9abcd-138">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="9abcd-139">In this tutorial, you create two listeners for your two domains.</span><span class="sxs-lookup"><span data-stu-id="9abcd-139">In this tutorial, you create two listeners for your two domains.</span></span> <span data-ttu-id="9abcd-140">In this example, listeners are created for the domains of *www.contoso.com* and *www.contoso.org*.</span><span class="sxs-lookup"><span data-stu-id="9abcd-140">In this example, listeners are created for the domains of *www.contoso.com* and *www.contoso.org*.</span></span>

<span data-ttu-id="9abcd-141">Add the backend listeners that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-141">Add the backend listeners that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span></span>

```azurecli-interactive
az network application-gateway http-listener create \
  --name contosoComListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.contoso.com
az network application-gateway http-listener create \
  --name contosoOrgListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.contoso.org   
  ```

### <a name="add-the-redirection-configuration"></a><span data-ttu-id="9abcd-142">Add the redirection configuration</span><span class="sxs-lookup"><span data-stu-id="9abcd-142">Add the redirection configuration</span></span>

<span data-ttu-id="9abcd-143">Add the redirection configuration that sends traffic from *www.consoto.org* to the listener for *www.contoso.com* in the application gateway using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-143">Add the redirection configuration that sends traffic from *www.consoto.org* to the listener for *www.contoso.com* in the application gateway using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span></span>

```azurecli-interactive
az network application-gateway redirect-config create \
  --name orgToCom \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --type Permanent \
  --target-listener contosoComListener \
  --include-path true \
  --include-query-string true
```

### <a name="add-routing-rules"></a><span data-ttu-id="9abcd-144">Add routing rules</span><span class="sxs-lookup"><span data-stu-id="9abcd-144">Add routing rules</span></span>

<span data-ttu-id="9abcd-145">Rules are processed in the order in which they are created, and traffic is directed using the first rule that matches the URL sent to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9abcd-145">Rules are processed in the order in which they are created, and traffic is directed using the first rule that matches the URL sent to the application gateway.</span></span> <span data-ttu-id="9abcd-146">The default basic rule that was created is not needed in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9abcd-146">The default basic rule that was created is not needed in this tutorial.</span></span> <span data-ttu-id="9abcd-147">In this example, you create two new rules named *contosoComRule* and *contosoOrgRule* and delete the default rule that was created.</span><span class="sxs-lookup"><span data-stu-id="9abcd-147">In this example, you create two new rules named *contosoComRule* and *contosoOrgRule* and delete the default rule that was created.</span></span>  <span data-ttu-id="9abcd-148">You can add the rules using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="9abcd-148">You can add the rules using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span></span>

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name contosoComRule \
  --resource-group myResourceGroupAG \
  --http-listener contosoComListener \
  --rule-type Basic \
  --address-pool appGatewayBackendPool
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name contosoOrgRule \
  --resource-group myResourceGroupAG \
  --http-listener contosoOrgListener \
  --rule-type Basic \
  --redirect-config orgToCom
az network application-gateway rule delete \
  --gateway-name myAppGateway \
  --name rule1 \
  --resource-group myResourceGroupAG
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="9abcd-149">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="9abcd-149">Create virtual machine scale sets</span></span>

<span data-ttu-id="9abcd-150">In this example, you create a virtual machine scale set that supports the default backend pool that was created.</span><span class="sxs-lookup"><span data-stu-id="9abcd-150">In this example, you create a virtual machine scale set that supports the default backend pool that was created.</span></span> <span data-ttu-id="9abcd-151">The scale set that you create is named *myvmss* and contains two virtual machine instances on which you install NGINX.</span><span class="sxs-lookup"><span data-stu-id="9abcd-151">The scale set that you create is named *myvmss* and contains two virtual machine instances on which you install NGINX.</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="9abcd-152">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="9abcd-152">Install NGINX</span></span>

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

## <a name="create-cname-record-in-your-domain"></a><span data-ttu-id="9abcd-153">Create CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="9abcd-153">Create CNAME record in your domain</span></span>

<span data-ttu-id="9abcd-154">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="9abcd-154">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="9abcd-155">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9abcd-155">You can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show) to get the DNS address of the application gateway.</span></span> <span data-ttu-id="9abcd-156">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span><span class="sxs-lookup"><span data-stu-id="9abcd-156">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span></span> <span data-ttu-id="9abcd-157">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="9abcd-157">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

```azurecli-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [dnsSettings.fqdn] \
  --output tsv
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="9abcd-158">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="9abcd-158">Test the application gateway</span></span>

<span data-ttu-id="9abcd-159">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="9abcd-159">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="9abcd-160">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9abcd-160">Such as, http://www.contoso.com.</span></span>

![Test contoso site in application gateway](./media/tutorial-internal-site-redirect-cli/application-gateway-nginxtest.png)

<span data-ttu-id="9abcd-162">Change the address to your other domain, for example http://www.contoso.org and you should see that the traffic has been redirected back to the listener for www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9abcd-162">Change the address to your other domain, for example http://www.contoso.org and you should see that the traffic has been redirected back to the listener for www.contoso.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abcd-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="9abcd-163">Next steps</span></span>

<span data-ttu-id="9abcd-164">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="9abcd-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9abcd-165">Set up the network</span><span class="sxs-lookup"><span data-stu-id="9abcd-165">Set up the network</span></span>
> * <span data-ttu-id="9abcd-166">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="9abcd-166">Create an application gateway</span></span>
> * <span data-ttu-id="9abcd-167">Add listeners and redirection rule</span><span class="sxs-lookup"><span data-stu-id="9abcd-167">Add listeners and redirection rule</span></span>
> * <span data-ttu-id="9abcd-168">Create a virtual machine scale set with the backend pool</span><span class="sxs-lookup"><span data-stu-id="9abcd-168">Create a virtual machine scale set with the backend pool</span></span>
> * <span data-ttu-id="9abcd-169">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="9abcd-169">Create a CNAME record in your domain</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9abcd-170">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="9abcd-170">Learn more about what you can do with application gateway</span></span>](./application-gateway-introduction.md)