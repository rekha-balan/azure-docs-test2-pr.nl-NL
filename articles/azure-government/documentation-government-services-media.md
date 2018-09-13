---
title: Azure Government Media Services | Microsoft Docs
description: This article provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: juliako
manager: erikre
ms.assetid: 1143caf9-b9b0-4a07-ae51-1d0b88022c17
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 03/13/2017
ms.author: juliako
ms.openlocfilehash: 5ca80c3da0ba3a5aee665b25e9416d3f5cf4fc0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669234"
---
# <a name="azure-government-media-services"></a><span data-ttu-id="3d759-103">Azure Government Media Services</span><span class="sxs-lookup"><span data-stu-id="3d759-103">Azure Government Media Services</span></span> 
 
<span data-ttu-id="3d759-104">For details on this service and how to use it, see the [Azure Media Services documentation](../media-services/index.md).</span><span class="sxs-lookup"><span data-stu-id="3d759-104">For details on this service and how to use it, see the [Azure Media Services documentation](../media-services/index.md).</span></span>

<span data-ttu-id="3d759-105">Azure Media Services (AMS) is currently generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="3d759-105">Azure Media Services (AMS) is currently generally available in Azure Government.</span></span>

## <a name="connecting"></a><span data-ttu-id="3d759-106">Connecting</span><span class="sxs-lookup"><span data-stu-id="3d759-106">Connecting</span></span>  

<span data-ttu-id="3d759-107">For information on how to connect to AMS, see [connecting with .NET](../media-services/media-services-dotnet-connect-programmatically.md) or [connecting with REST](../media-services/media-services-rest-connect-programmatically.md) topic.</span><span class="sxs-lookup"><span data-stu-id="3d759-107">For information on how to connect to AMS, see [connecting with .NET](../media-services/media-services-dotnet-connect-programmatically.md) or [connecting with REST](../media-services/media-services-rest-connect-programmatically.md) topic.</span></span>

<span data-ttu-id="3d759-108">When connecting to Media Services in Azure Government, use the following values:</span><span class="sxs-lookup"><span data-stu-id="3d759-108">When connecting to Media Services in Azure Government, use the following values:</span></span>

### <a name="acs-scope"></a><span data-ttu-id="3d759-109">ACS scope</span><span class="sxs-lookup"><span data-stu-id="3d759-109">ACS scope</span></span>

<span data-ttu-id="3d759-110">The context scope should be set to "urn:WindowsAzureMediaServices".</span><span class="sxs-lookup"><span data-stu-id="3d759-110">The context scope should be set to "urn:WindowsAzureMediaServices".</span></span>

### <a name="acs"></a><span data-ttu-id="3d759-111">ACS</span><span class="sxs-lookup"><span data-stu-id="3d759-111">ACS</span></span>

<span data-ttu-id="3d759-112">The ACS base address should be set to "https://ams-usge-0-acs-global-1-1.accesscontrol.usgovcloudapi.net"</span><span class="sxs-lookup"><span data-stu-id="3d759-112">The ACS base address should be set to "https://ams-usge-0-acs-global-1-1.accesscontrol.usgovcloudapi.net"</span></span>

### <a name="rest-endpoints"></a><span data-ttu-id="3d759-113">REST endpoints</span><span class="sxs-lookup"><span data-stu-id="3d759-113">REST endpoints</span></span>

<span data-ttu-id="3d759-114">The API server address depends on what region you are deployed to:</span><span class="sxs-lookup"><span data-stu-id="3d759-114">The API server address depends on what region you are deployed to:</span></span>

- <span data-ttu-id="3d759-115">US Gov Virginia: "https://ams-usge-1-hos-rest-1-1.usgovcloudapp.net/API/"</span><span class="sxs-lookup"><span data-stu-id="3d759-115">US Gov Virginia: "https://ams-usge-1-hos-rest-1-1.usgovcloudapp.net/API/"</span></span>
- <span data-ttu-id="3d759-116">US Gov Iowa: "https://ams-usgc-1-hos-rest-1-1.usgovcloudapp.net/API/"</span><span class="sxs-lookup"><span data-stu-id="3d759-116">US Gov Iowa: "https://ams-usgc-1-hos-rest-1-1.usgovcloudapp.net/API/"</span></span>

## <a name="analyzing"></a><span data-ttu-id="3d759-117">Analyzing</span><span class="sxs-lookup"><span data-stu-id="3d759-117">Analyzing</span></span>

<span data-ttu-id="3d759-118">The "Azure Media Indexer 2 Preview" Azure Media Analytics media processor is not available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="3d759-118">The "Azure Media Indexer 2 Preview" Azure Media Analytics media processor is not available in Azure Government.</span></span>
 
## <a name="cdn-integration"></a><span data-ttu-id="3d759-119">CDN integration</span><span class="sxs-lookup"><span data-stu-id="3d759-119">CDN integration</span></span>

<span data-ttu-id="3d759-120">There is no CDN integration with streaming endpoints in Azure Government DCs.</span><span class="sxs-lookup"><span data-stu-id="3d759-120">There is no CDN integration with streaming endpoints in Azure Government DCs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d759-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3d759-121">Next Steps</span></span>
<span data-ttu-id="3d759-122">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="3d759-122">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>

