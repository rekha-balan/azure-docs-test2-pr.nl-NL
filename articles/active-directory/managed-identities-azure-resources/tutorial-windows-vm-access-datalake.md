---
title: How to use a Windows VM system-assigned managed identity to access Azure Data Lake Store
description: A tutorial that shows you how to use a Windows VM system-assigned managed identity to access Azure Data Lake Store.
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
ms.openlocfilehash: 0acc5c8211d6f7715e97214c49ee4af37850e330
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855591"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-data-lake-store"></a><span data-ttu-id="44498-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44498-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Data Lake Store</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="44498-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44498-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access an Azure Data Lake Store.</span></span> <span data-ttu-id="44498-105">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="44498-105">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span></span> <span data-ttu-id="44498-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="44498-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44498-107">Grant your VM access to an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44498-107">Grant your VM access to an Azure Data Lake Store</span></span>
> * <span data-ttu-id="44498-108">Get an access token using the VM identity and use it to access an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44498-108">Get an access token using the VM identity and use it to access an Azure Data Lake Store</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44498-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="44498-109">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="44498-110">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="44498-110">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="44498-111">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="44498-111">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="44498-112">Enable system-assigned identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="44498-112">Enable system-assigned identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-azure-data-lake-store"></a><span data-ttu-id="44498-113">Grant your VM access to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44498-113">Grant your VM access to Azure Data Lake Store</span></span>

<span data-ttu-id="44498-114">Now you can grant your VM access to files and folders in an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44498-114">Now you can grant your VM access to files and folders in an Azure Data Lake Store.</span></span>  <span data-ttu-id="44498-115">For this step, you can use an existing Data Lake Store or create a new one.</span><span class="sxs-lookup"><span data-stu-id="44498-115">For this step, you can use an existing Data Lake Store or create a new one.</span></span>  <span data-ttu-id="44498-116">To create a new Data Lake Store using the Azure portal, follow this [Azure Data Lake Store quickstart](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="44498-116">To create a new Data Lake Store using the Azure portal, follow this [Azure Data Lake Store quickstart](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span></span> <span data-ttu-id="44498-117">There are also quickstarts that use the Azure CLI and Azure PowerShell in the [Azure Data Lake Store documentation](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="44498-117">There are also quickstarts that use the Azure CLI and Azure PowerShell in the [Azure Data Lake Store documentation](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="44498-118">In your Data Lake Store, create a new folder and grant your VM's system-assigned identity permission to read, write, and execute files in that folder:</span><span class="sxs-lookup"><span data-stu-id="44498-118">In your Data Lake Store, create a new folder and grant your VM's system-assigned identity permission to read, write, and execute files in that folder:</span></span>

1. <span data-ttu-id="44498-119">In the Azure portal, click **Data Lake Store** in the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="44498-119">In the Azure portal, click **Data Lake Store** in the left-hand navigation.</span></span>
2. <span data-ttu-id="44498-120">Click the Data Lake Store you want to use for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="44498-120">Click the Data Lake Store you want to use for this tutorial.</span></span>
3. <span data-ttu-id="44498-121">Click **Data Explorer** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="44498-121">Click **Data Explorer** in the command bar.</span></span>
4. <span data-ttu-id="44498-122">The root folder of the Data Lake Store is selected.</span><span class="sxs-lookup"><span data-stu-id="44498-122">The root folder of the Data Lake Store is selected.</span></span>  <span data-ttu-id="44498-123">Click **Access** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="44498-123">Click **Access** in the command bar.</span></span>
5. <span data-ttu-id="44498-124">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="44498-124">Click **Add**.</span></span>  <span data-ttu-id="44498-125">In the **Select** field, enter the name of your VM, for example **DevTestVM**.</span><span class="sxs-lookup"><span data-stu-id="44498-125">In the **Select** field, enter the name of your VM, for example **DevTestVM**.</span></span>  <span data-ttu-id="44498-126">Click to select your VM from the search results, then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="44498-126">Click to select your VM from the search results, then click **Select**.</span></span>
6. <span data-ttu-id="44498-127">Click **Select Permissions**.</span><span class="sxs-lookup"><span data-stu-id="44498-127">Click **Select Permissions**.</span></span>  <span data-ttu-id="44498-128">Select **Read** and **Execute**, add to **This folder**, and add as **An access permission only**.</span><span class="sxs-lookup"><span data-stu-id="44498-128">Select **Read** and **Execute**, add to **This folder**, and add as **An access permission only**.</span></span>  <span data-ttu-id="44498-129">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="44498-129">Click **Ok**.</span></span>  <span data-ttu-id="44498-130">The permission should be added successfully.</span><span class="sxs-lookup"><span data-stu-id="44498-130">The permission should be added successfully.</span></span>
7. <span data-ttu-id="44498-131">Close the **Access** blade.</span><span class="sxs-lookup"><span data-stu-id="44498-131">Close the **Access** blade.</span></span>
8. <span data-ttu-id="44498-132">For this tutorial, create a new folder.</span><span class="sxs-lookup"><span data-stu-id="44498-132">For this tutorial, create a new folder.</span></span>  <span data-ttu-id="44498-133">Click **New Folder** in the command bar, and give the new folder a name, for example **TestFolder**.</span><span class="sxs-lookup"><span data-stu-id="44498-133">Click **New Folder** in the command bar, and give the new folder a name, for example **TestFolder**.</span></span>  <span data-ttu-id="44498-134">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="44498-134">Click **Ok**.</span></span>
9. <span data-ttu-id="44498-135">Click on the folder you created, then click **Access** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="44498-135">Click on the folder you created, then click **Access** in the command bar.</span></span>
10. <span data-ttu-id="44498-136">Similar to step 5, click **Add**, in the **Select** field enter the name of your VM, select it and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="44498-136">Similar to step 5, click **Add**, in the **Select** field enter the name of your VM, select it and click **Select**.</span></span>
11. <span data-ttu-id="44498-137">Similar to step 6, click **Select Permissions**, select **Read**, **Write**, and **Execute**, add to **This folder**, and add as **An access permission entry and a default permission entry**.</span><span class="sxs-lookup"><span data-stu-id="44498-137">Similar to step 6, click **Select Permissions**, select **Read**, **Write**, and **Execute**, add to **This folder**, and add as **An access permission entry and a default permission entry**.</span></span>  <span data-ttu-id="44498-138">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="44498-138">Click **Ok**.</span></span>  <span data-ttu-id="44498-139">The permission should be added successfully.</span><span class="sxs-lookup"><span data-stu-id="44498-139">The permission should be added successfully.</span></span>

<span data-ttu-id="44498-140">Your VM's system-assigned managed identity can now perform all operations on files in the folder you created.</span><span class="sxs-lookup"><span data-stu-id="44498-140">Your VM's system-assigned managed identity can now perform all operations on files in the folder you created.</span></span>  <span data-ttu-id="44498-141">For more information on managing access to Data Lake Store, read this article on [Access Control in Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-access-control).</span><span class="sxs-lookup"><span data-stu-id="44498-141">For more information on managing access to Data Lake Store, read this article on [Access Control in Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-access-control).</span></span>

## <a name="get-an-access-token-using-the-vms-system-assigned-managed-identity-and-use-it-to-call-the-azure-data-lake-store-filesystem"></a><span data-ttu-id="44498-142">Get an access token using the VM's system-assigned managed identity and use it to call the Azure Data Lake Store filesystem</span><span class="sxs-lookup"><span data-stu-id="44498-142">Get an access token using the VM's system-assigned managed identity and use it to call the Azure Data Lake Store filesystem</span></span>

<span data-ttu-id="44498-143">Azure Data Lake Store natively supports Azure AD authentication, so it can directly accept access tokens obtained using managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="44498-143">Azure Data Lake Store natively supports Azure AD authentication, so it can directly accept access tokens obtained using managed identities for Azure resources.</span></span>  <span data-ttu-id="44498-144">To authenticate to the Data Lake Store filesystem you send an access token issued by Azure AD to your Data Lake Store filesystem endpoint, in an Authorization header in the format "Bearer <ACCESS_TOKEN_VALUE>".</span><span class="sxs-lookup"><span data-stu-id="44498-144">To authenticate to the Data Lake Store filesystem you send an access token issued by Azure AD to your Data Lake Store filesystem endpoint, in an Authorization header in the format "Bearer <ACCESS_TOKEN_VALUE>".</span></span>  <span data-ttu-id="44498-145">To learn more about Data Lake Store support for Azure AD authentication, read [Authentication with Data Lake Store using Azure Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lakes-store-authentication-using-azure-active-directory)</span><span class="sxs-lookup"><span data-stu-id="44498-145">To learn more about Data Lake Store support for Azure AD authentication, read [Authentication with Data Lake Store using Azure Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lakes-store-authentication-using-azure-active-directory)</span></span>

> [!NOTE]
> <span data-ttu-id="44498-146">The Data Lake Store filesystem client SDKs do not yet support managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="44498-146">The Data Lake Store filesystem client SDKs do not yet support managed identities for Azure resources.</span></span>  <span data-ttu-id="44498-147">This tutorial will be updated when support is added to the SDK.</span><span class="sxs-lookup"><span data-stu-id="44498-147">This tutorial will be updated when support is added to the SDK.</span></span>

<span data-ttu-id="44498-148">In this tutorial, you authenticate to the Data Lake Store filesystem REST API using PowerShell to make REST requests.</span><span class="sxs-lookup"><span data-stu-id="44498-148">In this tutorial, you authenticate to the Data Lake Store filesystem REST API using PowerShell to make REST requests.</span></span> <span data-ttu-id="44498-149">To use the VM's system-assigned managed identity for authentication, you need to make the requests from the VM.</span><span class="sxs-lookup"><span data-stu-id="44498-149">To use the VM's system-assigned managed identity for authentication, you need to make the requests from the VM.</span></span>

1. <span data-ttu-id="44498-150">In the portal, navigate to **Virtual Machines**, go to your Windows VM, and in the **Overview** click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="44498-150">In the portal, navigate to **Virtual Machines**, go to your Windows VM, and in the **Overview** click **Connect**.</span></span>
2. <span data-ttu-id="44498-151">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="44498-151">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3. <span data-ttu-id="44498-152">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span><span class="sxs-lookup"><span data-stu-id="44498-152">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span></span> 
4. <span data-ttu-id="44498-153">Using PowerShell’s `Invoke-WebRequest`, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44498-153">Using PowerShell’s `Invoke-WebRequest`, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Data Lake Store.</span></span>  <span data-ttu-id="44498-154">The resource identifier for Data Lake Store is "https://datalake.azure.net/".</span><span class="sxs-lookup"><span data-stu-id="44498-154">The resource identifier for Data Lake Store is "https://datalake.azure.net/".</span></span>  <span data-ttu-id="44498-155">Data Lake does an exact match on the resource identifier and the trailing slash is important.</span><span class="sxs-lookup"><span data-stu-id="44498-155">Data Lake does an exact match on the resource identifier and the trailing slash is important.</span></span>

   ```powershell
   $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fdatalake.azure.net%2F' -Method GET -Headers @{Metadata="true"}
   ```
    
   <span data-ttu-id="44498-156">Convert the response from a JSON object to a PowerShell object.</span><span class="sxs-lookup"><span data-stu-id="44498-156">Convert the response from a JSON object to a PowerShell object.</span></span> 
    
   ```powershell
   $content = $response.Content | ConvertFrom-Json
   ```

   <span data-ttu-id="44498-157">Extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="44498-157">Extract the access token from the response.</span></span>
    
   ```powershell
   $AccessToken = $content.access_token
   ```

5. <span data-ttu-id="44498-158">Using PowerShell's \`Invoke-WebRequest', make a request to your Data Lake Store's REST endpoint to list the folders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="44498-158">Using PowerShell's \`Invoke-WebRequest', make a request to your Data Lake Store's REST endpoint to list the folders in the root folder.</span></span>  <span data-ttu-id="44498-159">This is a simple way to check everything is configured correctly.</span><span class="sxs-lookup"><span data-stu-id="44498-159">This is a simple way to check everything is configured correctly.</span></span>  <span data-ttu-id="44498-160">It is important the string "Bearer" in the Authorization header has a capital "B".</span><span class="sxs-lookup"><span data-stu-id="44498-160">It is important the string "Bearer" in the Authorization header has a capital "B".</span></span>  <span data-ttu-id="44498-161">You can find the name of your Data Lake Store in the **Overview** section of the Data Lake Store blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="44498-161">You can find the name of your Data Lake Store in the **Overview** section of the Data Lake Store blade in the Azure portal.</span></span>

   ```powershell
   Invoke-WebRequest -Uri https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS -Headers @{Authorization="Bearer $AccessToken"}
   ```

   <span data-ttu-id="44498-162">A successful response looks like:</span><span class="sxs-lookup"><span data-stu-id="44498-162">A successful response looks like:</span></span>

   ```powershell
   StatusCode        : 200
   StatusDescription : OK
   Content           : {"FileStatuses":{"FileStatus":[{"length":0,"pathSuffix":"TestFolder","type":"DIRECTORY", "blockSize":0,"accessTime":1507934941392, "modificationTime":1507944835699,"replication":0, "permission":"770","ow..."
   RawContent        : HTTP/1.1 200 OK
                       Pragma: no-cache
                       x-ms-request-id: b4b31e16-e968-46a1-879a-3474aa7d4528
                       x-ms-webhdfs-version: 17.04.22.00
                       Status: 0x0
                       X-Content-Type-Options: nosniff
                       Strict-Transport-Security: ma...
   Forms             : {}
   Headers           : {[Pragma, no-cache], [x-ms-request-id, b4b31e16-e968-46a1-879a-3474aa7d4528],
                       [x-ms-webhdfs-version, 17.04.22.00], [Status, 0x0]...}
   Images            : {}
   InputFields       : {}
   Links             : {}
   ParsedHtml        : System.__ComObject
   RawContentLength  : 556
   ```

6. <span data-ttu-id="44498-163">Now you can try uploading a file to your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44498-163">Now you can try uploading a file to your Data Lake Store.</span></span>  <span data-ttu-id="44498-164">First, create a file to upload.</span><span class="sxs-lookup"><span data-stu-id="44498-164">First, create a file to upload.</span></span>

   ```powershell
   echo "Test file." > Test1.txt
   ```

7. <span data-ttu-id="44498-165">Using PowerShell's `Invoke-WebRequest`, make a request to your Data Lake Store's REST endpoint to upload the file to the folder you created earlier.</span><span class="sxs-lookup"><span data-stu-id="44498-165">Using PowerShell's `Invoke-WebRequest`, make a request to your Data Lake Store's REST endpoint to upload the file to the folder you created earlier.</span></span>  <span data-ttu-id="44498-166">This request takes two steps.</span><span class="sxs-lookup"><span data-stu-id="44498-166">This request takes two steps.</span></span>  <span data-ttu-id="44498-167">In the first step, you make a request and get a redirection to where the file should be uploaded.</span><span class="sxs-lookup"><span data-stu-id="44498-167">In the first step, you make a request and get a redirection to where the file should be uploaded.</span></span>  <span data-ttu-id="44498-168">In the second step, you actually upload the file.</span><span class="sxs-lookup"><span data-stu-id="44498-168">In the second step, you actually upload the file.</span></span>  <span data-ttu-id="44498-169">Remember to set the name of the folder and file appropriately if you used different values than in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="44498-169">Remember to set the name of the folder and file appropriately if you used different values than in this tutorial.</span></span> 

   ```powershell
   $HdfsRedirectResponse = Invoke-WebRequest -Uri https://<YOUR_ADLS_NAME>.azuredatalakestore.net/webhdfs/v1/TestFolder/Test1.txt?op=CREATE -Method PUT -Headers @{Authorization="Bearer $AccessToken"} -Infile Test1.txt -MaximumRedirection 0
   ```

   <span data-ttu-id="44498-170">If you inspect the value of `$HdfsRedirectResponse` it should look like the following response:</span><span class="sxs-lookup"><span data-stu-id="44498-170">If you inspect the value of `$HdfsRedirectResponse` it should look like the following response:</span></span>

   ```powershell
   PS C:\> $HdfsRedirectResponse

   StatusCode        : 307
   StatusDescription : Temporary Redirect
   Content           : {}
   RawContent        : HTTP/1.1 307 Temporary Redirect
                       Pragma: no-cache
                       x-ms-request-id: b7ab492f-b514-4483-aada-4aa0611d12b3
                       ContentLength: 0
                       x-ms-webhdfs-version: 17.04.22.00
                       Status: 0x0
                       X-Content-Type-Options: nosn...
   Headers           : {[Pragma, no-cache], [x-ms-request-id, b7ab492f-b514-4483-aada-4aa0611d12b3], 
                       [ContentLength, 0], [x-ms-webhdfs-version, 17.04.22.00]...}
   RawContentLength  : 0
   ```

   <span data-ttu-id="44498-171">Complete the upload by sending a request to the redirect endpoint:</span><span class="sxs-lookup"><span data-stu-id="44498-171">Complete the upload by sending a request to the redirect endpoint:</span></span>

   ```powershell
   Invoke-WebRequest -Uri $HdfsRedirectResponse.Headers.Location -Method PUT -Headers @{Authorization="Bearer $AccessToken"} -Infile Test1.txt -MaximumRedirection 0
   ```

   <span data-ttu-id="44498-172">A successful response look like:</span><span class="sxs-lookup"><span data-stu-id="44498-172">A successful response look like:</span></span>

   ```powershell
   StatusCode        : 201
   StatusDescription : Created
   Content           : {}
   RawContent        : HTTP/1.1 201 Created
                       Pragma: no-cache
                       x-ms-request-id: 1e70f36f-ead1-4566-acfa-d0c3ec1e2307
                       ContentLength: 0
                       x-ms-webhdfs-version: 17.04.22.00
                       Status: 0x0
                       X-Content-Type-Options: nosniff
                       Strict...
   Headers           : {[Pragma, no-cache], [x-ms-request-id, 1e70f36f-ead1-4566-acfa-d0c3ec1e2307],
                       [ContentLength, 0], [x-ms-webhdfs-version, 17.04.22.00]...}
   RawContentLength  : 0
   ```

<span data-ttu-id="44498-173">Using other Data Lake Store filesystem APIs you can append to files, download files, and more.</span><span class="sxs-lookup"><span data-stu-id="44498-173">Using other Data Lake Store filesystem APIs you can append to files, download files, and more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44498-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="44498-174">Next steps</span></span>

<span data-ttu-id="44498-175">In this tutorial, you learned how to use a system-assigned managed identity for a Windows virtual machine to access an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44498-175">In this tutorial, you learned how to use a system-assigned managed identity for a Windows virtual machine to access an Azure Data Lake Store.</span></span> <span data-ttu-id="44498-176">To learn more about Azure Data Lake Store see:</span><span class="sxs-lookup"><span data-stu-id="44498-176">To learn more about Azure Data Lake Store see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="44498-177">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44498-177">Azure Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)