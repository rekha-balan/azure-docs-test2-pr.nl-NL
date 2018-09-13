---
title: Add the default VM image to the Azure Stack marketplace | Microsoft Docs
description: Add the Windows Server 2016 VM default image to the Azure Stack marketplace.
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/20/2017
ms.author: sngun
ms.openlocfilehash: f3d61278db9b8cf1db40434cdb08846530630012
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550069"
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="533f2-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span><span class="sxs-lookup"><span data-stu-id="533f2-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="533f2-104">Before you can provision virtual machines, you must add the Windows Server VM image to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="533f2-104">Before you can provision virtual machines, you must add the Windows Server VM image to the Azure Stack marketplace.</span></span>

1. <span data-ttu-id="533f2-105">After deploying Azure Stack, sign in to the MAS-CON01 virtual machine.</span><span class="sxs-lookup"><span data-stu-id="533f2-105">After deploying Azure Stack, sign in to the MAS-CON01 virtual machine.</span></span>

2. <span data-ttu-id="533f2-106">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span><span class="sxs-lookup"><span data-stu-id="533f2-106">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="533f2-107">When prompted, select the **ISO** version of the download.</span><span class="sxs-lookup"><span data-stu-id="533f2-107">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="533f2-108">Record the path to the download location which is used later in these steps.</span><span class="sxs-lookup"><span data-stu-id="533f2-108">Record the path to the download location which is used later in these steps.</span></span>

3. <span data-ttu-id="533f2-109">Open PowerShell ISE as an administrator.</span><span class="sxs-lookup"><span data-stu-id="533f2-109">Open PowerShell ISE as an administrator.</span></span>

4. <span data-ttu-id="533f2-110">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="533f2-110">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>

5. <span data-ttu-id="533f2-111">[Download the Azure Stack tools from GitHub](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="533f2-111">[Download the Azure Stack tools from GitHub](azure-stack-powershell-download.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="533f2-112">Make sure that you download and extract the Azure Stack tool repository to a folder that is NOT under the C:\Windows\System32 directory.</span><span class="sxs-lookup"><span data-stu-id="533f2-112">Make sure that you download and extract the Azure Stack tool repository to a folder that is NOT under the C:\Windows\System32 directory.</span></span>  
   
6. <span data-ttu-id="533f2-113">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="533f2-113">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>
   ```powershell
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ```
7. <span data-ttu-id="533f2-114">Create the Azure Stack administrator's AzureRM environment by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="533f2-114">Create the Azure Stack administrator's AzureRM environment by using the following cmdlet:</span></span>
   ```powershell
   Add-AzureStackAzureRmEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external" 
   ```

8. <span data-ttu-id="533f2-115">Get the GUID value of the Azure Active Directory(AAD) tenant that is used to deploy the Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="533f2-115">Get the GUID value of the Azure Active Directory(AAD) tenant that is used to deploy the Azure Stack.</span></span> <span data-ttu-id="533f2-116">If your Azure Stack environment is deployed by using:</span><span class="sxs-lookup"><span data-stu-id="533f2-116">If your Azure Stack environment is deployed by using:</span></span>  

    <span data-ttu-id="533f2-117">a.</span><span class="sxs-lookup"><span data-stu-id="533f2-117">a.</span></span> <span data-ttu-id="533f2-118">**Azure Active Directory**, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="533f2-118">**Azure Active Directory**, use the following cmdlet:</span></span>
    
    ```PowerShell
    $TenantID = Get-DirectoryTenantID -AADTenantName "<myaadtenant>.onmicrosoft.com" -EnvironmentName AzureStackAdmin
    ```
    <span data-ttu-id="533f2-119">b.</span><span class="sxs-lookup"><span data-stu-id="533f2-119">b.</span></span> <span data-ttu-id="533f2-120">**Active Directory Federation Services**, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="533f2-120">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
    ```PowerShell
    $TenantID = Get-DirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin 
    ```
   
9. <span data-ttu-id="533f2-121">Add the Windows Server 2016 image to the Azure Stack marketplace by running the following script.</span><span class="sxs-lookup"><span data-stu-id="533f2-121">Add the Windows Server 2016 image to the Azure Stack marketplace by running the following script.</span></span> <span data-ttu-id="533f2-122">Replace *Path_to_ISO* with the path to the WS2016 ISO you downloaded.</span><span class="sxs-lookup"><span data-stu-id="533f2-122">Replace *Path_to_ISO* with the path to the WS2016 ISO you downloaded.</span></span> <span data-ttu-id="533f2-123">See the [Parameters](#parameters) section for information about the allowed parameters.</span><span class="sxs-lookup"><span data-stu-id="533f2-123">See the [Parameters](#parameters) section for information about the allowed parameters.</span></span>

   ```powershell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"
  
   # Store the AAD service administrator account credentials in a variable 
   $UserName='<Username of the service administrator account>'
   $Password='<Admin password provided when deploying Azure Stack>'|ConvertTo-SecureString -Force -AsPlainText
   $Credential=New-Object PSCredential($UserName,$Password)

   # Add a Windows Server 2016 Evaluation VM Image.
   New-Server2016VMImage -ISOPath $ISOPath -TenantId $TenantID -EnvironmentName "AzureStackAdmin" -Net35 $True -AzureStackCredentials $Credential
   ```
   <span data-ttu-id="533f2-124">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the **IncludeLatestCU** parameter when running the previous cmdlet.</span><span class="sxs-lookup"><span data-stu-id="533f2-124">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the **IncludeLatestCU** parameter when running the previous cmdlet.</span></span> 

   <span data-ttu-id="533f2-125">When you run the New-Server2016VMImage cmdlet, the output displays a warning message that says, “Unable to acquire token for tenant ‘Common’”, which you can ignore and the download continues.</span><span class="sxs-lookup"><span data-stu-id="533f2-125">When you run the New-Server2016VMImage cmdlet, the output displays a warning message that says, “Unable to acquire token for tenant ‘Common’”, which you can ignore and the download continues.</span></span> <span data-ttu-id="533f2-126">The output also displays the “Downloading” message for a while and if the download is successful, it ends with the “StatusCode : Created” message.</span><span class="sxs-lookup"><span data-stu-id="533f2-126">The output also displays the “Downloading” message for a while and if the download is successful, it ends with the “StatusCode : Created” message.</span></span>

## <a name="parameters"></a><span data-ttu-id="533f2-127">Parameters</span><span class="sxs-lookup"><span data-stu-id="533f2-127">Parameters</span></span>

|<span data-ttu-id="533f2-128">New-Server2016VMImage parameters</span><span class="sxs-lookup"><span data-stu-id="533f2-128">New-Server2016VMImage parameters</span></span>|<span data-ttu-id="533f2-129">Required?</span><span class="sxs-lookup"><span data-stu-id="533f2-129">Required?</span></span>|<span data-ttu-id="533f2-130">Description</span><span class="sxs-lookup"><span data-stu-id="533f2-130">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="533f2-131">ArmEndpoint</span><span class="sxs-lookup"><span data-stu-id="533f2-131">ArmEndpoint</span></span>|<span data-ttu-id="533f2-132">No</span><span class="sxs-lookup"><span data-stu-id="533f2-132">No</span></span>|<span data-ttu-id="533f2-133">The Azure Resource Manager endpoint for your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="533f2-133">The Azure Resource Manager endpoint for your Azure Stack environment.</span></span> <span data-ttu-id="533f2-134">The default is the one used by the Proof of Concept (PoC) environment.</span><span class="sxs-lookup"><span data-stu-id="533f2-134">The default is the one used by the Proof of Concept (PoC) environment.</span></span>|
|<span data-ttu-id="533f2-135">AzureStackCredentials</span><span class="sxs-lookup"><span data-stu-id="533f2-135">AzureStackCredentials</span></span>|<span data-ttu-id="533f2-136">Yes</span><span class="sxs-lookup"><span data-stu-id="533f2-136">Yes</span></span>|<span data-ttu-id="533f2-137">The credentials provided during deployment that are used to sign in to the Azure Stack Administrator portal.</span><span class="sxs-lookup"><span data-stu-id="533f2-137">The credentials provided during deployment that are used to sign in to the Azure Stack Administrator portal.</span></span> |
|<span data-ttu-id="533f2-138">EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="533f2-138">EnvironmentName</span></span>|<span data-ttu-id="533f2-139">yes</span><span class="sxs-lookup"><span data-stu-id="533f2-139">yes</span></span>|<span data-ttu-id="533f2-140">The Azure Stack administrtor's PowerShell environment name.</span><span class="sxs-lookup"><span data-stu-id="533f2-140">The Azure Stack administrtor's PowerShell environment name.</span></span> |
|<span data-ttu-id="533f2-141">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="533f2-141">IncludeLatestCU</span></span>|<span data-ttu-id="533f2-142">No</span><span class="sxs-lookup"><span data-stu-id="533f2-142">No</span></span>|<span data-ttu-id="533f2-143">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span><span class="sxs-lookup"><span data-stu-id="533f2-143">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="533f2-144">ISOPath</span><span class="sxs-lookup"><span data-stu-id="533f2-144">ISOPath</span></span>|<span data-ttu-id="533f2-145">Yes</span><span class="sxs-lookup"><span data-stu-id="533f2-145">Yes</span></span>|<span data-ttu-id="533f2-146">The full path to the downloaded Windows Server 2016 ISO.</span><span class="sxs-lookup"><span data-stu-id="533f2-146">The full path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="533f2-147">Net35</span><span class="sxs-lookup"><span data-stu-id="533f2-147">Net35</span></span>|<span data-ttu-id="533f2-148">No</span><span class="sxs-lookup"><span data-stu-id="533f2-148">No</span></span>|<span data-ttu-id="533f2-149">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span><span class="sxs-lookup"><span data-stu-id="533f2-149">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="533f2-150">By default, this value is set to true.</span><span class="sxs-lookup"><span data-stu-id="533f2-150">By default, this value is set to true.</span></span> <span data-ttu-id="533f2-151">It is mandatory that the image contains the .NET 3.5 runtime to install the SQL or MYSQL resource providers.</span><span class="sxs-lookup"><span data-stu-id="533f2-151">It is mandatory that the image contains the .NET 3.5 runtime to install the SQL or MYSQL resource providers.</span></span> |
|<span data-ttu-id="533f2-152">TenantID</span><span class="sxs-lookup"><span data-stu-id="533f2-152">TenantID</span></span>|<span data-ttu-id="533f2-153">Yes</span><span class="sxs-lookup"><span data-stu-id="533f2-153">Yes</span></span>|<span data-ttu-id="533f2-154">The GUID value of your Azure Stack Tenant ID.</span><span class="sxs-lookup"><span data-stu-id="533f2-154">The GUID value of your Azure Stack Tenant ID.</span></span>|
|<span data-ttu-id="533f2-155">Version</span><span class="sxs-lookup"><span data-stu-id="533f2-155">Version</span></span>|<span data-ttu-id="533f2-156">No</span><span class="sxs-lookup"><span data-stu-id="533f2-156">No</span></span>|<span data-ttu-id="533f2-157">This parameter allows you to choose whether to add a Core or Full (or both) Windows Server 2016 images.</span><span class="sxs-lookup"><span data-stu-id="533f2-157">This parameter allows you to choose whether to add a Core or Full (or both) Windows Server 2016 images.</span></span> <span data-ttu-id="533f2-158">Valid values include Full (the default this parameter is not provided), Core, and Both.</span><span class="sxs-lookup"><span data-stu-id="533f2-158">Valid values include Full (the default this parameter is not provided), Core, and Both.</span></span>|
|<span data-ttu-id="533f2-159">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="533f2-159">VHDSizeInMB</span></span>|<span data-ttu-id="533f2-160">No</span><span class="sxs-lookup"><span data-stu-id="533f2-160">No</span></span>|<span data-ttu-id="533f2-161">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="533f2-161">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="533f2-162">Default value is 40960 MB.</span><span class="sxs-lookup"><span data-stu-id="533f2-162">Default value is 40960 MB.</span></span>|
|<span data-ttu-id="533f2-163">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="533f2-163">CreateGalleryItem</span></span>|<span data-ttu-id="533f2-164">No</span><span class="sxs-lookup"><span data-stu-id="533f2-164">No</span></span>|<span data-ttu-id="533f2-165">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span><span class="sxs-lookup"><span data-stu-id="533f2-165">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="533f2-166">By default, this value is set to true.</span><span class="sxs-lookup"><span data-stu-id="533f2-166">By default, this value is set to true.</span></span>|
|<span data-ttu-id="533f2-167">location</span><span class="sxs-lookup"><span data-stu-id="533f2-167">location</span></span> |<span data-ttu-id="533f2-168">No</span><span class="sxs-lookup"><span data-stu-id="533f2-168">No</span></span> |<span data-ttu-id="533f2-169">Specifies the location to which the Windows Server 2016 image should be published.</span><span class="sxs-lookup"><span data-stu-id="533f2-169">Specifies the location to which the Windows Server 2016 image should be published.</span></span> <span data-ttu-id="533f2-170">By default, this value is set to local.</span><span class="sxs-lookup"><span data-stu-id="533f2-170">By default, this value is set to local.</span></span>|
|<span data-ttu-id="533f2-171">CUUri</span><span class="sxs-lookup"><span data-stu-id="533f2-171">CUUri</span></span> |<span data-ttu-id="533f2-172">No</span><span class="sxs-lookup"><span data-stu-id="533f2-172">No</span></span> |<span data-ttu-id="533f2-173">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span><span class="sxs-lookup"><span data-stu-id="533f2-173">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="533f2-174">CUPath</span><span class="sxs-lookup"><span data-stu-id="533f2-174">CUPath</span></span> |<span data-ttu-id="533f2-175">No</span><span class="sxs-lookup"><span data-stu-id="533f2-175">No</span></span> |<span data-ttu-id="533f2-176">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span><span class="sxs-lookup"><span data-stu-id="533f2-176">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="533f2-177">This option is helpful if you have deployed Azure Stack in a disconnected environment.</span><span class="sxs-lookup"><span data-stu-id="533f2-177">This option is helpful if you have deployed Azure Stack in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="533f2-178">Next Steps</span><span class="sxs-lookup"><span data-stu-id="533f2-178">Next Steps</span></span>

[<span data-ttu-id="533f2-179">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="533f2-179">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
