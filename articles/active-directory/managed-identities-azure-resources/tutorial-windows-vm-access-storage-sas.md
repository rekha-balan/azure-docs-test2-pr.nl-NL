---
title: Use a Windows VM system-assigned managed identity to access Azure Storage using a SAS credential
description: A tutorial that shows you how to use a Windows VM system-assigned managed identity to access Azure Storage, using a SAS credential instead of a storage account access key.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: f8f65cbbf3f2583e43416fc36050de6c55f105dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969191"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-storage-via-a-sas-credential"></a><span data-ttu-id="d9501-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage via a SAS credential</span><span class="sxs-lookup"><span data-stu-id="d9501-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage via a SAS credential</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="d9501-104">This tutorial shows you how to use a system-assigned identity for a Windows virtual machine (VM) to obtain a storage Shared Access Signature (SAS) credential.</span><span class="sxs-lookup"><span data-stu-id="d9501-104">This tutorial shows you how to use a system-assigned identity for a Windows virtual machine (VM) to obtain a storage Shared Access Signature (SAS) credential.</span></span> <span data-ttu-id="d9501-105">Specifically, a [Service SAS credential](/azure/storage/common/storage-dotnet-shared-access-signature-part-1?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#types-of-shared-access-signatures).</span><span class="sxs-lookup"><span data-stu-id="d9501-105">Specifically, a [Service SAS credential](/azure/storage/common/storage-dotnet-shared-access-signature-part-1?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#types-of-shared-access-signatures).</span></span> 

<span data-ttu-id="d9501-106">A Service SAS provides the ability to grant limited access to objects in a storage account, for limited time and a specific service (in our case, the blob service), without exposing an account access key.</span><span class="sxs-lookup"><span data-stu-id="d9501-106">A Service SAS provides the ability to grant limited access to objects in a storage account, for limited time and a specific service (in our case, the blob service), without exposing an account access key.</span></span> <span data-ttu-id="d9501-107">You can use a SAS credential as usual when doing storage operations, for example when using the Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="d9501-107">You can use a SAS credential as usual when doing storage operations, for example when using the Storage SDK.</span></span> <span data-ttu-id="d9501-108">For this tutorial, we demonstrate uploading and downloading a blob using Azure Storage PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9501-108">For this tutorial, we demonstrate uploading and downloading a blob using Azure Storage PowerShell.</span></span> <span data-ttu-id="d9501-109">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="d9501-109">You will learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9501-110">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="d9501-110">Create a storage account</span></span>
> * <span data-ttu-id="d9501-111">Grant your VM access to a storage account SAS in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9501-111">Grant your VM access to a storage account SAS in Resource Manager</span></span> 
> * <span data-ttu-id="d9501-112">Get an access token using your VM's identity, and use it to retrieve the SAS from Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9501-112">Get an access token using your VM's identity, and use it to retrieve the SAS from Resource Manager</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d9501-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d9501-113">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="d9501-114">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="d9501-114">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="d9501-115">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="d9501-115">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="d9501-116">Enable system-assigned identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="d9501-116">Enable system-assigned identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)


## <a name="create-a-storage-account"></a><span data-ttu-id="d9501-117">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="d9501-117">Create a storage account</span></span> 

<span data-ttu-id="d9501-118">If you don't already have one, you will now create a storage account.</span><span class="sxs-lookup"><span data-stu-id="d9501-118">If you don't already have one, you will now create a storage account.</span></span> <span data-ttu-id="d9501-119">You can also skip this step and grant your VM's system-assigned managed identity access to the SAS credential of an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="d9501-119">You can also skip this step and grant your VM's system-assigned managed identity access to the SAS credential of an existing storage account.</span></span> 

1. <span data-ttu-id="d9501-120">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d9501-120">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="d9501-121">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span><span class="sxs-lookup"><span data-stu-id="d9501-121">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span></span>
3. <span data-ttu-id="d9501-122">Enter a name for the storage account, which you will use later.</span><span class="sxs-lookup"><span data-stu-id="d9501-122">Enter a name for the storage account, which you will use later.</span></span>  
4. <span data-ttu-id="d9501-123">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span><span class="sxs-lookup"><span data-stu-id="d9501-123">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span></span> 
5. <span data-ttu-id="d9501-124">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d9501-124">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>
6. <span data-ttu-id="d9501-125">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9501-125">Click **Create**.</span></span>

    ![Create new storage account](./media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a><span data-ttu-id="d9501-127">Create a blob container in the storage account</span><span class="sxs-lookup"><span data-stu-id="d9501-127">Create a blob container in the storage account</span></span>

<span data-ttu-id="d9501-128">Later we will upload and download a file to the new storage account.</span><span class="sxs-lookup"><span data-stu-id="d9501-128">Later we will upload and download a file to the new storage account.</span></span> <span data-ttu-id="d9501-129">Because files require blob storage, we need to create a blob container in which to store the file.</span><span class="sxs-lookup"><span data-stu-id="d9501-129">Because files require blob storage, we need to create a blob container in which to store the file.</span></span>

1. <span data-ttu-id="d9501-130">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="d9501-130">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="d9501-131">Click the **Containers** link in the left panel, under "Blob service."</span><span class="sxs-lookup"><span data-stu-id="d9501-131">Click the **Containers** link in the left panel, under "Blob service."</span></span>
3. <span data-ttu-id="d9501-132">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span><span class="sxs-lookup"><span data-stu-id="d9501-132">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span></span>
4. <span data-ttu-id="d9501-133">Give the container a name, select an access level, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9501-133">Give the container a name, select an access level, then click **OK**.</span></span> <span data-ttu-id="d9501-134">The name you specified will be used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9501-134">The name you specified will be used later in the tutorial.</span></span> 

    ![Create storage container](./media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-system-assigned-managed-identity-access-to-use-a-storage-sas"></a><span data-ttu-id="d9501-136">Grant your VM's system-assigned managed identity access to use a storage SAS</span><span class="sxs-lookup"><span data-stu-id="d9501-136">Grant your VM's system-assigned managed identity access to use a storage SAS</span></span> 

<span data-ttu-id="d9501-137">Azure Storage does not natively support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="d9501-137">Azure Storage does not natively support Azure AD authentication.</span></span>  <span data-ttu-id="d9501-138">However, you can use a managed identity to retrieve a storage SAS from Resource Manager, then use the SAS to access storage.</span><span class="sxs-lookup"><span data-stu-id="d9501-138">However, you can use a managed identity to retrieve a storage SAS from Resource Manager, then use the SAS to access storage.</span></span>  <span data-ttu-id="d9501-139">In this step, you grant your VM's system-assigned managed identity access to your storage account SAS.</span><span class="sxs-lookup"><span data-stu-id="d9501-139">In this step, you grant your VM's system-assigned managed identity access to your storage account SAS.</span></span>   

1. <span data-ttu-id="d9501-140">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="d9501-140">Navigate back to your newly created storage account.</span></span>   
2. <span data-ttu-id="d9501-141">Click the **Access control (IAM)** link in the left panel.</span><span class="sxs-lookup"><span data-stu-id="d9501-141">Click the **Access control (IAM)** link in the left panel.</span></span>  
3. <span data-ttu-id="d9501-142">Click **+ Add** on top of the page to add a new role assignment for your VM</span><span class="sxs-lookup"><span data-stu-id="d9501-142">Click **+ Add** on top of the page to add a new role assignment for your VM</span></span>
4. <span data-ttu-id="d9501-143">Set **Role** to "Storage Account Contributor", on the right side of the page.</span><span class="sxs-lookup"><span data-stu-id="d9501-143">Set **Role** to "Storage Account Contributor", on the right side of the page.</span></span>  
5. <span data-ttu-id="d9501-144">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span><span class="sxs-lookup"><span data-stu-id="d9501-144">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span></span>  
6. <span data-ttu-id="d9501-145">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span><span class="sxs-lookup"><span data-stu-id="d9501-145">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span></span>  
7. <span data-ttu-id="d9501-146">Finally, under **Select** choose your Windows Virtual Machine in the dropdown, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d9501-146">Finally, under **Select** choose your Windows Virtual Machine in the dropdown, then click **Save**.</span></span> 

    ![Alt image text](./media/msi-tutorial-linux-vm-access-storage/msi-storage-role-sas.png)

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-azure-resource-manager"></a><span data-ttu-id="d9501-148">Get an access token using the VM's identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9501-148">Get an access token using the VM's identity and use it to call Azure Resource Manager</span></span> 

<span data-ttu-id="d9501-149">For the remainder of the tutorial, we will work from the VM we created earlier.</span><span class="sxs-lookup"><span data-stu-id="d9501-149">For the remainder of the tutorial, we will work from the VM we created earlier.</span></span>

<span data-ttu-id="d9501-150">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span><span class="sxs-lookup"><span data-stu-id="d9501-150">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span></span>  <span data-ttu-id="d9501-151">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span><span class="sxs-lookup"><span data-stu-id="d9501-151">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span></span>

1. <span data-ttu-id="d9501-152">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span><span class="sxs-lookup"><span data-stu-id="d9501-152">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span></span>
2. <span data-ttu-id="d9501-153">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="d9501-153">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3. <span data-ttu-id="d9501-154">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span><span class="sxs-lookup"><span data-stu-id="d9501-154">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span></span> 
4. <span data-ttu-id="d9501-155">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9501-155">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span></span>

    ```powershell
       $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Method GET -Headers @{Metadata="true"}
    ```
    
    > [!NOTE]
    > <span data-ttu-id="d9501-156">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9501-156">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="d9501-157">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="d9501-157">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    
    <span data-ttu-id="d9501-158">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span><span class="sxs-lookup"><span data-stu-id="d9501-158">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span></span> 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    <span data-ttu-id="d9501-159">Next, extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="d9501-159">Next, extract the access token from the response.</span></span>
    
    ```powershell
    $ArmToken = $content.access_token
    ```

## <a name="get-a-sas-credential-from-azure-resource-manager-to-make-storage-calls"></a><span data-ttu-id="d9501-160">Get a SAS credential from Azure Resource Manager to make storage calls</span><span class="sxs-lookup"><span data-stu-id="d9501-160">Get a SAS credential from Azure Resource Manager to make storage calls</span></span> 

<span data-ttu-id="d9501-161">Now use PowerShell to call Resource Manager using the access token we retrieved in the previous section, to create a storage SAS credential.</span><span class="sxs-lookup"><span data-stu-id="d9501-161">Now use PowerShell to call Resource Manager using the access token we retrieved in the previous section, to create a storage SAS credential.</span></span> <span data-ttu-id="d9501-162">Once we have the SAS credential, we can call storage operations.</span><span class="sxs-lookup"><span data-stu-id="d9501-162">Once we have the SAS credential, we can call storage operations.</span></span>

<span data-ttu-id="d9501-163">For this request we'll use the follow HTTP request parameters to create the SAS credential:</span><span class="sxs-lookup"><span data-stu-id="d9501-163">For this request we'll use the follow HTTP request parameters to create the SAS credential:</span></span>

```JSON
{
    "canonicalizedResource":"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>",
    "signedResource":"c",              // The kind of resource accessible with the SAS, in this case a container (c).
    "signedPermission":"rcw",          // Permissions for this SAS, in this case (r)ead, (c)reate, and (w)rite. Order is important.
    "signedProtocol":"https",          // Require the SAS be used on https protocol.
    "signedExpiry":"<EXPIRATION TIME>" // UTC expiration time for SAS in ISO 8601 format, for example 2017-09-22T00:06:00Z.
}
```

<span data-ttu-id="d9501-164">These parameters are included in the POST body of the request for the SAS credential.</span><span class="sxs-lookup"><span data-stu-id="d9501-164">These parameters are included in the POST body of the request for the SAS credential.</span></span> <span data-ttu-id="d9501-165">For more information on the parameters for creating a SAS credential, see the [List Service SAS REST reference](/rest/api/storagerp/storageaccounts/listservicesas).</span><span class="sxs-lookup"><span data-stu-id="d9501-165">For more information on the parameters for creating a SAS credential, see the [List Service SAS REST reference](/rest/api/storagerp/storageaccounts/listservicesas).</span></span>

<span data-ttu-id="d9501-166">First, convert the parameters to JSON, then call the storage `listServiceSas` endpoint to create the SAS credential:</span><span class="sxs-lookup"><span data-stu-id="d9501-166">First, convert the parameters to JSON, then call the storage `listServiceSas` endpoint to create the SAS credential:</span></span>

```powershell
$params = @{canonicalizedResource="/blob/<STORAGE-ACCOUNT-NAME>/<CONTAINER-NAME>";signedResource="c";signedPermission="rcw";signedProtocol="https";signedExpiry="2017-09-23T00:00:00Z"}
$jsonParams = $params | ConvertTo-Json
```

```powershell
$sasResponse = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE-ACCOUNT-NAME>/listServiceSas/?api-version=2017-06-01 -Method POST -Body $jsonParams -Headers @{Authorization="Bearer $ArmToken"}
```
> [!NOTE] 
> <span data-ttu-id="d9501-167">The URL is case-sensitive, so ensure you use the exact same case used earlier, when you named the Resource Group, including the uppercase "G" in "resourceGroups."</span><span class="sxs-lookup"><span data-stu-id="d9501-167">The URL is case-sensitive, so ensure you use the exact same case used earlier, when you named the Resource Group, including the uppercase "G" in "resourceGroups."</span></span> 

<span data-ttu-id="d9501-168">Now we can extract the SAS credential from the response:</span><span class="sxs-lookup"><span data-stu-id="d9501-168">Now we can extract the SAS credential from the response:</span></span>

```powershell
$sasContent = $sasResponse.Content | ConvertFrom-Json
$sasCred = $sasContent.serviceSasToken
```

<span data-ttu-id="d9501-169">If you inspect the SAS cred you'll see something like this:</span><span class="sxs-lookup"><span data-stu-id="d9501-169">If you inspect the SAS cred you'll see something like this:</span></span>

```powershell
PS C:\> $sasCred
sv=2015-04-05&sr=c&spr=https&se=2017-09-23T00%3A00%3A00Z&sp=rcw&sig=JVhIWG48nmxqhTIuN0uiFBppdzhwHdehdYan1W%2F4O0E%3D
```

<span data-ttu-id="d9501-170">Next we create a file called "test.txt".</span><span class="sxs-lookup"><span data-stu-id="d9501-170">Next we create a file called "test.txt".</span></span> <span data-ttu-id="d9501-171">Then use the SAS credential to authenticate with the `New-AzureStorageContent` cmdlet, upload the file to our blob container, then download the file.</span><span class="sxs-lookup"><span data-stu-id="d9501-171">Then use the SAS credential to authenticate with the `New-AzureStorageContent` cmdlet, upload the file to our blob container, then download the file.</span></span>

```bash
echo "This is a test text file." > test.txt
```

<span data-ttu-id="d9501-172">Be sure to install the Azure Storage cmdlets first, using `Install-Module Azure.Storage`.</span><span class="sxs-lookup"><span data-stu-id="d9501-172">Be sure to install the Azure Storage cmdlets first, using `Install-Module Azure.Storage`.</span></span> <span data-ttu-id="d9501-173">Then upload the blob you just created, using the `Set-AzureStorageBlobContent` PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9501-173">Then upload the blob you just created, using the `Set-AzureStorageBlobContent` PowerShell cmdlet:</span></span>

```powershell
$ctx = New-AzureStorageContext -StorageAccountName <STORAGE-ACCOUNT-NAME> -SasToken $sasCred
Set-AzureStorageBlobContent -File test.txt -Container <CONTAINER-NAME> -Blob testblob -Context $ctx
```

<span data-ttu-id="d9501-174">Response:</span><span class="sxs-lookup"><span data-stu-id="d9501-174">Response:</span></span>

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/21/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```

<span data-ttu-id="d9501-175">You can also download the blob you just uploaded, using the `Get-AzureStorageBlobContent` PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9501-175">You can also download the blob you just uploaded, using the `Get-AzureStorageBlobContent` PowerShell cmdlet:</span></span>

```powershell
Get-AzureStorageBlobContent -Blob testblob -Container <CONTAINER-NAME> -Destination test2.txt -Context $ctx
```

<span data-ttu-id="d9501-176">Response:</span><span class="sxs-lookup"><span data-stu-id="d9501-176">Response:</span></span>

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/21/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```

## <a name="next-steps"></a><span data-ttu-id="d9501-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="d9501-177">Next steps</span></span>

<span data-ttu-id="d9501-178">In this tutorial, you learned how to use a Windows VM's system-assigned managed identity to access Azure Storage using a SAS credential.</span><span class="sxs-lookup"><span data-stu-id="d9501-178">In this tutorial, you learned how to use a Windows VM's system-assigned managed identity to access Azure Storage using a SAS credential.</span></span>  <span data-ttu-id="d9501-179">To learn more about Azure Storage SAS see:</span><span class="sxs-lookup"><span data-stu-id="d9501-179">To learn more about Azure Storage SAS see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="d9501-180">Using shared access signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="d9501-180">Using shared access signatures (SAS)</span></span>](/azure/storage/common/storage-dotnet-shared-access-signature-part-1)


