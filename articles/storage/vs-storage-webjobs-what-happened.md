---
title: What happened to my WebJob project (Visual Studio Azure Storage connected service)? | Microsoft Docs
description: Describes what happened in a Azure WebJob project after connecting to a storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662882"
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a>What happened to my WebJob project (Visual Studio Azure Storage connected service)?
## <a name="references-added"></a>References Added
The Azure Storage NuGet package was added to or updated in your Visual Studio project.  
This package adds the following .NET references:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Connection string for Azure Storage added
In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.

For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).

