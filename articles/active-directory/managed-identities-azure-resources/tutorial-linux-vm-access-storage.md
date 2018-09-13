---
title: Use a Linux VM system-assigned managed identity to access Azure Storage
description: A tutorial that walks you through the process of using a Linux VM system-assigned managed identity to access Azure Storage.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/09/2018
ms.author: daveba
ms.openlocfilehash: 05e054dad28faf5dfba5ed8ac63bbe851c62afe4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966240"
---
# <a name="tutorial-use-a-linux-vm-system-assigned-managed-identity-to-access-azure-storage"></a><span data-ttu-id="0d74d-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0d74d-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Storage</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="0d74d-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0d74d-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Storage.</span></span> <span data-ttu-id="0d74d-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="0d74d-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d74d-106">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="0d74d-106">Create a storage account</span></span>
> * <span data-ttu-id="0d74d-107">Create a blob container in a storage account</span><span class="sxs-lookup"><span data-stu-id="0d74d-107">Create a blob container in a storage account</span></span>
> * <span data-ttu-id="0d74d-108">Grant the Linux VM's Managed Identity access to an Azure Storage container</span><span class="sxs-lookup"><span data-stu-id="0d74d-108">Grant the Linux VM's Managed Identity access to an Azure Storage container</span></span>
> * <span data-ttu-id="0d74d-109">Get an access token and use it to call Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0d74d-109">Get an access token and use it to call Azure Storage</span></span>

> [!NOTE]
> <span data-ttu-id="0d74d-110">Azure Active Directory authentication for Azure Storage is in public preview.</span><span class="sxs-lookup"><span data-stu-id="0d74d-110">Azure Active Directory authentication for Azure Storage is in public preview.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d74d-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0d74d-111">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="0d74d-112">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d74d-112">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="0d74d-113">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="0d74d-113">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

- [<span data-ttu-id="0d74d-114">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="0d74d-114">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

<span data-ttu-id="0d74d-115">To run the CLI script examples in this tutorial, you have two options:</span><span class="sxs-lookup"><span data-stu-id="0d74d-115">To run the CLI script examples in this tutorial, you have two options:</span></span>

- <span data-ttu-id="0d74d-116">Use [Azure Cloud Shell](~/articles/cloud-shell/overview.md) either from the Azure portal, or via the **Try It** button, located in the top right corner of each code block.</span><span class="sxs-lookup"><span data-stu-id="0d74d-116">Use [Azure Cloud Shell](~/articles/cloud-shell/overview.md) either from the Azure portal, or via the **Try It** button, located in the top right corner of each code block.</span></span>
- <span data-ttu-id="0d74d-117">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.23 or later) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="0d74d-117">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.23 or later) if you prefer to use a local CLI console.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="0d74d-118">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="0d74d-118">Create a storage account</span></span> 

<span data-ttu-id="0d74d-119">In this section, you create a storage account.</span><span class="sxs-lookup"><span data-stu-id="0d74d-119">In this section, you create a storage account.</span></span> 

1. <span data-ttu-id="0d74d-120">Click the **+ Create a resource** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d74d-120">Click the **+ Create a resource** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="0d74d-121">Click **Storage**, then **Storage account - blob, file, table, queue**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-121">Click **Storage**, then **Storage account - blob, file, table, queue**.</span></span>
3. <span data-ttu-id="0d74d-122">Under **Name**, enter a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="0d74d-122">Under **Name**, enter a name for the storage account.</span></span>  
4. <span data-ttu-id="0d74d-123">**Deployment model** and **Account kind** should be set to **Resource manager** and **Storage (general purpose v1)**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-123">**Deployment model** and **Account kind** should be set to **Resource manager** and **Storage (general purpose v1)**.</span></span> 
5. <span data-ttu-id="0d74d-124">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0d74d-124">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>
6. <span data-ttu-id="0d74d-125">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-125">Click **Create**.</span></span>

    ![Create new storage account](./media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-and-upload-a-file-to-the-storage-account"></a><span data-ttu-id="0d74d-127">Create a blob container and upload a file to the storage account</span><span class="sxs-lookup"><span data-stu-id="0d74d-127">Create a blob container and upload a file to the storage account</span></span>

<span data-ttu-id="0d74d-128">Files require blob storage so you need to create a blob container in which to store the file.</span><span class="sxs-lookup"><span data-stu-id="0d74d-128">Files require blob storage so you need to create a blob container in which to store the file.</span></span> <span data-ttu-id="0d74d-129">You then upload  a file to the blob container in the new storage account.</span><span class="sxs-lookup"><span data-stu-id="0d74d-129">You then upload  a file to the blob container in the new storage account.</span></span>

1. <span data-ttu-id="0d74d-130">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="0d74d-130">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="0d74d-131">Under **Blob Service**, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-131">Under **Blob Service**, click **Containers**.</span></span>
3. <span data-ttu-id="0d74d-132">Click **+ Container** on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="0d74d-132">Click **+ Container** on the top of the page.</span></span>
4. <span data-ttu-id="0d74d-133">Under **New container**, enter a name for the container and under **Public access level** keep the default value .</span><span class="sxs-lookup"><span data-stu-id="0d74d-133">Under **New container**, enter a name for the container and under **Public access level** keep the default value .</span></span>

    ![Create storage container](./media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

5. <span data-ttu-id="0d74d-135">Using an editor of your choice, create a file titled *hello world.txt* on your local machine.</span><span class="sxs-lookup"><span data-stu-id="0d74d-135">Using an editor of your choice, create a file titled *hello world.txt* on your local machine.</span></span>  <span data-ttu-id="0d74d-136">Open the file and add the text (without the quotes) "Hello world!</span><span class="sxs-lookup"><span data-stu-id="0d74d-136">Open the file and add the text (without the quotes) "Hello world!</span></span> <span data-ttu-id="0d74d-137">:)" and then save it.</span><span class="sxs-lookup"><span data-stu-id="0d74d-137">:)" and then save it.</span></span> 

6. <span data-ttu-id="0d74d-138">Upload the file to the newly created container by clicking on the container name, then **Upload**</span><span class="sxs-lookup"><span data-stu-id="0d74d-138">Upload the file to the newly created container by clicking on the container name, then **Upload**</span></span>
7. <span data-ttu-id="0d74d-139">In the **Upload blob** pane, under **Files**, click the folder icon and browse to the file **hello_world.txt** on your local machine, select the file, then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-139">In the **Upload blob** pane, under **Files**, click the folder icon and browse to the file **hello_world.txt** on your local machine, select the file, then click **Upload**.</span></span>

    ![Upload text file](./media/msi-tutorial-linux-vm-access-storage/upload-text-file.png)

## <a name="grant-your-vm-access-to-an-azure-storage-container"></a><span data-ttu-id="0d74d-141">Grant your VM access to an Azure Storage container</span><span class="sxs-lookup"><span data-stu-id="0d74d-141">Grant your VM access to an Azure Storage container</span></span> 

<span data-ttu-id="0d74d-142">You can use the VM's managed identity to retrieve the data in the Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="0d74d-142">You can use the VM's managed identity to retrieve the data in the Azure storage blob.</span></span>   

1. <span data-ttu-id="0d74d-143">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="0d74d-143">Navigate back to your newly created storage account.</span></span>  
2. <span data-ttu-id="0d74d-144">Click the **Access control (IAM)** link in the left panel.</span><span class="sxs-lookup"><span data-stu-id="0d74d-144">Click the **Access control (IAM)** link in the left panel.</span></span>  
3. <span data-ttu-id="0d74d-145">Click **+ Add** on top of the page to add a new role assignment for your VM.</span><span class="sxs-lookup"><span data-stu-id="0d74d-145">Click **+ Add** on top of the page to add a new role assignment for your VM.</span></span>
4. <span data-ttu-id="0d74d-146">Under **Role**, from the dropdown, select **Storage Blob Data Reader (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-146">Under **Role**, from the dropdown, select **Storage Blob Data Reader (Preview)**.</span></span> 
5. <span data-ttu-id="0d74d-147">In the next dropdown, under **Assign access to**, choose **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-147">In the next dropdown, under **Assign access to**, choose **Virtual Machine**.</span></span>  
6. <span data-ttu-id="0d74d-148">Next, ensure the proper subscription is listed in **Subscription** dropdown and then set **Resource Group** to **All resource groups**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-148">Next, ensure the proper subscription is listed in **Subscription** dropdown and then set **Resource Group** to **All resource groups**.</span></span>  
7. <span data-ttu-id="0d74d-149">Under **Select**, choose your VM and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-149">Under **Select**, choose your VM and then click **Save**.</span></span>

    ![Assign permissions](./media/tutorial-linux-vm-access-storage/access-storage-perms.png)

## <a name="get-an-access-token-and-use-it-to-call-azure-storage"></a><span data-ttu-id="0d74d-151">Get an access token and use it to call Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0d74d-151">Get an access token and use it to call Azure Storage</span></span>

<span data-ttu-id="0d74d-152">Azure Storage natively supports Azure AD authentication, so it can directly accept access tokens obtained using a Managed Identity.</span><span class="sxs-lookup"><span data-stu-id="0d74d-152">Azure Storage natively supports Azure AD authentication, so it can directly accept access tokens obtained using a Managed Identity.</span></span> <span data-ttu-id="0d74d-153">This is part of Azure Storage's integration with Azure AD, and is different from supplying credentials on the connection string.</span><span class="sxs-lookup"><span data-stu-id="0d74d-153">This is part of Azure Storage's integration with Azure AD, and is different from supplying credentials on the connection string.</span></span>

<span data-ttu-id="0d74d-154">To complete the following steps, you need to work from the VM created earlier and you need an SSH client to connect to it.</span><span class="sxs-lookup"><span data-stu-id="0d74d-154">To complete the following steps, you need to work from the VM created earlier and you need an SSH client to connect to it.</span></span> <span data-ttu-id="0d74d-155">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="0d74d-155">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="0d74d-156">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](~/articles/virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](~/articles/virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0d74d-156">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](~/articles/virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](~/articles/virtual-machines/linux/mac-create-ssh-keys.md).</span></span>

1. <span data-ttu-id="0d74d-157">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0d74d-157">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect**.</span></span> <span data-ttu-id="0d74d-158">Copy the string to connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="0d74d-158">Copy the string to connect to your VM.</span></span>
2. <span data-ttu-id="0d74d-159">**Connect** to the VM with the SSH client of your choice.</span><span class="sxs-lookup"><span data-stu-id="0d74d-159">**Connect** to the VM with the SSH client of your choice.</span></span> 
3. <span data-ttu-id="0d74d-160">In the terminal window, using CURL, make a request to the local Managed Identity endpoint to get an access token for Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0d74d-160">In the terminal window, using CURL, make a request to the local Managed Identity endpoint to get an access token for Azure Storage.</span></span>
    
    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fstorage.azure.com%2F' -H Metadata:true
    ```
4. <span data-ttu-id="0d74d-161">Now use the access token to access Azure Storage, for example to read the contents of the sample file which you previously uploaded to the container.</span><span class="sxs-lookup"><span data-stu-id="0d74d-161">Now use the access token to access Azure Storage, for example to read the contents of the sample file which you previously uploaded to the container.</span></span> <span data-ttu-id="0d74d-162">Replace the values of `<STORAGE ACCOUNT>`, `<CONTAINER NAME>`, and `<FILE NAME>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0d74d-162">Replace the values of `<STORAGE ACCOUNT>`, `<CONTAINER NAME>`, and `<FILE NAME>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.</span></span>

   ```bash
   curl https://<STORAGE ACCOUNT>.blob.core.windows.net/<CONTAINER NAME>/<FILE NAME> -H "x-ms-version: 2017-11-09" -H "Authorization: Bearer <ACCESS TOKEN>"
   ```

   <span data-ttu-id="0d74d-163">The response contains the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="0d74d-163">The response contains the contents of the file:</span></span>

   ```bash
   Hello world! :)
   ```

## <a name="next-steps"></a><span data-ttu-id="0d74d-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d74d-164">Next steps</span></span>

<span data-ttu-id="0d74d-165">In this tutorial, you learned how enable a Linux VM system-assigned managed identity to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0d74d-165">In this tutorial, you learned how enable a Linux VM system-assigned managed identity to access Azure Storage.</span></span>  <span data-ttu-id="0d74d-166">To learn more about Azure Storage see:</span><span class="sxs-lookup"><span data-stu-id="0d74d-166">To learn more about Azure Storage see:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d74d-167">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0d74d-167">Azure Storage</span></span>](/azure/storage/common/storage-introduction)
