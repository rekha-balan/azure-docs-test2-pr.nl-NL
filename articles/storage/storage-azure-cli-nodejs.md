---
title: Using the Azure CLI 1.0 with Azure Storage | Microsoft Docs
description: Learn how to use the Azure Command-Line Interface (Azure CLI) 1.0 with Azure Storage to create and manage storage accounts and work with Azure blobs and files. The Azure CLI is a cross-platform tool
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: caae601ff23573a7463c6eeefc7fd585d4923a73
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552186"
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="f1d1f-104">Using the Azure CLI 1.0 with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f1d1f-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="f1d1f-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f1d1f-105">Overview</span></span>

<span data-ttu-id="f1d1f-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="f1d1f-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="f1d1f-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="f1d1f-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="f1d1f-110">This guide assumes that you understand the basic concepts of Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="f1d1f-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="f1d1f-112">Be sure to update the script variables based on your configuration before running each script.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="f1d1f-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="f1d1f-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="f1d1f-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span><span class="sxs-lookup"><span data-stu-id="f1d1f-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="f1d1f-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="f1d1f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="f1d1f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="f1d1f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="f1d1f-120">**After creating a Microsoft Azure subscription and account:**</span><span class="sxs-lookup"><span data-stu-id="f1d1f-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="f1d1f-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="f1d1f-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="f1d1f-123">Type the _azure_ command and you should see the following output.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Azure Command Output][Image1]
3. <span data-ttu-id="f1d1f-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="f1d1f-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="f1d1f-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="f1d1f-128">The script will first ask you to set two variables for your storage account and key.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="f1d1f-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="f1d1f-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="f1d1f-131">In your local computer, open your preferred text editor (vim for example).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="f1d1f-132">Type the above script into your text editor.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="f1d1f-133">Now, you need to update the script variables based on your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="f1d1f-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="f1d1f-135">**Important:** The name of the storage account must be unique in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="f1d1f-136">It must be lowercase, too!</span><span class="sxs-lookup"><span data-stu-id="f1d1f-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="f1d1f-137">**<storage_account_key>** The access key of your storage account.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="f1d1f-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="f1d1f-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="f1d1f-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f1d1f-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="f1d1f-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="f1d1f-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="f1d1f-142">To run this script, simply type the script file name in the bash console.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="f1d1f-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="f1d1f-144">The following screenshot shows an example output:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="f1d1f-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="f1d1f-146">Manage storage accounts with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f1d1f-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="f1d1f-147">Connect to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f1d1f-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="f1d1f-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="f1d1f-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f1d1f-150">Create a new storage account</span><span class="sxs-lookup"><span data-stu-id="f1d1f-150">Create a new storage account</span></span>
<span data-ttu-id="f1d1f-151">To use Azure storage, you will need a storage account.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="f1d1f-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="f1d1f-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="f1d1f-154">Set a default Azure storage account in environment variables</span><span class="sxs-lookup"><span data-stu-id="f1d1f-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="f1d1f-155">You can have multiple storage accounts in your subscription.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="f1d1f-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="f1d1f-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f1d1f-158">Another way to set a default storage account is using connection string.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="f1d1f-159">Firstly get the connection string by command:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="f1d1f-160">Then copy the output connection string and set it to environment variable:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f1d1f-161">Create and manage blobs</span><span class="sxs-lookup"><span data-stu-id="f1d1f-161">Create and manage blobs</span></span>
<span data-ttu-id="f1d1f-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f1d1f-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="f1d1f-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f1d1f-165">Create a container</span><span class="sxs-lookup"><span data-stu-id="f1d1f-165">Create a container</span></span>
<span data-ttu-id="f1d1f-166">Every blob in Azure storage must be in a container.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f1d1f-167">You can create a private container using the `azure storage container create` command:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="f1d1f-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="f1d1f-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="f1d1f-170">By default, the new container is private and can be accessed only by the account owner.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="f1d1f-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="f1d1f-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="f1d1f-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f1d1f-174">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="f1d1f-174">Upload a blob into a container</span></span>
<span data-ttu-id="f1d1f-175">Azure Blob Storage supports block blobs and page blobs.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f1d1f-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="f1d1f-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="f1d1f-178">By default, this command uploads the local files to a block blob.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="f1d1f-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="f1d1f-180">Download blobs from a container</span><span class="sxs-lookup"><span data-stu-id="f1d1f-180">Download blobs from a container</span></span>
<span data-ttu-id="f1d1f-181">The following example demonstrates how to download blobs from a container.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="f1d1f-182">Copy blobs</span><span class="sxs-lookup"><span data-stu-id="f1d1f-182">Copy blobs</span></span>
<span data-ttu-id="f1d1f-183">You can copy blobs within or across storage accounts and regions asynchronously.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f1d1f-184">The following example demonstrates how to copy blobs from one storage account to another.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="f1d1f-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="f1d1f-186">This sample performs an asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="f1d1f-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="f1d1f-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f1d1f-189">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="f1d1f-189">Delete a blob</span></span>
<span data-ttu-id="f1d1f-190">To delete a blob, use the below command:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f1d1f-191">Create and manage file shares</span><span class="sxs-lookup"><span data-stu-id="f1d1f-191">Create and manage file shares</span></span>
<span data-ttu-id="f1d1f-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="f1d1f-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f1d1f-194">You can manage file shares and file data via the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="f1d1f-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f1d1f-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f1d1f-196">Create a file share</span><span class="sxs-lookup"><span data-stu-id="f1d1f-196">Create a file share</span></span>
<span data-ttu-id="f1d1f-197">An Azure File share is an SMB file share in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f1d1f-198">All directories and files must be created in a file share.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f1d1f-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="f1d1f-200">The following example creates a file share named **myshare**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f1d1f-201">Create a directory</span><span class="sxs-lookup"><span data-stu-id="f1d1f-201">Create a directory</span></span>
<span data-ttu-id="f1d1f-202">A directory provides an optional hierarchical structure for an Azure file share.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="f1d1f-203">The following example creates a directory named **myDir** in the file share.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="f1d1f-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="f1d1f-205">However, you must ensure that all parent directories exist.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="f1d1f-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="f1d1f-207">Upload a local file to directory</span><span class="sxs-lookup"><span data-stu-id="f1d1f-207">Upload a local file to directory</span></span>
<span data-ttu-id="f1d1f-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="f1d1f-209">Edit the file path so that it points to a valid file on your local machine:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="f1d1f-210">Note that a file in the share can be up to 1 TB in size.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="f1d1f-211">List the files in the share root or directory</span><span class="sxs-lookup"><span data-stu-id="f1d1f-211">List the files in the share root or directory</span></span>
<span data-ttu-id="f1d1f-212">You can list the files and subdirectories in a share root or a directory using the following command:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="f1d1f-213">Note that the directory name is optional for the listing operation.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="f1d1f-214">If omitted, the command lists the contents of the root directory of the share.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="f1d1f-215">Copy files</span><span class="sxs-lookup"><span data-stu-id="f1d1f-215">Copy files</span></span>
<span data-ttu-id="f1d1f-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="f1d1f-217">Below we demonstrate how to perform these copy operations using CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="f1d1f-218">To copy a file to the new directory:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="f1d1f-219">To copy a blob to a file directory:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="f1d1f-220">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f1d1f-220">Next Steps</span></span>

<span data-ttu-id="f1d1f-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span><span class="sxs-lookup"><span data-stu-id="f1d1f-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="f1d1f-222">Azure CLI commands in Resource Manager mode</span><span class="sxs-lookup"><span data-stu-id="f1d1f-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="f1d1f-223">Azure CLI commands in Azure Service Management mode</span><span class="sxs-lookup"><span data-stu-id="f1d1f-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="f1d1f-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="f1d1f-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-azure-cli/azure_command.png

