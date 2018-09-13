---
title: How to use Blob storage (object storage) from Ruby | Microsoft Docs
description: Store unstructured data in the cloud with Azure Blob storage (object storage).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 7f7d0c52b2b50a360711477e8e0eafc07ddcf374
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549118"
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="6a699-103">How to use Blob storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="6a699-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6a699-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6a699-104">Overview</span></span>
<span data-ttu-id="6a699-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span><span class="sxs-lookup"><span data-stu-id="6a699-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="6a699-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span><span class="sxs-lookup"><span data-stu-id="6a699-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="6a699-107">Blob storage is also referred to as object storage.</span><span class="sxs-lookup"><span data-stu-id="6a699-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="6a699-108">This guide will show you how to perform common scenarios using Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6a699-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="6a699-109">The samples are written using the Ruby API.</span><span class="sxs-lookup"><span data-stu-id="6a699-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="6a699-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span><span class="sxs-lookup"><span data-stu-id="6a699-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="6a699-111">Create a Ruby application</span><span class="sxs-lookup"><span data-stu-id="6a699-111">Create a Ruby application</span></span>
<span data-ttu-id="6a699-112">Create a Ruby application.</span><span class="sxs-lookup"><span data-stu-id="6a699-112">Create a Ruby application.</span></span> <span data-ttu-id="6a699-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="6a699-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="6a699-114">Configure your application to access Storage</span><span class="sxs-lookup"><span data-stu-id="6a699-114">Configure your application to access Storage</span></span>
<span data-ttu-id="6a699-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="6a699-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="6a699-116">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="6a699-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="6a699-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="6a699-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="6a699-118">Type "gem install azure" in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="6a699-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="6a699-119">Import the package</span><span class="sxs-lookup"><span data-stu-id="6a699-119">Import the package</span></span>
<span data-ttu-id="6a699-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="6a699-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="6a699-121">Set up an Azure Storage Connection</span><span class="sxs-lookup"><span data-stu-id="6a699-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="6a699-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6a699-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="6a699-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span><span class="sxs-lookup"><span data-stu-id="6a699-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="6a699-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="6a699-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="6a699-125">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a699-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a699-126">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="6a699-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="6a699-127">In the Settings blade on the right, click **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="6a699-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="6a699-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span><span class="sxs-lookup"><span data-stu-id="6a699-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="6a699-129">You can use either of these.</span><span class="sxs-lookup"><span data-stu-id="6a699-129">You can use either of these.</span></span>
5. <span data-ttu-id="6a699-130">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="6a699-130">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="6a699-131">To obtain these values from a classic storage account in the classic Azure portal:</span><span class="sxs-lookup"><span data-stu-id="6a699-131">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="6a699-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6a699-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6a699-133">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="6a699-133">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="6a699-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span><span class="sxs-lookup"><span data-stu-id="6a699-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="6a699-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span><span class="sxs-lookup"><span data-stu-id="6a699-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="6a699-136">For access key, you can use either the primary one or the secondary one.</span><span class="sxs-lookup"><span data-stu-id="6a699-136">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="6a699-137">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="6a699-137">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="6a699-138">Create a container</span><span class="sxs-lookup"><span data-stu-id="6a699-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="6a699-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span><span class="sxs-lookup"><span data-stu-id="6a699-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="6a699-140">To create a container, use the **create\_container()** method.</span><span class="sxs-lookup"><span data-stu-id="6a699-140">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="6a699-141">The following code example creates a container or prints the error if there is any.</span><span class="sxs-lookup"><span data-stu-id="6a699-141">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="6a699-142">If you want to make the files in the container public, you can set the container's permissions.</span><span class="sxs-lookup"><span data-stu-id="6a699-142">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="6a699-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span><span class="sxs-lookup"><span data-stu-id="6a699-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="6a699-144">Valid values for the **:public\_access\_level** option are:</span><span class="sxs-lookup"><span data-stu-id="6a699-144">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="6a699-145">**blob:** Specifies public read access for blobs.</span><span class="sxs-lookup"><span data-stu-id="6a699-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="6a699-146">Blob data within this container can be read via anonymous request, but container data is not available.</span><span class="sxs-lookup"><span data-stu-id="6a699-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="6a699-147">Clients cannot enumerate blobs within the container via anonymous request.</span><span class="sxs-lookup"><span data-stu-id="6a699-147">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="6a699-148">**container:** Specifies full public read access for container and blob data.</span><span class="sxs-lookup"><span data-stu-id="6a699-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="6a699-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span><span class="sxs-lookup"><span data-stu-id="6a699-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="6a699-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span><span class="sxs-lookup"><span data-stu-id="6a699-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="6a699-151">The following code example changes the public access level to **container**:</span><span class="sxs-lookup"><span data-stu-id="6a699-151">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6a699-152">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="6a699-152">Upload a blob into a container</span></span>
<span data-ttu-id="6a699-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span><span class="sxs-lookup"><span data-stu-id="6a699-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="6a699-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span><span class="sxs-lookup"><span data-stu-id="6a699-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="6a699-155">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="6a699-155">List the blobs in a container</span></span>
<span data-ttu-id="6a699-156">To list the containers, use **list_containers()** method.</span><span class="sxs-lookup"><span data-stu-id="6a699-156">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="6a699-157">To list the blobs within a container, use **list\_blobs()** method.</span><span class="sxs-lookup"><span data-stu-id="6a699-157">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="6a699-158">This outputs the urls of all the blobs in all the containers for the account.</span><span class="sxs-lookup"><span data-stu-id="6a699-158">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="6a699-159">Download blobs</span><span class="sxs-lookup"><span data-stu-id="6a699-159">Download blobs</span></span>
<span data-ttu-id="6a699-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span><span class="sxs-lookup"><span data-stu-id="6a699-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="6a699-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span><span class="sxs-lookup"><span data-stu-id="6a699-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="6a699-162">Delete a Blob</span><span class="sxs-lookup"><span data-stu-id="6a699-162">Delete a Blob</span></span>
<span data-ttu-id="6a699-163">Finally, to delete a blob, use the **delete\_blob()** method.</span><span class="sxs-lookup"><span data-stu-id="6a699-163">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="6a699-164">The following code example demonstrates how to delete a blob.</span><span class="sxs-lookup"><span data-stu-id="6a699-164">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="6a699-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a699-165">Next steps</span></span>
<span data-ttu-id="6a699-166">To learn about more complex storage tasks, follow these links:</span><span class="sxs-lookup"><span data-stu-id="6a699-166">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="6a699-167">Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="6a699-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="6a699-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="6a699-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="6a699-169">Transfer data with the AzCopy Command-Line Utility</span><span class="sxs-lookup"><span data-stu-id="6a699-169">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

