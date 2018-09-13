---
title: Create a VM (Classic) with multiple NICs - Azure PowerShell | Microsoft Docs
description: Learn how to create a VM (Classic) with multiple NICs using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6e2bb0e228aa28c79969cba07352061abbb47951
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670551"
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="d14ad-103">Create a VM (Classic) with multiple NICs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d14ad-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="d14ad-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span><span class="sxs-lookup"><span data-stu-id="d14ad-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="d14ad-105">Multiple NICs enable separation of traffic types across NICs.</span><span class="sxs-lookup"><span data-stu-id="d14ad-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="d14ad-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="d14ad-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="d14ad-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span><span class="sxs-lookup"><span data-stu-id="d14ad-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d14ad-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d14ad-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d14ad-109">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="d14ad-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="d14ad-110">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="d14ad-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d14ad-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d14ad-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="d14ad-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span><span class="sxs-lookup"><span data-stu-id="d14ad-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d14ad-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d14ad-113">Prerequisites</span></span>

<span data-ttu-id="d14ad-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span><span class="sxs-lookup"><span data-stu-id="d14ad-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="d14ad-115">To create these resources, complete the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="d14ad-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="d14ad-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span><span class="sxs-lookup"><span data-stu-id="d14ad-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="d14ad-117">Create the back-end VMs</span><span class="sxs-lookup"><span data-stu-id="d14ad-117">Create the back-end VMs</span></span>
<span data-ttu-id="d14ad-118">The back-end VMs depend on the creation of the following resources:</span><span class="sxs-lookup"><span data-stu-id="d14ad-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="d14ad-119">**Backend subnet**.</span><span class="sxs-lookup"><span data-stu-id="d14ad-119">**Backend subnet**.</span></span> <span data-ttu-id="d14ad-120">The database servers will be part of a separate subnet, to segregate traffic.</span><span class="sxs-lookup"><span data-stu-id="d14ad-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="d14ad-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="d14ad-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="d14ad-122">**Storage account for data disks**.</span><span class="sxs-lookup"><span data-stu-id="d14ad-122">**Storage account for data disks**.</span></span> <span data-ttu-id="d14ad-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span><span class="sxs-lookup"><span data-stu-id="d14ad-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="d14ad-124">Make sure the Azure location you deploy to support premium storage.</span><span class="sxs-lookup"><span data-stu-id="d14ad-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="d14ad-125">**Availability set**.</span><span class="sxs-lookup"><span data-stu-id="d14ad-125">**Availability set**.</span></span> <span data-ttu-id="d14ad-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span><span class="sxs-lookup"><span data-stu-id="d14ad-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="d14ad-127">Step 1 - Start your script</span><span class="sxs-lookup"><span data-stu-id="d14ad-127">Step 1 - Start your script</span></span>
<span data-ttu-id="d14ad-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="d14ad-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="d14ad-129">Follow the steps below to change the script to work in your environment.</span><span class="sxs-lookup"><span data-stu-id="d14ad-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="d14ad-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="d14ad-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="d14ad-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span><span class="sxs-lookup"><span data-stu-id="d14ad-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="d14ad-132">Step 2 - Create necessary resources for your VMs</span><span class="sxs-lookup"><span data-stu-id="d14ad-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="d14ad-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span><span class="sxs-lookup"><span data-stu-id="d14ad-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="d14ad-134">You also need to specify an image, and a local administrator account for the VMs.</span><span class="sxs-lookup"><span data-stu-id="d14ad-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="d14ad-135">To create these resources, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="d14ad-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="d14ad-136">Create a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="d14ad-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="d14ad-137">Create a new premium storage account.</span><span class="sxs-lookup"><span data-stu-id="d14ad-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="d14ad-138">Set the storage account created above as the current storage account for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d14ad-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="d14ad-139">Select an image for the VM.</span><span class="sxs-lookup"><span data-stu-id="d14ad-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="d14ad-140">Set the local administrator account credentials.</span><span class="sxs-lookup"><span data-stu-id="d14ad-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="d14ad-141">Step 3 - Create VMs</span><span class="sxs-lookup"><span data-stu-id="d14ad-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="d14ad-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span><span class="sxs-lookup"><span data-stu-id="d14ad-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="d14ad-143">To create the NICs and VMs, execute the following steps.</span><span class="sxs-lookup"><span data-stu-id="d14ad-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="d14ad-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="d14ad-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="d14ad-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span><span class="sxs-lookup"><span data-stu-id="d14ad-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="d14ad-146">Provision the VM as a Windows VM.</span><span class="sxs-lookup"><span data-stu-id="d14ad-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.Password
    ```

4. <span data-ttu-id="d14ad-147">Set the default NIC and assign it a static IP address.</span><span class="sxs-lookup"><span data-stu-id="d14ad-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="d14ad-148">Add a second NIC for each VM.</span><span class="sxs-lookup"><span data-stu-id="d14ad-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="d14ad-149">Create to data disks for each VM.</span><span class="sxs-lookup"><span data-stu-id="d14ad-149">Create to data disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="d14ad-150">Create each VM, and end the loop.</span><span class="sxs-lookup"><span data-stu-id="d14ad-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="d14ad-151">Step 4 - Run the script</span><span class="sxs-lookup"><span data-stu-id="d14ad-151">Step 4 - Run the script</span></span>
<span data-ttu-id="d14ad-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="d14ad-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="d14ad-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="d14ad-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="d14ad-154">You will see the initial output, as shown below.</span><span class="sxs-lookup"><span data-stu-id="d14ad-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="d14ad-155">Fill out the information needed in the credentials prompt and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d14ad-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="d14ad-156">The output below is returned.</span><span class="sxs-lookup"><span data-stu-id="d14ad-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
