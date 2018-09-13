---
title: Create an application gateway that hosts multiple web sites  - Azure portal | Microsoft Docs
description: Learn how to create an application gateway that hosts multiple web sites using the Azure portal.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 12/28/2017
ms.author: victorh
ms.openlocfilehash: 8f2e2500c39f42ebd7fefb3cec941088edf126f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865403"
---
# <a name="create-and-configure-an-application-gateway-to-host-multiple-web-sites-using-the-azure-portal"></a><span data-ttu-id="1b633-103">Create and configure an application gateway to host multiple web sites using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1b633-103">Create and configure an application gateway to host multiple web sites using the Azure portal</span></span>

<span data-ttu-id="1b633-104">You can use the Azure portal to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b633-104">You can use the Azure portal to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="1b633-105">In this tutorial, you define backend address pools using virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1b633-105">In this tutorial, you define backend address pools using virtual machines.</span></span> <span data-ttu-id="1b633-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="1b633-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span></span> <span data-ttu-id="1b633-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="1b633-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span></span>

<span data-ttu-id="1b633-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1b633-108">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b633-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1b633-109">Create an application gateway</span></span>
> * <span data-ttu-id="1b633-110">Create virtual machines for backend servers</span><span class="sxs-lookup"><span data-stu-id="1b633-110">Create virtual machines for backend servers</span></span>
> * <span data-ttu-id="1b633-111">Create backend pools with the backend servers</span><span class="sxs-lookup"><span data-stu-id="1b633-111">Create backend pools with the backend servers</span></span>
> * <span data-ttu-id="1b633-112">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="1b633-112">Create backend listeners</span></span>
> * <span data-ttu-id="1b633-113">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="1b633-113">Create routing rules</span></span>
> * <span data-ttu-id="1b633-114">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1b633-114">Create a CNAME record in your domain</span></span>

![Multi-site routing example](./media/create-multiple-sites-portal/scenario.png)

<span data-ttu-id="1b633-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1b633-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="1b633-117">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="1b633-117">Log in to Azure</span></span>

<span data-ttu-id="1b633-118">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1b633-118">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="1b633-119">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1b633-119">Create an application gateway</span></span>

<span data-ttu-id="1b633-120">A virtual network is needed for communication between the resources that you create.</span><span class="sxs-lookup"><span data-stu-id="1b633-120">A virtual network is needed for communication between the resources that you create.</span></span> <span data-ttu-id="1b633-121">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span><span class="sxs-lookup"><span data-stu-id="1b633-121">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span></span> <span data-ttu-id="1b633-122">You can create a virtual network at the same time that you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b633-122">You can create a virtual network at the same time that you create the application gateway.</span></span>

1. <span data-ttu-id="1b633-123">Click **New** found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b633-123">Click **New** found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="1b633-124">Select **Networking** and then select **Application Gateway** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="1b633-124">Select **Networking** and then select **Application Gateway** in the Featured list.</span></span>
3. <span data-ttu-id="1b633-125">Enter these values for the application gateway:</span><span class="sxs-lookup"><span data-stu-id="1b633-125">Enter these values for the application gateway:</span></span>

    - <span data-ttu-id="1b633-126">*myAppGateway* - for the name of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b633-126">*myAppGateway* - for the name of the application gateway.</span></span>
    - <span data-ttu-id="1b633-127">*myResourceGroupAG* - for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="1b633-127">*myResourceGroupAG* - for the new resource group.</span></span>

    ![Create new application gateway](./media/create-multiple-sites-portal/application-gateway-create.png)

4. <span data-ttu-id="1b633-129">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-129">Accept the default values for the other settings and then click **OK**.</span></span>
5. <span data-ttu-id="1b633-130">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="1b633-130">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span></span>

    - <span data-ttu-id="1b633-131">*myVNet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1b633-131">*myVNet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="1b633-132">*10.0.0.0/16* - for the virtual network address space.</span><span class="sxs-lookup"><span data-stu-id="1b633-132">*10.0.0.0/16* - for the virtual network address space.</span></span>
    - <span data-ttu-id="1b633-133">*myAGSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="1b633-133">*myAGSubnet* - for the subnet name.</span></span>
    - <span data-ttu-id="1b633-134">*10.0.0.0/24* - for the subnet address space.</span><span class="sxs-lookup"><span data-stu-id="1b633-134">*10.0.0.0/24* - for the subnet address space.</span></span>

    ![Create virtual network](./media/create-multiple-sites-portal/application-gateway-vnet.png)

6. <span data-ttu-id="1b633-136">Click **OK** to create the virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="1b633-136">Click **OK** to create the virtual network and subnet.</span></span>
7. <span data-ttu-id="1b633-137">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span><span class="sxs-lookup"><span data-stu-id="1b633-137">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span></span> <span data-ttu-id="1b633-138">In this example, the public IP address is named *myAGPublicIPAddress*.</span><span class="sxs-lookup"><span data-stu-id="1b633-138">In this example, the public IP address is named *myAGPublicIPAddress*.</span></span> <span data-ttu-id="1b633-139">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-139">Accept the default values for the other settings and then click **OK**.</span></span>
8. <span data-ttu-id="1b633-140">Accept the default values for the Listener configuration, leave the Web application firewall disabled, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-140">Accept the default values for the Listener configuration, leave the Web application firewall disabled, and then click **OK**.</span></span>
9. <span data-ttu-id="1b633-141">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b633-141">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span></span> <span data-ttu-id="1b633-142">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span><span class="sxs-lookup"><span data-stu-id="1b633-142">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span></span>

### <a name="add-a-subnet"></a><span data-ttu-id="1b633-143">Add a subnet</span><span class="sxs-lookup"><span data-stu-id="1b633-143">Add a subnet</span></span>

1. <span data-ttu-id="1b633-144">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="1b633-144">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span></span>
2. <span data-ttu-id="1b633-145">Click **Subnets**, and then click **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="1b633-145">Click **Subnets**, and then click **Subnet**.</span></span>

    ![Create subnet](./media/create-multiple-sites-portal/application-gateway-subnet.png)

3. <span data-ttu-id="1b633-147">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-147">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span></span>

## <a name="create-virtual-machines"></a><span data-ttu-id="1b633-148">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="1b633-148">Create virtual machines</span></span>

<span data-ttu-id="1b633-149">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b633-149">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span></span> <span data-ttu-id="1b633-150">You also install IIS on the virtual machines to verify that traffic is routing correctly.</span><span class="sxs-lookup"><span data-stu-id="1b633-150">You also install IIS on the virtual machines to verify that traffic is routing correctly.</span></span>

1. <span data-ttu-id="1b633-151">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="1b633-151">Click **New**.</span></span>
2. <span data-ttu-id="1b633-152">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="1b633-152">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span></span>
3. <span data-ttu-id="1b633-153">Enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="1b633-153">Enter these values for the virtual machine:</span></span>

    - <span data-ttu-id="1b633-154">*contosoVM* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1b633-154">*contosoVM* - for the name of the virtual machine.</span></span>
    - <span data-ttu-id="1b633-155">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="1b633-155">*azureuser* - for the administrator user name.</span></span>
    - <span data-ttu-id="1b633-156">*Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="1b633-156">*Azure123456!*</span></span> <span data-ttu-id="1b633-157">for the password.</span><span class="sxs-lookup"><span data-stu-id="1b633-157">for the password.</span></span>
    - <span data-ttu-id="1b633-158">Select **Use existing**, and then select *myResourceGroupAG*.</span><span class="sxs-lookup"><span data-stu-id="1b633-158">Select **Use existing**, and then select *myResourceGroupAG*.</span></span>

4. <span data-ttu-id="1b633-159">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-159">Click **OK**.</span></span>
5. <span data-ttu-id="1b633-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="1b633-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
6. <span data-ttu-id="1b633-161">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span><span class="sxs-lookup"><span data-stu-id="1b633-161">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span></span> 
7. <span data-ttu-id="1b633-162">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1b633-162">Click **Disabled** to disable boot diagnostics.</span></span>
8. <span data-ttu-id="1b633-163">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b633-163">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>

### <a name="install-iis"></a><span data-ttu-id="1b633-164">Install IIS</span><span class="sxs-lookup"><span data-stu-id="1b633-164">Install IIS</span></span>

1. <span data-ttu-id="1b633-165">Open the interactive shell and make sure that it is set to **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1b633-165">Open the interactive shell and make sure that it is set to **PowerShell**.</span></span>

    ![Install custom extension](./media/create-multiple-sites-portal/application-gateway-extension.png)

2. <span data-ttu-id="1b633-167">Run the following command to install IIS on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="1b633-167">Run the following command to install IIS on the virtual machine:</span></span> 

    ```azurepowershell-interactive
    $publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1");  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }
    Set-AzureRmVMExtension `
      -ResourceGroupName myResourceGroupAG `
      -Location eastus `
      -ExtensionName IIS `
      -VMName contosoVM `
      -Publisher Microsoft.Compute `
      -ExtensionType CustomScriptExtension `
      -TypeHandlerVersion 1.4 `
      -Settings $publicSettings
    ```

3. <span data-ttu-id="1b633-168">Create the second virtual machine and install IIS using the steps that you just finished.</span><span class="sxs-lookup"><span data-stu-id="1b633-168">Create the second virtual machine and install IIS using the steps that you just finished.</span></span> <span data-ttu-id="1b633-169">Enter the names of *fabrikamVM* for the name and for the value of VMName in Set-AzureRmVMExtension.</span><span class="sxs-lookup"><span data-stu-id="1b633-169">Enter the names of *fabrikamVM* for the name and for the value of VMName in Set-AzureRmVMExtension.</span></span>

## <a name="create-backend-pools-with-the-virtual-machines"></a><span data-ttu-id="1b633-170">Create backend pools with the virtual machines</span><span class="sxs-lookup"><span data-stu-id="1b633-170">Create backend pools with the virtual machines</span></span>

1. <span data-ttu-id="1b633-171">Click **All resources** and then click **myAppGateway**.</span><span class="sxs-lookup"><span data-stu-id="1b633-171">Click **All resources** and then click **myAppGateway**.</span></span>
2. <span data-ttu-id="1b633-172">Click **Backend pools**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1b633-172">Click **Backend pools**, and then click **Add**.</span></span>
3. <span data-ttu-id="1b633-173">Enter a name of *contosoPool* and add *contosoVM* using **Add target**.</span><span class="sxs-lookup"><span data-stu-id="1b633-173">Enter a name of *contosoPool* and add *contosoVM* using **Add target**.</span></span>

    ![Add backend servers](./media/create-multiple-sites-portal/application-gateway-multisite-backendpool.png)

4. <span data-ttu-id="1b633-175">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-175">Click **OK**.</span></span>
5. <span data-ttu-id="1b633-176">Click **Backend pools** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1b633-176">Click **Backend pools** and then click **Add**.</span></span>
6. <span data-ttu-id="1b633-177">Create the *fabrikamPool* with the *fabrikamVM* using the steps that you just finished.</span><span class="sxs-lookup"><span data-stu-id="1b633-177">Create the *fabrikamPool* with the *fabrikamVM* using the steps that you just finished.</span></span>

## <a name="create-backend-listeners"></a><span data-ttu-id="1b633-178">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="1b633-178">Create backend listeners</span></span>

1. <span data-ttu-id="1b633-179">Click **Listeners** and then click **Multi-site**.</span><span class="sxs-lookup"><span data-stu-id="1b633-179">Click **Listeners** and then click **Multi-site**.</span></span>
2. <span data-ttu-id="1b633-180">Enter these values for the listener:</span><span class="sxs-lookup"><span data-stu-id="1b633-180">Enter these values for the listener:</span></span>
    
    - <span data-ttu-id="1b633-181">*contosoListener* - for the name of the listener.</span><span class="sxs-lookup"><span data-stu-id="1b633-181">*contosoListener* - for the name of the listener.</span></span>
    - <span data-ttu-id="1b633-182">*www.contoso.com* - replace this host name example with your domain name.</span><span class="sxs-lookup"><span data-stu-id="1b633-182">*www.contoso.com* - replace this host name example with your domain name.</span></span>

3. <span data-ttu-id="1b633-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-183">Click **OK**.</span></span>
4. <span data-ttu-id="1b633-184">Create a second listener using the name of *fabrikamListener* and use your second domain name.</span><span class="sxs-lookup"><span data-stu-id="1b633-184">Create a second listener using the name of *fabrikamListener* and use your second domain name.</span></span> <span data-ttu-id="1b633-185">In this example, *www.fabrikam.com* is used.</span><span class="sxs-lookup"><span data-stu-id="1b633-185">In this example, *www.fabrikam.com* is used.</span></span>

## <a name="create-routing-rules"></a><span data-ttu-id="1b633-186">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="1b633-186">Create routing rules</span></span>

<span data-ttu-id="1b633-187">Rules are processed in the order they are listed, and traffic is directed using the first rule that matches regardless of specificity.</span><span class="sxs-lookup"><span data-stu-id="1b633-187">Rules are processed in the order they are listed, and traffic is directed using the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="1b633-188">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span><span class="sxs-lookup"><span data-stu-id="1b633-188">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 

<span data-ttu-id="1b633-189">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b633-189">In this example, you create two new rules and delete the default rule that was created when you created the application gateway.</span></span> 

1. <span data-ttu-id="1b633-190">Click **Rules** and then click **Basic**.</span><span class="sxs-lookup"><span data-stu-id="1b633-190">Click **Rules** and then click **Basic**.</span></span>
2. <span data-ttu-id="1b633-191">Enter *contosoRule* for the name.</span><span class="sxs-lookup"><span data-stu-id="1b633-191">Enter *contosoRule* for the name.</span></span>
3. <span data-ttu-id="1b633-192">Select *contosoListener* for the listener.</span><span class="sxs-lookup"><span data-stu-id="1b633-192">Select *contosoListener* for the listener.</span></span>
4. <span data-ttu-id="1b633-193">Select *contosoPool* for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="1b633-193">Select *contosoPool* for the backend pool.</span></span>

    ![Create a path-based rule](./media/create-multiple-sites-portal/application-gateway-multisite-rule.png)

5. <span data-ttu-id="1b633-195">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b633-195">Click **OK**.</span></span>
6. <span data-ttu-id="1b633-196">Create a second rule using the names of *fabrikamRule*, *fabrikamListener*, and *fabrikamPool*.</span><span class="sxs-lookup"><span data-stu-id="1b633-196">Create a second rule using the names of *fabrikamRule*, *fabrikamListener*, and *fabrikamPool*.</span></span>
7. <span data-ttu-id="1b633-197">Delete the default rule named *rule1* by clicking it, and then clicking **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1b633-197">Delete the default rule named *rule1* by clicking it, and then clicking **Delete**.</span></span>

## <a name="create-a-cname-record-in-your-domain"></a><span data-ttu-id="1b633-198">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1b633-198">Create a CNAME record in your domain</span></span>

<span data-ttu-id="1b633-199">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="1b633-199">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="1b633-200">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="1b633-200">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

1. <span data-ttu-id="1b633-201">Click **All resources**, and then click **myAGPublicIPAddress**.</span><span class="sxs-lookup"><span data-stu-id="1b633-201">Click **All resources**, and then click **myAGPublicIPAddress**.</span></span>

    ![Record application gateway DNS address](./media/create-multiple-sites-portal/application-gateway-multisite-dns.png)

2. <span data-ttu-id="1b633-203">Copy the DNS address and use it as the value for a new CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="1b633-203">Copy the DNS address and use it as the value for a new CNAME record in your domain.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="1b633-204">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="1b633-204">Test the application gateway</span></span>

1. <span data-ttu-id="1b633-205">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="1b633-205">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="1b633-206">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1b633-206">Such as, http://www.contoso.com.</span></span>

    ![Test contoso site in application gateway](./media/create-multiple-sites-portal/application-gateway-iistest.png)

2. <span data-ttu-id="1b633-208">Change the address to your other domain and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="1b633-208">Change the address to your other domain and you should see something like the following example:</span></span>

    ![Test fabrikam site in application gateway](./media/create-multiple-sites-portal/application-gateway-iistest2.png)

## <a name="next-steps"></a><span data-ttu-id="1b633-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b633-210">Next steps</span></span>

<span data-ttu-id="1b633-211">In this article, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="1b633-211">In this article, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b633-212">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1b633-212">Create an application gateway</span></span>
> * <span data-ttu-id="1b633-213">Create virtual machines for backend servers</span><span class="sxs-lookup"><span data-stu-id="1b633-213">Create virtual machines for backend servers</span></span>
> * <span data-ttu-id="1b633-214">Create backend pools with the backend servers</span><span class="sxs-lookup"><span data-stu-id="1b633-214">Create backend pools with the backend servers</span></span>
> * <span data-ttu-id="1b633-215">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="1b633-215">Create backend listeners</span></span>
> * <span data-ttu-id="1b633-216">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="1b633-216">Create routing rules</span></span>
> * <span data-ttu-id="1b633-217">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1b633-217">Create a CNAME record in your domain</span></span>
