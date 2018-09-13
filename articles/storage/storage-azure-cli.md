---
title: Using the Azure CLI 2.0 with Azure Storage | Microsoft Docs
description: Learn how to use the Azure Command-Line Interface (Azure CLI) 2.0 with Azure Storage to create and manage storage accounts and work with Azure blobs and files. The Azure CLI 2.0 is a cross-platform tool written in Python.
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 02/18/2017
ms.author: marsma
ms.openlocfilehash: be44ca9d14d6dbb7a50d5c42c163bc66531bb90f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552728"
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="f9bfc-104">Using the Azure CLI 2.0 with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f9bfc-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="f9bfc-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="f9bfc-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="f9bfc-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="f9bfc-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="f9bfc-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="f9bfc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f9bfc-110">Prerequisites</span></span>
<span data-ttu-id="f9bfc-111">This guide assumes that you understand the basic concepts of Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="f9bfc-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="f9bfc-113">Accounts</span><span class="sxs-lookup"><span data-stu-id="f9bfc-113">Accounts</span></span>
* <span data-ttu-id="f9bfc-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="f9bfc-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="f9bfc-116">Install the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9bfc-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="f9bfc-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="f9bfc-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="f9bfc-119">Working with the CLI</span><span class="sxs-lookup"><span data-stu-id="f9bfc-119">Working with the CLI</span></span>

<span data-ttu-id="f9bfc-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="f9bfc-121">Type the `az` command, and you should be presented with output similar to:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-121">Type the `az` command, and you should be presented with output similar to:</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account   : Commands to manage subscriptions.
    acr       : Commands to manage Azure container registries.
    acs       : Commands to manage Azure container services.
    ad        : Synchronize on-premises directories and manage Azure Active Directory (AAD)
                resources.
    appservice: Commands to manage your Azure web apps and App Service plans.
    cloud     : Manage the Azure clouds registered.
    component : Commands to manage and update Azure CLI 2.0 components.
    configure : Configure Azure CLI 2.0 or view your configuration. The command is
                interactive, so just type `az configure` and respond to the prompts.
    container : Set up automated builds and deployments for multi-container Docker applications.
    disk      : Commands to manage 'Managed Disks'.
    feature   : Commands to manage resource provider features, such as previews.
    feedback  : Loving or hating the CLI?  Let us know!
    group     : Commands to manage resource groups.
    image     : Commands to manage custom virtual machine images based on managed disks/snapshots.
    lock
    login     : Log in to access Azure subscriptions.
    logout    : Log out to remove access to Azure subscriptions.
    network   : Manages Network resources.
    policy    : Commands to manage resource policies.
    provider  : Manage resource providers.
    resource  : Generic commands to manage Azure resources.
    role      : Use role assignments to manage access to your Azure resources.
    snapshot  : Commands to manage snapshots.
    storage   : Durable, highly available, and massively scalable cloud storage.
    tag       : Manage resource tags.
    vm        : Provision Linux and Windows virtual machines in minutes.
    vmss      : Create highly available, auto-scalable Linux or Windows virtual machines.
```

<span data-ttu-id="f9bfc-122">In your command-line interface, execute the command `az storage -h` to list the `storage` group commands and its subgroups.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-122">In your command-line interface, execute the command `az storage -h` to list the `storage` group commands and its subgroups.</span></span> <span data-ttu-id="f9bfc-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Orgin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Effectively scale apps according to traffic using queues.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="f9bfc-124">Connect the CLI to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f9bfc-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="f9bfc-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="f9bfc-126">There are several ways you can log in:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="f9bfc-127">**Interactive login**: `az login`</span><span class="sxs-lookup"><span data-stu-id="f9bfc-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="f9bfc-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="f9bfc-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="f9bfc-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="f9bfc-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="f9bfc-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="f9bfc-131">Azure CLI 2.0 sample script</span><span class="sxs-lookup"><span data-stu-id="f9bfc-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="f9bfc-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="f9bfc-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="f9bfc-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create -n $container_name

echo "Uploading the file..."
az storage blob upload -f $file_to_upload -c $container_name -n $blob_name

echo "Listing the blobs..."
az storage blob list -c $container_name

echo "Downloading the file..."
az storage blob download -c $container_name -n $blob_name -f $destination_file

echo "Done"
```

<span data-ttu-id="f9bfc-135">**Configure and run the script**</span><span class="sxs-lookup"><span data-stu-id="f9bfc-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="f9bfc-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="f9bfc-137">Next, update the script's variables to reflect your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="f9bfc-138">Replace the following values as specified:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="f9bfc-139">**\<storage_account_name\>** The name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="f9bfc-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="f9bfc-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span><span class="sxs-lookup"><span data-stu-id="f9bfc-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="f9bfc-142">**\<blob_name\>** A name for the destination blob in the container.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="f9bfc-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="f9bfc-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f9bfc-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="f9bfc-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="f9bfc-145">After you've updated the necessary variables, save the script and exit your editor.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="f9bfc-146">The next steps assume you've named your script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="f9bfc-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="f9bfc-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="f9bfc-148">Execute the script.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-148">Execute the script.</span></span> <span data-ttu-id="f9bfc-149">For example, in Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="f9bfc-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="f9bfc-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
Success
---------
True
Uploading the file...                                           Percent complete: %100.0
Listing the blobs...
Name           Blob Type      Length  Content Type              Last Modified
-------------  -----------  --------  ------------------------  -------------------------
test_blob.txt  BlockBlob         771  application/octet-stream  2016-12-21T15:35:30+00:00
Downloading the file...
Name
-------------
test_blob.txt
Done
```

> [!TIP]
> <span data-ttu-id="f9bfc-151">The preceding output is in **table** format.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="f9bfc-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="f9bfc-153">Manage storage accounts</span><span class="sxs-lookup"><span data-stu-id="f9bfc-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f9bfc-154">Create a new storage account</span><span class="sxs-lookup"><span data-stu-id="f9bfc-154">Create a new storage account</span></span>
<span data-ttu-id="f9bfc-155">To use Azure Storage, you need a storage account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="f9bfc-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create -l <location> -n <account_name> -g <resource_group> --sku <account_sku>
```

* <span data-ttu-id="f9bfc-157">`-l` [Required]: Location.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-157">`-l` [Required]: Location.</span></span> <span data-ttu-id="f9bfc-158">For example, "West US".</span><span class="sxs-lookup"><span data-stu-id="f9bfc-158">For example, "West US".</span></span>
* <span data-ttu-id="f9bfc-159">`-n` [Required]: The storage account name.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-159">`-n` [Required]: The storage account name.</span></span> <span data-ttu-id="f9bfc-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="f9bfc-161">`-g` [Required]: Name of resource group.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-161">`-g` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="f9bfc-162">`--sku` [Required]: The storage account SKU.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="f9bfc-163">Allowed values:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="f9bfc-164">Set default Azure storage account environment variables</span><span class="sxs-lookup"><span data-stu-id="f9bfc-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="f9bfc-165">You can have multiple storage accounts in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="f9bfc-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f9bfc-167">Another way to set a default storage account is by using a connection string.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="f9bfc-168">First, get the connection string with the `show-connection-string` command:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string -n <account_name> -g <resource_group>
```

<span data-ttu-id="f9bfc-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span><span class="sxs-lookup"><span data-stu-id="f9bfc-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

> [!NOTE]
> <span data-ttu-id="f9bfc-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f9bfc-171">Create and manage blobs</span><span class="sxs-lookup"><span data-stu-id="f9bfc-171">Create and manage blobs</span></span>
<span data-ttu-id="f9bfc-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f9bfc-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="f9bfc-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/fileservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/fileservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f9bfc-175">Create a container</span><span class="sxs-lookup"><span data-stu-id="f9bfc-175">Create a container</span></span>
<span data-ttu-id="f9bfc-176">Every blob in Azure storage must be in a container.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f9bfc-177">You can create a container by using the `az storage container create` command:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create -n <container_name>
```

<span data-ttu-id="f9bfc-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="f9bfc-179">`off` (default): Container data is private to the account owner.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="f9bfc-180">`blob`: Public read access for blobs.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="f9bfc-181">`container`: Public read and list access to the entire container.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="f9bfc-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="f9bfc-183">Upload a blob to a container</span><span class="sxs-lookup"><span data-stu-id="f9bfc-183">Upload a blob to a container</span></span>
<span data-ttu-id="f9bfc-184">Azure Blob storage supports block, append, and page blobs.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="f9bfc-185">Upload blobs to a container by using the `blob upload` command:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload -f <local_file_path> -c <container_name> -n <blob_name>
```

 <span data-ttu-id="f9bfc-186">By default, the `blob upload` command uploads \*.vhd files to page blobs, or block blobs otherwise.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-186">By default, the `blob upload` command uploads \*.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="f9bfc-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="f9bfc-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/fileservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/fileservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="f9bfc-189">Download blobs from a container</span><span class="sxs-lookup"><span data-stu-id="f9bfc-189">Download blobs from a container</span></span>
<span data-ttu-id="f9bfc-190">This example demonstrates how to download a blob from a container:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download -c mycontainer -n myblob.png -f ~/mydownloadedblob.png
```

### <a name="copy-blobs"></a><span data-ttu-id="f9bfc-191">Copy blobs</span><span class="sxs-lookup"><span data-stu-id="f9bfc-191">Copy blobs</span></span>
<span data-ttu-id="f9bfc-192">You can copy blobs within or across storage accounts and regions asynchronously.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-192">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f9bfc-193">The following example demonstrates how to copy blobs from one storage account to another.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-193">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="f9bfc-194">We first create a container in another account, specifying that its blobs are publicly, anonymously accessible.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-194">We first create a container in another account, specifying that its blobs are publicly, anonymously accessible.</span></span> <span data-ttu-id="f9bfc-195">Next, we upload a file to the container, and finally, copy the blob from that container into the **mycontainer** container in the current account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-195">Next, we upload a file to the container, and finally, copy the blob from that container into the **mycontainer** container in the current account.</span></span>

```azurecli
az storage container create -n mycontainer2 --account-name <accountName2> --account-key <accountKey2> --public-access blob

az storage blob upload -f ~/Images/HelloWorld.png -c mycontainer2 -n myBlockBlob2 --account-name <accountName2> --account-key <accountKey2>

az storage blob copy start -u https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2 -b myBlobBlob -c mycontainer
```

<span data-ttu-id="f9bfc-196">The source blob URL (specified by `-u`) must either be publicly accessible, or include a shared access signature (SAS) token.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-196">The source blob URL (specified by `-u`) must either be publicly accessible, or include a shared access signature (SAS) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f9bfc-197">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="f9bfc-197">Delete a blob</span></span>
<span data-ttu-id="f9bfc-198">To delete a blob, use the `blob delete` command:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-198">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete -c <container_name> -n <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f9bfc-199">Create and manage file shares</span><span class="sxs-lookup"><span data-stu-id="f9bfc-199">Create and manage file shares</span></span>
<span data-ttu-id="f9bfc-200">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-200">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="f9bfc-201">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-201">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f9bfc-202">You can manage file shares and file data via the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-202">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="f9bfc-203">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f9bfc-203">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f9bfc-204">Create a file share</span><span class="sxs-lookup"><span data-stu-id="f9bfc-204">Create a file share</span></span>
<span data-ttu-id="f9bfc-205">An Azure File share is an SMB file share in Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-205">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f9bfc-206">All directories and files must be created in a file share.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-206">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f9bfc-207">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-207">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="f9bfc-208">The following example creates a file share named **myshare**.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-208">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create -n myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f9bfc-209">Create a directory</span><span class="sxs-lookup"><span data-stu-id="f9bfc-209">Create a directory</span></span>
<span data-ttu-id="f9bfc-210">A directory provides an optional hierarchical structure for an Azure file share.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-210">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="f9bfc-211">The following example creates a directory named **myDir** in the file share.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-211">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create -n myDir -s myshare
```

<span data-ttu-id="f9bfc-212">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-212">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="f9bfc-213">However, you must ensure that all parent directories exist.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-213">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="f9bfc-214">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-214">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="f9bfc-215">Upload a local file to a share</span><span class="sxs-lookup"><span data-stu-id="f9bfc-215">Upload a local file to a share</span></span>
<span data-ttu-id="f9bfc-216">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-216">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="f9bfc-217">The `--source` argument specifies the existing local file to upload.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-217">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="f9bfc-218">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-218">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="f9bfc-219">A file in the share can be up to 1 TB in size.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-219">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="f9bfc-220">List the files in a share</span><span class="sxs-lookup"><span data-stu-id="f9bfc-220">List the files in a share</span></span>
<span data-ttu-id="f9bfc-221">You can list files and directories in a share by using the `az storage file list` command:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-221">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list -s myshare

# List the files in a directory within a share
az storage file list -s myshare/myDir

# List the files in a path within a share
az storage file list -s myshare -p myDir/mySubDir/MySubDir2
```

### <a name="copy-files"></a><span data-ttu-id="f9bfc-222">Copy files</span><span class="sxs-lookup"><span data-stu-id="f9bfc-222">Copy files</span></span>      
<span data-ttu-id="f9bfc-223">You can copy a file to another file, a file to a blob, or a blob to a file.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-223">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="f9bfc-224">For example, to copy a file to a directory in a different share:</span><span class="sxs-lookup"><span data-stu-id="f9bfc-224">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="f9bfc-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9bfc-225">Next steps</span></span>
<span data-ttu-id="f9bfc-226">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9bfc-226">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="f9bfc-227">Get started with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9bfc-227">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="f9bfc-228">Azure CLI 2.0 command reference</span><span class="sxs-lookup"><span data-stu-id="f9bfc-228">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="f9bfc-229">Azure CLI 2.0 on GitHub</span><span class="sxs-lookup"><span data-stu-id="f9bfc-229">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
