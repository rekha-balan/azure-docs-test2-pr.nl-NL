---
title: Tools for Azure Stack storage | Microsoft Docs
description: Learn about Azure Stack storage data transfer tools
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2018
ms.author: mabrigg
ms.reviewer: xiaofmao
ms.openlocfilehash: 91ba9b388566cc72f3024943005af499b7c3f3ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865470"
---
# <a name="use-data-transfer-tools-for-azure-stack-storage"></a><span data-ttu-id="513f7-103">Use data transfer tools for Azure Stack storage</span><span class="sxs-lookup"><span data-stu-id="513f7-103">Use data transfer tools for Azure Stack storage</span></span>

<span data-ttu-id="513f7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="513f7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="513f7-105">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functions.</span><span class="sxs-lookup"><span data-stu-id="513f7-105">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functions.</span></span> <span data-ttu-id="513f7-106">You can use a set of Azure storage tools if you want to manage or move data to or from Azure Stack storage.</span><span class="sxs-lookup"><span data-stu-id="513f7-106">You can use a set of Azure storage tools if you want to manage or move data to or from Azure Stack storage.</span></span> <span data-ttu-id="513f7-107">This article provides an  overview of the available tools.</span><span class="sxs-lookup"><span data-stu-id="513f7-107">This article provides an  overview of the available tools.</span></span>

<span data-ttu-id="513f7-108">Your requirements determine which of the following tools works best for you:</span><span class="sxs-lookup"><span data-stu-id="513f7-108">Your requirements determine which of the following tools works best for you:</span></span>

* [<span data-ttu-id="513f7-109">AzCopy</span><span class="sxs-lookup"><span data-stu-id="513f7-109">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="513f7-110">A storage-specific, command-line utility that you can download to copy data from one object to another object within your storage account, or between storage accounts.</span><span class="sxs-lookup"><span data-stu-id="513f7-110">A storage-specific, command-line utility that you can download to copy data from one object to another object within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="513f7-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="513f7-111">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="513f7-112">A task-based, command-line shell and scripting language designed especially for system administration.</span><span class="sxs-lookup"><span data-stu-id="513f7-112">A task-based, command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="513f7-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="513f7-113">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="513f7-114">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span><span class="sxs-lookup"><span data-stu-id="513f7-114">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="513f7-115">Microsoft storage explorer</span><span class="sxs-lookup"><span data-stu-id="513f7-115">Microsoft storage explorer</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="513f7-116">An easy-to-use stand-alone app with a user interface.</span><span class="sxs-lookup"><span data-stu-id="513f7-116">An easy-to-use stand-alone app with a user interface.</span></span>

* [<span data-ttu-id="513f7-117">Blobfuse </span><span class="sxs-lookup"><span data-stu-id="513f7-117">Blobfuse </span></span>](#blobfuse)

    <span data-ttu-id="513f7-118">A virtual file system driver for Azure Blob Storage, which allows you to access your existing block blob data in your Storage account through the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="513f7-118">A virtual file system driver for Azure Blob Storage, which allows you to access your existing block blob data in your Storage account through the Linux file system.</span></span> 

<span data-ttu-id="513f7-119">Due to the storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="513f7-119">Due to the storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span></span> <span data-ttu-id="513f7-120">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack storage: Differences and considerations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-120">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azcopy"></a><span data-ttu-id="513f7-121">AzCopy</span><span class="sxs-lookup"><span data-stu-id="513f7-121">AzCopy</span></span>

<span data-ttu-id="513f7-122">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure blob and table storage using simple commands with optimal performance.</span><span class="sxs-lookup"><span data-stu-id="513f7-122">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure blob and table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="513f7-123">You can copy data from one object to another within your storage account, or between storage accounts.</span><span class="sxs-lookup"><span data-stu-id="513f7-123">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

### <a name="download-and-install-azcopy"></a><span data-ttu-id="513f7-124">Download and install AzCopy</span><span class="sxs-lookup"><span data-stu-id="513f7-124">Download and install AzCopy</span></span>

<span data-ttu-id="513f7-125">There are two versions of the AzCopy utility: AzCopy on Windows and AzCopy on Linux.</span><span class="sxs-lookup"><span data-stu-id="513f7-125">There are two versions of the AzCopy utility: AzCopy on Windows and AzCopy on Linux.</span></span>

 - <span data-ttu-id="513f7-126">**AzCopy on Windows**</span><span class="sxs-lookup"><span data-stu-id="513f7-126">**AzCopy on Windows**</span></span>
    - <span data-ttu-id="513f7-127">Download the supported version of AzCopy for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-127">Download the supported version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="513f7-128">You can install and use AzCopy on Azure Stack the same way as Azure.</span><span class="sxs-lookup"><span data-stu-id="513f7-128">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="513f7-129">To learn more, see [AzCopy on Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="513f7-129">To learn more, see [AzCopy on Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy).</span></span>
        - <span data-ttu-id="513f7-130">For the 1802 update, or newer versions, [download AzCopy 7.1.0](https://aka.ms/azcopyforazurestack20170417).</span><span class="sxs-lookup"><span data-stu-id="513f7-130">For the 1802 update, or newer versions, [download AzCopy 7.1.0](https://aka.ms/azcopyforazurestack20170417).</span></span>
        - <span data-ttu-id="513f7-131">For previous versions, [download AzCopy 5.0.0](https://aka.ms/azcopyforazurestack20170417).</span><span class="sxs-lookup"><span data-stu-id="513f7-131">For previous versions, [download AzCopy 5.0.0](https://aka.ms/azcopyforazurestack20170417).</span></span>

 - <span data-ttu-id="513f7-132">**AzCopy on Linux**</span><span class="sxs-lookup"><span data-stu-id="513f7-132">**AzCopy on Linux**</span></span>

    - <span data-ttu-id="513f7-133">AzCopy on Linux supports Azure Stack 1802 update or newer versions.</span><span class="sxs-lookup"><span data-stu-id="513f7-133">AzCopy on Linux supports Azure Stack 1802 update or newer versions.</span></span> <span data-ttu-id="513f7-134">You can install and use AzCopy on Azure Stack the same way as Azure.</span><span class="sxs-lookup"><span data-stu-id="513f7-134">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="513f7-135">To learn more, see [AzCopy on Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux).</span><span class="sxs-lookup"><span data-stu-id="513f7-135">To learn more, see [AzCopy on Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux).</span></span>

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="513f7-136">AzCopy command examples for data transfer</span><span class="sxs-lookup"><span data-stu-id="513f7-136">AzCopy command examples for data transfer</span></span>

<span data-ttu-id="513f7-137">The following examples follow typical scenarios for copying data to and from Azure Stack blobs.</span><span class="sxs-lookup"><span data-stu-id="513f7-137">The following examples follow typical scenarios for copying data to and from Azure Stack blobs.</span></span> <span data-ttu-id="513f7-138">To learn more, see [AzCopy on Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux) and [AzCopy on Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux).</span><span class="sxs-lookup"><span data-stu-id="513f7-138">To learn more, see [AzCopy on Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux) and [AzCopy on Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux).</span></span>

### <a name="download-all-blobs-to-a-local-disk"></a><span data-ttu-id="513f7-139">Download all blobs to a local disk</span><span class="sxs-lookup"><span data-stu-id="513f7-139">Download all blobs to a local disk</span></span>

<span data-ttu-id="513f7-140">**Windows**</span><span class="sxs-lookup"><span data-stu-id="513f7-140">**Windows**</span></span>

````AzCopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
````

<span data-ttu-id="513f7-141">**Linux**</span><span class="sxs-lookup"><span data-stu-id="513f7-141">**Linux**</span></span>

````AzCopy
azcopy \
    --source https://myaccount.blob.local.azurestack.external/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
````

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="513f7-142">Upload single file to virtual directory</span><span class="sxs-lookup"><span data-stu-id="513f7-142">Upload single file to virtual directory</span></span>

<span data-ttu-id="513f7-143">**Windows**</span><span class="sxs-lookup"><span data-stu-id="513f7-143">**Windows**</span></span>

```AzCopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="513f7-144">**Linux**</span><span class="sxs-lookup"><span data-stu-id="513f7-144">**Linux**</span></span>

````AzCopy
azcopy \
    --source /mnt/myfiles/abc.txt \
    --destination https://myaccount.blob.local.azurestack.external/mycontainer/vd/abc.txt \
    --dest-key <key>
````

### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="513f7-145">Move data between Azure and Azure Stack storage</span><span class="sxs-lookup"><span data-stu-id="513f7-145">Move data between Azure and Azure Stack storage</span></span>

<span data-ttu-id="513f7-146">Asynchronous data transfer between Azure storage and Azure Stack is not supported.</span><span class="sxs-lookup"><span data-stu-id="513f7-146">Asynchronous data transfer between Azure storage and Azure Stack is not supported.</span></span> <span data-ttu-id="513f7-147">You need to specify the transfer with the **/SyncCopy** or **--sync-copy** option.</span><span class="sxs-lookup"><span data-stu-id="513f7-147">You need to specify the transfer with the **/SyncCopy** or **--sync-copy** option.</span></span>

<span data-ttu-id="513f7-148">**Windows**</span><span class="sxs-lookup"><span data-stu-id="513f7-148">**Windows**</span></span>

````AzCopy
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
````

<span data-ttu-id="513f7-149">**Linux**</span><span class="sxs-lookup"><span data-stu-id="513f7-149">**Linux**</span></span>

````AzCopy
azcopy \
    --source https://myaccount1.blob.local.azurestack.external/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --sync-copy
````

### <a name="azcopy-known-issues"></a><span data-ttu-id="513f7-150">Azcopy known issues</span><span class="sxs-lookup"><span data-stu-id="513f7-150">Azcopy known issues</span></span>

 - <span data-ttu-id="513f7-151">Any AzCopy operation on a file store is not available because file storage is not yet available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-151">Any AzCopy operation on a file store is not available because file storage is not yet available in Azure Stack.</span></span>
 - <span data-ttu-id="513f7-152">Asynchronous data transfer between Azure storage and Azure Stack is not supported.</span><span class="sxs-lookup"><span data-stu-id="513f7-152">Asynchronous data transfer between Azure storage and Azure Stack is not supported.</span></span> <span data-ttu-id="513f7-153">You can specify the transfer with the **/SyncCopy** option to copy the data.</span><span class="sxs-lookup"><span data-stu-id="513f7-153">You can specify the transfer with the **/SyncCopy** option to copy the data.</span></span>
 - <span data-ttu-id="513f7-154">The Linux version of Azcopy only supports 1802 update or later versions.</span><span class="sxs-lookup"><span data-stu-id="513f7-154">The Linux version of Azcopy only supports 1802 update or later versions.</span></span> <span data-ttu-id="513f7-155">And it doesn’t support Table service.</span><span class="sxs-lookup"><span data-stu-id="513f7-155">And it doesn’t support Table service.</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="513f7-156">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="513f7-156">Azure PowerShell</span></span>

<span data-ttu-id="513f7-157">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-157">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="513f7-158">It's a task-based, command-line shell and scripting language designed especially for system administration.</span><span class="sxs-lookup"><span data-stu-id="513f7-158">It's a task-based, command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="513f7-159">Install and Configure PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="513f7-159">Install and Configure PowerShell for Azure Stack</span></span>

<span data-ttu-id="513f7-160">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-160">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="513f7-161">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span><span class="sxs-lookup"><span data-stu-id="513f7-161">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="513f7-162">PowerShell Sample script for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="513f7-162">PowerShell Sample script for Azure Stack</span></span> 

<span data-ttu-id="513f7-163">This sample assume you have successfully [Installed PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-163">This sample assume you have successfully [Installed PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="513f7-164">This script will help you complete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environment.</span><span class="sxs-lookup"><span data-stu-id="513f7-164">This script will help you complete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environment.</span></span> <span data-ttu-id="513f7-165">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account, and upload an existing image file (blob) to that container.</span><span class="sxs-lookup"><span data-stu-id="513f7-165">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account, and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="513f7-166">After the script lists all blobs in that container, it will create a new destination directory on your local computer and download the image file.</span><span class="sxs-lookup"><span data-stu-id="513f7-166">After the script lists all blobs in that container, it will create a new destination directory on your local computer and download the image file.</span></span>

1. <span data-ttu-id="513f7-167">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-167">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>
2. <span data-ttu-id="513f7-168">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-168">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>
3. <span data-ttu-id="513f7-169">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span><span class="sxs-lookup"><span data-stu-id="513f7-169">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="513f7-170">Copy the script below and paste to the new script file.</span><span class="sxs-lookup"><span data-stu-id="513f7-170">Copy the script below and paste to the new script file.</span></span>
5. <span data-ttu-id="513f7-171">Update the script variables based on your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="513f7-171">Update the script variables based on your configuration settings.</span></span>
   > [!NOTE]
   > <span data-ttu-id="513f7-172">This script has to be run at the root directory for **AzureStack_Tools**.</span><span class="sxs-lookup"><span data-stu-id="513f7-172">This script has to be run at the root directory for **AzureStack_Tools**.</span></span>

```PowerShell  
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with the name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name to your new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name to your new storage account. It must be lowercase.
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name to your new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import the Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure the PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set the GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudience

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Add-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from the container:
# Get a reference to a list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create the destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into the local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
````

### <a name="powershell-known-issues"></a><span data-ttu-id="513f7-173">PowerShell known issues</span><span class="sxs-lookup"><span data-stu-id="513f7-173">PowerShell known issues</span></span>

<span data-ttu-id="513f7-174">The current compatible Azure PowerShell module version for Azure Stack is 1.2.11 for the user operations.</span><span class="sxs-lookup"><span data-stu-id="513f7-174">The current compatible Azure PowerShell module version for Azure Stack is 1.2.11 for the user operations.</span></span> <span data-ttu-id="513f7-175">It’s different from the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="513f7-175">It’s different from the latest version of Azure PowerShell.</span></span> <span data-ttu-id="513f7-176">This difference impacts storage services operation:</span><span class="sxs-lookup"><span data-stu-id="513f7-176">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="513f7-177">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.11 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span><span class="sxs-lookup"><span data-stu-id="513f7-177">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.11 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span></span>

   ```
   # This command gets a specific key for a storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```

   <span data-ttu-id="513f7-178">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="513f7-178">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="513f7-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="513f7-179">Azure CLI</span></span>

<span data-ttu-id="513f7-180">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span><span class="sxs-lookup"><span data-stu-id="513f7-180">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="513f7-181">You can install it on macOS, Linux, and Windows and run it from the command line.</span><span class="sxs-lookup"><span data-stu-id="513f7-181">You can install it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="513f7-182">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="513f7-182">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span> <span data-ttu-id="513f7-183">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span><span class="sxs-lookup"><span data-stu-id="513f7-183">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="513f7-184">Azure Stack requires Azure CLI version 2.0.</span><span class="sxs-lookup"><span data-stu-id="513f7-184">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="513f7-185">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-version-profiles-azurecli2.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-185">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-version-profiles-azurecli2.md).</span></span> <span data-ttu-id="513f7-186">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack storage account, see [Using the Azure CLI2.0 with Azure storage](../../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="513f7-186">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack storage account, see [Using the Azure CLI2.0 with Azure storage](../../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="513f7-187">Azure CLI sample script for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="513f7-187">Azure CLI sample script for Azure Stack</span></span>

<span data-ttu-id="513f7-188">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack storage resources.</span><span class="sxs-lookup"><span data-stu-id="513f7-188">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack storage resources.</span></span> <span data-ttu-id="513f7-189">The script completes the following actions:</span><span class="sxs-lookup"><span data-stu-id="513f7-189">The script completes the following actions:</span></span>

* <span data-ttu-id="513f7-190">Creates a new container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="513f7-190">Creates a new container in your storage account.</span></span>
* <span data-ttu-id="513f7-191">Uploads an existing file (as a blob) to the container.</span><span class="sxs-lookup"><span data-stu-id="513f7-191">Uploads an existing file (as a blob) to the container.</span></span>
* <span data-ttu-id="513f7-192">Lists all blobs in the container.</span><span class="sxs-lookup"><span data-stu-id="513f7-192">Lists all blobs in the container.</span></span>
* <span data-ttu-id="513f7-193">Downloads the file to a destination on your local computer that you specify.</span><span class="sxs-lookup"><span data-stu-id="513f7-193">Downloads the file to a destination on your local computer that you specify.</span></span>

<span data-ttu-id="513f7-194">Before you run this script, make sure that you can successfully connect to, and sign in to the target Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-194">Before you run this script, make sure that you can successfully connect to, and sign in to the target Azure Stack.</span></span>

1. <span data-ttu-id="513f7-195">Open your favorite text editor, then copy and paste the preceding script into the editor.</span><span class="sxs-lookup"><span data-stu-id="513f7-195">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>
2. <span data-ttu-id="513f7-196">Update the script's variables to reflect your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="513f7-196">Update the script's variables to reflect your configuration settings.</span></span>
3. <span data-ttu-id="513f7-197">After you've updated the necessary variables, save the script, and exit your editor.</span><span class="sxs-lookup"><span data-stu-id="513f7-197">After you've updated the necessary variables, save the script, and exit your editor.</span></span> <span data-ttu-id="513f7-198">The next steps assume you've named your script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="513f7-198">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>
4. <span data-ttu-id="513f7-199">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="513f7-199">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="513f7-200">Execute the script.</span><span class="sxs-lookup"><span data-stu-id="513f7-200">Execute the script.</span></span> <span data-ttu-id="513f7-201">For example, in Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="513f7-201">For example, in Bash: `./my_storage_sample.sh`</span></span>

```bash
#!/bin/bash
# A simple Azure Stack storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating the resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating the storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating the blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading the file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing the blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading the file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
````

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="513f7-202">Microsoft Azure storage explorer</span><span class="sxs-lookup"><span data-stu-id="513f7-202">Microsoft Azure storage explorer</span></span>

<span data-ttu-id="513f7-203">Microsoft Azure storage explorer is a standalone app from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="513f7-203">Microsoft Azure storage explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="513f7-204">It allows you to easily work with both Azure storage and Azure Stack storage data on Windows, macOS and Linux computers.</span><span class="sxs-lookup"><span data-stu-id="513f7-204">It allows you to easily work with both Azure storage and Azure Stack storage data on Windows, macOS and Linux computers.</span></span> <span data-ttu-id="513f7-205">If you want an easy way to manage your Azure Stack storage data, then consider using Microsoft Azure storage explorer.</span><span class="sxs-lookup"><span data-stu-id="513f7-205">If you want an easy way to manage your Azure Stack storage data, then consider using Microsoft Azure storage explorer.</span></span>

* <span data-ttu-id="513f7-206">To learn more about configuring Azure storage explorer to work with Azure Stack, see [Connect storage explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="513f7-206">To learn more about configuring Azure storage explorer to work with Azure Stack, see [Connect storage explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>
* <span data-ttu-id="513f7-207">To learn more about Microsoft Azure storage explorer, see [Get started with storage explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="513f7-207">To learn more about Microsoft Azure storage explorer, see [Get started with storage explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="blobfuse"></a><span data-ttu-id="513f7-208">Blobfuse</span><span class="sxs-lookup"><span data-stu-id="513f7-208">Blobfuse</span></span> 

<span data-ttu-id="513f7-209">[Blobfuse](https://github.com/Azure/azure-storage-fuse) is a virtual file system driver for Azure Blob Storage, which allows you to access your existing block blob data in your Storage account through the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="513f7-209">[Blobfuse](https://github.com/Azure/azure-storage-fuse) is a virtual file system driver for Azure Blob Storage, which allows you to access your existing block blob data in your Storage account through the Linux file system.</span></span> <span data-ttu-id="513f7-210">Azure Blob Storage is an object storage service and therefore does not have a hierarchical namespace.</span><span class="sxs-lookup"><span data-stu-id="513f7-210">Azure Blob Storage is an object storage service and therefore does not have a hierarchical namespace.</span></span> <span data-ttu-id="513f7-211">Blobfuse provides this namespace using the virtual direcectory scheme with the use of forward-slash `/` as a delimiter.</span><span class="sxs-lookup"><span data-stu-id="513f7-211">Blobfuse provides this namespace using the virtual direcectory scheme with the use of forward-slash `/` as a delimiter.</span></span> <span data-ttu-id="513f7-212">Blobfuse works on both Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="513f7-212">Blobfuse works on both Azure and Azure Stack.</span></span> 

<span data-ttu-id="513f7-213">To learn more about mounting Blob storage as a file system with Blobfuse on Linux, see [How to mount Blob storage as a file system with Blobfuse](https://docs.microsoft.com/azure/storage/blobs/storage-how-to-mount-container-linux).</span><span class="sxs-lookup"><span data-stu-id="513f7-213">To learn more about mounting Blob storage as a file system with Blobfuse on Linux, see [How to mount Blob storage as a file system with Blobfuse](https://docs.microsoft.com/azure/storage/blobs/storage-how-to-mount-container-linux).</span></span> 

<span data-ttu-id="513f7-214">For Azure Stack, **blobEndpoint** needs to be specified besides accountName, accountKey/sasToken, containerName, while configuring your Storage account credentials in the step of preparing for mounting.</span><span class="sxs-lookup"><span data-stu-id="513f7-214">For Azure Stack, **blobEndpoint** needs to be specified besides accountName, accountKey/sasToken, containerName, while configuring your Storage account credentials in the step of preparing for mounting.</span></span> 

<span data-ttu-id="513f7-215">In the Azure Stack development Kit, the blobEndpoint should be `myaccount.blob.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="513f7-215">In the Azure Stack development Kit, the blobEndpoint should be `myaccount.blob.local.azurestack.external`.</span></span> <span data-ttu-id="513f7-216">In Azure Stack integrated system, contact your cloud administrator if you’re not sure about your endpoint.</span><span class="sxs-lookup"><span data-stu-id="513f7-216">In Azure Stack integrated system, contact your cloud administrator if you’re not sure about your endpoint.</span></span> 

<span data-ttu-id="513f7-217">Please be aware that accountKey and sasToken can only be configured one at a time.</span><span class="sxs-lookup"><span data-stu-id="513f7-217">Please be aware that accountKey and sasToken can only be configured one at a time.</span></span> <span data-ttu-id="513f7-218">When storage account key is given, the credentials configuration file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="513f7-218">When storage account key is given, the credentials configuration file is in the following format:</span></span> 

```text  
    accountName myaccount 
    accountKey myaccesskey== 
    containerName mycontainer 
    blobEndpoint myaccount.blob.local.azurestack.external
```

<span data-ttu-id="513f7-219">When shared access token is given, the credentials configuration file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="513f7-219">When shared access token is given, the credentials configuration file is in the following format:</span></span>

```text  
    accountName myaccount 
    sasToken ?mysastoken 
    containerName mycontainer 
    blobEndpoint myaccount.blob.local.azurestack.external
```

## <a name="next-steps"></a><span data-ttu-id="513f7-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="513f7-220">Next steps</span></span>

* [<span data-ttu-id="513f7-221">Connect storage explorer to an Azure Stack subscription</span><span class="sxs-lookup"><span data-stu-id="513f7-221">Connect storage explorer to an Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="513f7-222">Get started with storage explorer</span><span class="sxs-lookup"><span data-stu-id="513f7-222">Get started with storage explorer</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="513f7-223">Azure-consistent storage: differences and considerations</span><span class="sxs-lookup"><span data-stu-id="513f7-223">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="513f7-224">Introduction to Microsoft Azure storage</span><span class="sxs-lookup"><span data-stu-id="513f7-224">Introduction to Microsoft Azure storage</span></span>](../../storage/common/storage-introduction.md)
