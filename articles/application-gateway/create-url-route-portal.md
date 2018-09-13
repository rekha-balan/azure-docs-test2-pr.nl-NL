---
title: Create an application gateway with URL path-based routing rules - Azure portal | Microsoft Docs
description: Learn how to create URL path-based routing rules for an application gateway and virtual machine scale set using the Azure portal.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 01/26/2018
ms.author: victorh
ms.openlocfilehash: 7e8f06e2d1b489b79218514d8b115c389f057d56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867182"
---
# <a name="create-an-application-gateway-with-path-based-routing-rules-using-the-azure-portal"></a><span data-ttu-id="008cf-103">Create an application gateway with path-based routing rules using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="008cf-103">Create an application gateway with path-based routing rules using the Azure portal</span></span>

<span data-ttu-id="008cf-104">You can use the Azure portal to configure [URL path-based routing rules](url-route-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="008cf-104">You can use the Azure portal to configure [URL path-based routing rules](url-route-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="008cf-105">In this tutorial, you create backend pools using virtual machines.</span><span class="sxs-lookup"><span data-stu-id="008cf-105">In this tutorial, you create backend pools using virtual machines.</span></span> <span data-ttu-id="008cf-106">You then create routing rules that make sure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="008cf-106">You then create routing rules that make sure web traffic arrives at the appropriate servers in the pools.</span></span>

<span data-ttu-id="008cf-107">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="008cf-107">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="008cf-108">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="008cf-108">Create an application gateway</span></span>
> * <span data-ttu-id="008cf-109">Create virtual machines for backend servers</span><span class="sxs-lookup"><span data-stu-id="008cf-109">Create virtual machines for backend servers</span></span>
> * <span data-ttu-id="008cf-110">Create backend pools with the backend servers</span><span class="sxs-lookup"><span data-stu-id="008cf-110">Create backend pools with the backend servers</span></span>
> * <span data-ttu-id="008cf-111">Create a backend listener</span><span class="sxs-lookup"><span data-stu-id="008cf-111">Create a backend listener</span></span>
> * <span data-ttu-id="008cf-112">Create a path-based routing rule</span><span class="sxs-lookup"><span data-stu-id="008cf-112">Create a path-based routing rule</span></span>

![URL routing example](./media/create-url-route-portal/scenario.png)

<span data-ttu-id="008cf-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="008cf-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="008cf-115">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="008cf-115">Log in to Azure</span></span>

<span data-ttu-id="008cf-116">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="008cf-116">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="008cf-117">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="008cf-117">Create an application gateway</span></span>

<span data-ttu-id="008cf-118">A virtual network is needed for communication between the resources that you create.</span><span class="sxs-lookup"><span data-stu-id="008cf-118">A virtual network is needed for communication between the resources that you create.</span></span> <span data-ttu-id="008cf-119">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span><span class="sxs-lookup"><span data-stu-id="008cf-119">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span></span> <span data-ttu-id="008cf-120">You can create a virtual network at the same time that you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="008cf-120">You can create a virtual network at the same time that you create the application gateway.</span></span>

1. <span data-ttu-id="008cf-121">Click **New** found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="008cf-121">Click **New** found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="008cf-122">Select **Networking** and then select **Application Gateway** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="008cf-122">Select **Networking** and then select **Application Gateway** in the Featured list.</span></span>
3. <span data-ttu-id="008cf-123">Enter these values for the application gateway:</span><span class="sxs-lookup"><span data-stu-id="008cf-123">Enter these values for the application gateway:</span></span>

    - <span data-ttu-id="008cf-124">*myAppGateway* - for the name of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="008cf-124">*myAppGateway* - for the name of the application gateway.</span></span>
    - <span data-ttu-id="008cf-125">*myResourceGroupAG* - for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="008cf-125">*myResourceGroupAG* - for the new resource group.</span></span>

    ![Create new application gateway](./media/create-url-route-portal/application-gateway-create.png)

4. <span data-ttu-id="008cf-127">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-127">Accept the default values for the other settings and then click **OK**.</span></span>
5. <span data-ttu-id="008cf-128">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="008cf-128">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span></span>

    - <span data-ttu-id="008cf-129">*myVNet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="008cf-129">*myVNet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="008cf-130">*10.0.0.0/16* - for the virtual network address space.</span><span class="sxs-lookup"><span data-stu-id="008cf-130">*10.0.0.0/16* - for the virtual network address space.</span></span>
    - <span data-ttu-id="008cf-131">*myAGSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="008cf-131">*myAGSubnet* - for the subnet name.</span></span>
    - <span data-ttu-id="008cf-132">*10.0.0.0/24* - for the subnet address space.</span><span class="sxs-lookup"><span data-stu-id="008cf-132">*10.0.0.0/24* - for the subnet address space.</span></span>

    ![Create virtual network](./media/create-url-route-portal/application-gateway-vnet.png)

6. <span data-ttu-id="008cf-134">Click **OK** to create the virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="008cf-134">Click **OK** to create the virtual network and subnet.</span></span>
7. <span data-ttu-id="008cf-135">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span><span class="sxs-lookup"><span data-stu-id="008cf-135">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span></span> <span data-ttu-id="008cf-136">In this example, the public IP address is named *myAGPublicIPAddress*.</span><span class="sxs-lookup"><span data-stu-id="008cf-136">In this example, the public IP address is named *myAGPublicIPAddress*.</span></span> <span data-ttu-id="008cf-137">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-137">Accept the default values for the other settings and then click **OK**.</span></span>
8. <span data-ttu-id="008cf-138">Accept the default values for the Listener configuration, leave the Web application firewall disabled, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-138">Accept the default values for the Listener configuration, leave the Web application firewall disabled, and then click **OK**.</span></span>
9. <span data-ttu-id="008cf-139">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span><span class="sxs-lookup"><span data-stu-id="008cf-139">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span></span> <span data-ttu-id="008cf-140">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span><span class="sxs-lookup"><span data-stu-id="008cf-140">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span></span>

### <a name="add-a-subnet"></a><span data-ttu-id="008cf-141">Add a subnet</span><span class="sxs-lookup"><span data-stu-id="008cf-141">Add a subnet</span></span>

1. <span data-ttu-id="008cf-142">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="008cf-142">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span></span>
2. <span data-ttu-id="008cf-143">Click **Subnets**, and then click **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="008cf-143">Click **Subnets**, and then click **Subnet**.</span></span>

    ![Create subnet](./media/create-url-route-portal/application-gateway-subnet.png)

3. <span data-ttu-id="008cf-145">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-145">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span></span>

## <a name="create-virtual-machines"></a><span data-ttu-id="008cf-146">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="008cf-146">Create virtual machines</span></span>

<span data-ttu-id="008cf-147">In this example, you create three virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="008cf-147">In this example, you create three virtual machines to be used as backend servers for the application gateway.</span></span> <span data-ttu-id="008cf-148">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="008cf-148">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span></span>

1. <span data-ttu-id="008cf-149">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="008cf-149">Click **New**.</span></span>
2. <span data-ttu-id="008cf-150">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="008cf-150">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span></span>
3. <span data-ttu-id="008cf-151">Enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="008cf-151">Enter these values for the virtual machine:</span></span>

    - <span data-ttu-id="008cf-152">*myVM1* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="008cf-152">*myVM1* - for the name of the virtual machine.</span></span>
    - <span data-ttu-id="008cf-153">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="008cf-153">*azureuser* - for the administrator user name.</span></span>
    - <span data-ttu-id="008cf-154">*Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="008cf-154">*Azure123456!*</span></span> <span data-ttu-id="008cf-155">for the password.</span><span class="sxs-lookup"><span data-stu-id="008cf-155">for the password.</span></span>
    - <span data-ttu-id="008cf-156">Select **Use existing**, and then select *myResourceGroupAG*.</span><span class="sxs-lookup"><span data-stu-id="008cf-156">Select **Use existing**, and then select *myResourceGroupAG*.</span></span>

4. <span data-ttu-id="008cf-157">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-157">Click **OK**.</span></span>
5. <span data-ttu-id="008cf-158">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="008cf-158">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
6. <span data-ttu-id="008cf-159">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span><span class="sxs-lookup"><span data-stu-id="008cf-159">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span></span> 
7. <span data-ttu-id="008cf-160">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="008cf-160">Click **Disabled** to disable boot diagnostics.</span></span>
8. <span data-ttu-id="008cf-161">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="008cf-161">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>

### <a name="install-iis"></a><span data-ttu-id="008cf-162">Install IIS</span><span class="sxs-lookup"><span data-stu-id="008cf-162">Install IIS</span></span>

1. <span data-ttu-id="008cf-163">Open the interactive shell and make sure that it is set to **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="008cf-163">Open the interactive shell and make sure that it is set to **PowerShell**.</span></span>

    ![Install custom extension](./media/create-url-route-portal/application-gateway-extension.png)

2. <span data-ttu-id="008cf-165">Run the following command to install IIS on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="008cf-165">Run the following command to install IIS on the virtual machine:</span></span> 

    ```azurepowershell-interactive
    $publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1");  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }
    Set-AzureRmVMExtension `
      -ResourceGroupName myResourceGroupAG `
      -Location eastus `
      -ExtensionName IIS `
      -VMName myVM1 `
      -Publisher Microsoft.Compute `
      -ExtensionType CustomScriptExtension `
      -TypeHandlerVersion 1.4 `
      -Settings $publicSettings
    ```

3. <span data-ttu-id="008cf-166">Create two more virtual machines and install IIS using the steps that you just finished.</span><span class="sxs-lookup"><span data-stu-id="008cf-166">Create two more virtual machines and install IIS using the steps that you just finished.</span></span> <span data-ttu-id="008cf-167">Enter the names of *myVM2* and *myVM3* for the names and for the values of VMName in Set-AzureRmVMExtension.</span><span class="sxs-lookup"><span data-stu-id="008cf-167">Enter the names of *myVM2* and *myVM3* for the names and for the values of VMName in Set-AzureRmVMExtension.</span></span>

## <a name="create-backend-pools-with-the-virtual-machines"></a><span data-ttu-id="008cf-168">Create backend pools with the virtual machines</span><span class="sxs-lookup"><span data-stu-id="008cf-168">Create backend pools with the virtual machines</span></span>

1. <span data-ttu-id="008cf-169">Click **All resources** and then click **myAppGateway**.</span><span class="sxs-lookup"><span data-stu-id="008cf-169">Click **All resources** and then click **myAppGateway**.</span></span>
2. <span data-ttu-id="008cf-170">Click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="008cf-170">Click **Backend pools**.</span></span> <span data-ttu-id="008cf-171">A default pool was automatically created with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="008cf-171">A default pool was automatically created with the application gateway.</span></span> <span data-ttu-id="008cf-172">Click **appGateayBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="008cf-172">Click **appGateayBackendPool**.</span></span>
3. <span data-ttu-id="008cf-173">Click **Add target** to add *myVM1* to appGatewayBackendPool.</span><span class="sxs-lookup"><span data-stu-id="008cf-173">Click **Add target** to add *myVM1* to appGatewayBackendPool.</span></span>

    ![Add backend servers](./media/create-url-route-portal/application-gateway-backend.png)

4. <span data-ttu-id="008cf-175">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="008cf-175">Click **Save**.</span></span>
5. <span data-ttu-id="008cf-176">Click **Backend pools** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="008cf-176">Click **Backend pools** and then click **Add**.</span></span>
6. <span data-ttu-id="008cf-177">Enter a name of *imagesBackendPool* and add *myVM2* using **Add target**.</span><span class="sxs-lookup"><span data-stu-id="008cf-177">Enter a name of *imagesBackendPool* and add *myVM2* using **Add target**.</span></span>
7. <span data-ttu-id="008cf-178">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-178">Click **OK**.</span></span>
8. <span data-ttu-id="008cf-179">Click **Add** again to add another backend pool with a name of *videoBackendPool* and add *myVM3* to it.</span><span class="sxs-lookup"><span data-stu-id="008cf-179">Click **Add** again to add another backend pool with a name of *videoBackendPool* and add *myVM3* to it.</span></span>

## <a name="create-a-backend-listener"></a><span data-ttu-id="008cf-180">Create a backend listener</span><span class="sxs-lookup"><span data-stu-id="008cf-180">Create a backend listener</span></span>

1. <span data-ttu-id="008cf-181">Click **Listeners** and the click **Basic**.</span><span class="sxs-lookup"><span data-stu-id="008cf-181">Click **Listeners** and the click **Basic**.</span></span>
2. <span data-ttu-id="008cf-182">Enter *myBackendListener* for the name, *myFrontendPort* for the name of the frontend port, and then *8080* as the port for the listener.</span><span class="sxs-lookup"><span data-stu-id="008cf-182">Enter *myBackendListener* for the name, *myFrontendPort* for the name of the frontend port, and then *8080* as the port for the listener.</span></span>
3. <span data-ttu-id="008cf-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-183">Click **OK**.</span></span>

## <a name="create-a-path-based-routing-rule"></a><span data-ttu-id="008cf-184">Create a path-based routing rule</span><span class="sxs-lookup"><span data-stu-id="008cf-184">Create a path-based routing rule</span></span>

1. <span data-ttu-id="008cf-185">Click **Rules** and then click **Path-based**.</span><span class="sxs-lookup"><span data-stu-id="008cf-185">Click **Rules** and then click **Path-based**.</span></span>
2. <span data-ttu-id="008cf-186">Enter *rule2* for the name.</span><span class="sxs-lookup"><span data-stu-id="008cf-186">Enter *rule2* for the name.</span></span>
3. <span data-ttu-id="008cf-187">Enter *Images* for the name of the first path.</span><span class="sxs-lookup"><span data-stu-id="008cf-187">Enter *Images* for the name of the first path.</span></span> <span data-ttu-id="008cf-188">Enter */images/*\* for the path.</span><span class="sxs-lookup"><span data-stu-id="008cf-188">Enter */images/*\* for the path.</span></span> <span data-ttu-id="008cf-189">Select **imagesBackendPool** for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="008cf-189">Select **imagesBackendPool** for the backend pool.</span></span>
4. <span data-ttu-id="008cf-190">Enter *Video* for the name of the second path.</span><span class="sxs-lookup"><span data-stu-id="008cf-190">Enter *Video* for the name of the second path.</span></span> <span data-ttu-id="008cf-191">Enter */video/*\* for the path.</span><span class="sxs-lookup"><span data-stu-id="008cf-191">Enter */video/*\* for the path.</span></span> <span data-ttu-id="008cf-192">Select **videoBackendPool** for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="008cf-192">Select **videoBackendPool** for the backend pool.</span></span>

    ![Create a path-based rule](./media/create-url-route-portal/application-gateway-route-rule.png)

5. <span data-ttu-id="008cf-194">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="008cf-194">Click **OK**.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="008cf-195">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="008cf-195">Test the application gateway</span></span>

1. <span data-ttu-id="008cf-196">Click **All resources**, and then click **myAGPublicIPAddress**.</span><span class="sxs-lookup"><span data-stu-id="008cf-196">Click **All resources**, and then click **myAGPublicIPAddress**.</span></span>

    ![Record application gateway public IP address](./media/create-url-route-portal/application-gateway-record-ag-address.png)

2. <span data-ttu-id="008cf-198">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="008cf-198">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="008cf-199">Such as, http://40.121.222.19.</span><span class="sxs-lookup"><span data-stu-id="008cf-199">Such as, http://40.121.222.19.</span></span>

    ![Test base URL in application gateway](./media/create-url-route-portal/application-gateway-iistest.png)

3. <span data-ttu-id="008cf-201">Change the URL to http://&lt;ip-address&gt;:8080/images/test.htm, substituting &lt;ip-address&gt; with your IP address, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="008cf-201">Change the URL to http://&lt;ip-address&gt;:8080/images/test.htm, substituting &lt;ip-address&gt; with your IP address, and you should see something like the following example:</span></span>

    ![Test images URL in application gateway](./media/create-url-route-portal/application-gateway-iistest-images.png)

4. <span data-ttu-id="008cf-203">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting &lt;ip-address&gt; with your IP address, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="008cf-203">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting &lt;ip-address&gt; with your IP address, and you should see something like the following example:</span></span>

    ![Test video URL in application gateway](./media/create-url-route-portal/application-gateway-iistest-video.png)

## <a name="next-steps"></a><span data-ttu-id="008cf-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="008cf-205">Next steps</span></span>

<span data-ttu-id="008cf-206">In this article, you learned how to</span><span class="sxs-lookup"><span data-stu-id="008cf-206">In this article, you learned how to</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="008cf-207">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="008cf-207">Create an application gateway</span></span>
> * <span data-ttu-id="008cf-208">Create virtual machines for backend servers</span><span class="sxs-lookup"><span data-stu-id="008cf-208">Create virtual machines for backend servers</span></span>
> * <span data-ttu-id="008cf-209">Create backend pools with the backend servers</span><span class="sxs-lookup"><span data-stu-id="008cf-209">Create backend pools with the backend servers</span></span>
> * <span data-ttu-id="008cf-210">Create a backend listener</span><span class="sxs-lookup"><span data-stu-id="008cf-210">Create a backend listener</span></span>
> * <span data-ttu-id="008cf-211">Create a path-based routing rule</span><span class="sxs-lookup"><span data-stu-id="008cf-211">Create a path-based routing rule</span></span>

<span data-ttu-id="008cf-212">To learn more about application gateways and their associated resources, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="008cf-212">To learn more about application gateways and their associated resources, continue to the how-to articles.</span></span>
