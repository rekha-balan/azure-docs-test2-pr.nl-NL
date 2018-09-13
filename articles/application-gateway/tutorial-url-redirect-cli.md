---
title: Create an application gateway with URL path-based redirection - Azure CLI
description: Learn how to create an application gateway with URL path-based redirected traffic using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: c9797c57c7820213f601bdb056471d43637d5b09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857723"
---
# <a name="tutorial-create-an-application-gateway-with-url-path-based-redirection-using-the-azure-cli"></a><span data-ttu-id="557e6-103">Tutorial: Create an application gateway with URL path-based redirection using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="557e6-103">Tutorial: Create an application gateway with URL path-based redirection using the Azure CLI</span></span>

<span data-ttu-id="557e6-104">You can use the Azure CLI to configure [URL path-based routing rules](application-gateway-url-route-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="557e6-104">You can use the Azure CLI to configure [URL path-based routing rules](application-gateway-url-route-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="557e6-105">In this tutorial, you create backend pools using [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="557e6-105">In this tutorial, you create backend pools using [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span> <span data-ttu-id="557e6-106">You then create URL routing rules that make sure web traffic is redirected to the appropriate backend pool.</span><span class="sxs-lookup"><span data-stu-id="557e6-106">You then create URL routing rules that make sure web traffic is redirected to the appropriate backend pool.</span></span>

<span data-ttu-id="557e6-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="557e6-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="557e6-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="557e6-108">Set up the network</span></span>
> * <span data-ttu-id="557e6-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="557e6-109">Create an application gateway</span></span>
> * <span data-ttu-id="557e6-110">Add listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="557e6-110">Add listeners and routing rules</span></span>
> * <span data-ttu-id="557e6-111">Create virtual machine scale sets for backend pools</span><span class="sxs-lookup"><span data-stu-id="557e6-111">Create virtual machine scale sets for backend pools</span></span>

<span data-ttu-id="557e6-112">The following example shows site traffic coming from both ports 8080 and 8081 and being directed to the same backend pools:</span><span class="sxs-lookup"><span data-stu-id="557e6-112">The following example shows site traffic coming from both ports 8080 and 8081 and being directed to the same backend pools:</span></span>

![URL routing example](./media/tutorial-url-redirect-cli/scenario.png)

<span data-ttu-id="557e6-114">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-url-redirect-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="557e6-114">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-url-redirect-powershell.md).</span></span>

<span data-ttu-id="557e6-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="557e6-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="557e6-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="557e6-116">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="557e6-117">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="557e6-117">To find the version, run `az --version`.</span></span> <span data-ttu-id="557e6-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="557e6-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="557e6-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="557e6-119">Create a resource group</span></span>

<span data-ttu-id="557e6-120">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="557e6-120">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="557e6-121">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="557e6-121">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="557e6-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="557e6-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="557e6-123">Create network resources</span><span class="sxs-lookup"><span data-stu-id="557e6-123">Create network resources</span></span> 

<span data-ttu-id="557e6-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="557e6-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="557e6-125">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-125">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="557e6-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="557e6-127">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="557e6-127">Create an application gateway</span></span>

<span data-ttu-id="557e6-128">Use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named myAppGateway.</span><span class="sxs-lookup"><span data-stu-id="557e6-128">Use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create the application gateway named myAppGateway.</span></span> <span data-ttu-id="557e6-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="557e6-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="557e6-130">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="557e6-130">The application gateway is assigned to *myAGSubnet* and *myPublicIPSddress* that you previously created.</span></span>

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

 <span data-ttu-id="557e6-131">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="557e6-131">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="557e6-132">After the application gateway is created, you can see these new features:</span><span class="sxs-lookup"><span data-stu-id="557e6-132">After the application gateway is created, you can see these new features:</span></span>

- <span data-ttu-id="557e6-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="557e6-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="557e6-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="557e6-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="557e6-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="557e6-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="557e6-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="557e6-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="557e6-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="557e6-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>


### <a name="add-backend-pools-and-ports"></a><span data-ttu-id="557e6-138">Add backend pools and ports</span><span class="sxs-lookup"><span data-stu-id="557e6-138">Add backend pools and ports</span></span>

<span data-ttu-id="557e6-139">You can add backend address pools named *imagesBackendPool* and *videoBackendPool* to your application gateway by using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address-pool_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-139">You can add backend address pools named *imagesBackendPool* and *videoBackendPool* to your application gateway by using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address-pool_create).</span></span> <span data-ttu-id="557e6-140">You add the frontend ports for the pools using [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-140">You add the frontend ports for the pools using [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span></span> 

```azurecli-interactive
az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name imagesBackendPool

az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name videoBackendPool

az network application-gateway frontend-port create \
  --port 8080 \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name bport

az network application-gateway frontend-port create \
  --port 8081 \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name rport
```

## <a name="add-listeners-and-rules"></a><span data-ttu-id="557e6-141">Add listeners and rules</span><span class="sxs-lookup"><span data-stu-id="557e6-141">Add listeners and rules</span></span>

### <a name="add-listeners"></a><span data-ttu-id="557e6-142">Add listeners</span><span class="sxs-lookup"><span data-stu-id="557e6-142">Add listeners</span></span>

<span data-ttu-id="557e6-143">Add the backend listeners named *backendListener* and *redirectedListener* that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-143">Add the backend listeners named *backendListener* and *redirectedListener* that are needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span></span>


```azurecli-interactive
az network application-gateway http-listener create \
  --name backendListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port bport \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway

az network application-gateway http-listener create \
  --name redirectedListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port rport \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway
```

### <a name="add-the-default-url-path-map"></a><span data-ttu-id="557e6-144">Add the default URL path map</span><span class="sxs-lookup"><span data-stu-id="557e6-144">Add the default URL path map</span></span>

<span data-ttu-id="557e6-145">URL path maps make sure that specific URLs are routed to specific backend pools.</span><span class="sxs-lookup"><span data-stu-id="557e6-145">URL path maps make sure that specific URLs are routed to specific backend pools.</span></span> <span data-ttu-id="557e6-146">You can create URL path maps named *imagePathRule* and *videoPathRule* using [az network application-gateway url-path-map create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_create) and [az network application-gateway url-path-map rule create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_rule_create)</span><span class="sxs-lookup"><span data-stu-id="557e6-146">You can create URL path maps named *imagePathRule* and *videoPathRule* using [az network application-gateway url-path-map create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_create) and [az network application-gateway url-path-map rule create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_rule_create)</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
  --gateway-name myAppGateway \
  --name urlpathmap \
  --paths /images/* \
  --resource-group myResourceGroupAG \
  --address-pool imagesBackendPool \
  --default-address-pool appGatewayBackendPool \
  --default-http-settings appGatewayBackendHttpSettings \
  --http-settings appGatewayBackendHttpSettings \
  --rule-name imagePathRule

az network application-gateway url-path-map rule create \
  --gateway-name myAppGateway \
  --name videoPathRule \
  --resource-group myResourceGroupAG \
  --path-map-name urlpathmap \
  --paths /video/* \
  --address-pool videoBackendPool
```

### <a name="add-redirection-configuration"></a><span data-ttu-id="557e6-147">Add redirection configuration</span><span class="sxs-lookup"><span data-stu-id="557e6-147">Add redirection configuration</span></span>

<span data-ttu-id="557e6-148">You can configure redirection for the listener using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway#az-network_application_gateway_redirect_config_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-148">You can configure redirection for the listener using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway#az-network_application_gateway_redirect_config_create).</span></span>

```azurecli-interactive
az network application-gateway redirect-config create \
  --gateway-name myAppGateway \
  --name redirectConfig \
  --resource-group myResourceGroupAG \
  --type Found \
  --include-path true \
  --include-query-string true \
  --target-listener backendListener
```

### <a name="add-the-redirection-url-path-map"></a><span data-ttu-id="557e6-149">Add the redirection URL path map</span><span class="sxs-lookup"><span data-stu-id="557e6-149">Add the redirection URL path map</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
  --gateway-name myAppGateway \
  --name redirectpathmap \
  --paths /images/* \
  --resource-group myResourceGroupAG \
  --redirect-config redirectConfig \
  --rule-name redirectPathRule
```

### <a name="add-routing-rules"></a><span data-ttu-id="557e6-150">Add routing rules</span><span class="sxs-lookup"><span data-stu-id="557e6-150">Add routing rules</span></span>

<span data-ttu-id="557e6-151">The routing rules associate the URL path maps with the listeners that you created.</span><span class="sxs-lookup"><span data-stu-id="557e6-151">The routing rules associate the URL path maps with the listeners that you created.</span></span> <span data-ttu-id="557e6-152">You can add the rules named *defaultRule* and *redirectedRule* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="557e6-152">You can add the rules named *defaultRule* and *redirectedRule* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span></span>

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name defaultRule \
  --resource-group myResourceGroupAG \
  --http-listener backendListener \
  --rule-type PathBasedRouting \
  --url-path-map urlpathmap \
  --address-pool appGatewayBackendPool

az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name redirectedRule \
  --resource-group myResourceGroupAG \
  --http-listener redirectedListener \
  --rule-type PathBasedRouting \
  --url-path-map redirectpathmap \
  --address-pool appGatewayBackendPool
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="557e6-153">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="557e6-153">Create virtual machine scale sets</span></span>

<span data-ttu-id="557e6-154">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span><span class="sxs-lookup"><span data-stu-id="557e6-154">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span></span> <span data-ttu-id="557e6-155">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="557e6-155">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="557e6-156">Each scale set contains two virtual machine instances on which you install NGINX.</span><span class="sxs-lookup"><span data-stu-id="557e6-156">Each scale set contains two virtual machine instances on which you install NGINX.</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
  if [ $i -eq 1 ]
  then
    poolName="appGatewayBackendPool" 
  fi
  if [ $i -eq 2 ]
  then
    poolName="imagesBackendPool"
  fi
  if [ $i -eq 3 ]
  then
    poolName="videoBackendPool"
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

### <a name="install-nginx"></a><span data-ttu-id="557e6-157">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="557e6-157">Install NGINX</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
  az vmss extension set \
    --publisher Microsoft.Azure.Extensions \
    --version 2.0 \
    --name CustomScript \
    --resource-group myResourceGroupAG \
    --vmss-name myvmss$i \
    --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"], "commandToExecute": "./install_nginx.sh" }'

done
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="557e6-158">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="557e6-158">Test the application gateway</span></span>

<span data-ttu-id="557e6-159">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="557e6-159">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="557e6-160">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="557e6-160">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="557e6-161">Such as, *http://40.121.222.19*, *http://40.121.222.19:8080/images/test.htm*, *http://40.121.222.19:8080/video/test.htm*, or *http://40.121.222.19:8081/images/test.htm*.</span><span class="sxs-lookup"><span data-stu-id="557e6-161">Such as, *http://40.121.222.19*, *http://40.121.222.19:8080/images/test.htm*, *http://40.121.222.19:8080/video/test.htm*, or *http://40.121.222.19:8081/images/test.htm*.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Test base URL in application gateway](./media/tutorial-url-redirect-cli/application-gateway-nginx.png)

<span data-ttu-id="557e6-163">Change the URL to http://&lt;ip-address&gt;:8080/images/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="557e6-163">Change the URL to http://&lt;ip-address&gt;:8080/images/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test images URL in application gateway](./media/tutorial-url-redirect-cli/application-gateway-nginx-images.png)

<span data-ttu-id="557e6-165">Change the URL to http://&lt;ip-address&gt;:8080/video/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="557e6-165">Change the URL to http://&lt;ip-address&gt;:8080/video/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test video URL in application gateway](./media/tutorial-url-redirect-cli/application-gateway-nginx-video.png)

<span data-ttu-id="557e6-167">Now, change the URL to http://&lt;ip-address&gt;:8081/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see traffic redirected back to the images backend pool at http://&lt;ip-address&gt;:8080/images.</span><span class="sxs-lookup"><span data-stu-id="557e6-167">Now, change the URL to http://&lt;ip-address&gt;:8081/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see traffic redirected back to the images backend pool at http://&lt;ip-address&gt;:8080/images.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="557e6-168">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="557e6-168">Clean up resources</span></span>

<span data-ttu-id="557e6-169">When no longer needed, remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="557e6-169">When no longer needed, remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroupAG --location eastus
```
## <a name="next-steps"></a><span data-ttu-id="557e6-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="557e6-170">Next steps</span></span>

<span data-ttu-id="557e6-171">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="557e6-171">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="557e6-172">Set up the network</span><span class="sxs-lookup"><span data-stu-id="557e6-172">Set up the network</span></span>
> * <span data-ttu-id="557e6-173">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="557e6-173">Create an application gateway</span></span>
> * <span data-ttu-id="557e6-174">Add listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="557e6-174">Add listeners and routing rules</span></span>
> * <span data-ttu-id="557e6-175">Create virtual machine scale sets for backend pools</span><span class="sxs-lookup"><span data-stu-id="557e6-175">Create virtual machine scale sets for backend pools</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="557e6-176">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="557e6-176">Learn more about what you can do with application gateway</span></span>](application-gateway-introduction.md)