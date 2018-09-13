---
title: Using Azure PowerShell with Azure Storage | Microsoft Docs
description: Learn how to use the Azure PowerShell cmdlets for Azure Storage to create and manage storage accounts; work with blobs, tables, queues, and files; configure and query storage analytics, and create shared access signatures.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: b268dedabb9254bb2cb765d6efefd6a5148d7dca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556333"
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="06726-103">Using Azure PowerShell with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="06726-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="06726-104">Overview</span><span class="sxs-lookup"><span data-stu-id="06726-104">Overview</span></span>
<span data-ttu-id="06726-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="06726-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span><span class="sxs-lookup"><span data-stu-id="06726-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="06726-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span><span class="sxs-lookup"><span data-stu-id="06726-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="06726-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06726-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="06726-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](https://msdn.microsoft.com/library/azure/mt269418.aspx) to perform a variety of development and administration tasks with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](https://msdn.microsoft.com/library/azure/mt269418.aspx) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="06726-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="06726-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="06726-112">You should update the script variables based on your configuration before running each script.</span><span class="sxs-lookup"><span data-stu-id="06726-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="06726-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="06726-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="06726-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="06726-115">Getting started with Azure Storage and PowerShell in 5 minutes</span><span class="sxs-lookup"><span data-stu-id="06726-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="06726-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="06726-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="06726-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span><span class="sxs-lookup"><span data-stu-id="06726-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="06726-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span><span class="sxs-lookup"><span data-stu-id="06726-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="06726-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="06726-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="06726-120">**After creating a Microsoft Azure subscription and account:**</span><span class="sxs-lookup"><span data-stu-id="06726-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="06726-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="06726-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="06726-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="06726-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="06726-123">Type **Administrative Tools** and click to run it.</span><span class="sxs-lookup"><span data-stu-id="06726-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="06726-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span><span class="sxs-lookup"><span data-stu-id="06726-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="06726-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span><span class="sxs-lookup"><span data-stu-id="06726-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="06726-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="06726-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span><span class="sxs-lookup"><span data-stu-id="06726-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="06726-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="06726-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="06726-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span><span class="sxs-lookup"><span data-stu-id="06726-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="06726-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span><span class="sxs-lookup"><span data-stu-id="06726-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="06726-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span><span class="sxs-lookup"><span data-stu-id="06726-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="06726-132">Press CTRL+C to copy it to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="06726-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
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
    ```

6. <span data-ttu-id="06726-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span><span class="sxs-lookup"><span data-stu-id="06726-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="06726-134">Click **File** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="06726-134">Click **File** > **Save**.</span></span> <span data-ttu-id="06726-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span><span class="sxs-lookup"><span data-stu-id="06726-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="06726-136">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="06726-136">Click **Save**.</span></span>
7. <span data-ttu-id="06726-137">Now, you need to update the script variables based on your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="06726-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="06726-138">You must update the **$SubscriptionName** variable with your own subscription.</span><span class="sxs-lookup"><span data-stu-id="06726-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="06726-139">You can keep the other variables as specified in the script or update them as you wish.</span><span class="sxs-lookup"><span data-stu-id="06726-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="06726-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span><span class="sxs-lookup"><span data-stu-id="06726-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="06726-141">Follow one of the following three ways to locate the name of your subscription:</span><span class="sxs-lookup"><span data-stu-id="06726-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="06726-142">a.</span><span class="sxs-lookup"><span data-stu-id="06726-142">a.</span></span> <span data-ttu-id="06726-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span><span class="sxs-lookup"><span data-stu-id="06726-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="06726-144">Copy the following script to the new script file and click **Debug** > **Run**.</span><span class="sxs-lookup"><span data-stu-id="06726-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="06726-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="06726-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="06726-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span><span class="sxs-lookup"><span data-stu-id="06726-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="06726-147">b.</span><span class="sxs-lookup"><span data-stu-id="06726-147">b.</span></span> <span data-ttu-id="06726-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="06726-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="06726-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span><span class="sxs-lookup"><span data-stu-id="06726-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="06726-151">c.</span><span class="sxs-lookup"><span data-stu-id="06726-151">c.</span></span> <span data-ttu-id="06726-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span><span class="sxs-lookup"><span data-stu-id="06726-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="06726-153">Click **Subscriptions** to see a list of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="06726-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="06726-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span><span class="sxs-lookup"><span data-stu-id="06726-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Azure Classic Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="06726-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="06726-157">**Important:** The name of the storage account must be unique in Azure.</span><span class="sxs-lookup"><span data-stu-id="06726-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="06726-158">It must be lowercase, too!</span><span class="sxs-lookup"><span data-stu-id="06726-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="06726-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span><span class="sxs-lookup"><span data-stu-id="06726-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="06726-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span><span class="sxs-lookup"><span data-stu-id="06726-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="06726-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="06726-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="06726-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="06726-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="06726-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="06726-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="06726-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span><span class="sxs-lookup"><span data-stu-id="06726-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="06726-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span><span class="sxs-lookup"><span data-stu-id="06726-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="06726-166">The following screenshot shows an example output:</span><span class="sxs-lookup"><span data-stu-id="06726-166">The following screenshot shows an example output:</span></span>

![Download Blobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="06726-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="06726-169">For detailed information and instructions, we encourage you to read the following sections.</span><span class="sxs-lookup"><span data-stu-id="06726-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="06726-170">Prerequisites for using Azure PowerShell with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="06726-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="06726-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span><span class="sxs-lookup"><span data-stu-id="06726-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="06726-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="06726-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="06726-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="06726-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span><span class="sxs-lookup"><span data-stu-id="06726-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="06726-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="06726-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="06726-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span><span class="sxs-lookup"><span data-stu-id="06726-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="06726-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span><span class="sxs-lookup"><span data-stu-id="06726-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="06726-178">How to manage storage accounts in Azure</span><span class="sxs-lookup"><span data-stu-id="06726-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="06726-179">Let's take a look at managing storage accounts in Azure with PowerShell</span><span class="sxs-lookup"><span data-stu-id="06726-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="06726-180">How to set a default Azure subscription</span><span class="sxs-lookup"><span data-stu-id="06726-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="06726-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span><span class="sxs-lookup"><span data-stu-id="06726-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="06726-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tutorial.</span><span class="sxs-lookup"><span data-stu-id="06726-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tutorial.</span></span> <span data-ttu-id="06726-183">This guide uses the Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="06726-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="06726-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span><span class="sxs-lookup"><span data-stu-id="06726-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="06726-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span><span class="sxs-lookup"><span data-stu-id="06726-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="06726-186">Azure authenticates and saves the credential information, and then closes the window.</span><span class="sxs-lookup"><span data-stu-id="06726-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="06726-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span><span class="sxs-lookup"><span data-stu-id="06726-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="06726-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span><span class="sxs-lookup"><span data-stu-id="06726-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="06726-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span><span class="sxs-lookup"><span data-stu-id="06726-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="06726-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span><span class="sxs-lookup"><span data-stu-id="06726-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="06726-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span><span class="sxs-lookup"><span data-stu-id="06726-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="06726-192">How to create a new Azure storage account</span><span class="sxs-lookup"><span data-stu-id="06726-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="06726-193">To use Azure storage, you will need a storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="06726-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span><span class="sxs-lookup"><span data-stu-id="06726-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="06726-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span><span class="sxs-lookup"><span data-stu-id="06726-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="06726-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="06726-197">The following example creates a new storage account in the "West US" datacenter.</span><span class="sxs-lookup"><span data-stu-id="06726-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="06726-198">The name of your storage account must be unique within Azure and must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="06726-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="06726-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="06726-200">How to set a default Azure storage account</span><span class="sxs-lookup"><span data-stu-id="06726-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="06726-201">You can have multiple storage accounts in your subscription.</span><span class="sxs-lookup"><span data-stu-id="06726-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="06726-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="06726-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="06726-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span><span class="sxs-lookup"><span data-stu-id="06726-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="06726-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="06726-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span><span class="sxs-lookup"><span data-stu-id="06726-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="06726-206">This command returns the subscription properties on the current subscription including its current storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="06726-207">How to list all Azure storage accounts in a subscription</span><span class="sxs-lookup"><span data-stu-id="06726-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="06726-208">Each Azure subscription can have up to 100 storage accounts.</span><span class="sxs-lookup"><span data-stu-id="06726-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="06726-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="06726-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="06726-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span><span class="sxs-lookup"><span data-stu-id="06726-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="06726-211">How to create an Azure storage context</span><span class="sxs-lookup"><span data-stu-id="06726-211">How to create an Azure storage context</span></span>
<span data-ttu-id="06726-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span><span class="sxs-lookup"><span data-stu-id="06726-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="06726-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span><span class="sxs-lookup"><span data-stu-id="06726-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="06726-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span><span class="sxs-lookup"><span data-stu-id="06726-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="06726-215">For more information, see [New-AzureStorageContext](http://msdn.microsoft.com/library/azure/dn806380.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-215">For more information, see [New-AzureStorageContext](http://msdn.microsoft.com/library/azure/dn806380.aspx).</span></span>  

<span data-ttu-id="06726-216">Use one of the following three ways to create a storage context:</span><span class="sxs-lookup"><span data-stu-id="06726-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="06726-217">Run the [Get-AzureStorageKey](http://msdn.microsoft.com/library/azure/dn495235.aspx) cmdlet to find out the primary storage access key for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-217">Run the [Get-AzureStorageKey](http://msdn.microsoft.com/library/azure/dn495235.aspx) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="06726-218">Next, call the [New-AzureStorageContext](http://msdn.microsoft.com/library/azure/dn806380.aspx) cmdlet to create a storage context:</span><span class="sxs-lookup"><span data-stu-id="06726-218">Next, call the [New-AzureStorageContext](http://msdn.microsoft.com/library/azure/dn806380.aspx) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="06726-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span><span class="sxs-lookup"><span data-stu-id="06726-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="06726-220">For more information, see [New-AzureStorageContainerSASToken](http://msdn.microsoft.com/library/azure/dn806416.aspx) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="06726-220">For more information, see [New-AzureStorageContainerSASToken](http://msdn.microsoft.com/library/azure/dn806416.aspx) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="06726-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span><span class="sxs-lookup"><span data-stu-id="06726-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="06726-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span><span class="sxs-lookup"><span data-stu-id="06726-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="06726-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span><span class="sxs-lookup"><span data-stu-id="06726-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="06726-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="06726-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="06726-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span><span class="sxs-lookup"><span data-stu-id="06726-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="06726-226">How to retrieve and regenerate Azure storage keys</span><span class="sxs-lookup"><span data-stu-id="06726-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="06726-227">An Azure Storage account comes with two account keys.</span><span class="sxs-lookup"><span data-stu-id="06726-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="06726-228">You can use the following cmdlet to retrieve your keys.</span><span class="sxs-lookup"><span data-stu-id="06726-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="06726-229">Use the following cmdlet to retrieve a specific key.</span><span class="sxs-lookup"><span data-stu-id="06726-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="06726-230">Valid values are Primary and Secondary.</span><span class="sxs-lookup"><span data-stu-id="06726-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="06726-231">If you would like to regenerate your keys, use the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="06726-232">Valid values for -KeyType are "Primary" and "Secondary"</span><span class="sxs-lookup"><span data-stu-id="06726-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="06726-233">How to manage Azure blobs</span><span class="sxs-lookup"><span data-stu-id="06726-233">How to manage Azure blobs</span></span>
<span data-ttu-id="06726-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="06726-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="06726-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span><span class="sxs-lookup"><span data-stu-id="06726-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="06726-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="06726-237">How to create a container</span><span class="sxs-lookup"><span data-stu-id="06726-237">How to create a container</span></span>
<span data-ttu-id="06726-238">Every blob in Azure storage must be in a container.</span><span class="sxs-lookup"><span data-stu-id="06726-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="06726-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span><span class="sxs-lookup"><span data-stu-id="06726-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="06726-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span><span class="sxs-lookup"><span data-stu-id="06726-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="06726-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span><span class="sxs-lookup"><span data-stu-id="06726-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="06726-242">By default, the new container is private and can be accessed only by the account owner.</span><span class="sxs-lookup"><span data-stu-id="06726-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="06726-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span><span class="sxs-lookup"><span data-stu-id="06726-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="06726-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span><span class="sxs-lookup"><span data-stu-id="06726-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="06726-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="06726-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="06726-246">How to upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="06726-246">How to upload a blob into a container</span></span>
<span data-ttu-id="06726-247">Azure Blob Storage supports block blobs and page blobs.</span><span class="sxs-lookup"><span data-stu-id="06726-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="06726-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="06726-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806379.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806379.aspx) cmdlet.</span></span> <span data-ttu-id="06726-250">By default, this command uploads the local files to a block blob.</span><span class="sxs-lookup"><span data-stu-id="06726-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="06726-251">To specify the type for the blob, you can use the -BlobType parameter.</span><span class="sxs-lookup"><span data-stu-id="06726-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="06726-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span><span class="sxs-lookup"><span data-stu-id="06726-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="06726-253">The [Set-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806379.aspx) cmdlet uploads the local files to your container:</span><span class="sxs-lookup"><span data-stu-id="06726-253">The [Set-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806379.aspx) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="06726-254">How to download blobs from a container</span><span class="sxs-lookup"><span data-stu-id="06726-254">How to download blobs from a container</span></span>
<span data-ttu-id="06726-255">The following example demonstrates how to download blobs from a container.</span><span class="sxs-lookup"><span data-stu-id="06726-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="06726-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span><span class="sxs-lookup"><span data-stu-id="06726-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="06726-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet.</span></span> <span data-ttu-id="06726-258">Next, the example uses the [Get-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806418.aspx) cmdlet to download blobs into the local destination folder.</span><span class="sxs-lookup"><span data-stu-id="06726-258">Next, the example uses the [Get-AzureStorageBlobContent](http://msdn.microsoft.com/library/azure/dn806418.aspx) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="06726-259">How to copy blobs from one storage container to another</span><span class="sxs-lookup"><span data-stu-id="06726-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="06726-260">You can copy blobs across storage accounts and regions asynchronously.</span><span class="sxs-lookup"><span data-stu-id="06726-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="06726-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span><span class="sxs-lookup"><span data-stu-id="06726-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="06726-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span><span class="sxs-lookup"><span data-stu-id="06726-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="06726-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](http://msdn.microsoft.com/library/azure/dn806394.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](http://msdn.microsoft.com/library/azure/dn806394.aspx) cmdlet.</span></span> <span data-ttu-id="06726-264">The example assumes that the source and destination storage accounts and containers already exist.</span><span class="sxs-lookup"><span data-stu-id="06726-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="06726-265">Note that this example performs an asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="06726-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="06726-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](http://msdn.microsoft.com/library/azure/dn806406.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](http://msdn.microsoft.com/library/azure/dn806406.aspx) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="06726-267">How to copy blobs from a secondary location</span><span class="sxs-lookup"><span data-stu-id="06726-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="06726-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span><span class="sxs-lookup"><span data-stu-id="06726-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="06726-269">How to delete a blob</span><span class="sxs-lookup"><span data-stu-id="06726-269">How to delete a blob</span></span>
<span data-ttu-id="06726-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span><span class="sxs-lookup"><span data-stu-id="06726-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="06726-271">The following example deletes all the blobs in a given container.</span><span class="sxs-lookup"><span data-stu-id="06726-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="06726-272">The example first sets variables for a storage account, and then creates a storage context.</span><span class="sxs-lookup"><span data-stu-id="06726-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="06726-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [Remove-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806399.aspx) cmdlet to remove blobs from a container in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="06726-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [Remove-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806399.aspx) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="06726-274">How to manage Azure blob snapshots</span><span class="sxs-lookup"><span data-stu-id="06726-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="06726-275">Azure lets you create a snapshot of a blob.</span><span class="sxs-lookup"><span data-stu-id="06726-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="06726-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span><span class="sxs-lookup"><span data-stu-id="06726-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="06726-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span><span class="sxs-lookup"><span data-stu-id="06726-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="06726-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span><span class="sxs-lookup"><span data-stu-id="06726-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="06726-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="06726-280">How to create a blob snapshot</span><span class="sxs-lookup"><span data-stu-id="06726-280">How to create a blob snapshot</span></span>
<span data-ttu-id="06726-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span><span class="sxs-lookup"><span data-stu-id="06726-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="06726-282">The following example first sets variables for a storage account, and then creates a storage context.</span><span class="sxs-lookup"><span data-stu-id="06726-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="06726-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span><span class="sxs-lookup"><span data-stu-id="06726-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="06726-284">How to list a blob's snapshots</span><span class="sxs-lookup"><span data-stu-id="06726-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="06726-285">You can create as many snapshots as you want for a blob.</span><span class="sxs-lookup"><span data-stu-id="06726-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="06726-286">You can list the snapshots associated with your blob to track your current snapshots.</span><span class="sxs-lookup"><span data-stu-id="06726-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="06726-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet to list the snapshots of that blob.</span><span class="sxs-lookup"><span data-stu-id="06726-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="06726-288">How to copy a snapshot of a blob</span><span class="sxs-lookup"><span data-stu-id="06726-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="06726-289">You can copy a snapshot of a blob to restore the snapshot.</span><span class="sxs-lookup"><span data-stu-id="06726-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="06726-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="06726-291">The following example first sets variables for a storage account, and then creates a storage context.</span><span class="sxs-lookup"><span data-stu-id="06726-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="06726-292">Next, the example defines the container and blob name variables.</span><span class="sxs-lookup"><span data-stu-id="06726-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="06726-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span><span class="sxs-lookup"><span data-stu-id="06726-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](http://msdn.microsoft.com/library/azure/dn806392.aspx) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="06726-294">Then, the example runs the [Start-AzureStorageBlobCopy](http://msdn.microsoft.com/library/azure/dn806394.aspx) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span><span class="sxs-lookup"><span data-stu-id="06726-294">Then, the example runs the [Start-AzureStorageBlobCopy](http://msdn.microsoft.com/library/azure/dn806394.aspx) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="06726-295">Be sure to update the variables based on your configuration before running the example.</span><span class="sxs-lookup"><span data-stu-id="06726-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="06726-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span><span class="sxs-lookup"><span data-stu-id="06726-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="06726-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span><span class="sxs-lookup"><span data-stu-id="06726-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="06726-298">How to manage Azure tables and table entities</span><span class="sxs-lookup"><span data-stu-id="06726-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="06726-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="06726-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="06726-300">The main components of the service are tables, entities, and properties.</span><span class="sxs-lookup"><span data-stu-id="06726-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="06726-301">A table is a collection of entities.</span><span class="sxs-lookup"><span data-stu-id="06726-301">A table is a collection of entities.</span></span> <span data-ttu-id="06726-302">An entity is a set of properties.</span><span class="sxs-lookup"><span data-stu-id="06726-302">An entity is a set of properties.</span></span> <span data-ttu-id="06726-303">Each entity can have up to 252 properties, which are all name-value pairs.</span><span class="sxs-lookup"><span data-stu-id="06726-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="06726-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span><span class="sxs-lookup"><span data-stu-id="06726-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="06726-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="06726-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="06726-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="06726-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span><span class="sxs-lookup"><span data-stu-id="06726-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="06726-308">How to create a table</span><span class="sxs-lookup"><span data-stu-id="06726-308">How to create a table</span></span>
<span data-ttu-id="06726-309">Every table must reside in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="06726-310">The following example demonstrates how to create a table in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="06726-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-312">Next, it uses the [New-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806417.aspx) cmdlet to create a table in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-312">Next, it uses the [New-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806417.aspx) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="06726-313">How to retrieve a table</span><span class="sxs-lookup"><span data-stu-id="06726-313">How to retrieve a table</span></span>
<span data-ttu-id="06726-314">You can query and retrieve one or all tables in a Storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="06726-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="06726-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="06726-317">How to delete a table</span><span class="sxs-lookup"><span data-stu-id="06726-317">How to delete a table</span></span>
<span data-ttu-id="06726-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806393.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806393.aspx) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="06726-319">How to manage table entities</span><span class="sxs-lookup"><span data-stu-id="06726-319">How to manage table entities</span></span>
<span data-ttu-id="06726-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span><span class="sxs-lookup"><span data-stu-id="06726-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="06726-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="06726-322">How to add table entities</span><span class="sxs-lookup"><span data-stu-id="06726-322">How to add table entities</span></span>
<span data-ttu-id="06726-323">To add an entity to a table, first create an object that defines your entity properties.</span><span class="sxs-lookup"><span data-stu-id="06726-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="06726-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="06726-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="06726-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="06726-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="06726-326">The server manages the value of **Timestamp**, which cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="06726-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="06726-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span><span class="sxs-lookup"><span data-stu-id="06726-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="06726-328">**PartitionKey**: Determines the partition that the entity is stored in.</span><span class="sxs-lookup"><span data-stu-id="06726-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="06726-329">**RowKey**: Uniquely identifies the entity within the partition.</span><span class="sxs-lookup"><span data-stu-id="06726-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="06726-330">You may define up to 252 custom properties for an entity.</span><span class="sxs-lookup"><span data-stu-id="06726-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="06726-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="06726-332">The following example demonstrates how to add entities to a table.</span><span class="sxs-lookup"><span data-stu-id="06726-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="06726-333">The example shows how to retrieve the employee table and add several entities into it.</span><span class="sxs-lookup"><span data-stu-id="06726-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="06726-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-335">Next, it retrieves the given table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-335">Next, it retrieves the given table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span></span> <span data-ttu-id="06726-336">If the table does not exist, the [New-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806417.aspx) cmdlet is used to create a table in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-336">If the table does not exist, the [New-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806417.aspx) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="06726-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span><span class="sxs-lookup"><span data-stu-id="06726-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="06726-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span><span class="sxs-lookup"><span data-stu-id="06726-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="06726-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span><span class="sxs-lookup"><span data-stu-id="06726-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="06726-340">How to query table entities</span><span class="sxs-lookup"><span data-stu-id="06726-340">How to query table entities</span></span>
<span data-ttu-id="06726-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="06726-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="06726-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span><span class="sxs-lookup"><span data-stu-id="06726-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="06726-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span></span> <span data-ttu-id="06726-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span><span class="sxs-lookup"><span data-stu-id="06726-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="06726-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span><span class="sxs-lookup"><span data-stu-id="06726-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="06726-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="06726-348">When you run this query, it returns all entities that match the filter criteria.</span><span class="sxs-lookup"><span data-stu-id="06726-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="06726-349">How to delete table entities</span><span class="sxs-lookup"><span data-stu-id="06726-349">How to delete table entities</span></span>
<span data-ttu-id="06726-350">You can delete an entity using its partition and row keys.</span><span class="sxs-lookup"><span data-stu-id="06726-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="06726-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span><span class="sxs-lookup"><span data-stu-id="06726-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="06726-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](http://msdn.microsoft.com/library/azure/dn806411.aspx) cmdlet.</span></span> <span data-ttu-id="06726-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span><span class="sxs-lookup"><span data-stu-id="06726-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="06726-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span><span class="sxs-lookup"><span data-stu-id="06726-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="06726-356">How to manage Azure queues and queue messages</span><span class="sxs-lookup"><span data-stu-id="06726-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="06726-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="06726-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="06726-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span><span class="sxs-lookup"><span data-stu-id="06726-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="06726-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="06726-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="06726-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="06726-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span><span class="sxs-lookup"><span data-stu-id="06726-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="06726-362">How to create a queue</span><span class="sxs-lookup"><span data-stu-id="06726-362">How to create a queue</span></span>
<span data-ttu-id="06726-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-364">Next, it calls [New-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806382.aspx) cmdlet to create a queue named 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="06726-364">Next, it calls [New-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806382.aspx) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="06726-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="06726-366">How to retrieve a queue</span><span class="sxs-lookup"><span data-stu-id="06726-366">How to retrieve a queue</span></span>
<span data-ttu-id="06726-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="06726-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="06726-369">If you call the [Get-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet without any parameters, it gets a list of all the queues.</span><span class="sxs-lookup"><span data-stu-id="06726-369">If you call the [Get-AzureStorageQueue](http://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="06726-370">How to delete a queue</span><span class="sxs-lookup"><span data-stu-id="06726-370">How to delete a queue</span></span>
<span data-ttu-id="06726-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="06726-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="06726-373">How to insert a message into a queue</span><span class="sxs-lookup"><span data-stu-id="06726-373">How to insert a message into a queue</span></span>
<span data-ttu-id="06726-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="06726-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="06726-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="06726-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="06726-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span><span class="sxs-lookup"><span data-stu-id="06726-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="06726-377">The following example demonstrates how to add message to a queue.</span><span class="sxs-lookup"><span data-stu-id="06726-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="06726-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span><span class="sxs-lookup"><span data-stu-id="06726-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="06726-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06726-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="06726-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="06726-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="06726-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span><span class="sxs-lookup"><span data-stu-id="06726-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="06726-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="06726-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="06726-383">How to de-queue at the next message</span><span class="sxs-lookup"><span data-stu-id="06726-383">How to de-queue at the next message</span></span>
<span data-ttu-id="06726-384">Your code de-queues a message from a queue in two steps.</span><span class="sxs-lookup"><span data-stu-id="06726-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="06726-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span><span class="sxs-lookup"><span data-stu-id="06726-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="06726-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span><span class="sxs-lookup"><span data-stu-id="06726-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="06726-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="06726-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="06726-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span><span class="sxs-lookup"><span data-stu-id="06726-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="06726-389">Your code calls **DeleteMessage** right after the message has been processed.</span><span class="sxs-lookup"><span data-stu-id="06726-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="06726-390">How to manage Azure file shares and files</span><span class="sxs-lookup"><span data-stu-id="06726-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="06726-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="06726-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="06726-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="06726-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="06726-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="06726-394">How to set and query storage analytics</span><span class="sxs-lookup"><span data-stu-id="06726-394">How to set and query storage analytics</span></span>
<span data-ttu-id="06726-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="06726-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="06726-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span><span class="sxs-lookup"><span data-stu-id="06726-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="06726-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span><span class="sxs-lookup"><span data-stu-id="06726-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="06726-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span><span class="sxs-lookup"><span data-stu-id="06726-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="06726-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="06726-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="06726-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="06726-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="06726-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="06726-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="06726-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span><span class="sxs-lookup"><span data-stu-id="06726-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="06726-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06726-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="06726-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span><span class="sxs-lookup"><span data-stu-id="06726-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="06726-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span><span class="sxs-lookup"><span data-stu-id="06726-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="06726-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span><span class="sxs-lookup"><span data-stu-id="06726-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="06726-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span><span class="sxs-lookup"><span data-stu-id="06726-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="06726-409">This is not allowed for tables or queues.</span><span class="sxs-lookup"><span data-stu-id="06726-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="06726-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span><span class="sxs-lookup"><span data-stu-id="06726-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="06726-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span><span class="sxs-lookup"><span data-stu-id="06726-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="06726-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span><span class="sxs-lookup"><span data-stu-id="06726-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="06726-413">A shared access signature can be in one of two forms:</span><span class="sxs-lookup"><span data-stu-id="06726-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="06726-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span><span class="sxs-lookup"><span data-stu-id="06726-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="06726-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span><span class="sxs-lookup"><span data-stu-id="06726-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="06726-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="06726-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="06726-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span><span class="sxs-lookup"><span data-stu-id="06726-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="06726-418">This type of SAS is revocable.</span><span class="sxs-lookup"><span data-stu-id="06726-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="06726-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="06726-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="06726-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span><span class="sxs-lookup"><span data-stu-id="06726-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="06726-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span><span class="sxs-lookup"><span data-stu-id="06726-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="06726-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span><span class="sxs-lookup"><span data-stu-id="06726-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="06726-423">How to create a policy-based Shared Access Signature token</span><span class="sxs-lookup"><span data-stu-id="06726-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="06726-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span><span class="sxs-lookup"><span data-stu-id="06726-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="06726-425">Then, call the [New-AzureStorageTableSASToken](http://msdn.microsoft.com/library/azure/dn806400.aspx) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span><span class="sxs-lookup"><span data-stu-id="06726-425">Then, call the [New-AzureStorageTableSASToken](http://msdn.microsoft.com/library/azure/dn806400.aspx) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="06726-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span><span class="sxs-lookup"><span data-stu-id="06726-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="06726-427">Use the [New-AzureStorageTableSASToken](http://msdn.microsoft.com/library/azure/dn806400.aspx) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span><span class="sxs-lookup"><span data-stu-id="06726-427">Use the [New-AzureStorageTableSASToken](http://msdn.microsoft.com/library/azure/dn806400.aspx) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="06726-428">How to create a stored access policy</span><span class="sxs-lookup"><span data-stu-id="06726-428">How to create a stored access policy</span></span>
<span data-ttu-id="06726-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span><span class="sxs-lookup"><span data-stu-id="06726-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="06726-430">How to update a stored access policy</span><span class="sxs-lookup"><span data-stu-id="06726-430">How to update a stored access policy</span></span>
<span data-ttu-id="06726-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span><span class="sxs-lookup"><span data-stu-id="06726-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="06726-432">How to delete a stored access policy</span><span class="sxs-lookup"><span data-stu-id="06726-432">How to delete a stored access policy</span></span>
<span data-ttu-id="06726-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span><span class="sxs-lookup"><span data-stu-id="06726-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="06726-434">How to use Azure Storage for U.S. government and Azure China</span><span class="sxs-lookup"><span data-stu-id="06726-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="06726-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="06726-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="06726-436">You can deploy new Azure environments for U.S government and Azure China.</span><span class="sxs-lookup"><span data-stu-id="06726-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="06726-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="06726-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="06726-438">Follow these steps to get you started:</span><span class="sxs-lookup"><span data-stu-id="06726-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="06726-439">Run the [Get-AzureEnvironment](https://msdn.microsoft.com/library/azure/dn790368.aspx) cmdlet to see the available Azure environments:</span><span class="sxs-lookup"><span data-stu-id="06726-439">Run the [Get-AzureEnvironment](https://msdn.microsoft.com/library/azure/dn790368.aspx) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="06726-440">Add an Azure China account to Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="06726-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="06726-441">Create a storage context for an AzureChinaCloud account:</span><span class="sxs-lookup"><span data-stu-id="06726-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="06726-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span><span class="sxs-lookup"><span data-stu-id="06726-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="06726-443">Run the [Get-AzureEnvironment](https://msdn.microsoft.com/library/azure/dn790368.aspx) cmdlet to see the available Azure environments:</span><span class="sxs-lookup"><span data-stu-id="06726-443">Run the [Get-AzureEnvironment](https://msdn.microsoft.com/library/azure/dn790368.aspx) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="06726-444">Add an Azure US Government account to Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="06726-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="06726-445">Create a storage context for an AzureUSGovernment account:</span><span class="sxs-lookup"><span data-stu-id="06726-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="06726-446">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="06726-446">For more information, see:</span></span>

* <span data-ttu-id="06726-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="06726-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="06726-448">Overview of Differences When Creating an Application on China Service</span><span class="sxs-lookup"><span data-stu-id="06726-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="06726-449">Next Steps</span><span class="sxs-lookup"><span data-stu-id="06726-449">Next Steps</span></span>
<span data-ttu-id="06726-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06726-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="06726-451">Here are some related articles and resources for learning more about them.</span><span class="sxs-lookup"><span data-stu-id="06726-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="06726-452">Azure Storage Documentation</span><span class="sxs-lookup"><span data-stu-id="06726-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="06726-453">Azure Storage PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="06726-453">Azure Storage PowerShell Cmdlets</span></span>](http://msdn.microsoft.com/library/azure/dn806401.aspx)
* [<span data-ttu-id="06726-454">Windows PowerShell Reference</span><span class="sxs-lookup"><span data-stu-id="06726-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next



