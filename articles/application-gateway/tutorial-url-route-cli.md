---
title: Tutorial - Route web traffic based on the URL - Azure CLI
description: Learn how to route web traffic based on the URL to specific scalable pools of servers using the Azure CLI.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 7a0eb5a979972a5e6c0ab1c29c2353b1016cfacb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870853"
---
# <a name="tutorial-route-web-traffic-based-on-the-url-using-the-azure-cli"></a><span data-ttu-id="5a328-103">Tutorial: Route web traffic based on the URL using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a328-103">Tutorial: Route web traffic based on the URL using the Azure CLI</span></span>

<span data-ttu-id="5a328-104">You can use Azure CLI to configure web traffic routing to specific scalable server pools based on the URL that is used to access your application.</span><span class="sxs-lookup"><span data-stu-id="5a328-104">You can use Azure CLI to configure web traffic routing to specific scalable server pools based on the URL that is used to access your application.</span></span> <span data-ttu-id="5a328-105">In this tutorial, you create an [Azure Application Gateway](application-gateway-introduction.md) with three backend pools using [Virtual Machine Scale Sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a328-105">In this tutorial, you create an [Azure Application Gateway](application-gateway-introduction.md) with three backend pools using [Virtual Machine Scale Sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span> <span data-ttu-id="5a328-106">Each of the backend pools serves a specific purpose such as, common data, images, and video.</span><span class="sxs-lookup"><span data-stu-id="5a328-106">Each of the backend pools serves a specific purpose such as, common data, images, and video.</span></span>  <span data-ttu-id="5a328-107">Routing traffic to separate pools ensures that your customers get the information that they need when they need it.</span><span class="sxs-lookup"><span data-stu-id="5a328-107">Routing traffic to separate pools ensures that your customers get the information that they need when they need it.</span></span>

<span data-ttu-id="5a328-108">To enable traffic routing, you create [routing rules](application-gateway-url-route-overview.md) assigned to listeners that listen on specific ports to ensure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="5a328-108">To enable traffic routing, you create [routing rules](application-gateway-url-route-overview.md) assigned to listeners that listen on specific ports to ensure web traffic arrives at the appropriate servers in the pools.</span></span>

<span data-ttu-id="5a328-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="5a328-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a328-110">Set up the network</span><span class="sxs-lookup"><span data-stu-id="5a328-110">Set up the network</span></span>
> * <span data-ttu-id="5a328-111">Create listeners, URL path map, and rules</span><span class="sxs-lookup"><span data-stu-id="5a328-111">Create listeners, URL path map, and rules</span></span>
> * <span data-ttu-id="5a328-112">Create scalable backend pools</span><span class="sxs-lookup"><span data-stu-id="5a328-112">Create scalable backend pools</span></span>


![URL routing example](./media/tutorial-url-route-cli/scenario.png)

<span data-ttu-id="5a328-114">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-url-route-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a328-114">If you prefer, you can complete this tutorial using [Azure PowerShell](tutorial-url-route-powershell.md).</span></span>

<span data-ttu-id="5a328-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="5a328-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5a328-116">If you choose to install and use the CLI locally, this tutorial requires you to run the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="5a328-116">If you choose to install and use the CLI locally, this tutorial requires you to run the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5a328-117">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5a328-117">To find the version, run `az --version`.</span></span> <span data-ttu-id="5a328-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5a328-118">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="5a328-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="5a328-119">Create a resource group</span></span>

<span data-ttu-id="5a328-120">A resource group is a logical container where Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="5a328-120">A resource group is a logical container where Azure resources are deployed and managed.</span></span> <span data-ttu-id="5a328-121">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5a328-121">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="5a328-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="5a328-122">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="5a328-123">Create network resources</span><span class="sxs-lookup"><span data-stu-id="5a328-123">Create network resources</span></span> 

<span data-ttu-id="5a328-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="5a328-124">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="5a328-125">Then add a subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-125">Then add a subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="5a328-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-126">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway-with-url-map"></a><span data-ttu-id="5a328-127">Create the application gateway with URL map</span><span class="sxs-lookup"><span data-stu-id="5a328-127">Create the application gateway with URL map</span></span>

<span data-ttu-id="5a328-128">Use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create an application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="5a328-128">Use [az network application-gateway create](/cli/azure/network/application-gateway#create) to create an application gateway named *myAppGateway*.</span></span> <span data-ttu-id="5a328-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="5a328-129">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> <span data-ttu-id="5a328-130">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="5a328-130">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> 

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

 <span data-ttu-id="5a328-131">It may take several minutes to create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="5a328-131">It may take several minutes to create the application gateway.</span></span> <span data-ttu-id="5a328-132">After the application gateway is created, you can see these new features:</span><span class="sxs-lookup"><span data-stu-id="5a328-132">After the application gateway is created, you can see these new features:</span></span>

- <span data-ttu-id="5a328-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="5a328-133">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="5a328-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="5a328-134">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="5a328-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="5a328-135">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="5a328-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="5a328-136">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="5a328-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="5a328-137">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>


### <a name="add-image-and-video-backend-pools-and-port"></a><span data-ttu-id="5a328-138">Add image and video backend pools and port</span><span class="sxs-lookup"><span data-stu-id="5a328-138">Add image and video backend pools and port</span></span>

<span data-ttu-id="5a328-139">Add backend pools named *imagesBackendPool* and *videoBackendPool* to your application gateway by using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address-pool_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-139">Add backend pools named *imagesBackendPool* and *videoBackendPool* to your application gateway by using [az network application-gateway address-pool create](/cli/azure/network/application-gateway#az-network_application_gateway_address-pool_create).</span></span> <span data-ttu-id="5a328-140">You add the frontend port for the pools using [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-140">You add the frontend port for the pools using [az network application-gateway frontend-port create](/cli/azure/network/application-gateway#az-network_application_gateway_frontend_port_create).</span></span> 

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
  --name port8080
```

### <a name="add-backend-listener"></a><span data-ttu-id="5a328-141">Add backend listener</span><span class="sxs-lookup"><span data-stu-id="5a328-141">Add backend listener</span></span>

<span data-ttu-id="5a328-142">Add the backend listener named *backendListener* that's needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-142">Add the backend listener named *backendListener* that's needed to route traffic using [az network application-gateway http-listener create](/cli/azure/network/application-gateway#az-network_application_gateway_http_listener_create).</span></span>


```azurecli-interactive
az network application-gateway http-listener create \
  --name backendListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port port8080 \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway
```

### <a name="add-url-path-map"></a><span data-ttu-id="5a328-143">Add URL path map</span><span class="sxs-lookup"><span data-stu-id="5a328-143">Add URL path map</span></span>

<span data-ttu-id="5a328-144">URL path maps ensure that specific URLs are routed to specific backend pools.</span><span class="sxs-lookup"><span data-stu-id="5a328-144">URL path maps ensure that specific URLs are routed to specific backend pools.</span></span> <span data-ttu-id="5a328-145">Create URL path maps named *imagePathRule* and *videoPathRule* using [az network application-gateway url-path-map create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_create) and [az network application-gateway url-path-map rule create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_rule_create)</span><span class="sxs-lookup"><span data-stu-id="5a328-145">Create URL path maps named *imagePathRule* and *videoPathRule* using [az network application-gateway url-path-map create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_create) and [az network application-gateway url-path-map rule create](/cli/azure/network/application-gateway#az-network_application_gateway_url_path_map_rule_create)</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
  --gateway-name myAppGateway \
  --name myPathMap \
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
  --path-map-name myPathMap \
  --paths /video/* \
  --address-pool videoBackendPool
```

### <a name="add-routing-rule"></a><span data-ttu-id="5a328-146">Add routing rule</span><span class="sxs-lookup"><span data-stu-id="5a328-146">Add routing rule</span></span>

<span data-ttu-id="5a328-147">The routing rule associates the URL maps with the listener that you created.</span><span class="sxs-lookup"><span data-stu-id="5a328-147">The routing rule associates the URL maps with the listener that you created.</span></span> <span data-ttu-id="5a328-148">Add a rule named *rule2* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="5a328-148">Add a rule named *rule2* using [az network application-gateway rule create](/cli/azure/network/application-gateway#az-network_application_gateway_rule_create).</span></span>

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name rule2 \
  --resource-group myResourceGroupAG \
  --http-listener backendListener \
  --rule-type PathBasedRouting \
  --url-path-map myPathMap \
  --address-pool appGatewayBackendPool
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="5a328-149">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="5a328-149">Create virtual machine scale sets</span></span>

<span data-ttu-id="5a328-150">In this tutorial, you create three virtual machine scale sets that support the three backend pools you created.</span><span class="sxs-lookup"><span data-stu-id="5a328-150">In this tutorial, you create three virtual machine scale sets that support the three backend pools you created.</span></span> <span data-ttu-id="5a328-151">You create scale sets named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="5a328-151">You create scale sets named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="5a328-152">Each scale set contains two virtual machine instances where you install NGINX.</span><span class="sxs-lookup"><span data-stu-id="5a328-152">Each scale set contains two virtual machine instances where you install NGINX.</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="5a328-153">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="5a328-153">Install NGINX</span></span>

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

## <a name="test-the-application-gateway"></a><span data-ttu-id="5a328-154">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="5a328-154">Test the application gateway</span></span>

<span data-ttu-id="5a328-155">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="5a328-155">To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="5a328-156">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="5a328-156">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="5a328-157">Such as, *http://40.121.222.19*, *http://40.121.222.19:8080/images/test.htm*, or *http://40.121.222.19:8080/video/test.htm*.</span><span class="sxs-lookup"><span data-stu-id="5a328-157">Such as, *http://40.121.222.19*, *http://40.121.222.19:8080/images/test.htm*, or *http://40.121.222.19:8080/video/test.htm*.</span></span>

```azurecli-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Test base URL in application gateway](./media/tutorial-url-route-cli/application-gateway-nginx.png)

<span data-ttu-id="5a328-159">Change the URL to http://&lt;ip-address&gt;:8080/images/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="5a328-159">Change the URL to http://&lt;ip-address&gt;:8080/images/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test images URL in application gateway](./media/tutorial-url-route-cli/application-gateway-nginx-images.png)

<span data-ttu-id="5a328-161">Change the URL to http://&lt;ip-address&gt;:8080/video/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example.</span><span class="sxs-lookup"><span data-stu-id="5a328-161">Change the URL to http://&lt;ip-address&gt;:8080/video/test.html, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example.</span></span>

![Test video URL in application gateway](./media/tutorial-url-route-cli/application-gateway-nginx-video.png)

## <a name="clean-up-resources"></a><span data-ttu-id="5a328-163">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="5a328-163">Clean up resources</span></span>

<span data-ttu-id="5a328-164">When no longer needed, remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5a328-164">When no longer needed, remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroupAG --location eastus
```

## <a name="next-steps"></a><span data-ttu-id="5a328-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a328-165">Next steps</span></span>

<span data-ttu-id="5a328-166">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="5a328-166">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a328-167">Set up the network</span><span class="sxs-lookup"><span data-stu-id="5a328-167">Set up the network</span></span>
> * <span data-ttu-id="5a328-168">Create listeners, URL path map, and rules</span><span class="sxs-lookup"><span data-stu-id="5a328-168">Create listeners, URL path map, and rules</span></span>
> * <span data-ttu-id="5a328-169">Create scalable backend pools</span><span class="sxs-lookup"><span data-stu-id="5a328-169">Create scalable backend pools</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a328-170">Create an application gateway with URL path-based redirection</span><span class="sxs-lookup"><span data-stu-id="5a328-170">Create an application gateway with URL path-based redirection</span></span>](./tutorial-url-redirect-cli.md)
