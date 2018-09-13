---
title: Use a Linux VM system-assigned managed identity to access Azure Storage
description: A tutorial that walks you through the process of using a Linux VM system-assigned managed identity to access Azure Storage.
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
ms.openlocfilehash: 095da0b2f234fa4c883ff8512516c87fe193fccf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868932"
---
# <a name="tutorial-use-a-linux-vm-system-assigned-managed-identity-to-access-azure-storage-via-access-key"></a><span data-ttu-id="c4e0f-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Storage via access key</span><span class="sxs-lookup"><span data-stu-id="c4e0f-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Storage via access key</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="c4e0f-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to retrieve storage account access keys.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to retrieve storage account access keys.</span></span> <span data-ttu-id="c4e0f-105">You can use a storage access key as usual when doing storage operations, for example when using the Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-105">You can use a storage access key as usual when doing storage operations, for example when using the Storage SDK.</span></span> <span data-ttu-id="c4e0f-106">For this tutorial, we upload and download blobs using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-106">For this tutorial, we upload and download blobs using Azure CLI.</span></span> <span data-ttu-id="c4e0f-107">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-107">You will learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c4e0f-108">Grant your VM access to storage account access keys in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4e0f-108">Grant your VM access to storage account access keys in Resource Manager</span></span> 
> * <span data-ttu-id="c4e0f-109">Get an access token using your VM's identity, and use it to retrieve the storage access keys from Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4e0f-109">Get an access token using your VM's identity, and use it to retrieve the storage access keys from Resource Manager</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c4e0f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4e0f-110">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="c4e0f-111">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="c4e0f-111">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="c4e0f-112">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="c4e0f-112">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

- [<span data-ttu-id="c4e0f-113">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="c4e0f-113">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="create-a-storage-account"></a><span data-ttu-id="c4e0f-114">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="c4e0f-114">Create a storage account</span></span> 

<span data-ttu-id="c4e0f-115">If you don't already have one, you will now create a storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-115">If you don't already have one, you will now create a storage account.</span></span>  <span data-ttu-id="c4e0f-116">You can also skip this step and grant your VM system-assigned managed identity access to the keys of an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-116">You can also skip this step and grant your VM system-assigned managed identity access to the keys of an existing storage account.</span></span> 

1. <span data-ttu-id="c4e0f-117">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-117">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="c4e0f-118">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-118">Click **Storage**, then **Storage Account**, and a new "Create storage account" panel will display.</span></span>
3. <span data-ttu-id="c4e0f-119">Enter a **Name** for the storage account, which you will use later.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-119">Enter a **Name** for the storage account, which you will use later.</span></span>  
4. <span data-ttu-id="c4e0f-120">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-120">**Deployment model** and **Account kind** should be set to "Resource manager" and "General purpose", respectively.</span></span> 
5. <span data-ttu-id="c4e0f-121">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-121">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>
6. <span data-ttu-id="c4e0f-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-122">Click **Create**.</span></span>

    ![Create new storage account](./media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a><span data-ttu-id="c4e0f-124">Create a blob container in the storage account</span><span class="sxs-lookup"><span data-stu-id="c4e0f-124">Create a blob container in the storage account</span></span>

<span data-ttu-id="c4e0f-125">Later we will upload and download a file to the new storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-125">Later we will upload and download a file to the new storage account.</span></span> <span data-ttu-id="c4e0f-126">Because files require blob storage, we need to create a blob container in which to store the file.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-126">Because files require blob storage, we need to create a blob container in which to store the file.</span></span>

1. <span data-ttu-id="c4e0f-127">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-127">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="c4e0f-128">Click the **Containers** link in the left, under "Blob service."</span><span class="sxs-lookup"><span data-stu-id="c4e0f-128">Click the **Containers** link in the left, under "Blob service."</span></span>
3. <span data-ttu-id="c4e0f-129">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-129">Click **+ Container** on the top of the page, and a "New container" panel slides out.</span></span>
4. <span data-ttu-id="c4e0f-130">Give the container a name, select an access level, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-130">Give the container a name, select an access level, then click **OK**.</span></span> <span data-ttu-id="c4e0f-131">The name you specified will be used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-131">The name you specified will be used later in the tutorial.</span></span> 

    ![Create storage container](./media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-system-assigned-managed-identity-access-to-use-storage-account-access-keys"></a><span data-ttu-id="c4e0f-133">Grant your VM's system-assigned managed identity access to use storage account access keys</span><span class="sxs-lookup"><span data-stu-id="c4e0f-133">Grant your VM's system-assigned managed identity access to use storage account access keys</span></span>

<span data-ttu-id="c4e0f-134">Azure Storage does not natively support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-134">Azure Storage does not natively support Azure AD authentication.</span></span>  <span data-ttu-id="c4e0f-135">However, you can use managed identities for Azure resources to retrieve storage account access keys from the Resource Manager, then use a key to access storage.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-135">However, you can use managed identities for Azure resources to retrieve storage account access keys from the Resource Manager, then use a key to access storage.</span></span>  <span data-ttu-id="c4e0f-136">In this step, you grant your VM's system-assigned managed identity access to the keys to your storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-136">In this step, you grant your VM's system-assigned managed identity access to the keys to your storage account.</span></span>   

1. <span data-ttu-id="c4e0f-137">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-137">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="c4e0f-138">Click the **Access control (IAM)** link in the left panel.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-138">Click the **Access control (IAM)** link in the left panel.</span></span>  
3. <span data-ttu-id="c4e0f-139">Click **+ Add** on top of the page to add a new role assignment for your VM</span><span class="sxs-lookup"><span data-stu-id="c4e0f-139">Click **+ Add** on top of the page to add a new role assignment for your VM</span></span>
4. <span data-ttu-id="c4e0f-140">Set **Role** to "Storage Account Key Operator Service Role", on the right side of the page.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-140">Set **Role** to "Storage Account Key Operator Service Role", on the right side of the page.</span></span> 
5. <span data-ttu-id="c4e0f-141">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span><span class="sxs-lookup"><span data-stu-id="c4e0f-141">In the next dropdown, set **Assign access to** the resource "Virtual Machine".</span></span>  
6. <span data-ttu-id="c4e0f-142">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span><span class="sxs-lookup"><span data-stu-id="c4e0f-142">Next, ensure the proper subscription is listed in **Subscription** dropdown, then set **Resource Group** to "All resource groups".</span></span>  
7. <span data-ttu-id="c4e0f-143">Finally, under **Select** choose your Linux Virtual Machine in the dropdown, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-143">Finally, under **Select** choose your Linux Virtual Machine in the dropdown, then click **Save**.</span></span> 

    ![Alt image text](./media/msi-tutorial-linux-vm-access-storage/msi-storage-role.png)

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-azure-resource-manager"></a><span data-ttu-id="c4e0f-145">Get an access token using the VM's identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4e0f-145">Get an access token using the VM's identity and use it to call Azure Resource Manager</span></span>

<span data-ttu-id="c4e0f-146">For the remainder of the tutorial, we will work from the VM we created earlier.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-146">For the remainder of the tutorial, we will work from the VM we created earlier.</span></span>

<span data-ttu-id="c4e0f-147">To complete these steps, you will need an SSH client.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-147">To complete these steps, you will need an SSH client.</span></span> <span data-ttu-id="c4e0f-148">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="c4e0f-148">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/install_guide).</span></span> <span data-ttu-id="c4e0f-149">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c4e0f-149">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>

1. <span data-ttu-id="c4e0f-150">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect** at the top.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-150">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect** at the top.</span></span> <span data-ttu-id="c4e0f-151">Copy the string to connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-151">Copy the string to connect to your VM.</span></span> 
2. <span data-ttu-id="c4e0f-152">Connect to your VM using your SSH client.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-152">Connect to your VM using your SSH client.</span></span>  
3. <span data-ttu-id="c4e0f-153">Next, you will be prompted to enter in your **Password** you added when creating the **Linux VM**.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-153">Next, you will be prompted to enter in your **Password** you added when creating the **Linux VM**.</span></span> <span data-ttu-id="c4e0f-154">You should then be successfully signed in.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-154">You should then be successfully signed in.</span></span>  
4. <span data-ttu-id="c4e0f-155">Use CURL to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-155">Use CURL to get an access token for Azure Resource Manager.</span></span>  

    <span data-ttu-id="c4e0f-156">The CURL request and response for the access token is below:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-156">The CURL request and response for the access token is below:</span></span>
    
    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true
    ```
    
    > [!NOTE]
    > <span data-ttu-id="c4e0f-157">In the previous request, the value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-157">In the previous request, the value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="c4e0f-158">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-158">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    > <span data-ttu-id="c4e0f-159">In the following response, the access_token element as been shortened for brevity.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-159">In the following response, the access_token element as been shortened for brevity.</span></span>
    
    ```bash
    {"access_token":"eyJ0eXAiOiJ...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://management.azure.com",
    "token_type":"Bearer"} 
     ```
    
## <a name="get-storage-account-access-keys-from-azure-resource-manager-to-make-storage-calls"></a><span data-ttu-id="c4e0f-160">Get storage account access keys from Azure Resource Manager to make storage calls</span><span class="sxs-lookup"><span data-stu-id="c4e0f-160">Get storage account access keys from Azure Resource Manager to make storage calls</span></span>  

<span data-ttu-id="c4e0f-161">Now use CURL to call Resource Manager using the access token we retrieved in the previous section, to retrieve the storage access key.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-161">Now use CURL to call Resource Manager using the access token we retrieved in the previous section, to retrieve the storage access key.</span></span> <span data-ttu-id="c4e0f-162">Once we have the storage access key, we can call storage upload/download operations.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-162">Once we have the storage access key, we can call storage upload/download operations.</span></span> <span data-ttu-id="c4e0f-163">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<STORAGE ACCOUNT NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-163">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<STORAGE ACCOUNT NAME>` parameter values with your own values.</span></span> <span data-ttu-id="c4e0f-164">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-164">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier:</span></span>

```bash 
curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>/listKeys?api-version=2016-12-01 --request POST -d "" -H "Authorization: Bearer <ACCESS TOKEN>" 
```

> [!NOTE]
> <span data-ttu-id="c4e0f-165">The text in the prior URL is case sensitive, so ensure if you are using upper-lowercase for your Resource Groups to reflect it accordingly.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-165">The text in the prior URL is case sensitive, so ensure if you are using upper-lowercase for your Resource Groups to reflect it accordingly.</span></span> <span data-ttu-id="c4e0f-166">Additionally, it’s important to know that this is a POST request not a GET request and ensure you pass a value to capture a length limit with -d that can be NULL.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-166">Additionally, it’s important to know that this is a POST request not a GET request and ensure you pass a value to capture a length limit with -d that can be NULL.</span></span>  

<span data-ttu-id="c4e0f-167">The CURL response gives you the list of Keys:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-167">The CURL response gives you the list of Keys:</span></span>  

```bash 
{"keys":[{"keyName":"key1","permissions":"Full","value":"iqDPNt..."},{"keyName":"key2","permissions":"Full","value":"U+uI0B..."}]} 
```
<span data-ttu-id="c4e0f-168">Create a sample blob file to upload to your blob storage container.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-168">Create a sample blob file to upload to your blob storage container.</span></span> <span data-ttu-id="c4e0f-169">On a Linux VM you can do this with the following command.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-169">On a Linux VM you can do this with the following command.</span></span> 

```bash
echo "This is a test file." > test.txt
```

<span data-ttu-id="c4e0f-170">Next, authenticate with the CLI `az storage` command using the storage access key, and upload the file to the blob container.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-170">Next, authenticate with the CLI `az storage` command using the storage access key, and upload the file to the blob container.</span></span> <span data-ttu-id="c4e0f-171">For this step, you will need to [install the latest Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) on your VM, if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-171">For this step, you will need to [install the latest Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) on your VM, if you haven't already.</span></span>
 

```azurecli-interactive
az storage blob upload -c <CONTAINER NAME> -n test.txt -f test.txt --account-name <STORAGE ACCOUNT NAME> --account-key <STORAGE ACCOUNT KEY>
```

<span data-ttu-id="c4e0f-172">Response:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-172">Response:</span></span> 

```JSON
Finished[#############################################################]  100.0000%
{
  "etag": "\"0x8D4F9929765C139\"",
  "lastModified": "2017-09-12T03:58:56+00:00"
}
```

<span data-ttu-id="c4e0f-173">Additionally, you can download the file using the Azure CLI and authenticating with the storage access key.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-173">Additionally, you can download the file using the Azure CLI and authenticating with the storage access key.</span></span> 

<span data-ttu-id="c4e0f-174">Request:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-174">Request:</span></span> 

```azurecli-interactive
az storage blob download -c <CONTAINER NAME> -n test.txt -f test-download.txt --account-name <STORAGE ACCOUNT NAME> --account-key <STORAGE ACCOUNT KEY>
```

<span data-ttu-id="c4e0f-175">Response:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-175">Response:</span></span> 

```JSON
{
  "content": null,
  "metadata": {},
  "name": "test.txt",
  "properties": {
    "appendBlobCommittedBlockCount": null,
    "blobType": "BlockBlob",
    "contentLength": 21,
    "contentRange": "bytes 0-20/21",
    "contentSettings": {
      "cacheControl": null,
      "contentDisposition": null,
      "contentEncoding": null,
      "contentLanguage": null,
      "contentMd5": "LSghAvpnElYyfUdn7CO8aw==",
      "contentType": "text/plain"
    },
    "copy": {
      "completionTime": null,
      "id": null,
      "progress": null,
      "source": null,
      "status": null,
      "statusDescription": null
    },
    "etag": "\"0x8D5067F30D0C283\"",
    "lastModified": "2017-09-28T14:42:49+00:00",
    "lease": {
      "duration": null,
      "state": "available",
      "status": "unlocked"
    },
    "pageBlobSequenceNumber": null,
    "serverEncrypted": false
  },
  "snapshot": null
}
```

## <a name="next-steps"></a><span data-ttu-id="c4e0f-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4e0f-176">Next steps</span></span>

<span data-ttu-id="c4e0f-177">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access Azure Storage using an access key.</span><span class="sxs-lookup"><span data-stu-id="c4e0f-177">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access Azure Storage using an access key.</span></span>  <span data-ttu-id="c4e0f-178">To learn more about Azure Storage access keys see:</span><span class="sxs-lookup"><span data-stu-id="c4e0f-178">To learn more about Azure Storage access keys see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c4e0f-179">Manage your storage access keys</span><span class="sxs-lookup"><span data-stu-id="c4e0f-179">Manage your storage access keys</span></span>](/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys)
