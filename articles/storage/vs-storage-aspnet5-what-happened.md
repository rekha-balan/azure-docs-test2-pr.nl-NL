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
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="69619-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span><span class="sxs-lookup"><span data-stu-id="69619-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="69619-104">References added</span><span class="sxs-lookup"><span data-stu-id="69619-104">References added</span></span>
<span data-ttu-id="69619-105">The Azure Storage NuGet package was added to your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="69619-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="69619-106">This package adds the following .NET references:</span><span class="sxs-lookup"><span data-stu-id="69619-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="69619-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="69619-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="69619-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="69619-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="69619-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="69619-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="69619-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="69619-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="69619-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="69619-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="69619-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="69619-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="69619-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="69619-113">**System.Data**</span></span>
* <span data-ttu-id="69619-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="69619-114">**System.Spatial**</span></span>

<span data-ttu-id="69619-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span><span class="sxs-lookup"><span data-stu-id="69619-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="69619-116">Connection string for Azure Storage added</span><span class="sxs-lookup"><span data-stu-id="69619-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="69619-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span><span class="sxs-lookup"><span data-stu-id="69619-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="69619-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="69619-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

