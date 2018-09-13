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
ms.date: 04/12/2018
ms.author: daveba
ms.openlocfilehash: 46be9469e67a4f456be100823d475b8720262b1b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867377"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-storage"></a><span data-ttu-id="7c7a3-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c7a3-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Storage</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="7c7a3-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Azure Storage.</span></span> <span data-ttu-id="7c7a3-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="7c7a3-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c7a3-106">Create a blob container in a storage account</span><span class="sxs-lookup"><span data-stu-id="7c7a3-106">Create a blob container in a storage account</span></span>
> * <span data-ttu-id="7c7a3-107">Grant your Windows VM's system-assigned managed identity access to a storage account</span><span class="sxs-lookup"><span data-stu-id="7c7a3-107">Grant your Windows VM's system-assigned managed identity access to a storage account</span></span> 
> * <span data-ttu-id="7c7a3-108">Get an access and use it to call Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c7a3-108">Get an access and use it to call Azure Storage</span></span> 

> [!NOTE]
> <span data-ttu-id="7c7a3-109">Azure Active Directory authentication for Azure Storage is in public preview.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-109">Azure Active Directory authentication for Azure Storage is in public preview.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c7a3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c7a3-110">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="7c7a3-111">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="7c7a3-111">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="7c7a3-112">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="7c7a3-112">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="7c7a3-113">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="7c7a3-113">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="create-a-storage-account"></a><span data-ttu-id="7c7a3-114">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="7c7a3-114">Create a storage account</span></span> 

<span data-ttu-id="7c7a3-115">In this section, you create a storage account.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-115">In this section, you create a storage account.</span></span> 

1. <span data-ttu-id="7c7a3-116">Click the **+ Create a resource** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-116">Click the **+ Create a resource** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="7c7a3-117">Click **Storage**, then **Storage account - blob, file, table, queue**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-117">Click **Storage**, then **Storage account - blob, file, table, queue**.</span></span>
3. <span data-ttu-id="7c7a3-118">Under **Name**, enter a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-118">Under **Name**, enter a name for the storage account.</span></span>  
4. <span data-ttu-id="7c7a3-119">**Deployment model** and **Account kind** should be set to **Resource manager** and **Storage (general purpose v1)**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-119">**Deployment model** and **Account kind** should be set to **Resource manager** and **Storage (general purpose v1)**.</span></span> 
5. <span data-ttu-id="7c7a3-120">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-120">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>
6. <span data-ttu-id="7c7a3-121">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-121">Click **Create**.</span></span>

    ![Create new storage account](./media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-and-upload-a-file-to-the-storage-account"></a><span data-ttu-id="7c7a3-123">Create a blob container and upload a file to the storage account</span><span class="sxs-lookup"><span data-stu-id="7c7a3-123">Create a blob container and upload a file to the storage account</span></span>

<span data-ttu-id="7c7a3-124">Files require blob storage so you need to create a blob container in which to store the file.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-124">Files require blob storage so you need to create a blob container in which to store the file.</span></span> <span data-ttu-id="7c7a3-125">You then upload a file to the blob container in the new storage account.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-125">You then upload a file to the blob container in the new storage account.</span></span>

1. <span data-ttu-id="7c7a3-126">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-126">Navigate back to your newly created storage account.</span></span>
2. <span data-ttu-id="7c7a3-127">Under **Blob Service**, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-127">Under **Blob Service**, click **Containers**.</span></span>
3. <span data-ttu-id="7c7a3-128">Click **+ Container** on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-128">Click **+ Container** on the top of the page.</span></span>
4. <span data-ttu-id="7c7a3-129">Under **New container**, enter a name for the container and under **Public access level** keep the default value .</span><span class="sxs-lookup"><span data-stu-id="7c7a3-129">Under **New container**, enter a name for the container and under **Public access level** keep the default value .</span></span>

    ![Create storage container](./media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

5. <span data-ttu-id="7c7a3-131">Using an editor of your choice, create a file titled *hello world.txt* on your local machine.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-131">Using an editor of your choice, create a file titled *hello world.txt* on your local machine.</span></span>  <span data-ttu-id="7c7a3-132">Open the file and add the text (without the quotes) "Hello world!</span><span class="sxs-lookup"><span data-stu-id="7c7a3-132">Open the file and add the text (without the quotes) "Hello world!</span></span> <span data-ttu-id="7c7a3-133">:)" and then save it.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-133">:)" and then save it.</span></span> 
6. <span data-ttu-id="7c7a3-134">Upload the file to the newly created container by clicking on the container name, then **Upload**</span><span class="sxs-lookup"><span data-stu-id="7c7a3-134">Upload the file to the newly created container by clicking on the container name, then **Upload**</span></span>
7. <span data-ttu-id="7c7a3-135">In the **Upload blob** pane, under **Files**, click the folder icon and browse to the file **hello_world.txt** on your local machine, select the file, then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-135">In the **Upload blob** pane, under **Files**, click the folder icon and browse to the file **hello_world.txt** on your local machine, select the file, then click **Upload**.</span></span>
    <span data-ttu-id="7c7a3-136">![Upload text file](./media/msi-tutorial-linux-vm-access-storage/upload-text-file.png)</span><span class="sxs-lookup"><span data-stu-id="7c7a3-136">![Upload text file](./media/msi-tutorial-linux-vm-access-storage/upload-text-file.png)</span></span>

## <a name="grant-your-vm-access-to-an-azure-storage-container"></a><span data-ttu-id="7c7a3-137">Grant your VM access to an Azure Storage container</span><span class="sxs-lookup"><span data-stu-id="7c7a3-137">Grant your VM access to an Azure Storage container</span></span> 

<span data-ttu-id="7c7a3-138">You can use the VM's system-assigned managed identity to retrieve the data in the Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-138">You can use the VM's system-assigned managed identity to retrieve the data in the Azure storage blob.</span></span>   

1. <span data-ttu-id="7c7a3-139">Navigate back to your newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-139">Navigate back to your newly created storage account.</span></span>  
2. <span data-ttu-id="7c7a3-140">Click the **Access control (IAM)** link in the left panel.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-140">Click the **Access control (IAM)** link in the left panel.</span></span>  
3. <span data-ttu-id="7c7a3-141">Click **+ Add** on top of the page to add a new role assignment for your VM.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-141">Click **+ Add** on top of the page to add a new role assignment for your VM.</span></span>
4. <span data-ttu-id="7c7a3-142">Under **Role**, from the dropdown, select **Storage Blob Data Reader (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-142">Under **Role**, from the dropdown, select **Storage Blob Data Reader (Preview)**.</span></span> 
5. <span data-ttu-id="7c7a3-143">In the next dropdown, under **Assign access to**, choose **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-143">In the next dropdown, under **Assign access to**, choose **Virtual Machine**.</span></span>  
6. <span data-ttu-id="7c7a3-144">Next, ensure the proper subscription is listed in **Subscription** dropdown and then set **Resource Group** to **All resource groups**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-144">Next, ensure the proper subscription is listed in **Subscription** dropdown and then set **Resource Group** to **All resource groups**.</span></span>  
7. <span data-ttu-id="7c7a3-145">Under **Select**, choose your VM and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-145">Under **Select**, choose your VM and then click **Save**.</span></span> 

    ![Assign permissions](./media/tutorial-linux-vm-access-storage/access-storage-perms.png)

## <a name="get-an-access-token-and-use-it-to-call-azure-storage"></a><span data-ttu-id="7c7a3-147">Get an access token and use it to call Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c7a3-147">Get an access token and use it to call Azure Storage</span></span> 

<span data-ttu-id="7c7a3-148">Azure Storage natively supports Azure AD authentication, so it can directly accept access tokens obtained using a managed identity.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-148">Azure Storage natively supports Azure AD authentication, so it can directly accept access tokens obtained using a managed identity.</span></span> <span data-ttu-id="7c7a3-149">This is part of Azure Storage's integration with Azure AD, and is different from supplying credentials on the connection string.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-149">This is part of Azure Storage's integration with Azure AD, and is different from supplying credentials on the connection string.</span></span>

<span data-ttu-id="7c7a3-150">Here's a .Net code example of opening a connection to Azure Storage using an access token and then reading the contents of the file you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-150">Here's a .Net code example of opening a connection to Azure Storage using an access token and then reading the contents of the file you created earlier.</span></span> <span data-ttu-id="7c7a3-151">This code must run on the VM to be able to access the VM's managed identity endpoint.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-151">This code must run on the VM to be able to access the VM's managed identity endpoint.</span></span> <span data-ttu-id="7c7a3-152">.Net Framework 4.6 or higher is required to use the access token method.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-152">.Net Framework 4.6 or higher is required to use the access token method.</span></span> <span data-ttu-id="7c7a3-153">Replace the value of `<URI to blob file>` accordingly.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-153">Replace the value of `<URI to blob file>` accordingly.</span></span> <span data-ttu-id="7c7a3-154">You can obtain this value by navigating to file you created and uploaded to blob storage and copying the **URL** under **Properties** the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-154">You can obtain this value by navigating to file you created and uploaded to blob storage and copying the **URL** under **Properties** the **Overview** page.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Net;
using System.Web.Script.Serialization; 
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;

namespace StorageOAuthToken
{
    class Program
    {
        static void Main(string[] args)
        {
            //get token
            string accessToken = GetMSIToken("https://storage.azure.com/");
           
            //create token credential
            TokenCredential tokenCredential = new TokenCredential(accessToken);

            //create storage credentials
            StorageCredentials storageCredentials = new StorageCredentials(tokenCredential);

            Uri blobAddress = new Uri("<URI to blob file>");

            //create block blob using storage credentials
            CloudBlockBlob blob = new CloudBlockBlob(blobAddress, storageCredentials);
        
            //retrieve blob contents
            Console.WriteLine(blob.DownloadText());
            Console.ReadLine();
        }

        static string GetMSIToken(string resourceID)
        {
            string accessToken = string.Empty;
            // Build request to acquire MSI token
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=" + resourceID);
            request.Headers["Metadata"] = "true";
            request.Method = "GET";

            try
            {
                // Call /token endpoint
                HttpWebResponse response = (HttpWebResponse)request.GetResponse();

                // Pipe response Stream to a StreamReader, and extract access token
                StreamReader streamResponse = new StreamReader(response.GetResponseStream());
                string stringResponse = streamResponse.ReadToEnd();
                JavaScriptSerializer j = new JavaScriptSerializer();
                Dictionary<string, string> list = (Dictionary<string, string>)j.Deserialize(stringResponse, typeof(Dictionary<string, string>));
                accessToken = list["access_token"];
                return accessToken;
            }
            catch (Exception e)
            {
                string errorText = String.Format("{0} \n\n{1}", e.Message, e.InnerException != null ? e.InnerException.Message : "Acquire token failed");
                return accessToken;
            }
        }            
    }
}
```

<span data-ttu-id="7c7a3-155">The response contains the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="7c7a3-155">The response contains the contents of the file:</span></span>

`Hello world! :)`

## <a name="next-steps"></a><span data-ttu-id="7c7a3-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c7a3-156">Next steps</span></span>

<span data-ttu-id="7c7a3-157">In this tutorial, you learned how enable a Windows VM's system-assigned identity to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7c7a3-157">In this tutorial, you learned how enable a Windows VM's system-assigned identity to access Azure Storage.</span></span>  <span data-ttu-id="7c7a3-158">To learn more about Azure Storage see:</span><span class="sxs-lookup"><span data-stu-id="7c7a3-158">To learn more about Azure Storage see:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c7a3-159">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c7a3-159">Azure Storage</span></span>](/azure/storage/common/storage-introduction)



