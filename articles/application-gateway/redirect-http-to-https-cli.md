---
title: Create an application gateway with a certificate - Azure CLI | Microsoft Docs
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
ms.openlocfilehash: c515ff9ab5f5b796be131c61cf1a53f2de45ed41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967425"
---
# <a name="create-an-application-gateway-with-http-to-https-redirection-using-the-azure-cli"></a><span data-ttu-id="a983a-103">Create an application gateway with HTTP to HTTPS redirection using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a983a-103">Create an application gateway with HTTP to HTTPS redirection using the Azure CLI</span></span>

<span data-ttu-id="a983a-104">You can use the Azure CLI to create an [application gateway](overview.md) with a certificate for SSL termination.</span><span class="sxs-lookup"><span data-stu-id="a983a-104">You can use the Azure CLI to create an [application gateway](overview.md) with a certificate for SSL termination.</span></span> <span data-ttu-id="a983a-105">A routing rule is used to redirect HTTP traffic to the HTTPS port in your application gateway.</span><span class="sxs-lookup"><span data-stu-id="a983a-105">A routing rule is used to redirect HTTP traffic to the HTTPS port in your application gateway.</span></span> <span data-ttu-id="a983a-106">In this example, you also create a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for the backend pool of the application gateway that contains two virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="a983a-106">In this example, you also create a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for the backend pool of the application gateway that contains two virtual machine instances.</span></span>

<span data-ttu-id="a983a-107">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a983a-107">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a983a-108">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a983a-108">Create a self-signed certificate</span></span>
> * <span data-ttu-id="a983a-109">Set up a network</span><span class="sxs-lookup"><span data-stu-id="a983a-109">Set up a network</span></span>
> * <span data-ttu-id="a983a-110">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="a983a-110">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="a983a-111">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="a983a-111">Add a listener and redirection rule</span></span>
> * <span data-ttu-id="a983a-112">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="a983a-112">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="a983a-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a983a-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a983a-114">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="a983a-114">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a983a-115">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="a983a-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="a983a-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a983a-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="a983a-117">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a983a-117">Create a self-signed certificate</span></span>

<span data-ttu-id="a983a-118">For production use, you should import a valid certificate signed by a trusted provider.</span><span class="sxs-lookup"><span data-stu-id="a983a-118">For production use, you should import a valid certificate signed by a trusted provider.</span></span> <span data-ttu-id="a983a-119">For this tutorial, you create a self-signed certificate and pfx file using the openssl command.</span><span class="sxs-lookup"><span data-stu-id="a983a-119">For this tutorial, you create a self-signed certificate and pfx file using the openssl command.</span></span>

```azurecli-interactive
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out appgwcert.crt
```

<span data-ttu-id="a983a-120">Enter values that make sense for your certificate.</span><span class="sxs-lookup"><span data-stu-id="a983a-120">Enter values that make sense for your certificate.</span></span> <span data-ttu-id="a983a-121">You can accept the default values.</span><span class="sxs-lookup"><span data-stu-id="a983a-121">You can accept the default values.</span></span>

```azurecli-interactive
openssl pkcs12 -export -out appgwcert.pfx -inkey privateKey.key -in appgwcert.crt
```

<span data-ttu-id="a983a-122">Enter the password for the certificate.</span><span class="sxs-lookup"><span data-stu-id="a983a-122">Enter the password for the certificate.</span></span> <span data-ttu-id="a983a-123">In this example, *Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="a983a-123">In this example, *Azure123456!*</span></span> <span data-ttu-id="a983a-124">is being used.</span><span class="sxs-lookup"><span data-stu-id="a983a-124">is being used.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="a983a-125">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="a983a-125">Create a resource group</span></span>

<span data-ttu-id="a983a-126">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="a983a-126">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="a983a-127">Create a resource group using [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a983a-127">Create a resource group using [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="a983a-128">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="a983a-128">The following example creates a resource group named *myResourceGroupAG* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="a983a-129">Create network resources</span><span class="sxs-lookup"><span data-stu-id="a983a-129">Create network resources</span></span>

<span data-ttu-id="a983a-130">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span><span class="sxs-lookup"><span data-stu-id="a983a-130">Create the virtual network named *myVNet* and the subnet named *myAGSubnet* using [az network vnet create](/cli/azure/network/vnet#az-net).</span></span> <span data-ttu-id="a983a-131">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="a983a-131">You can then add the subnet named *myBackendSubnet* that's needed by the backend servers using [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create).</span></span> <span data-ttu-id="a983a-132">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span><span class="sxs-lookup"><span data-stu-id="a983a-132">Create the public IP address named *myAGPublicIPAddress* using [az network public-ip create](/cli/azure/network/public-ip#az-network_public_ip_create).</span></span>

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

## <a name="create-the-application-gateway"></a><span data-ttu-id="a983a-133">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="a983a-133">Create the application gateway</span></span>

<span data-ttu-id="a983a-134">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-network_application_gateway_create) to create the application gateway named *myAppGateway*.</span><span class="sxs-lookup"><span data-stu-id="a983a-134">You can use [az network application-gateway create](/cli/azure/network/application-gateway#az-network_application_gateway_create) to create the application gateway named *myAppGateway*.</span></span> <span data-ttu-id="a983a-135">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="a983a-135">When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings.</span></span> 

<span data-ttu-id="a983a-136">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span><span class="sxs-lookup"><span data-stu-id="a983a-136">The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress* that you previously created.</span></span> <span data-ttu-id="a983a-137">In this example, you associate the certificate that you created and its password when you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a983a-137">In this example, you associate the certificate that you created and its password when you create the application gateway.</span></span> 

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

 <span data-ttu-id="a983a-138">It may take several minutes for the application gateway to be created.</span><span class="sxs-lookup"><span data-stu-id="a983a-138">It may take several minutes for the application gateway to be created.</span></span> <span data-ttu-id="a983a-139">After the application gateway is created, you can see these new features of it:</span><span class="sxs-lookup"><span data-stu-id="a983a-139">After the application gateway is created, you can see these new features of it:</span></span>

- <span data-ttu-id="a983a-140">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span><span class="sxs-lookup"><span data-stu-id="a983a-140">*appGatewayBackendPool* - An application gateway must have at least one backend address pool.</span></span>
- <span data-ttu-id="a983a-141">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span><span class="sxs-lookup"><span data-stu-id="a983a-141">*appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.</span></span>
- <span data-ttu-id="a983a-142">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="a983a-142">*appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.</span></span>
- <span data-ttu-id="a983a-143">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="a983a-143">*appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.</span></span>
- <span data-ttu-id="a983a-144">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span><span class="sxs-lookup"><span data-stu-id="a983a-144">*rule1* - The default routing rule that is associated with *appGatewayHttpListener*.</span></span>

## <a name="add-a-listener-and-redirection-rule"></a><span data-ttu-id="a983a-145">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="a983a-145">Add a listener and redirection rule</span></span>

### <a name="add-the-http-port"></a><span data-ttu-id="a983a-146">Add the HTTP port</span><span class="sxs-lookup"><span data-stu-id="a983a-146">Add the HTTP port</span></span>

<span data-ttu-id="a983a-147">You can use [az network application-gateway frontend-port create](/cli/azure/network/application-gateway/frontend-port#az-network_application_gateway_frontend_port_create) to add the HTTP port to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a983a-147">You can use [az network application-gateway frontend-port create](/cli/azure/network/application-gateway/frontend-port#az-network_application_gateway_frontend_port_create) to add the HTTP port to the application gateway.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create \
  --port 80 \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name httpPort
```

### <a name="add-the-http-listener"></a><span data-ttu-id="a983a-148">Add the HTTP listener</span><span class="sxs-lookup"><span data-stu-id="a983a-148">Add the HTTP listener</span></span>

<span data-ttu-id="a983a-149">You can use [az network application-gateway http-listener create](/cli/azure/network/application-gateway/http-listener#az-network_application_gateway_http_listener_create) to add the listener named *myListener* to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a983a-149">You can use [az network application-gateway http-listener create](/cli/azure/network/application-gateway/http-listener#az-network_application_gateway_http_listener_create) to add the listener named *myListener* to the application gateway.</span></span>

```azurecli-interactive
az network application-gateway http-listener create \
  --name myListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port httpPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway
```

### <a name="add-the-redirection-configuration"></a><span data-ttu-id="a983a-150">Add the redirection configuration</span><span class="sxs-lookup"><span data-stu-id="a983a-150">Add the redirection configuration</span></span>

<span data-ttu-id="a983a-151">Add the HTTP to HTTPS redirection configuration to the application gateway using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span><span class="sxs-lookup"><span data-stu-id="a983a-151">Add the HTTP to HTTPS redirection configuration to the application gateway using [az network application-gateway redirect-config create](/cli/azure/network/application-gateway/redirect-config#az-network_application_gateway_redirect_config_create).</span></span>

```azurecli-interactive
az network application-gateway redirect-config create \
  --name httpToHttps \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --type Permanent \
  --target-listener appGatewayHttpListener \
  --include-path true \
  --include-query-string true
```

### <a name="add-the-routing-rule"></a><span data-ttu-id="a983a-152">Add the routing rule</span><span class="sxs-lookup"><span data-stu-id="a983a-152">Add the routing rule</span></span>

<span data-ttu-id="a983a-153">Add the routing rule named *rule2* with the redirection configuration to the application gateway using [az network application-gateway rule create](/cli/azure/network/application-gateway/rule#az-network_application_gateway_rule_create).</span><span class="sxs-lookup"><span data-stu-id="a983a-153">Add the routing rule named *rule2* with the redirection configuration to the application gateway using [az network application-gateway rule create](/cli/azure/network/application-gateway/rule#az-network_application_gateway_rule_create).</span></span>

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name rule2 \
  --resource-group myResourceGroupAG \
  --http-listener myListener \
  --rule-type Basic \
  --redirect-config httpToHttps
```

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="a983a-154">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a983a-154">Create a virtual machine scale set</span></span>

<span data-ttu-id="a983a-155">In this example, you create a virtual machine scale set named *myvmss* that provides servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a983a-155">In this example, you create a virtual machine scale set named *myvmss* that provides servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="a983a-156">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="a983a-156">The virtual machines in the scale set are associated with *myBackendSubnet* and *appGatewayBackendPool*.</span></span> <span data-ttu-id="a983a-157">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="a983a-157">To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="a983a-158">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="a983a-158">Install NGINX</span></span>

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

## <a name="test-the-application-gateway"></a><span data-ttu-id="a983a-159">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="a983a-159">Test the application gateway</span></span>

<span data-ttu-id="a983a-160">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span><span class="sxs-lookup"><span data-stu-id="a983a-160">To get the public IP address of the application gateway, you can use [az network public-ip show](/cli/azure/network/public-ip#az-network_public_ip_show).</span></span> <span data-ttu-id="a983a-161">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="a983a-161">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [ipAddress] \
  --output tsv
```

![Secure warning](./media/redirect-http-to-https-cli/application-gateway-secure.png)

<span data-ttu-id="a983a-163">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span><span class="sxs-lookup"><span data-stu-id="a983a-163">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span></span> <span data-ttu-id="a983a-164">Your secured NGINX site is then displayed as in the following example:</span><span class="sxs-lookup"><span data-stu-id="a983a-164">Your secured NGINX site is then displayed as in the following example:</span></span>

![Test base URL in application gateway](./media/redirect-http-to-https-cli/application-gateway-nginxtest.png)

## <a name="next-steps"></a><span data-ttu-id="a983a-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="a983a-166">Next steps</span></span>

<span data-ttu-id="a983a-167">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="a983a-167">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a983a-168">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a983a-168">Create a self-signed certificate</span></span>
> * <span data-ttu-id="a983a-169">Set up a network</span><span class="sxs-lookup"><span data-stu-id="a983a-169">Set up a network</span></span>
> * <span data-ttu-id="a983a-170">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="a983a-170">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="a983a-171">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="a983a-171">Add a listener and redirection rule</span></span>
> * <span data-ttu-id="a983a-172">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="a983a-172">Create a virtual machine scale set with the default backend pool</span></span>


