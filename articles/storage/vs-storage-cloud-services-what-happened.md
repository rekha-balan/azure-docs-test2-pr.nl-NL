---
title: What happened to my cloud service project? | Microsoft Docs
description: Describes what happens in a cloud services project after connecting to an Azure storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549081"
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="cf521-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span><span class="sxs-lookup"><span data-stu-id="cf521-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="cf521-105">References added</span><span class="sxs-lookup"><span data-stu-id="cf521-105">References added</span></span>
<span data-ttu-id="cf521-106">The Azure Storage NuGet package was added to your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="cf521-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="cf521-107">This package adds the following .NET references:</span><span class="sxs-lookup"><span data-stu-id="cf521-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="cf521-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="cf521-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="cf521-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="cf521-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="cf521-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="cf521-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="cf521-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="cf521-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="cf521-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="cf521-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="cf521-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="cf521-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="cf521-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="cf521-114">**System.Data**</span></span>
* <span data-ttu-id="cf521-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="cf521-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="cf521-116">Connection string for Azure Storage added</span><span class="sxs-lookup"><span data-stu-id="cf521-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="cf521-117">Elements were created with the selected storage account's connection string and key.</span><span class="sxs-lookup"><span data-stu-id="cf521-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="cf521-118">Modifications were made to the following files:</span><span class="sxs-lookup"><span data-stu-id="cf521-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="cf521-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="cf521-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="cf521-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="cf521-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="cf521-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="cf521-121">**ServiceConfiguration.Local.cscfg**</span></span>

