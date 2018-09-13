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
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="ab11f-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span><span class="sxs-lookup"><span data-stu-id="ab11f-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="ab11f-105">References Added</span><span class="sxs-lookup"><span data-stu-id="ab11f-105">References Added</span></span>
<span data-ttu-id="ab11f-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="ab11f-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="ab11f-107">This package adds the following .NET references:</span><span class="sxs-lookup"><span data-stu-id="ab11f-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="ab11f-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="ab11f-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="ab11f-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="ab11f-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="ab11f-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="ab11f-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="ab11f-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ab11f-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="ab11f-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="ab11f-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="ab11f-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="ab11f-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="ab11f-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="ab11f-114">**System.Data**</span></span>
* <span data-ttu-id="ab11f-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="ab11f-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="ab11f-116">Connection string for Azure Storage added</span><span class="sxs-lookup"><span data-stu-id="ab11f-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="ab11f-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span><span class="sxs-lookup"><span data-stu-id="ab11f-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="ab11f-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="ab11f-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

