---
title: Create a VM with multiple NICs - Azure PowerShell | Microsoft Docs
description: Learn how to create a VM with multiple NICs using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3a11afd8fbd6a5e6b94cf1ebee7ea20665421bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662051"
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="8e14b-103">Create a VM with multiple NICs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e14b-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-deploy-multinic-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-multinic-arm-cli.md)
> * [Template](virtual-network-deploy-multinic-arm-template.md)
> * [PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md)
> * [Azure CLI (Classic)](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).  This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="8e14b-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span><span class="sxs-lookup"><span data-stu-id="8e14b-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e14b-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e14b-112">Prerequisites</span></span>
<span data-ttu-id="8e14b-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span><span class="sxs-lookup"><span data-stu-id="8e14b-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="8e14b-114">To create these resources, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e14b-114">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="8e14b-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="8e14b-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="8e14b-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="8e14b-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span><span class="sxs-lookup"><span data-stu-id="8e14b-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> Make sure your storage account names are unique. You cannot have duplicate storage account names in Azure.
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="8e14b-120">Create the back-end VMs</span><span class="sxs-lookup"><span data-stu-id="8e14b-120">Create the back-end VMs</span></span>
<span data-ttu-id="8e14b-121">The back-end VMs depend on the creation of the following resources:</span><span class="sxs-lookup"><span data-stu-id="8e14b-121">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="8e14b-122">**Storage account for data disks**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-122">**Storage account for data disks**.</span></span> <span data-ttu-id="8e14b-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span><span class="sxs-lookup"><span data-stu-id="8e14b-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="8e14b-124">Make sure the Azure location you deploy to support premium storage.</span><span class="sxs-lookup"><span data-stu-id="8e14b-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="8e14b-125">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-125">**NICs**.</span></span> <span data-ttu-id="8e14b-126">Each VM will have two NICs, one for database access, and one for management.</span><span class="sxs-lookup"><span data-stu-id="8e14b-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="8e14b-127">**Availability set**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-127">**Availability set**.</span></span> <span data-ttu-id="8e14b-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e14b-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="8e14b-129">Step 1 - Start your script</span><span class="sxs-lookup"><span data-stu-id="8e14b-129">Step 1 - Start your script</span></span>
<span data-ttu-id="8e14b-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="8e14b-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="8e14b-131">Follow the steps below to change the script to work in your environment.</span><span class="sxs-lookup"><span data-stu-id="8e14b-131">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="8e14b-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="8e14b-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="8e14b-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span><span class="sxs-lookup"><span data-stu-id="8e14b-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="8e14b-134">Retrieve the existing resources needed for your deployment.</span><span class="sxs-lookup"><span data-stu-id="8e14b-134">Retrieve the existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="8e14b-135">Step 2 - Create necessary resources for your VMs</span><span class="sxs-lookup"><span data-stu-id="8e14b-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="8e14b-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span><span class="sxs-lookup"><span data-stu-id="8e14b-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="8e14b-137">You alos need the local administrator account credentials for each VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-137">You alos need the local administrator account credentials for each VM.</span></span> <span data-ttu-id="8e14b-138">To create these resources, execute the following steps.</span><span class="sxs-lookup"><span data-stu-id="8e14b-138">To create these resources, execute the following steps.</span></span>

1. <span data-ttu-id="8e14b-139">Create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="8e14b-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="8e14b-140">Create a new premium storage account in the resource group created above.</span><span class="sxs-lookup"><span data-stu-id="8e14b-140">Create a new premium storage account in the resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="8e14b-141">Create a new availability set.</span><span class="sxs-lookup"><span data-stu-id="8e14b-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="8e14b-142">Get the local administrator account credentials to be used for each VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-142">Get the local administrator account credentials to be used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="8e14b-143">Step 3 - Create the NICs and back-end VMs</span><span class="sxs-lookup"><span data-stu-id="8e14b-143">Step 3 - Create the NICs and back-end VMs</span></span>
<span data-ttu-id="8e14b-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span><span class="sxs-lookup"><span data-stu-id="8e14b-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="8e14b-145">To create the NICs and VMs, execute the following steps.</span><span class="sxs-lookup"><span data-stu-id="8e14b-145">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="8e14b-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="8e14b-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="8e14b-147">Create the NIC used for database access.</span><span class="sxs-lookup"><span data-stu-id="8e14b-147">Create the NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="8e14b-148">Create the NIC used for remote access.</span><span class="sxs-lookup"><span data-stu-id="8e14b-148">Create the NIC used for remote access.</span></span> <span data-ttu-id="8e14b-149">Notice how this NIC has an NSG associated to it.</span><span class="sxs-lookup"><span data-stu-id="8e14b-149">Notice how this NIC has an NSG associated to it.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="8e14b-150">Create `vmConfig` object.</span><span class="sxs-lookup"><span data-stu-id="8e14b-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="8e14b-151">Create two data disks per VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-151">Create two data disks per VM.</span></span> <span data-ttu-id="8e14b-152">Notice that the data disks are in the premium storage account created earlier.</span><span class="sxs-lookup"><span data-stu-id="8e14b-152">Notice that the data disks are in the premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="8e14b-153">Configure the operating system, and image to be used for the VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-153">Configure the operating system, and image to be used for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="8e14b-154">Add the two NICs created above to the `vmConfig` object.</span><span class="sxs-lookup"><span data-stu-id="8e14b-154">Add the two NICs created above to the `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="8e14b-155">Create the OS disk and create the VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-155">Create the OS disk and create the VM.</span></span> <span data-ttu-id="8e14b-156">Notice the `}` ending the `for` loop.</span><span class="sxs-lookup"><span data-stu-id="8e14b-156">Notice the `}` ending the `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="8e14b-157">Step 4 - Run the script</span><span class="sxs-lookup"><span data-stu-id="8e14b-157">Step 4 - Run the script</span></span>
<span data-ttu-id="8e14b-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="8e14b-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="8e14b-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="8e14b-160">You will see the initial output, as follows:</span><span class="sxs-lookup"><span data-stu-id="8e14b-160">You will see the initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="8e14b-161">After a few minutes, fill out the credentials prompt and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e14b-161">After a few minutes, fill out the credentials prompt and click **OK**.</span></span> <span data-ttu-id="8e14b-162">The output below represents a single VM.</span><span class="sxs-lookup"><span data-stu-id="8e14b-162">The output below represents a single VM.</span></span> <span data-ttu-id="8e14b-163">Notice the entire process took 8 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="8e14b-163">Notice the entire process took 8 minutes to complete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
