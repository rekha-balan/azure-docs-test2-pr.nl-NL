---
title: How to use Azure Blob storage from iOS | Microsoft Docs
description: Store unstructured data in the cloud with Azure Blob storage (object storage).
services: storage
documentationcenter: ios
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: b6e5d2dce97c2f10d0e440a0bde05d50d8965833
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555190"
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="a0481-103">How to use Blob storage from iOS</span><span class="sxs-lookup"><span data-stu-id="a0481-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a0481-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a0481-104">Overview</span></span>
<span data-ttu-id="a0481-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a0481-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="a0481-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="a0481-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="a0481-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span><span class="sxs-lookup"><span data-stu-id="a0481-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="a0481-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="a0481-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="a0481-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span><span class="sxs-lookup"><span data-stu-id="a0481-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="a0481-110">Import the Azure Storage iOS library into your application</span><span class="sxs-lookup"><span data-stu-id="a0481-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="a0481-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span><span class="sxs-lookup"><span data-stu-id="a0481-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span>

## <a name="cocoapod"></a><span data-ttu-id="a0481-112">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="a0481-112">CocoaPod</span></span>
1. <span data-ttu-id="a0481-113">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span><span class="sxs-lookup"><span data-stu-id="a0481-113">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
   
    <span data-ttu-id="a0481-114">sudo gem install cocoapods</span><span class="sxs-lookup"><span data-stu-id="a0481-114">sudo gem install cocoapods</span></span>

2. <span data-ttu-id="a0481-115">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span><span class="sxs-lookup"><span data-stu-id="a0481-115">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="a0481-116">Add the following to _Podfile_ and save.</span><span class="sxs-lookup"><span data-stu-id="a0481-116">Add the following to _Podfile_ and save.</span></span>
   
    <span data-ttu-id="a0481-117">pod 'AZSClient'</span><span class="sxs-lookup"><span data-stu-id="a0481-117">pod 'AZSClient'</span></span>

3. <span data-ttu-id="a0481-118">In the terminal window, navigate to the project directory and run the following command</span><span class="sxs-lookup"><span data-stu-id="a0481-118">In the terminal window, navigate to the project directory and run the following command</span></span>
   
    <span data-ttu-id="a0481-119">pod install</span><span class="sxs-lookup"><span data-stu-id="a0481-119">pod install</span></span>

4. <span data-ttu-id="a0481-120">If your .xcodeproj is open in Xcode, close it.</span><span class="sxs-lookup"><span data-stu-id="a0481-120">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="a0481-121">In your project directory open the newly created project file which will have the .xcworkspace extension.</span><span class="sxs-lookup"><span data-stu-id="a0481-121">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="a0481-122">This is the file you'll work from for now on.</span><span class="sxs-lookup"><span data-stu-id="a0481-122">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="a0481-123">Framework</span><span class="sxs-lookup"><span data-stu-id="a0481-123">Framework</span></span>
<span data-ttu-id="a0481-124">In order to use the Azure Storage iOS library, you will first need to build the framework file.</span><span class="sxs-lookup"><span data-stu-id="a0481-124">In order to use the Azure Storage iOS library, you will first need to build the framework file.</span></span>

1. <span data-ttu-id="a0481-125">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="a0481-125">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="a0481-126">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open AZSClient.xcodeproj in Xcode.</span><span class="sxs-lookup"><span data-stu-id="a0481-126">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open AZSClient.xcodeproj in Xcode.</span></span>
3. <span data-ttu-id="a0481-127">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span><span class="sxs-lookup"><span data-stu-id="a0481-127">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="a0481-128">Build the project (⌘+B).</span><span class="sxs-lookup"><span data-stu-id="a0481-128">Build the project (⌘+B).</span></span> <span data-ttu-id="a0481-129">This will create an AZSClient.framework file on your Desktop.</span><span class="sxs-lookup"><span data-stu-id="a0481-129">This will create an AZSClient.framework file on your Desktop.</span></span>

<span data-ttu-id="a0481-130">You can then import the framework file into your application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="a0481-130">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="a0481-131">Create a new project or open up your existing project in Xcode.</span><span class="sxs-lookup"><span data-stu-id="a0481-131">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="a0481-132">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span><span class="sxs-lookup"><span data-stu-id="a0481-132">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
3. <span data-ttu-id="a0481-133">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span><span class="sxs-lookup"><span data-stu-id="a0481-133">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
4. <span data-ttu-id="a0481-134">Click *Add Other...*. Navigate to and add the `AZSClient.framework` file you just created.</span><span class="sxs-lookup"><span data-stu-id="a0481-134">Click *Add Other...*. Navigate to and add the `AZSClient.framework` file you just created.</span></span>
5. <span data-ttu-id="a0481-135">Under the *Linked Frameworks and Libraries* section, click the Add button (+) again.</span><span class="sxs-lookup"><span data-stu-id="a0481-135">Under the *Linked Frameworks and Libraries* section, click the Add button (+) again.</span></span>
6. <span data-ttu-id="a0481-136">In the list of libraries already provided, search for `libxml2.2.dylib` and add it to your project.</span><span class="sxs-lookup"><span data-stu-id="a0481-136">In the list of libraries already provided, search for `libxml2.2.dylib` and add it to your project.</span></span>
7. <span data-ttu-id="a0481-137">Click the *Build Settings* tab at the top of the project editor.</span><span class="sxs-lookup"><span data-stu-id="a0481-137">Click the *Build Settings* tab at the top of the project editor.</span></span>
8. <span data-ttu-id="a0481-138">Under the *Search Paths* section, double-click *Framework Search Paths* and add the path to your `AZSClient.framework` file.</span><span class="sxs-lookup"><span data-stu-id="a0481-138">Under the *Search Paths* section, double-click *Framework Search Paths* and add the path to your `AZSClient.framework` file.</span></span>

## <a name="import-statement"></a><span data-ttu-id="a0481-139">Import Statement</span><span class="sxs-lookup"><span data-stu-id="a0481-139">Import Statement</span></span>
<span data-ttu-id="a0481-140">You will need to include the following import statement in the file where you want to invoke the Azure Storage API.</span><span class="sxs-lookup"><span data-stu-id="a0481-140">You will need to include the following import statement in the file where you want to invoke the Azure Storage API.</span></span>

```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="a0481-141">Asynchronous Operations</span><span class="sxs-lookup"><span data-stu-id="a0481-141">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="a0481-142">All methods that perform a request against the service are asynchronous operations.</span><span class="sxs-lookup"><span data-stu-id="a0481-142">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="a0481-143">In the code samples, you'll find that these methods have a completion handler.</span><span class="sxs-lookup"><span data-stu-id="a0481-143">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="a0481-144">Code inside the completion handler will run **after** the request is completed.</span><span class="sxs-lookup"><span data-stu-id="a0481-144">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="a0481-145">Code after the completion handler will run **while** the request is being made.</span><span class="sxs-lookup"><span data-stu-id="a0481-145">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="a0481-146">Create a container</span><span class="sxs-lookup"><span data-stu-id="a0481-146">Create a container</span></span>
<span data-ttu-id="a0481-147">Every blob in Azure Storage must reside in a container.</span><span class="sxs-lookup"><span data-stu-id="a0481-147">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="a0481-148">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="a0481-148">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="a0481-149">When choosing a name for your container, be mindful of the naming rules mentioned above.</span><span class="sxs-lookup"><span data-stu-id="a0481-149">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="a0481-150">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span><span class="sxs-lookup"><span data-stu-id="a0481-150">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="a0481-151">Set Container Permissions</span><span class="sxs-lookup"><span data-stu-id="a0481-151">Set Container Permissions</span></span>
<span data-ttu-id="a0481-152">A container's permissions are configured for **Private** access by default.</span><span class="sxs-lookup"><span data-stu-id="a0481-152">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="a0481-153">However, containers provide a few different options for container access:</span><span class="sxs-lookup"><span data-stu-id="a0481-153">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="a0481-154">**Private**: Container and blob data can be read by the account owner only.</span><span class="sxs-lookup"><span data-stu-id="a0481-154">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="a0481-155">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span><span class="sxs-lookup"><span data-stu-id="a0481-155">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="a0481-156">Clients cannot enumerate blobs within the container via anonymous request.</span><span class="sxs-lookup"><span data-stu-id="a0481-156">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="a0481-157">**Container**: Container and blob data can be read via anonymous request.</span><span class="sxs-lookup"><span data-stu-id="a0481-157">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="a0481-158">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span><span class="sxs-lookup"><span data-stu-id="a0481-158">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="a0481-159">The following example shows you how to create a container with **Container** access permissions which will allow public, read-only access for all users on the Internet:</span><span class="sxs-lookup"><span data-stu-id="a0481-159">The following example shows you how to create a container with **Container** access permissions which will allow public, read-only access for all users on the Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a0481-160">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="a0481-160">Upload a blob into a container</span></span>
<span data-ttu-id="a0481-161">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span><span class="sxs-lookup"><span data-stu-id="a0481-161">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="a0481-162">At this moment, the Azure Storage iOS library only supports block blobs.</span><span class="sxs-lookup"><span data-stu-id="a0481-162">At this moment, the Azure Storage iOS library only supports block blobs.</span></span> <span data-ttu-id="a0481-163">In the majority of cases, block blob is the recommended type to use.</span><span class="sxs-lookup"><span data-stu-id="a0481-163">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="a0481-164">The following example shows how to upload a block blob from an NSString.</span><span class="sxs-lookup"><span data-stu-id="a0481-164">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="a0481-165">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span><span class="sxs-lookup"><span data-stu-id="a0481-165">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="a0481-166">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="a0481-166">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="a0481-167">In this sample, we used a public container so you can also verify that this worked by going to the blobs URI:</span><span class="sxs-lookup"><span data-stu-id="a0481-167">In this sample, we used a public container so you can also verify that this worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="a0481-168">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream or a local file.</span><span class="sxs-lookup"><span data-stu-id="a0481-168">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="a0481-169">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="a0481-169">List the blobs in a container</span></span>
<span data-ttu-id="a0481-170">The following example shows how to list all blobs in a container.</span><span class="sxs-lookup"><span data-stu-id="a0481-170">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="a0481-171">When performing this operation, be mindful of the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a0481-171">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="a0481-172">**continuationToken** - The continuation token represents where the listing operation should start.</span><span class="sxs-lookup"><span data-stu-id="a0481-172">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="a0481-173">If no token is provided, it will list blobs from the beginning.</span><span class="sxs-lookup"><span data-stu-id="a0481-173">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="a0481-174">Any number of blobs can be listed, from zero up to a set maximum.</span><span class="sxs-lookup"><span data-stu-id="a0481-174">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="a0481-175">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span><span class="sxs-lookup"><span data-stu-id="a0481-175">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="a0481-176">**prefix** - You can specify the prefix to use for blob listing.</span><span class="sxs-lookup"><span data-stu-id="a0481-176">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="a0481-177">Only blobs that begin with this prefix will be listed.</span><span class="sxs-lookup"><span data-stu-id="a0481-177">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="a0481-178">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span><span class="sxs-lookup"><span data-stu-id="a0481-178">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="a0481-179">However, non-flat listing is currently not supported; this is coming soon.</span><span class="sxs-lookup"><span data-stu-id="a0481-179">However, non-flat listing is currently not supported; this is coming soon.</span></span> <span data-ttu-id="a0481-180">For now, this value should be **YES**.</span><span class="sxs-lookup"><span data-stu-id="a0481-180">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="a0481-181">**blobListingDetails** - You can specify which items to include when listing blobs</span><span class="sxs-lookup"><span data-stu-id="a0481-181">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="a0481-182">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span><span class="sxs-lookup"><span data-stu-id="a0481-182">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="a0481-183">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span><span class="sxs-lookup"><span data-stu-id="a0481-183">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="a0481-184">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span><span class="sxs-lookup"><span data-stu-id="a0481-184">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="a0481-185">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span><span class="sxs-lookup"><span data-stu-id="a0481-185">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="a0481-186">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span><span class="sxs-lookup"><span data-stu-id="a0481-186">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="a0481-187">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span><span class="sxs-lookup"><span data-stu-id="a0481-187">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="a0481-188">**maxResults** - The maximum number of results to return for this operation.</span><span class="sxs-lookup"><span data-stu-id="a0481-188">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="a0481-189">Use -1 to not set a limit.</span><span class="sxs-lookup"><span data-stu-id="a0481-189">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="a0481-190">**completionHandler** - The block of code to execute with the results of the listing operation.</span><span class="sxs-lookup"><span data-stu-id="a0481-190">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="a0481-191">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span><span class="sxs-lookup"><span data-stu-id="a0481-191">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="a0481-192">Download a blob</span><span class="sxs-lookup"><span data-stu-id="a0481-192">Download a blob</span></span>
<span data-ttu-id="a0481-193">The following example shows how to download a blob to a NSString object.</span><span class="sxs-lookup"><span data-stu-id="a0481-193">The following example shows how to download a blob to a NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="a0481-194">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="a0481-194">Delete a blob</span></span>
<span data-ttu-id="a0481-195">The following example shows how to delete a blob.</span><span class="sxs-lookup"><span data-stu-id="a0481-195">The following example shows how to delete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="a0481-196">Delete a blob container</span><span class="sxs-lookup"><span data-stu-id="a0481-196">Delete a blob container</span></span>
<span data-ttu-id="a0481-197">The following example shows how to delete a container.</span><span class="sxs-lookup"><span data-stu-id="a0481-197">The following example shows how to delete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="a0481-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0481-198">Next steps</span></span>
<span data-ttu-id="a0481-199">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span><span class="sxs-lookup"><span data-stu-id="a0481-199">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="a0481-200">Azure Storage Client Library for iOS</span><span class="sxs-lookup"><span data-stu-id="a0481-200">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="a0481-201">Azure Storage iOS Reference Documentation</span><span class="sxs-lookup"><span data-stu-id="a0481-201">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="a0481-202">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="a0481-202">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="a0481-203">Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="a0481-203">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="a0481-204">If you have questions regarding this library feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="a0481-204">If you have questions regarding this library feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="a0481-205">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="a0481-205">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

