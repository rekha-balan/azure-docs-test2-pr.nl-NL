---
title: Use a Linux VM system-assigned managed identity to access Azure Data Lake Store
description: A tutorial that shows you how to use a Linux VM system-assigned managed identity to access Azure Data Lake Store.
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
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: 2a3a46b5f2adf052f04530a8d587a577b14b709b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870682"
---
# <a name="tutorial-use-a-linux-vm-system-assigned-managed-identity-to-access-azure-data-lake-store"></a><span data-ttu-id="56ba5-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56ba5-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Data Lake Store</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="56ba5-104">This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56ba5-104">This tutorial shows you how to use a system-assigned managed identity for a Linux virtual machine (VM) to access Cosmos DB.</span></span> <span data-ttu-id="56ba5-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="56ba5-105">You learn how to:</span></span> 

<span data-ttu-id="56ba5-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="56ba5-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56ba5-107">Grant your VM access to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="56ba5-107">Grant your VM access to Azure Data Lake Store.</span></span>
> * <span data-ttu-id="56ba5-108">Get an access token by using the VM's system-assigned managed identity to access Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="56ba5-108">Get an access token by using the VM's system-assigned managed identity to access Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56ba5-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56ba5-109">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="56ba5-110">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="56ba5-110">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="56ba5-111">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="56ba5-111">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

- [<span data-ttu-id="56ba5-112">Enable system-assigned identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="56ba5-112">Enable system-assigned identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-azure-data-lake-store"></a><span data-ttu-id="56ba5-113">Grant your VM access to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56ba5-113">Grant your VM access to Azure Data Lake Store</span></span>

<span data-ttu-id="56ba5-114">Now you can grant your VM access to files and folders in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="56ba5-114">Now you can grant your VM access to files and folders in Azure Data Lake Store.</span></span> <span data-ttu-id="56ba5-115">For this step, you can use an existing Data Lake Store instance or create a new one.</span><span class="sxs-lookup"><span data-stu-id="56ba5-115">For this step, you can use an existing Data Lake Store instance or create a new one.</span></span> <span data-ttu-id="56ba5-116">To create a Data Lake Store instance by using the Azure portal, follow the [Azure Data Lake Store quickstart](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="56ba5-116">To create a Data Lake Store instance by using the Azure portal, follow the [Azure Data Lake Store quickstart](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span></span> <span data-ttu-id="56ba5-117">There are also quickstarts that use Azure CLI and Azure PowerShell in the [Azure Data Lake Store documentation](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="56ba5-117">There are also quickstarts that use Azure CLI and Azure PowerShell in the [Azure Data Lake Store documentation](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="56ba5-118">In Data Lake Store, create a new folder and grant our Linux VM system-assigned managed identity permission to read, write, and execute files in that folder:</span><span class="sxs-lookup"><span data-stu-id="56ba5-118">In Data Lake Store, create a new folder and grant our Linux VM system-assigned managed identity permission to read, write, and execute files in that folder:</span></span>

1. <span data-ttu-id="56ba5-119">In the Azure portal, select **Data Lake Store** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="56ba5-119">In the Azure portal, select **Data Lake Store** in the left pane.</span></span>
2. <span data-ttu-id="56ba5-120">Select the Data Lake Store instance that you want to use.</span><span class="sxs-lookup"><span data-stu-id="56ba5-120">Select the Data Lake Store instance that you want to use.</span></span>
3. <span data-ttu-id="56ba5-121">Select **Data Explorer** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="56ba5-121">Select **Data Explorer** on the command bar.</span></span>
4. <span data-ttu-id="56ba5-122">The root folder of the Data Lake Store instance is selected.</span><span class="sxs-lookup"><span data-stu-id="56ba5-122">The root folder of the Data Lake Store instance is selected.</span></span> <span data-ttu-id="56ba5-123">Select **Access** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="56ba5-123">Select **Access** on the command bar.</span></span>
5. <span data-ttu-id="56ba5-124">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-124">Select **Add**.</span></span>  <span data-ttu-id="56ba5-125">In the **Select** box, enter the name of your VM--for example, **DevTestVM**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-125">In the **Select** box, enter the name of your VM--for example, **DevTestVM**.</span></span> <span data-ttu-id="56ba5-126">Select your VM from the search results, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-126">Select your VM from the search results, and then click **Select**.</span></span>
6. <span data-ttu-id="56ba5-127">Click **Select Permissions**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-127">Click **Select Permissions**.</span></span>  <span data-ttu-id="56ba5-128">Select **Read** and **Execute**, add to **This folder**, and add as **An access permission only**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-128">Select **Read** and **Execute**, add to **This folder**, and add as **An access permission only**.</span></span> <span data-ttu-id="56ba5-129">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-129">Select **Ok**.</span></span>  <span data-ttu-id="56ba5-130">The permission should be added successfully.</span><span class="sxs-lookup"><span data-stu-id="56ba5-130">The permission should be added successfully.</span></span>
7. <span data-ttu-id="56ba5-131">Close the **Access** pane.</span><span class="sxs-lookup"><span data-stu-id="56ba5-131">Close the **Access** pane.</span></span>
8. <span data-ttu-id="56ba5-132">For this tutorial, create a new folder.</span><span class="sxs-lookup"><span data-stu-id="56ba5-132">For this tutorial, create a new folder.</span></span> <span data-ttu-id="56ba5-133">Select **New Folder** on the command bar, and give the new folder a name--for example **TestFolder**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-133">Select **New Folder** on the command bar, and give the new folder a name--for example **TestFolder**.</span></span>  <span data-ttu-id="56ba5-134">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-134">Select **Ok**.</span></span>
9. <span data-ttu-id="56ba5-135">Select the folder that you created, and then select **Access** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="56ba5-135">Select the folder that you created, and then select **Access** on the command bar.</span></span>
10. <span data-ttu-id="56ba5-136">Similar to step 5, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-136">Similar to step 5, select **Add**.</span></span> <span data-ttu-id="56ba5-137">In the **Select** box, enter the name of your VM.</span><span class="sxs-lookup"><span data-stu-id="56ba5-137">In the **Select** box, enter the name of your VM.</span></span> <span data-ttu-id="56ba5-138">Select your VM from the search results, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-138">Select your VM from the search results, and then click **Select**.</span></span>
11. <span data-ttu-id="56ba5-139">Similar to step 6, select **Select Permissions**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-139">Similar to step 6, select **Select Permissions**.</span></span> <span data-ttu-id="56ba5-140">Select **Read**, **Write**, and **Execute**, add to **This folder**, and add as **An access permission entry and a default permission entry**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-140">Select **Read**, **Write**, and **Execute**, add to **This folder**, and add as **An access permission entry and a default permission entry**.</span></span> <span data-ttu-id="56ba5-141">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-141">Select **Ok**.</span></span>  <span data-ttu-id="56ba5-142">The permission should be added successfully.</span><span class="sxs-lookup"><span data-stu-id="56ba5-142">The permission should be added successfully.</span></span>

<span data-ttu-id="56ba5-143">Managed identities for Azure resources can now perform all operations on files in the folder that you created.</span><span class="sxs-lookup"><span data-stu-id="56ba5-143">Managed identities for Azure resources can now perform all operations on files in the folder that you created.</span></span> <span data-ttu-id="56ba5-144">For more information on managing access to Data Lake Store, see [Access Control in Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-access-control).</span><span class="sxs-lookup"><span data-stu-id="56ba5-144">For more information on managing access to Data Lake Store, see [Access Control in Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-access-control).</span></span>

## <a name="get-an-access-token-and-call-the-data-lake-store-file-system"></a><span data-ttu-id="56ba5-145">Get an access token and call the Data Lake Store file system</span><span class="sxs-lookup"><span data-stu-id="56ba5-145">Get an access token and call the Data Lake Store file system</span></span>

<span data-ttu-id="56ba5-146">Azure Data Lake Store natively supports Azure AD authentication, so it can directly accept access tokens obtained via using managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="56ba5-146">Azure Data Lake Store natively supports Azure AD authentication, so it can directly accept access tokens obtained via using managed identities for Azure resources.</span></span> <span data-ttu-id="56ba5-147">To authenticate to the Data Lake Store file system, you send an access token issued by Azure AD to your Data Lake Store file system endpoint.</span><span class="sxs-lookup"><span data-stu-id="56ba5-147">To authenticate to the Data Lake Store file system, you send an access token issued by Azure AD to your Data Lake Store file system endpoint.</span></span> <span data-ttu-id="56ba5-148">The access token is in an authorization header in the format "Bearer \<ACCESS_TOKEN_VALUE\>".</span><span class="sxs-lookup"><span data-stu-id="56ba5-148">The access token is in an authorization header in the format "Bearer \<ACCESS_TOKEN_VALUE\>".</span></span>  <span data-ttu-id="56ba5-149">To learn more about Data Lake Store support for Azure AD authentication, see [Authentication with Data Lake Store using Azure Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lakes-store-authentication-using-azure-active-directory).</span><span class="sxs-lookup"><span data-stu-id="56ba5-149">To learn more about Data Lake Store support for Azure AD authentication, see [Authentication with Data Lake Store using Azure Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lakes-store-authentication-using-azure-active-directory).</span></span>

<span data-ttu-id="56ba5-150">In this tutorial, you authenticate to the REST API for the Data Lake Store file system by using cURL to make REST requests.</span><span class="sxs-lookup"><span data-stu-id="56ba5-150">In this tutorial, you authenticate to the REST API for the Data Lake Store file system by using cURL to make REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="56ba5-151">The client SDKs for the Data Lake Store file system do not yet support managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="56ba5-151">The client SDKs for the Data Lake Store file system do not yet support managed identities for Azure resources.</span></span>

<span data-ttu-id="56ba5-152">To complete these steps, you need an SSH client.</span><span class="sxs-lookup"><span data-stu-id="56ba5-152">To complete these steps, you need an SSH client.</span></span> <span data-ttu-id="56ba5-153">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="56ba5-153">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="56ba5-154">If you need assistance configuring your SSH client's keys, see [How to use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md) or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="56ba5-154">If you need assistance configuring your SSH client's keys, see [How to use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md) or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>

1. <span data-ttu-id="56ba5-155">In the portal, browse to your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="56ba5-155">In the portal, browse to your Linux VM.</span></span> <span data-ttu-id="56ba5-156">In **Overview**, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="56ba5-156">In **Overview**, select **Connect**.</span></span>  
2. <span data-ttu-id="56ba5-157">Connect to the VM by using the SSH client of your choice.</span><span class="sxs-lookup"><span data-stu-id="56ba5-157">Connect to the VM by using the SSH client of your choice.</span></span> 
3. <span data-ttu-id="56ba5-158">In the terminal window, by using cURL, make a request to the local managed identities Azure for Azure resources endpoint to get an access token for the Data Lake Store file system.</span><span class="sxs-lookup"><span data-stu-id="56ba5-158">In the terminal window, by using cURL, make a request to the local managed identities Azure for Azure resources endpoint to get an access token for the Data Lake Store file system.</span></span> <span data-ttu-id="56ba5-159">The resource identifier for Data Lake Store is "https://datalake.azure.net/".</span><span class="sxs-lookup"><span data-stu-id="56ba5-159">The resource identifier for Data Lake Store is "https://datalake.azure.net/".</span></span>  <span data-ttu-id="56ba5-160">It's important to include the trailing slash in the resource identifier.</span><span class="sxs-lookup"><span data-stu-id="56ba5-160">It's important to include the trailing slash in the resource identifier.</span></span>
    
   ```bash
   curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fdatalake.azure.net%2F' -H Metadata:true   
   ```
    
   <span data-ttu-id="56ba5-161">A successful response returns the access token that you use to authenticate to Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="56ba5-161">A successful response returns the access token that you use to authenticate to Data Lake Store:</span></span>

   ```bash
   {"access_token":"eyJ0eXAiOiJ...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1508119757",
    "not_before":"1508115857",
    "resource":"https://datalake.azure.net/",
    "token_type":"Bearer"}
   ```

4. <span data-ttu-id="56ba5-162">By using cURL, make a request to your Data Lake Store file system's REST endpoint to list the folders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="56ba5-162">By using cURL, make a request to your Data Lake Store file system's REST endpoint to list the folders in the root folder.</span></span> <span data-ttu-id="56ba5-163">This is a simple way to check that everything is configured correctly.</span><span class="sxs-lookup"><span data-stu-id="56ba5-163">This is a simple way to check that everything is configured correctly.</span></span> <span data-ttu-id="56ba5-164">Copy the value of the access token from the previous step.</span><span class="sxs-lookup"><span data-stu-id="56ba5-164">Copy the value of the access token from the previous step.</span></span> <span data-ttu-id="56ba5-165">It's important that the string "Bearer" in the Authorization header has a capital "B."</span><span class="sxs-lookup"><span data-stu-id="56ba5-165">It's important that the string "Bearer" in the Authorization header has a capital "B."</span></span> <span data-ttu-id="56ba5-166">You can find the name of your Data Lake Store instance in the **Overview** section of the **Data Lake Store** pane in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56ba5-166">You can find the name of your Data Lake Store instance in the **Overview** section of the **Data Lake Store** pane in the Azure portal.</span></span>

   ```bash
   curl https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS -H "Authorization: Bearer <ACCESS_TOKEN>"
   ```
    
   <span data-ttu-id="56ba5-167">A successful response looks like this:</span><span class="sxs-lookup"><span data-stu-id="56ba5-167">A successful response looks like this:</span></span>

   ```bash
   {"FileStatuses":{"FileStatus":[{"length":0,"pathSuffix":"TestFolder","type":"DIRECTORY","blockSize":0,"accessTime":1507934941392,"modificationTime":1508105430590,"replication":0,"permission":"770","owner":"bd0e76d8-ad45-4fe1-8941-04a7bf27f071","group":"bd0e76d8-ad45-4fe1-8941-04a7bf27f071"}]}}
   ```

5. <span data-ttu-id="56ba5-168">Now you can try uploading a file to your Data Lake Store instance.</span><span class="sxs-lookup"><span data-stu-id="56ba5-168">Now you can try uploading a file to your Data Lake Store instance.</span></span> <span data-ttu-id="56ba5-169">First, create a file to upload.</span><span class="sxs-lookup"><span data-stu-id="56ba5-169">First, create a file to upload.</span></span>

   ```bash
   echo "Test file." > Test1.txt
   ```

6. <span data-ttu-id="56ba5-170">By using cURL, make a request to your Data Lake Store file system's REST endpoint to upload the file to the folder that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="56ba5-170">By using cURL, make a request to your Data Lake Store file system's REST endpoint to upload the file to the folder that you created earlier.</span></span> <span data-ttu-id="56ba5-171">The upload involves a redirect, and cURL follows the redirect automatically.</span><span class="sxs-lookup"><span data-stu-id="56ba5-171">The upload involves a redirect, and cURL follows the redirect automatically.</span></span> 

   ```bash
   curl -i -X PUT -L -T Test1.txt -H "Authorization: Bearer <ACCESS_TOKEN>" 'https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/<FOLDER_NAME>/Test1.txt?op=CREATE' 
   ```

    <span data-ttu-id="56ba5-172">A successful response looks like this:</span><span class="sxs-lookup"><span data-stu-id="56ba5-172">A successful response looks like this:</span></span>

   ```bash
   HTTP/1.1 100 Continue
   HTTP/1.1 307 Temporary Redirect
   Cache-Control: no-cache, no-cache, no-store, max-age=0
   Pragma: no-cache
   Expires: -1
   Location: https://mytestadls.azuredatalakestore.net/webhdfs/v1/TestFolder/Test1.txt?op=CREATE&write=true
   x-ms-request-id: 756f6b24-0cca-47ef-aa12-52c3b45b954c
   ContentLength: 0
   x-ms-webhdfs-version: 17.04.22.00
   Status: 0x0
   X-Content-Type-Options: nosniff
   Strict-Transport-Security: max-age=15724800; includeSubDomains
   Date: Sun, 15 Oct 2017 22:10:30 GMT
   Content-Length: 0
       
   HTTP/1.1 100 Continue
       
   HTTP/1.1 201 Created
   Cache-Control: no-cache, no-cache, no-store, max-age=0
   Pragma: no-cache
   Expires: -1
   Location: https://mytestadls.azuredatalakestore.net/webhdfs/v1/TestFolder/Test1.txt?op=CREATE&write=true
   x-ms-request-id: af5baa07-3c79-43af-a01a-71d63d53e6c4
   ContentLength: 0
   x-ms-webhdfs-version: 17.04.22.00
   Status: 0x0
   X-Content-Type-Options: nosniff
   Strict-Transport-Security: max-age=15724800; includeSubDomains
   Date: Sun, 15 Oct 2017 22:10:30 GMT
   Content-Length: 0
   ```

<span data-ttu-id="56ba5-173">By using other APIs for the Data Lake Store file system, you can append to files, download files, and more.</span><span class="sxs-lookup"><span data-stu-id="56ba5-173">By using other APIs for the Data Lake Store file system, you can append to files, download files, and more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56ba5-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="56ba5-174">Next steps</span></span>

<span data-ttu-id="56ba5-175">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="56ba5-175">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access an Azure Data Lake Store.</span></span> <span data-ttu-id="56ba5-176">To learn more about Azure Data Lake Store see:</span><span class="sxs-lookup"><span data-stu-id="56ba5-176">To learn more about Azure Data Lake Store see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="56ba5-177">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56ba5-177">Azure Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)
