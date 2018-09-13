---
title: Introduction to Azure Stack storage
description: Learn about Azure Stack storage
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: 092aba28-04bc-44c0-90e1-e79d82f4ff42
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/21/2018
ms.author: mabrigg
ms.openlocfilehash: d97a5f8aff57f4bbfd7d5222a87d258fa5c92da8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857463"
---
# <a name="introduction-to-azure-stack-storage"></a><span data-ttu-id="800c7-103">Introduction to Azure Stack storage</span><span class="sxs-lookup"><span data-stu-id="800c7-103">Introduction to Azure Stack storage</span></span>

<span data-ttu-id="800c7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="800c7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="overview"></a><span data-ttu-id="800c7-105">Overview</span><span class="sxs-lookup"><span data-stu-id="800c7-105">Overview</span></span>

<span data-ttu-id="800c7-106">Azure Stack Storage is a set of cloud storage services that includes Blobs, Tables and Queues which are consistent with Azure Storage services.</span><span class="sxs-lookup"><span data-stu-id="800c7-106">Azure Stack Storage is a set of cloud storage services that includes Blobs, Tables and Queues which are consistent with Azure Storage services.</span></span>

## <a name="azure-stack-storage-services"></a><span data-ttu-id="800c7-107">Azure Stack Storage services</span><span class="sxs-lookup"><span data-stu-id="800c7-107">Azure Stack Storage services</span></span>

<span data-ttu-id="800c7-108">Azure Stack storage provides the following three services:</span><span class="sxs-lookup"><span data-stu-id="800c7-108">Azure Stack storage provides the following three services:</span></span>

- <span data-ttu-id="800c7-109">**Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="800c7-109">**Blob Storage**</span></span>

    <span data-ttu-id="800c7-110">Blob storage stores unstructured object data.</span><span class="sxs-lookup"><span data-stu-id="800c7-110">Blob storage stores unstructured object data.</span></span> <span data-ttu-id="800c7-111">A blob can be any type of text or binary data, such as a document, media file, or application installer.</span><span class="sxs-lookup"><span data-stu-id="800c7-111">A blob can be any type of text or binary data, such as a document, media file, or application installer.</span></span>

- <span data-ttu-id="800c7-112">**Table Storage**</span><span class="sxs-lookup"><span data-stu-id="800c7-112">**Table Storage**</span></span>

    <span data-ttu-id="800c7-113">Table storage stores structured datasets.</span><span class="sxs-lookup"><span data-stu-id="800c7-113">Table storage stores structured datasets.</span></span> <span data-ttu-id="800c7-114">Table storage is a NoSQL key-attribute data store, which allows for rapid development and fast access to large quantities of data.</span><span class="sxs-lookup"><span data-stu-id="800c7-114">Table storage is a NoSQL key-attribute data store, which allows for rapid development and fast access to large quantities of data.</span></span>

- <span data-ttu-id="800c7-115">**Queue Storage**</span><span class="sxs-lookup"><span data-stu-id="800c7-115">**Queue Storage**</span></span>

    <span data-ttu-id="800c7-116">Queue storage provides reliable messaging for workflow processing and for communication between components of cloud services.</span><span class="sxs-lookup"><span data-stu-id="800c7-116">Queue storage provides reliable messaging for workflow processing and for communication between components of cloud services.</span></span>

<span data-ttu-id="800c7-117">An Azure Stack storage account is a secure account that gives you access to services in Azure Stack Storage.</span><span class="sxs-lookup"><span data-stu-id="800c7-117">An Azure Stack storage account is a secure account that gives you access to services in Azure Stack Storage.</span></span> <span data-ttu-id="800c7-118">Your storage account provides the unique namespace for your storage resources.</span><span class="sxs-lookup"><span data-stu-id="800c7-118">Your storage account provides the unique namespace for your storage resources.</span></span> <span data-ttu-id="800c7-119">The following diagram shows the relationships between the Azure Stack storage resources in a storage account:</span><span class="sxs-lookup"><span data-stu-id="800c7-119">The following diagram shows the relationships between the Azure Stack storage resources in a storage account:</span></span>

![Azure Stack Storage overview](media/azure-stack-storage-overview/AzureStackStorageOverview.png)

### <a name="blob-storage"></a><span data-ttu-id="800c7-121">Blob storage</span><span class="sxs-lookup"><span data-stu-id="800c7-121">Blob storage</span></span>

<span data-ttu-id="800c7-122">For users with a large amount of unstructured object data to store in the cloud, blob storage offers an effective and scalable solution.</span><span class="sxs-lookup"><span data-stu-id="800c7-122">For users with a large amount of unstructured object data to store in the cloud, blob storage offers an effective and scalable solution.</span></span> <span data-ttu-id="800c7-123">You can use blob storage to store content such as:</span><span class="sxs-lookup"><span data-stu-id="800c7-123">You can use blob storage to store content such as:</span></span>

- <span data-ttu-id="800c7-124">Documents</span><span class="sxs-lookup"><span data-stu-id="800c7-124">Documents</span></span>
- <span data-ttu-id="800c7-125">Social data such as photos, videos, music, and blogs</span><span class="sxs-lookup"><span data-stu-id="800c7-125">Social data such as photos, videos, music, and blogs</span></span>
- <span data-ttu-id="800c7-126">Backups of files, computers, databases, and devices</span><span class="sxs-lookup"><span data-stu-id="800c7-126">Backups of files, computers, databases, and devices</span></span>
- <span data-ttu-id="800c7-127">Images and text for web applications</span><span class="sxs-lookup"><span data-stu-id="800c7-127">Images and text for web applications</span></span>
- <span data-ttu-id="800c7-128">Configuration data for cloud applications</span><span class="sxs-lookup"><span data-stu-id="800c7-128">Configuration data for cloud applications</span></span>
- <span data-ttu-id="800c7-129">Big data, such as logs and other large datasets</span><span class="sxs-lookup"><span data-stu-id="800c7-129">Big data, such as logs and other large datasets</span></span>

<span data-ttu-id="800c7-130">Every blob is organized into a container.</span><span class="sxs-lookup"><span data-stu-id="800c7-130">Every blob is organized into a container.</span></span> <span data-ttu-id="800c7-131">Containers also provide a useful way to assign security policies to groups of objects.</span><span class="sxs-lookup"><span data-stu-id="800c7-131">Containers also provide a useful way to assign security policies to groups of objects.</span></span> <span data-ttu-id="800c7-132">A storage account can contain any number of containers, and a container can contain any number of blobs, up to the limit of storage account.</span><span class="sxs-lookup"><span data-stu-id="800c7-132">A storage account can contain any number of containers, and a container can contain any number of blobs, up to the limit of storage account.</span></span>

<span data-ttu-id="800c7-133">Blob storage offers three types of blobs:</span><span class="sxs-lookup"><span data-stu-id="800c7-133">Blob storage offers three types of blobs:</span></span>

- <span data-ttu-id="800c7-134">**Block blobs**</span><span class="sxs-lookup"><span data-stu-id="800c7-134">**Block blobs**</span></span>

    <span data-ttu-id="800c7-135">Block blobs are optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups, and etc.</span><span class="sxs-lookup"><span data-stu-id="800c7-135">Block blobs are optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups, and etc.</span></span>

- <span data-ttu-id="800c7-136">**Append blobs**</span><span class="sxs-lookup"><span data-stu-id="800c7-136">**Append blobs**</span></span>

    <span data-ttu-id="800c7-137">Append blobs are similar to block blobs, but are optimized for append operations.</span><span class="sxs-lookup"><span data-stu-id="800c7-137">Append blobs are similar to block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="800c7-138">An append blob can be updated only by adding a new block to the end.</span><span class="sxs-lookup"><span data-stu-id="800c7-138">An append blob can be updated only by adding a new block to the end.</span></span> <span data-ttu-id="800c7-139">Append blobs are a good choice for scenarios such as logging, where new data needs to be written only to the end of the blob.</span><span class="sxs-lookup"><span data-stu-id="800c7-139">Append blobs are a good choice for scenarios such as logging, where new data needs to be written only to the end of the blob.</span></span>

- <span data-ttu-id="800c7-140">**Page blobs**</span><span class="sxs-lookup"><span data-stu-id="800c7-140">**Page blobs**</span></span>

    <span data-ttu-id="800c7-141">Page blobs are optimized for representing IaaS disks and supporting random writes that is up to 1 TB in size.</span><span class="sxs-lookup"><span data-stu-id="800c7-141">Page blobs are optimized for representing IaaS disks and supporting random writes that is up to 1 TB in size.</span></span> <span data-ttu-id="800c7-142">An Azure Stack virtual machine attached IaaS disk is a VHD stored as a page blob.</span><span class="sxs-lookup"><span data-stu-id="800c7-142">An Azure Stack virtual machine attached IaaS disk is a VHD stored as a page blob.</span></span>

### <a name="table-storage"></a><span data-ttu-id="800c7-143">Table storage</span><span class="sxs-lookup"><span data-stu-id="800c7-143">Table storage</span></span>

<span data-ttu-id="800c7-144">Modern applications often demand data stores with greater scalability and flexibility than previous generations of software required.</span><span class="sxs-lookup"><span data-stu-id="800c7-144">Modern applications often demand data stores with greater scalability and flexibility than previous generations of software required.</span></span> <span data-ttu-id="800c7-145">Table storage offers highly available, massively scalable storage, so that your application can automatically scale to meet user demand.</span><span class="sxs-lookup"><span data-stu-id="800c7-145">Table storage offers highly available, massively scalable storage, so that your application can automatically scale to meet user demand.</span></span> <span data-ttu-id="800c7-146">Table storage is Microsoft's NoSQL key/attribute store -- it has a schemaless design, making it different from traditional relational databases.</span><span class="sxs-lookup"><span data-stu-id="800c7-146">Table storage is Microsoft's NoSQL key/attribute store -- it has a schemaless design, making it different from traditional relational databases.</span></span> <span data-ttu-id="800c7-147">With a schemaless data store, it's easy to adapt your data as the needs of your application evolve.</span><span class="sxs-lookup"><span data-stu-id="800c7-147">With a schemaless data store, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="800c7-148">Table storage is easy to use, so developers can create applications quickly.</span><span class="sxs-lookup"><span data-stu-id="800c7-148">Table storage is easy to use, so developers can create applications quickly.</span></span>

<span data-ttu-id="800c7-149">Table storage is a key-attribute store, which means that every value in a table is stored with a typed property name.</span><span class="sxs-lookup"><span data-stu-id="800c7-149">Table storage is a key-attribute store, which means that every value in a table is stored with a typed property name.</span></span> <span data-ttu-id="800c7-150">The property name can be used for filtering and specifying selection criteria.</span><span class="sxs-lookup"><span data-stu-id="800c7-150">The property name can be used for filtering and specifying selection criteria.</span></span> <span data-ttu-id="800c7-151">A collection of properties and their values comprise an entity.</span><span class="sxs-lookup"><span data-stu-id="800c7-151">A collection of properties and their values comprise an entity.</span></span> <span data-ttu-id="800c7-152">Since table storage is schemaless, two entities in the same table can contain different collections of properties, and those properties can be of different types.</span><span class="sxs-lookup"><span data-stu-id="800c7-152">Since table storage is schemaless, two entities in the same table can contain different collections of properties, and those properties can be of different types.</span></span>

<span data-ttu-id="800c7-153">You can use table storage to store flexible datasets, such as user data for web applications, address books, device information, and any other type of metadata that your service requires.</span><span class="sxs-lookup"><span data-stu-id="800c7-153">You can use table storage to store flexible datasets, such as user data for web applications, address books, device information, and any other type of metadata that your service requires.</span></span> <span data-ttu-id="800c7-154">For today's Internet-based applications, NoSQL databases like table storage offer a popular alternative to traditional relational databases.</span><span class="sxs-lookup"><span data-stu-id="800c7-154">For today's Internet-based applications, NoSQL databases like table storage offer a popular alternative to traditional relational databases.</span></span>

<span data-ttu-id="800c7-155">A storage account can contain any number of tables, and a table can contain any number of entities, up to the capacity limit of the storage account.</span><span class="sxs-lookup"><span data-stu-id="800c7-155">A storage account can contain any number of tables, and a table can contain any number of entities, up to the capacity limit of the storage account.</span></span>

### <a name="queue-storage"></a><span data-ttu-id="800c7-156">Queue storage</span><span class="sxs-lookup"><span data-stu-id="800c7-156">Queue storage</span></span>

<span data-ttu-id="800c7-157">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span><span class="sxs-lookup"><span data-stu-id="800c7-157">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="800c7-158">Queue storage provides a reliable messaging solution for asynchronous communication between application components, whether they're running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="800c7-158">Queue storage provides a reliable messaging solution for asynchronous communication between application components, whether they're running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="800c7-159">Queue storage also supports managing asynchronous tasks and building process workflows.</span><span class="sxs-lookup"><span data-stu-id="800c7-159">Queue storage also supports managing asynchronous tasks and building process workflows.</span></span>

<span data-ttu-id="800c7-160">A storage account can contain any number of queues, and a queue can contain any number of messages, up to the capacity limit of the storage account.</span><span class="sxs-lookup"><span data-stu-id="800c7-160">A storage account can contain any number of queues, and a queue can contain any number of messages, up to the capacity limit of the storage account.</span></span> <span data-ttu-id="800c7-161">Individual messages may be up to 64 KB in size.</span><span class="sxs-lookup"><span data-stu-id="800c7-161">Individual messages may be up to 64 KB in size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="800c7-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="800c7-162">Next steps</span></span>

- [<span data-ttu-id="800c7-163">Azure-consistent storage: differences and considerations</span><span class="sxs-lookup"><span data-stu-id="800c7-163">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)

- <span data-ttu-id="800c7-164">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="800c7-164">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../../storage/common/storage-introduction.md)</span></span>
