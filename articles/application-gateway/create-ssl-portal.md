---
title: Configure an application gateway with SSL termination - Azure portal | Microsoft Docs
description: Learn how to configure an application gateway and add a certificate for SSL termination using the Azure portal.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: article
ms.date: 5/15/2018
ms.author: victorh
ms.openlocfilehash: c64754595ef67b7c083ee8d47da5b412467c191b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866151"
---
# <a name="configure-an-application-gateway-with-ssl-termination-using-the-azure-portal"></a><span data-ttu-id="f9a77-103">Configure an application gateway with SSL termination using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f9a77-103">Configure an application gateway with SSL termination using the Azure portal</span></span>

<span data-ttu-id="f9a77-104">You can use the Azure portal to configure an [application gateway](overview.md) with a certificate for SSL termination that uses virtual machines for backend servers.</span><span class="sxs-lookup"><span data-stu-id="f9a77-104">You can use the Azure portal to configure an [application gateway](overview.md) with a certificate for SSL termination that uses virtual machines for backend servers.</span></span>

<span data-ttu-id="f9a77-105">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f9a77-105">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9a77-106">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f9a77-106">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f9a77-107">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f9a77-107">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f9a77-108">Create the virtual machines used as backend servers</span><span class="sxs-lookup"><span data-stu-id="f9a77-108">Create the virtual machines used as backend servers</span></span>

<span data-ttu-id="f9a77-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f9a77-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="f9a77-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f9a77-110">Log in to Azure</span></span>

<span data-ttu-id="f9a77-111">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f9a77-111">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f9a77-112">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f9a77-112">Create a self-signed certificate</span></span>

<span data-ttu-id="f9a77-113">In this section, you use [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate) to create a self-signed certificate that you upload to the Azure portal when you create the listener for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f9a77-113">In this section, you use [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate) to create a self-signed certificate that you upload to the Azure portal when you create the listener for the application gateway.</span></span>

<span data-ttu-id="f9a77-114">On your local computer, open a Windows PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f9a77-114">On your local computer, open a Windows PowerShell window as an administrator.</span></span> <span data-ttu-id="f9a77-115">Run the following command to create the certificate:</span><span class="sxs-lookup"><span data-stu-id="f9a77-115">Run the following command to create the certificate:</span></span>

```powershell
New-SelfSignedCertificate \
  -certstorelocation cert:\localmachine\my \
  -dnsname www.contoso.com
```

<span data-ttu-id="f9a77-116">You should see something like this response:</span><span class="sxs-lookup"><span data-stu-id="f9a77-116">You should see something like this response:</span></span>

```
PSParentPath: Microsoft.PowerShell.Security\Certificate::LocalMachine\my

Thumbprint                                Subject
----------                                -------
E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630  CN=www.contoso.com

Use [Export-PfxCertificate](https://docs.microsoft.com/powershell/module/pkiclient/export-pfxcertificate) with the Thumbprint that was returned to export a pfx file from the certificate:
```

```powershell
$pwd = ConvertTo-SecureString -String "Azure123456!" -Force -AsPlainText
Export-PfxCertificate \
  -cert cert:\localMachine\my\E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630 \
  -FilePath c:\appgwcert.pfx \
  -Password $pwd
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="f9a77-117">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="f9a77-117">Create an application gateway</span></span>

<span data-ttu-id="f9a77-118">A virtual network is needed for communication between the resources that you create.</span><span class="sxs-lookup"><span data-stu-id="f9a77-118">A virtual network is needed for communication between the resources that you create.</span></span> <span data-ttu-id="f9a77-119">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span><span class="sxs-lookup"><span data-stu-id="f9a77-119">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span></span> <span data-ttu-id="f9a77-120">You can create a virtual network at the same time that you create the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f9a77-120">You can create a virtual network at the same time that you create the application gateway.</span></span>

1. <span data-ttu-id="f9a77-121">Click **New** found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f9a77-121">Click **New** found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="f9a77-122">Select **Networking** and then select **Application Gateway** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="f9a77-122">Select **Networking** and then select **Application Gateway** in the Featured list.</span></span>
3. <span data-ttu-id="f9a77-123">Enter *myAppGateway* for the name of the application gateway and *myResourceGroupAG* for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="f9a77-123">Enter *myAppGateway* for the name of the application gateway and *myResourceGroupAG* for the new resource group.</span></span>
4. <span data-ttu-id="f9a77-124">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-124">Accept the default values for the other settings and then click **OK**.</span></span>
5. <span data-ttu-id="f9a77-125">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="f9a77-125">Click **Choose a virtual network**, click **Create new**, and then enter these values for the virtual network:</span></span>

    - <span data-ttu-id="f9a77-126">*myVNet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="f9a77-126">*myVNet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="f9a77-127">*10.0.0.0/16* - for the virtual network address space.</span><span class="sxs-lookup"><span data-stu-id="f9a77-127">*10.0.0.0/16* - for the virtual network address space.</span></span>
    - <span data-ttu-id="f9a77-128">*myAGSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="f9a77-128">*myAGSubnet* - for the subnet name.</span></span>
    - <span data-ttu-id="f9a77-129">*10.0.0.0/24* - for the subnet address space.</span><span class="sxs-lookup"><span data-stu-id="f9a77-129">*10.0.0.0/24* - for the subnet address space.</span></span>

    ![Create virtual network](./media/create-ssl-portal/application-gateway-vnet.png)

6. <span data-ttu-id="f9a77-131">Click **OK** to create the virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="f9a77-131">Click **OK** to create the virtual network and subnet.</span></span>
7. <span data-ttu-id="f9a77-132">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span><span class="sxs-lookup"><span data-stu-id="f9a77-132">Click **Choose a public IP address**, click **Create new**, and then enter the name of the public IP address.</span></span> <span data-ttu-id="f9a77-133">In this example, the public IP address is named *myAGPublicIPAddress*.</span><span class="sxs-lookup"><span data-stu-id="f9a77-133">In this example, the public IP address is named *myAGPublicIPAddress*.</span></span> <span data-ttu-id="f9a77-134">Accept the default values for the other settings and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-134">Accept the default values for the other settings and then click **OK**.</span></span>
8. <span data-ttu-id="f9a77-135">Click **HTTPS** for the protocol of the listener and make sure that the port is defined as **443**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-135">Click **HTTPS** for the protocol of the listener and make sure that the port is defined as **443**.</span></span>
9. <span data-ttu-id="f9a77-136">Click the folder icon and browse to the *appgwcert.pfx* certificate that you previously created to upload it.</span><span class="sxs-lookup"><span data-stu-id="f9a77-136">Click the folder icon and browse to the *appgwcert.pfx* certificate that you previously created to upload it.</span></span>
10. <span data-ttu-id="f9a77-137">Enter *mycert1* for the name of the certificate and *Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="f9a77-137">Enter *mycert1* for the name of the certificate and *Azure123456!*</span></span> <span data-ttu-id="f9a77-138">for the password, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-138">for the password, and then click **OK**.</span></span>

    ![Create new application gateway](./media/create-ssl-portal/application-gateway-create.png)

11. <span data-ttu-id="f9a77-140">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f9a77-140">Review the settings on the summary page, and then click **OK** to create the network resources and the application gateway.</span></span> <span data-ttu-id="f9a77-141">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span><span class="sxs-lookup"><span data-stu-id="f9a77-141">It may take several minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span></span>

### <a name="add-a-subnet"></a><span data-ttu-id="f9a77-142">Add a subnet</span><span class="sxs-lookup"><span data-stu-id="f9a77-142">Add a subnet</span></span>

1. <span data-ttu-id="f9a77-143">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="f9a77-143">Click **All resources** in the left-hand menu, and then click **myVNet** from the resources list.</span></span>
2. <span data-ttu-id="f9a77-144">Click **Subnets**, and then click **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-144">Click **Subnets**, and then click **Subnet**.</span></span>

    ![Create subnet](./media/create-ssl-portal/application-gateway-subnet.png)

3. <span data-ttu-id="f9a77-146">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-146">Enter *myBackendSubnet* for the name of the subnet and then click **OK**.</span></span>

## <a name="create-backend-servers"></a><span data-ttu-id="f9a77-147">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="f9a77-147">Create backend servers</span></span>

<span data-ttu-id="f9a77-148">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f9a77-148">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span></span> <span data-ttu-id="f9a77-149">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="f9a77-149">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="f9a77-150">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="f9a77-150">Create a virtual machine</span></span>

1. <span data-ttu-id="f9a77-151">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-151">Click **New**.</span></span>
2. <span data-ttu-id="f9a77-152">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span><span class="sxs-lookup"><span data-stu-id="f9a77-152">Click **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.</span></span>
3. <span data-ttu-id="f9a77-153">Enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="f9a77-153">Enter these values for the virtual machine:</span></span>

    - <span data-ttu-id="f9a77-154">*myVM* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f9a77-154">*myVM* - for the name of the virtual machine.</span></span>
    - <span data-ttu-id="f9a77-155">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="f9a77-155">*azureuser* - for the administrator user name.</span></span>
    - <span data-ttu-id="f9a77-156">*Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="f9a77-156">*Azure123456!*</span></span> <span data-ttu-id="f9a77-157">for the password.</span><span class="sxs-lookup"><span data-stu-id="f9a77-157">for the password.</span></span>
    - <span data-ttu-id="f9a77-158">Select **Use existing**, and then select *myResourceGroupAG*.</span><span class="sxs-lookup"><span data-stu-id="f9a77-158">Select **Use existing**, and then select *myResourceGroupAG*.</span></span>

4. <span data-ttu-id="f9a77-159">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-159">Click **OK**.</span></span>
5. <span data-ttu-id="f9a77-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
6. <span data-ttu-id="f9a77-161">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-161">Make sure that **myVNet** is selected for the virtual network and the subnet is **myBackendSubnet**.</span></span> 
7. <span data-ttu-id="f9a77-162">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f9a77-162">Click **Disabled** to disable boot diagnostics.</span></span>
8. <span data-ttu-id="f9a77-163">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-163">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>

### <a name="install-iis"></a><span data-ttu-id="f9a77-164">Install IIS</span><span class="sxs-lookup"><span data-stu-id="f9a77-164">Install IIS</span></span>

1. <span data-ttu-id="f9a77-165">Open the interactive shell and make sure that it is set to **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-165">Open the interactive shell and make sure that it is set to **PowerShell**.</span></span>

    ![Install custom extension](./media/create-ssl-portal/application-gateway-extension.png)

2. <span data-ttu-id="f9a77-167">Run the following command to install IIS on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="f9a77-167">Run the following command to install IIS on the virtual machine:</span></span> 

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

3. <span data-ttu-id="f9a77-168">Create a second virtual machine and install IIS using the steps that you just finished.</span><span class="sxs-lookup"><span data-stu-id="f9a77-168">Create a second virtual machine and install IIS using the steps that you just finished.</span></span> <span data-ttu-id="f9a77-169">Enter *myVM2* for its name and for VMName in Set-AzureRmVMExtension.</span><span class="sxs-lookup"><span data-stu-id="f9a77-169">Enter *myVM2* for its name and for VMName in Set-AzureRmVMExtension.</span></span>

### <a name="add-backend-servers"></a><span data-ttu-id="f9a77-170">Add backend servers</span><span class="sxs-lookup"><span data-stu-id="f9a77-170">Add backend servers</span></span>

3. <span data-ttu-id="f9a77-171">Click **All resources**, and then click **myAppGateway**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-171">Click **All resources**, and then click **myAppGateway**.</span></span>
4. <span data-ttu-id="f9a77-172">Click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-172">Click **Backend pools**.</span></span> <span data-ttu-id="f9a77-173">A default pool was automatically created with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f9a77-173">A default pool was automatically created with the application gateway.</span></span> <span data-ttu-id="f9a77-174">Click **appGateayBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-174">Click **appGateayBackendPool**.</span></span>
5. <span data-ttu-id="f9a77-175">Click **Add target** to add each virtual machine that you created to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="f9a77-175">Click **Add target** to add each virtual machine that you created to the backend pool.</span></span>

    ![Add backend servers](./media/create-ssl-portal/application-gateway-backend.png)

6. <span data-ttu-id="f9a77-177">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-177">Click **Save**.</span></span>

## <a name="test-the-application-gateway"></a><span data-ttu-id="f9a77-178">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="f9a77-178">Test the application gateway</span></span>

1. <span data-ttu-id="f9a77-179">Click **All resources**, and then click **myAGPublicIPAddress**.</span><span class="sxs-lookup"><span data-stu-id="f9a77-179">Click **All resources**, and then click **myAGPublicIPAddress**.</span></span>

    ![Record application gateway public IP address](./media/create-ssl-portal/application-gateway-ag-address.png)

2. <span data-ttu-id="f9a77-181">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="f9a77-181">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="f9a77-182">To accept the security warning if you used a self-signed certificate, select Details and then Go on to the webpage:</span><span class="sxs-lookup"><span data-stu-id="f9a77-182">To accept the security warning if you used a self-signed certificate, select Details and then Go on to the webpage:</span></span>

    ![Secure warning](./media/create-ssl-portal/application-gateway-secure.png)

    <span data-ttu-id="f9a77-184">Your secured IIS website is then displayed as in the following example:</span><span class="sxs-lookup"><span data-stu-id="f9a77-184">Your secured IIS website is then displayed as in the following example:</span></span>

    ![Test base URL in application gateway](./media/create-ssl-portal/application-gateway-iistest.png)

## <a name="next-steps"></a><span data-ttu-id="f9a77-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9a77-186">Next steps</span></span>

<span data-ttu-id="f9a77-187">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f9a77-187">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9a77-188">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f9a77-188">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f9a77-189">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f9a77-189">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f9a77-190">Create the virtual machines used as backend servers</span><span class="sxs-lookup"><span data-stu-id="f9a77-190">Create the virtual machines used as backend servers</span></span>

<span data-ttu-id="f9a77-191">To learn more about application gateways and their associated resources, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="f9a77-191">To learn more about application gateways and their associated resources, continue to the how-to articles.</span></span>