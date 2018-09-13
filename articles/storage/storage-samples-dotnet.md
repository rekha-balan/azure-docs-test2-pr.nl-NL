---
title: Azure Storage samples using .NET | Microsoft Docs
description: View, download, and run sample code and applications for Azure Storage. Discover getting started samples for blobs, queues, tables, and files, using the .NET storage client libraries.
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: ''
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670018"
---
# <a name="azure-storage-samples-using-net"></a>Azure Storage samples using .NET

## <a name="net-sample-index"></a>.NET sample index

The following table provides an overview of our samples repository and the scenarios covered in each sample. Click on the links to view the corresponding sample code in GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Endpoint</th><th style="font-size:110%">Scenario</th><th style="font-size:110%">Sample Code</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Blob</b></td>
<td>Append Blob</td> 
<td><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></td> 
</tr> 
<tr> 
<td>Block Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></td>
</tr> 
<tr> 
<td>Client-Side Encryption</td>
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></td>
</tr> 
<tr> 
<td>Copy Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>Create Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></td>
</tr> 
<tr> 
<td>Delete Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></td>
</tr> 
<tr> 
<td>Delete Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>Blob Metadata/Properties/Stats</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>Container ACL/Metadata/Properties</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></td>
</tr> 
<tr> 
<td>Get Page Ranges</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>Lease Blob/Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>List Blob/Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></td>
</tr> 
<tr> 
<td>Page Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr>   
<tr> 
<td>Service Properties</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></td>
</tr>           
<tr> 
<td>Snapshot Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></td>
</tr> 
<tr> 
<td rowspan="9"><b>File</b></td>
<td>Create Shares/Directories/Files</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr>
<tr> 
<td>Delete Shares/Directories/Files</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></td> 
</tr> 
<tr> 
<td>Directory Properties/Metadata</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr> 
<tr> 
<td>Download Files</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr> 
<tr> 
<td>File Properties/Metadata/Metrics</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr> 
<tr> 
<td>File Service Properties</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr> 
<tr> 
<td>List Directories and Files</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr>
<tr> 
<td>List Shares</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr>
<tr> 
<td>Share Properties/Metadata/Stats</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></td> 
</tr>
<tr> 
<td rowspan="8"><b>Queue</b></td>
<td>Add Message</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Client-Side Encryption</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></td> 
</tr> 
<tr> 
<td>Create Queues</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Delete Message/Queue</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Peek Message</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Queue ACL/Metadata/Stats</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Queue Service Properties</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td>Update Message</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>Table</b></td>
<td>Create Table</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></td> 
</tr> 
<tr> 
<td>Delete Entity/Table</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></td> 
</tr> 
<tr> 
<td>Insert/Merge/Replace Entity</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></td> 
</tr> 
<tr> 
<td>Query Entities</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></td> 
</tr> 
<tr> 
<td>Query Tables</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></td> 
</tr> 
<tr> 
<td>Table ACL/Properties</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></td> 
</tr> 
<tr> 
<td>Update Entity</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Azure Code Samples library

To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally. The Code Sample Library provides sample code in .zip format. Alternatively, you can browse and clone the GitHub repository for each sample.

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a>Getting started guides

Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.

* [Getting Started with Azure Blob Service in .NET](storage-dotnet-how-to-use-blobs.md)
* [Getting Started with Azure Queue Service in .NET](storage-dotnet-how-to-use-queues.md)
* [Getting Started with Azure Table Service in .NET](storage-dotnet-how-to-use-tables.md)
* [Getting Started with Azure File Service in .NET](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a>Next steps

For information on samples for other languages:

* Java: [Azure Storage samples using Java](storage-samples-java.md)
* All other languages: [Azure Storage samples](storage-samples.md)
