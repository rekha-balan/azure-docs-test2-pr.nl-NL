---
title: Use a Windows VM system-assigned managed identity to access Azure Storage
description: A tutorial that walks you through the process of using a Windows VM system-assigned managed identity to access Azure Storage.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: 92553fc8867a482c0af99c4ba3937dcc0d2f09e6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868515"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-storage-via-access-key"></a><span data-ttu-id="4c4bf-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage via access key</span><span class="sxs-lookup"><span data-stu-id="4c4bf-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage via access key</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="4c4bf-104">This tutorial shows you how to use a system-assigned managed identity for Windows virtual machine (VM) to retrieve storage account access keys.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-104">This tutorial shows you how to use a system-assigned managed identity for Windows virtual machine (VM) to retrieve storage account access keys.</span></span> <span data-ttu-id="4c4bf-105">You can use storage access keys as usual when doing storage operations, for example when using the Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-105">You can use storage access keys as usual when doing storage operations, for example when using the Storage SDK.</span></span> <span data-ttu-id="4c4bf-106">For this tutorial, we upload and download blobs using Azure Storage PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-106">For this tutorial, we upload and download blobs using Azure Storage PowerShell.</span></span> <span data-ttu-id="4c4bf-107">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-107">You will learn how to:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="4c4bf-108">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="4c4bf-108">Create a storage account</span></span>
> * <span data-ttu-id="4c4bf-109">Grant your VM access to storage account access keys in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c4bf-109">Grant your VM access to storage account access keys in Resource Manager</span></span> 
> * <span data-ttu-id="4c4bf-110">Get an access token using your VM's identity, and use it to retrieve the storage access keys from Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c4bf-110">Get an access token using your VM's identity, and use it to retrieve the storage access keys from Resource Manager</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4c4bf-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4c4bf-111">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="4c4bf-112">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c4bf-112">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="4c4bf-113">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="4c4bf-113">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="4c4bf-114">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="4c4bf-114">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="create-a-storage-account"></a><span data-ttu-id="4c4bf-115">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="4c4bf-115">Create a storage account</span></span> 

<span data-ttu-id="4c4bf-116">If you don't already have one, you will now create a storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-116">If you don't already have one, you will now create a storage account.</span></span> <span data-ttu-id="4c4bf-117">You can also skip this step and grant your VM's system-assigned managed identity access to the keys of an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-117">You can also skip this step and grant your VM's system-assigned managed identity access to the keys of an existing storage account.</span></span> 

1. <span data-ttu-id="4c4bf-118">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-118">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="4c4bf-119">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-119">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span></span>
3. <span data-ttu-id="4c4bf-120">Enter a name for the storage account, which you will use later.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-120">Enter a name for the storage account, which you will use later.</span></span>  
4. <span data-ttu-id="4c4bf-121">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-121">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span></span> 
5. <span data-ttu-id="4c4bf-122">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-122">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>
6. <span data-ttu-id="4c4bf-123">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-123">Click **Create**.</span></span>

    ![Create new storage account](./media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a><span data-ttu-id="4c4bf-125">Create a blob container in the storage account</span><span class="sxs-lookup"><span data-stu-id="4c4bf-125">Create a blob container in the storage account</span></span>

<span data-ttu-id="4c4bf-126">Later we will upload and download a file to the new storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-126">Later we will upload and download a file to the new storage account.</span></span> <span data-ttu-id="4c4bf-127">Because files require blob storage, we need to create a blob container in which to store the file.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-127">Because files require blob storage, we need to create a blob container in which to store the file.</span></span>

1. <span data-ttu-id="4c4bf-128">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-128">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="4c4bf-129">Click the **Containers** link in the left, under "Blob service."</span><span class="sxs-lookup"><span data-stu-id="4c4bf-129">Click the **Containers** link in the left, under "Blob service."</span></span>
3. <span data-ttu-id="4c4bf-130">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-130">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span></span>
4. <span data-ttu-id="4c4bf-131">Give the container a name, select an access level, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-131">Give the container a name, select an access level, then click **OK**.</span></span> <span data-ttu-id="4c4bf-132">The name you specified will be used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-132">The name you specified will be used later in the tutorial.</span></span> 

    ![Create storage container](./media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-system-assigned-managed-identity-access-to-use-storage-account-access-keys"></a><span data-ttu-id="4c4bf-134">Grant your VM's system-assigned managed identity access to use storage account access keys</span><span class="sxs-lookup"><span data-stu-id="4c4bf-134">Grant your VM's system-assigned managed identity access to use storage account access keys</span></span> 

<span data-ttu-id="4c4bf-135">Azure Storage does not natively support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-135">Azure Storage does not natively support Azure AD authentication.</span></span>  <span data-ttu-id="4c4bf-136">However, you can use your VM's system-assigned managed identity to retrieve storage account access keys from the Resource Manager, then use a key to access storage.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-136">However, you can use your VM's system-assigned managed identity to retrieve storage account access keys from the Resource Manager, then use a key to access storage.</span></span>  <span data-ttu-id="4c4bf-137">In this step, you grant your VM's system-assigned managed identity access to the keys to your storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-137">In this step, you grant your VM's system-assigned managed identity access to the keys to your storage account.</span></span>   

1. <span data-ttu-id="4c4bf-138">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-138">Navigate back to your newly created storage account.</span></span>  
2. <span data-ttu-id="4c4bf-139">Click the **Access control (IAM)** link in the left panel.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-139">Click the **Access control (IAM)** link in the left panel.</span></span>  
3. <span data-ttu-id="4c4bf-140">Click **+ Add** on top of the page to add a new role assignment for your VM</span><span class="sxs-lookup"><span data-stu-id="4c4bf-140">Click **+ Add** on top of the page to add a new role assignment for your VM</span></span>
4. <span data-ttu-id="4c4bf-141">Set **Role** to "Storage Account Key Operator Service Role", on the right side of the page.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-141">Set **Role** to "Storage Account Key Operator Service Role", on the right side of the page.</span></span> 
5. <span data-ttu-id="4c4bf-142">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span><span class="sxs-lookup"><span data-stu-id="4c4bf-142">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span></span>  
6. <span data-ttu-id="4c4bf-143">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span><span class="sxs-lookup"><span data-stu-id="4c4bf-143">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span></span>  
7. <span data-ttu-id="4c4bf-144">Finally, under **Select** choose your Windows Virtual Machine in the dropdown, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-144">Finally, under **Select** choose your Windows Virtual Machine in the dropdown, then click **Save**.</span></span> 

    ![Alt image text](./media/msi-tutorial-linux-vm-access-storage/msi-storage-role.png)

## <a name="get-an-access-token-using-the-vms-system-assigned-managed-identity-to-call-azure-resource-manager"></a><span data-ttu-id="4c4bf-146">Get an access token using the VM's system-assigned managed identity to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c4bf-146">Get an access token using the VM's system-assigned managed identity to call Azure Resource Manager</span></span> 

<span data-ttu-id="4c4bf-147">For the remainder of the tutorial, we will work from the VM we created earlier.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-147">For the remainder of the tutorial, we will work from the VM we created earlier.</span></span> 

<span data-ttu-id="4c4bf-148">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-148">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span></span>  <span data-ttu-id="4c4bf-149">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-149">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span></span>

1. <span data-ttu-id="4c4bf-150">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-150">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span></span> 
2. <span data-ttu-id="4c4bf-151">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-151">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3. <span data-ttu-id="4c4bf-152">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-152">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span></span>
4. <span data-ttu-id="4c4bf-153">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-153">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span></span>

    ```powershell
       $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Method GET -Headers @{Metadata="true"}
    ```
    
    > [!NOTE]
    > <span data-ttu-id="4c4bf-154">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-154">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="4c4bf-155">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-155">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    
    <span data-ttu-id="4c4bf-156">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-156">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span></span> 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    <span data-ttu-id="4c4bf-157">Next, extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-157">Next, extract the access token from the response.</span></span>
    
    ```powershell
    $ArmToken = $content.access_token
    ```
 
## <a name="get-storage-account-access-keys-from-azure-resource-manager-to-make-storage-calls"></a><span data-ttu-id="4c4bf-158">Get storage account access keys from Azure Resource Manager to make storage calls</span><span class="sxs-lookup"><span data-stu-id="4c4bf-158">Get storage account access keys from Azure Resource Manager to make storage calls</span></span>  

<span data-ttu-id="4c4bf-159">Now use PowerShell to call Resource Manager using the access token we retrieved in the previous section, to retrieve the storage access key.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-159">Now use PowerShell to call Resource Manager using the access token we retrieved in the previous section, to retrieve the storage access key.</span></span> <span data-ttu-id="4c4bf-160">Once we have the storage access key, we can call storage upload/download operations.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-160">Once we have the storage access key, we can call storage upload/download operations.</span></span>

```powershell
$keysResponse = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE-ACCOUNT>/listKeys/?api-version=2016-12-01 -Method POST -Headers @{Authorization="Bearer $ARMToken"}
```
> [!NOTE] 
> <span data-ttu-id="4c4bf-161">The URL is case-sensitive, so ensure you use the exact same case used earlier, when you named the Resource Group, including the uppercase "G" in "resourceGroups."</span><span class="sxs-lookup"><span data-stu-id="4c4bf-161">The URL is case-sensitive, so ensure you use the exact same case used earlier, when you named the Resource Group, including the uppercase "G" in "resourceGroups."</span></span> 

```powershell
$keysContent = $keysResponse.Content | ConvertFrom-Json
$key = $keysContent.keys[0].value
```

<span data-ttu-id="4c4bf-162">Next we create a file called "test.txt".</span><span class="sxs-lookup"><span data-stu-id="4c4bf-162">Next we create a file called "test.txt".</span></span> <span data-ttu-id="4c4bf-163">Then use the storage access key to authenticate with the `New-AzureStorageContent` cmdlet, upload the file to our blob container, then download the file.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-163">Then use the storage access key to authenticate with the `New-AzureStorageContent` cmdlet, upload the file to our blob container, then download the file.</span></span>

```bash
echo "This is a test text file." > test.txt
```

<span data-ttu-id="4c4bf-164">Be sure to install the Azure Storage cmdlets first, using `Install-Module Azure.Storage`.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-164">Be sure to install the Azure Storage cmdlets first, using `Install-Module Azure.Storage`.</span></span> <span data-ttu-id="4c4bf-165">Then upload the blob you just created, using the `Set-AzureStorageBlobContent` PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-165">Then upload the blob you just created, using the `Set-AzureStorageBlobContent` PowerShell cmdlet:</span></span>

```powershell
$ctx = New-AzureStorageContext -StorageAccountName <STORAGE-ACCOUNT> -StorageAccountKey $key
Set-AzureStorageBlobContent -File test.txt -Container <CONTAINER-NAME> -Blob testblob -Context $ctx
```

<span data-ttu-id="4c4bf-166">Response:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-166">Response:</span></span>

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/13/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```

<span data-ttu-id="4c4bf-167">You can also download the blob you just uploaded, using the `Get-AzureStorageBlobContent` PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-167">You can also download the blob you just uploaded, using the `Get-AzureStorageBlobContent` PowerShell cmdlet:</span></span>

```powershell
Get-AzureStorageBlobContent -Blob testblob -Container <CONTAINER-NAME> -Destination test2.txt -Context $ctx
```

<span data-ttu-id="4c4bf-168">Response:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-168">Response:</span></span>

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/13/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```

## <a name="next-steps"></a><span data-ttu-id="4c4bf-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c4bf-169">Next steps</span></span>

<span data-ttu-id="4c4bf-170">In this tutorial, you learned how to create a system-assigned managed identity to access Azure Storage using an access key.</span><span class="sxs-lookup"><span data-stu-id="4c4bf-170">In this tutorial, you learned how to create a system-assigned managed identity to access Azure Storage using an access key.</span></span>  <span data-ttu-id="4c4bf-171">To learn more about Azure Storage access keys see:</span><span class="sxs-lookup"><span data-stu-id="4c4bf-171">To learn more about Azure Storage access keys see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="4c4bf-172">Manage your storage access keys</span><span class="sxs-lookup"><span data-stu-id="4c4bf-172">Manage your storage access keys</span></span>](/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys)

