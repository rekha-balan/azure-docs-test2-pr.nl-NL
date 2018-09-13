---
title: Enable web application firewall - Azure CLI
description: Learn how to restrict web traffic with a web application firewall on an application gateway using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 20a15f5062780e0a9fb687b5f35bb214d16119f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868859"
---
# <a name="tutorial-enable-web-application-firewall-using-the-azure-cli"></a><span data-ttu-id="d5166-103">Tutorial: Enable web application firewall using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5166-103">Tutorial: Enable web application firewall using the Azure CLI</span></span>

<span data-ttu-id="d5166-104">You can restrict traffic on an [application gateway](overview.md) with a [web application firewall](waf-overview.md) (WAF).</span><span class="sxs-lookup"><span data-stu-id="d5166-104">You can restrict traffic on an [application gateway](overview.md) with a [web application firewall](waf-overview.md) (WAF).</span></span> <span data-ttu-id="d5166-105">The WAF uses [OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) rules to protect your application.</span><span class="sxs-lookup"><span data-stu-id="d5166-105">The WAF uses [OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) rules to protect your application.</span></span> <span data-ttu-id="d5166-106">These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.</span><span class="sxs-lookup"><span data-stu-id="d5166-106">These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.</span></span> 

<span data-ttu-id="d5166-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="d5166-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5166-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="d5166-108">Set up the network</span></span>
> * <span data-ttu-id="d5166-109">Create an application gateway with WAF enabled</span><span class="sxs-lookup"><span data-stu-id="d5166-109">Create an application gateway with WAF enabled</span></span>
> * <span data-ttu-id="d5166-110">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="d5166-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="d5166-111">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="d5166-111">Create a storage account and configure diagnostics</span></span>

![Web application firewall example](./media/tutorial-restrict-web-traffic-cli/scenario-waf.png)

<span data-ttu-id="d5166-113">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-restrict-web-traffic-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5166-113">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-restrict-web-traffic-powershell.md).</span></span>

<span data-ttu-id="d5166-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d5166-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d5166-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="d5166-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d5166-116">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d5166-116">To find the version, run `az --version`.</span></span> <span data-ttu-id="d5166-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d5166-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d5166-118">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="d5166-118">Create a resource group</span></span>

<span data-ttu-id="d5166-119">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="d5166-119">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="d5166-120">Create an Azure resource group named *myResourceGroupAG* with [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-120">Create an Azure resource group named *myResourceGroupAG* with [az group create](/cli/azure/group#az-group-create).</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="d5166-121">Create network resources</span><span class="sxs-lookup"><span data-stu-id="d5166-121">Create network resources</span></span>

<span data-ttu-id="d5166-122">The virtual network and subnets are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="d5166-122">The virtual network and subnets are used to provide network connectivity to the application gateway and its associated resources.</span></span> <span data-ttu-id="d5166-123">Create the virtual network named *myVNet* and subnet named *myAGSubnet* with [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create) and [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-123">Create the virtual network named *myVNet* and subnet named *myAGSubnet* with [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create) and [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create).</span></span> <span data-ttu-id="d5166-124">Create a public IP address named *myAGPublicIPAddress* with [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-124">Create a public IP address named *myAGPublicIPAddress* with [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create).</span></span>

```azurecli-interactive
az network vnet create \
  --name myVNet \
  --resource-group myResourceGroupAG \
  --location eastus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name myBackendSubnet \
  --subnet-prefix 10.0.1.0/24

az network vnet subnet create \
  --name myAGSubnet \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --address-prefix 10.0.2.0/24

az network public-ip create \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress
```

## <a name="create-an-application-gateway-with-a-waf"></a><span data-ttu-id="d5166-125">Create an application gateway with a WAF</span><span class="sxs-lookup"><span data-stu-id="d5166-125">Create an application gateway with a WAF</span></span>

<span data-ttu-id="d5166-126">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="d5166-126">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-application-gateway-create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="d5166-127">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="d5166-127">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="d5166-128">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="d5166-128">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span></span>

```azurecli-interactive
az network application-gateway create \
  --name myAppGateway \
  --location eastus \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --subnet myAGSubnet \
  --capacity 2 \
  --sku WAF_Medium \
  --http-settings-cookie-based-affinity Disabled \
  --frontend-port 80 \
  --http-settings-port 80 \
  --http-settings-protocol Http \
  --public-ip-address myAGPublicIPAddress

az network application-gateway waf-config set \
  --enabled true \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --firewall-mode Detection \
  --rule-set-version 3.0
```

<span data-ttu-id="d5166-129">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="d5166-129">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="d5166-130">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="d5166-130">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="d5166-131">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="d5166-131">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="d5166-132">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="d5166-132">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="d5166-133">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="d5166-133">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="d5166-134">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="d5166-134">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="d5166-135">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="d5166-135">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="d5166-136">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="d5166-136">Create a virtual machine scale set</span></span>

<span data-ttu-id="d5166-137">In this example, you create a virtual machine scale set that provides two servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="d5166-137">In this example, you create a virtual machine scale set that provides two servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="d5166-138">The virtual machines in the scale set are associated with the *myBackendSubnet* subnet.</span><span class="sxs-lookup"><span data-stu-id="d5166-138">The virtual machines in the scale set are associated with the *myBackendSubnet* subnet.</span></span> <span data-ttu-id="d5166-139">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-139">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="d5166-140">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="d5166-140">Install NGINX</span></span>

```azurecli-interactive
az vmss extension set \
  --publisher Microsoft.Azure.Extensions \
  --version 2.0 \
  --name CustomScript \
  --resource-group myResourceGroupAG \
  --vmss-name myvmss \
  --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],"commandToExecute": "./install_nginx.sh" }'
```

## <a name="create-a-storage-account-and-configure-diagnostics"></a><span data-ttu-id="d5166-141">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="d5166-141">Create a storage account and configure diagnostics</span></span>

<span data-ttu-id="d5166-142">In this tutorial, the application gateway uses a storage account to store data for detection and prevention purposes.</span><span class="sxs-lookup"><span data-stu-id="d5166-142">In this tutorial, the application gateway uses a storage account to store data for detection and prevention purposes.</span></span> <span data-ttu-id="d5166-143">You could also use Log Analytics or Event Hub to record data.</span><span class="sxs-lookup"><span data-stu-id="d5166-143">You could also use Log Analytics or Event Hub to record data.</span></span> 

### <a name="create-a-storage-account"></a><span data-ttu-id="d5166-144">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="d5166-144">Create a storage account</span></span>

<span data-ttu-id="d5166-145">Create a storage account named *myagstore1* with [az storage account create](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-145">Create a storage account named *myagstore1* with [az storage account create](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create).</span></span>

```azurecli-interactive
az storage account create \
  --name myagstore1 \
  --resource-group myResourceGroupAG \
  --location eastus \
  --sku Standard_LRS \
  --encryption blob
```

### <a name="configure-diagnostics"></a><span data-ttu-id="d5166-146">Configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="d5166-146">Configure diagnostics</span></span>

<span data-ttu-id="d5166-147">Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs.</span><span class="sxs-lookup"><span data-stu-id="d5166-147">Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs.</span></span> <span data-ttu-id="d5166-148">Substitute `<subscriptionId>` with your subscription identifier and then configure diagnostics with [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings?view=azure-cli-latest#az-monitor-diagnostic-settings-create).</span><span class="sxs-lookup"><span data-stu-id="d5166-148">Substitute `<subscriptionId>` with your subscription identifier and then configure diagnostics with [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings?view=azure-cli-latest#az-monitor-diagnostic-settings-create).</span></span>

```azurecli-interactive
appgwid=$(az network application-gateway show --name myAppGateway --resource-group myResourceGroupAG --query id -o tsv)

storeid=$(az storage account show --name myagstore1 --resource-group myResourceGroupAG --query id -o tsv)

az monitor diagnostic-settings create --name appgwdiag --resource $appgwid \
  --logs '[ { "category": "ApplicationGatewayAccessLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } }, { "category": "ApplicationGatewayPerformanceLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } }, { "category": "ApplicationGatewayFirewallLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } } ]' \
  --storage-account $storeid
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="d5166-149">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="d5166-149">Test the application gateway</span></span>

<span data-ttu-id="d5166-150">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="d5166-150">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> <span data-ttu-id="d5166-151">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="d5166-151">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Test base URL in application gateway](./media/tutorial-restrict-web-traffic-cli/application-gateway-nginxtest.png)

## <a name="clean-up-resources"></a><span data-ttu-id="d5166-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d5166-153">Clean up resources</span></span>

<span data-ttu-id="d5166-154">When no longer needed, remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d5166-154">When no longer needed, remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroupAG --location eastus
```

## <a name="next-steps"></a><span data-ttu-id="d5166-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5166-155">Next steps</span></span>

<span data-ttu-id="d5166-156">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="d5166-156">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5166-157">Set up the network</span><span class="sxs-lookup"><span data-stu-id="d5166-157">Set up the network</span></span>
> * <span data-ttu-id="d5166-158">Create an application gateway with WAF enabled</span><span class="sxs-lookup"><span data-stu-id="d5166-158">Create an application gateway with WAF enabled</span></span>
> * <span data-ttu-id="d5166-159">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="d5166-159">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="d5166-160">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="d5166-160">Create a storage account and configure diagnostics</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5166-161">Create an application gateway with SSL termination</span><span class="sxs-lookup"><span data-stu-id="d5166-161">Create an application gateway with SSL termination</span></span>](./tutorial-ssl-cli.md)