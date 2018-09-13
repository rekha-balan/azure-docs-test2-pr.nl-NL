---
title: Quickstart - Direct web traffic with Azure Application Gateway - Azure portal | Microsoft Docs
description: Learn how use the Azure portal to create an Azure Application Gateway that directs web traffic to virtual machines in a backend pool.
services: application-gateway
author: vhorne
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: quickstart
ms.workload: infrastructure-services
ms.date: 02/14/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: effda81d8755486a65472eb546c6b8688aea0a3b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967306"
---
# <a name="quickstart-direct-web-traffic-with-azure-application-gateway---azure-portal"></a><span data-ttu-id="838ac-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure portal</span><span class="sxs-lookup"><span data-stu-id="838ac-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure portal</span></span>

<span data-ttu-id="838ac-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span><span class="sxs-lookup"><span data-stu-id="838ac-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span></span>

<span data-ttu-id="838ac-105">This quickstart shows you how to use the Azure portal to quickly create the application gateway with two virtual machines in its backend pool.</span><span class="sxs-lookup"><span data-stu-id="838ac-105">This quickstart shows you how to use the Azure portal to quickly create the application gateway with two virtual machines in its backend pool.</span></span> <span data-ttu-id="838ac-106">You then test it to make sure it's working correctly.</span><span class="sxs-lookup"><span data-stu-id="838ac-106">You then test it to make sure it's working correctly.</span></span>

<span data-ttu-id="838ac-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="838ac-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="838ac-108">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="838ac-108">Log in to Azure</span></span>

<span data-ttu-id="838ac-109">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="838ac-109">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="838ac-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="838ac-110">Create an application gateway</span></span>

<span data-ttu-id="838ac-111">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span><span class="sxs-lookup"><span data-stu-id="838ac-111">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span></span> <span data-ttu-id="838ac-112">You can create a virtual network at the same time that you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-112">You can create a virtual network at the same time that you create the application gateway.</span></span> <span data-ttu-id="838ac-113">Two subnets are created in this example: one for the application gateway, and the other for the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="838ac-113">Two subnets are created in this example: one for the application gateway, and the other for the virtual machines.</span></span> 

1. <span data-ttu-id="838ac-114">Click **Create a resource** found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="838ac-114">Click **Create a resource** found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="838ac-115">Select **Networking** and then select **Application Gateway** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="838ac-115">Select **Networking** and then select **Application Gateway** in the Featured list.</span></span>
3. <span data-ttu-id="838ac-116">Enter these values for the application gateway:</span><span class="sxs-lookup"><span data-stu-id="838ac-116">Enter these values for the application gateway:</span></span>

    - <span data-ttu-id="838ac-117">*myAppGateway* - for the name of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-117">*myAppGateway* - for the name of the application gateway.</span></span>
    - <span data-ttu-id="838ac-118">*myResourceGroupAG* - for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="838ac-118">*myResourceGroupAG* - for the new resource group.</span></span>

    ![Create new application gateway](./media/quick-create-portal/application-gateway-create.png)

4. <span data-ttu-id="838ac-120">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="838ac-120">Accept the default values for the other settings and then click **OK**.</span></span>
5. <span data-ttu-id="838ac-121">Click **Choose a virtual network** > **Create new**, and then enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="838ac-121">Click **Choose a virtual network** > **Create new**, and then enter these values for the virtual network:</span></span>

    - <span data-ttu-id="838ac-122">*myVNet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="838ac-122">*myVNet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="838ac-123">*10.0.0.0/16* - for the virtual network address space.</span><span class="sxs-lookup"><span data-stu-id="838ac-123">*10.0.0.0/16* - for the virtual network address space.</span></span>
    - <span data-ttu-id="838ac-124">*myAGSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="838ac-124">*myAGSubnet* - for the subnet name.</span></span>
    - <span data-ttu-id="838ac-125">*10.0.0.0/24* - for the subnet address space.</span><span class="sxs-lookup"><span data-stu-id="838ac-125">*10.0.0.0/24* - for the subnet address space.</span></span>

    ![Create virtual network](./media/quick-create-portal/application-gateway-vnet.png)

6. <span data-ttu-id="838ac-127">Click **OK** to create the virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="838ac-127">Click **OK** to create the virtual network and subnet.</span></span>
6. <span data-ttu-id="838ac-128">Click **Choose a public IP address** > **Create new**, and then enter the name of the public IP address.</span><span class="sxs-lookup"><span data-stu-id="838ac-128">Click **Choose a public IP address** > **Create new**, and then enter the name of the public IP address.</span></span> <span data-ttu-id="838ac-129">In this example, the public IP address is named *myAGPublicIPAddress*.</span><span class="sxs-lookup"><span data-stu-id="838ac-129">In this example, the public IP address is named *myAGPublicIPAddress*.</span></span> <span data-ttu-id="838ac-130">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="838ac-130">Accept the default values for the other settings and then click **OK**.</span></span>
8. <span data-ttu-id="838ac-131">Accept the default values for the listener configuration, leave the web application firewall disabled, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="838ac-131">Accept the default values for the listener configuration, leave the web application firewall disabled, and then click **OK**.</span></span>
9. <span data-ttu-id="838ac-132">Review the settings on the summary page, and then click **OK** to create the virtual network, the public IP address, and the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-132">Review the settings on the summary page, and then click **OK** to create the virtual network, the public IP address, and the application gateway.</span></span> <span data-ttu-id="838ac-133">It may take up to 30 minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span><span class="sxs-lookup"><span data-stu-id="838ac-133">It may take up to 30 minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span></span>

### <a name="add-a-subnet"></a><span data-ttu-id="838ac-134">Add a subnet</span><span class="sxs-lookup"><span data-stu-id="838ac-134">Add a subnet</span></span>

1. <span data-ttu-id="838ac-135">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="838ac-135">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span></span>
2. <span data-ttu-id="838ac-136">Click **Subnets** > **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="838ac-136">Click **Subnets** > **Subnet**.</span></span>

    ![Create subnet](./media/quick-create-portal/application-gateway-subnet.png)

3. <span data-ttu-id="838ac-138">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="838ac-138">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span></span>

## <a name="create-backend-servers"></a><span data-ttu-id="838ac-139">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="838ac-139">Create backend servers</span></span>

<span data-ttu-id="838ac-140">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-140">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span></span> 

### <a name="create-a-virtual-machine"></a><span data-ttu-id="838ac-141">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="838ac-141">Create a virtual machine</span></span>

1. <span data-ttu-id="838ac-142">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="838ac-142">Click **New**.</span></span>
2. <span data-ttu-id="838ac-143">Select **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="838ac-143">Select **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span></span>
3. <span data-ttu-id="838ac-144">Enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="838ac-144">Enter these values for the virtual machine:</span></span>

    - <span data-ttu-id="838ac-145">*myVM* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="838ac-145">*myVM* - for the name of the virtual machine.</span></span>
    - <span data-ttu-id="838ac-146">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="838ac-146">*azureuser* - for the administrator user name.</span></span>
    - <span data-ttu-id="838ac-147">*Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="838ac-147">*Azure123456!*</span></span> <span data-ttu-id="838ac-148">for the password.</span><span class="sxs-lookup"><span data-stu-id="838ac-148">for the password.</span></span>
    - <span data-ttu-id="838ac-149">Select **Use existing**, and then select *myResourceGroupAG*.</span><span class="sxs-lookup"><span data-stu-id="838ac-149">Select **Use existing**, and then select *myResourceGroupAG*.</span></span>

4. <span data-ttu-id="838ac-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="838ac-150">Click **OK**.</span></span>
5. <span data-ttu-id="838ac-151">Select **DS1_V2** for the size of the virtual machine and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="838ac-151">Select **DS1_V2** for the size of the virtual machine and then click **Select**.</span></span>
6. <span data-ttu-id="838ac-152">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span><span class="sxs-lookup"><span data-stu-id="838ac-152">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span></span> 
7. <span data-ttu-id="838ac-153">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="838ac-153">Click **Disabled** to disable boot diagnostics.</span></span>
8. <span data-ttu-id="838ac-154">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="838ac-154">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>

### <a name="install-iis"></a><span data-ttu-id="838ac-155">Install IIS</span><span class="sxs-lookup"><span data-stu-id="838ac-155">Install IIS</span></span>

<span data-ttu-id="838ac-156">You install IIS on the virtual machines to verify that the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="838ac-156">You install IIS on the virtual machines to verify that the application gateway was successfully created.</span></span>

1. <span data-ttu-id="838ac-157">Open the interactive shell and make sure that it is set to **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="838ac-157">Open the interactive shell and make sure that it is set to **PowerShell**.</span></span>

    ![Install custom extension](./media/quick-create-portal/application-gateway-extension.png)

2. <span data-ttu-id="838ac-159">Run the following command to install IIS on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="838ac-159">Run the following command to install IIS on the virtual machine:</span></span> 

    ```azurepowershell-interactive
    Set-AzureRmVMExtension `
      -ResourceGroupName myResourceGroupAG `
      -ExtensionName IIS `
      -VMName myVM `
      -Publisher Microsoft.Compute `
      -ExtensionType CustomScriptExtension `
      -TypeHandlerVersion 1.4 `
      -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
      -Location EastUS
    ```

3. <span data-ttu-id="838ac-160">Create a second virtual machine and install IIS using the steps that you just finished.</span><span class="sxs-lookup"><span data-stu-id="838ac-160">Create a second virtual machine and install IIS using the steps that you just finished.</span></span> <span data-ttu-id="838ac-161">Enter *myVM2* for its name and for VMName in Set-AzureRmVMExtension.</span><span class="sxs-lookup"><span data-stu-id="838ac-161">Enter *myVM2* for its name and for VMName in Set-AzureRmVMExtension.</span></span>

### <a name="add-backend-servers"></a><span data-ttu-id="838ac-162">Add backend servers</span><span class="sxs-lookup"><span data-stu-id="838ac-162">Add backend servers</span></span>

<span data-ttu-id="838ac-163">After you create the virtual machines, you need to add them to the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-163">After you create the virtual machines, you need to add them to the backend pool in the application gateway.</span></span>

1. <span data-ttu-id="838ac-164">Click **All resources** > **myAppGateway**.</span><span class="sxs-lookup"><span data-stu-id="838ac-164">Click **All resources** > **myAppGateway**.</span></span>
2. <span data-ttu-id="838ac-165">Click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="838ac-165">Click **Backend pools**.</span></span> <span data-ttu-id="838ac-166">A default pool was automatically created with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="838ac-166">A default pool was automatically created with the application gateway.</span></span> <span data-ttu-id="838ac-167">Click **appGatewayBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="838ac-167">Click **appGatewayBackendPool**.</span></span>
3. <span data-ttu-id="838ac-168">Click **Add target** > **Virtual machine**, and then select *myVM*.</span><span class="sxs-lookup"><span data-stu-id="838ac-168">Click **Add target** > **Virtual machine**, and then select *myVM*.</span></span> <span data-ttu-id="838ac-169">Select **Add target** > **Virtual machine**, and then select *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="838ac-169">Select **Add target** > **Virtual machine**, and then select *myVM2*.</span></span>

    ![Add backend servers](./media/quick-create-portal/application-gateway-backend.png)

4. <span data-ttu-id="838ac-171">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="838ac-171">Click **Save**.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="838ac-172">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="838ac-172">Test the application gateway</span></span>

<span data-ttu-id="838ac-173">Installing IIS is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="838ac-173">Installing IIS is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span></span>

1. <span data-ttu-id="838ac-174">Find the public IP address for the application gateway on the Overview screen.</span><span class="sxs-lookup"><span data-stu-id="838ac-174">Find the public IP address for the application gateway on the Overview screen.</span></span> <span data-ttu-id="838ac-175">Click **All resources** > **myAGPublicIPAddress**.</span><span class="sxs-lookup"><span data-stu-id="838ac-175">Click **All resources** > **myAGPublicIPAddress**.</span></span>

    ![Record application gateway public IP address](./media/quick-create-portal/application-gateway-record-ag-address.png)

2. <span data-ttu-id="838ac-177">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="838ac-177">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

    ![Test application gateway](./media/quick-create-portal/application-gateway-iistest.png)

<span data-ttu-id="838ac-179">When you refresh the browser, you should see the name of the other VM appear.</span><span class="sxs-lookup"><span data-stu-id="838ac-179">When you refresh the browser, you should see the name of the other VM appear.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="838ac-180">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="838ac-180">Clean up resources</span></span>

<span data-ttu-id="838ac-181">First explore the resources that were created with the application gateway, and then when no longer needed, you can delete the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="838ac-181">First explore the resources that were created with the application gateway, and then when no longer needed, you can delete the resource group, application gateway, and all related resources.</span></span> <span data-ttu-id="838ac-182">To do so, select the resource group that contains the application gateway and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="838ac-182">To do so, select the resource group that contains the application gateway and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="838ac-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="838ac-183">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="838ac-184">Manage web traffic with an application gateway using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="838ac-184">Manage web traffic with an application gateway using the Azure CLI</span></span>](./tutorial-manage-web-traffic-cli.md)
