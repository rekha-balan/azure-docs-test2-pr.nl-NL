---
title: What happened to my ASP.NET 5 project (Visual Studio connected services) | Microsoft Docs
description: Describes what happens after connecting to an Azure storage account in a Visual Studio ASP.NET 5 project using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4390993772eaf35516e48ad7adcdcec5f1df8d71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553602"
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a>What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?
## <a name="references-added"></a>References added
The Azure Storage NuGet package was added to your Visual Studio project.  
This package adds the following .NET references:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.Configuration**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.

## <a name="connection-string-for-azure-storage-added"></a>Connection string for Azure Storage added
In the config.json file of your project, an element was created with the selected storage account's connection string and key.

For more information, see [ASP.NET 5](http://www.asp.net/vnext).

