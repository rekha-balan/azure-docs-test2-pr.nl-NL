---
title: Use Azure storage in Windows Store apps | Microsoft Docs
description: Learn how to create a Windows Store app that uses Azure Blob, Queue, Table, or File storage.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ea4c681f444ec2967b61eea9a02ac05685056399
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562968"
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a>How to use Azure Storage in Windows Store apps
## <a name="overview"></a>Overview
This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.

## <a name="download-required-tools"></a>Download required tools
* [Visual Studio](https://www.visualstudio.com/en-us/visual-studio-homepage-vs.aspx) makes it easy to build, debug, localize, package, and deploy Windows Store apps. Visual Studio 2012 or later is required.
* The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.
* [WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.

## <a name="develop-apps"></a>Develop apps
### <a name="getting-ready"></a>Getting ready
Create a new Windows Store app project in Visual Studio 2012 or later:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a>Using the library with the Blob and Queue services
At this point, your app is ready to call the Azure Blob and Queue services. Add the following **using** statements so that Azure Storage types can be referenced directly:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Next, add a button to your page. Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

This code assumes that you have two string variables, *accountName* and *accountKey*. They represent the name of your storage account and the account key that is associated with that account.

Build and run the application. Clicking the button will check whether a container named *container1* exists in your account and then create it if not.

### <a name="using-the-library-with-the-table-service"></a>Using the library with the Table service
Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library. Next, add a reference to the required WCF libraries by using the Package Manager Console:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Use the following command to point Package Manager to the location on your machine:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

This command will automatically add all required references to your project. If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

This code checks whether a table named *table1* exists in your account, and then creates it if not.

You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded. This library contains additional functionality, such as reflection-based serialization and generic queries. Note that this library does not support JavaScript.

[store-apps-storage-vs-project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-use-store-apps/store-apps-storage-package-manager.png



