---
title: Azure Data Factory Developer Reference
description: Learn about different ways to create, monitor, and manage Azure data factories
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e0f6c078b60df6bb7381d066bebb3e400b3b97ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551460"
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="6c5ae-103">Azure Data Factory Developer Reference</span><span class="sxs-lookup"><span data-stu-id="6c5ae-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="6c5ae-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span><span class="sxs-lookup"><span data-stu-id="6c5ae-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="6c5ae-105">Method</span><span class="sxs-lookup"><span data-stu-id="6c5ae-105">Method</span></span> | <span data-ttu-id="6c5ae-106">Resource Location</span><span class="sxs-lookup"><span data-stu-id="6c5ae-106">Resource Location</span></span> | <span data-ttu-id="6c5ae-107">Developer References</span><span class="sxs-lookup"><span data-stu-id="6c5ae-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c5ae-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6c5ae-108">Azure portal</span></span> |[https://portal.azure.com/](https://portal.azure.com) |[<span data-ttu-id="6c5ae-109">Get started with Azure Data Factory (Azure portal)</span><span class="sxs-lookup"><span data-stu-id="6c5ae-109">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="6c5ae-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c5ae-110">Azure PowerShell</span></span> |<span data-ttu-id="6c5ae-111">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="6c5ae-111">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="6c5ae-112">Cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="6c5ae-112">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="6c5ae-113">.NET Class Library</span><span class="sxs-lookup"><span data-stu-id="6c5ae-113">.NET Class Library</span></span> |<span data-ttu-id="6c5ae-114">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span><span class="sxs-lookup"><span data-stu-id="6c5ae-114">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="6c5ae-115">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span><span class="sxs-lookup"><span data-stu-id="6c5ae-115">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span></span><br/><br/><span data-ttu-id="6c5ae-116"><b>Downloading the latest Nuget</b></span><span class="sxs-lookup"><span data-stu-id="6c5ae-116"><b>Downloading the latest Nuget</b></span></span><br/><span data-ttu-id="6c5ae-117">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span><span class="sxs-lookup"><span data-stu-id="6c5ae-117">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="6c5ae-118">**Using Package Manager Console in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="6c5ae-118">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="6c5ae-119">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span><span class="sxs-lookup"><span data-stu-id="6c5ae-119">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="6c5ae-120">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="6c5ae-120">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="6c5ae-121">.NET SDK Reference</span><span class="sxs-lookup"><span data-stu-id="6c5ae-121">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="6c5ae-122">REST API</span><span class="sxs-lookup"><span data-stu-id="6c5ae-122">REST API</span></span> |<span data-ttu-id="6c5ae-123">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span><span class="sxs-lookup"><span data-stu-id="6c5ae-123">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="6c5ae-124">REST API Reference</span><span class="sxs-lookup"><span data-stu-id="6c5ae-124">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

