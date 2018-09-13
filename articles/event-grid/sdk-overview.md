---
title: Azure Event Grid SDKs
description: Describes the SDKs for Azure Event Grid. These SDKs provide management, publishing and consumption.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 06/29/2018
ms.author: tomfitz
ms.openlocfilehash: 3c085074863aa166a5766116b6c63b7dc341ad96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870758"
---
# <a name="event-grid-sdks-for-management-and-publishing"></a><span data-ttu-id="34cdb-104">Event Grid SDKs for management and publishing</span><span class="sxs-lookup"><span data-stu-id="34cdb-104">Event Grid SDKs for management and publishing</span></span>

<span data-ttu-id="34cdb-105">Event Grid provides SDKs that enable you to programmatically manage your resources and post events.</span><span class="sxs-lookup"><span data-stu-id="34cdb-105">Event Grid provides SDKs that enable you to programmatically manage your resources and post events.</span></span>

## <a name="management-sdks"></a><span data-ttu-id="34cdb-106">Management SDKs</span><span class="sxs-lookup"><span data-stu-id="34cdb-106">Management SDKs</span></span>

<span data-ttu-id="34cdb-107">The management SDKs enable you to create, update, and delete event grid topics and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="34cdb-107">The management SDKs enable you to create, update, and delete event grid topics and subscriptions.</span></span> <span data-ttu-id="34cdb-108">Currently, the following SDKs are available:</span><span class="sxs-lookup"><span data-stu-id="34cdb-108">Currently, the following SDKs are available:</span></span>

* [<span data-ttu-id="34cdb-109">.NET</span><span class="sxs-lookup"><span data-stu-id="34cdb-109">.NET</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventGrid)
* [<span data-ttu-id="34cdb-110">Go</span><span class="sxs-lookup"><span data-stu-id="34cdb-110">Go</span></span>](https://github.com/Azure/azure-sdk-for-go)
* [<span data-ttu-id="34cdb-111">Java</span><span class="sxs-lookup"><span data-stu-id="34cdb-111">Java</span></span>](https://search.maven.org/#search%7Cga%7C1%7Cazure-mgmt-eventgrid)
* [<span data-ttu-id="34cdb-112">Node</span><span class="sxs-lookup"><span data-stu-id="34cdb-112">Node</span></span>](https://www.npmjs.com/package/azure-arm-eventgrid)
* [<span data-ttu-id="34cdb-113">Python</span><span class="sxs-lookup"><span data-stu-id="34cdb-113">Python</span></span>](https://pypi.python.org/pypi/azure-mgmt-eventgrid)
* [<span data-ttu-id="34cdb-114">Ruby</span><span class="sxs-lookup"><span data-stu-id="34cdb-114">Ruby</span></span>](https://rubygems.org/gems/azure_mgmt_event_grid)

## <a name="data-plane-sdks"></a><span data-ttu-id="34cdb-115">Data plane SDKs</span><span class="sxs-lookup"><span data-stu-id="34cdb-115">Data plane SDKs</span></span>

<span data-ttu-id="34cdb-116">The data plane SDKs enable you to post events to topics by taking care of authenticating, forming the event, and asynchronously posting to the specified endpoint.</span><span class="sxs-lookup"><span data-stu-id="34cdb-116">The data plane SDKs enable you to post events to topics by taking care of authenticating, forming the event, and asynchronously posting to the specified endpoint.</span></span> <span data-ttu-id="34cdb-117">They also enable you to consume first party events.</span><span class="sxs-lookup"><span data-stu-id="34cdb-117">They also enable you to consume first party events.</span></span> <span data-ttu-id="34cdb-118">Currently, the following SDKs are available:</span><span class="sxs-lookup"><span data-stu-id="34cdb-118">Currently, the following SDKs are available:</span></span>

* [<span data-ttu-id="34cdb-119">.NET</span><span class="sxs-lookup"><span data-stu-id="34cdb-119">.NET</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventGrid)
* [<span data-ttu-id="34cdb-120">Go</span><span class="sxs-lookup"><span data-stu-id="34cdb-120">Go</span></span>](https://github.com/Azure/azure-sdk-for-go)
* [<span data-ttu-id="34cdb-121">Java</span><span class="sxs-lookup"><span data-stu-id="34cdb-121">Java</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventgrid)
* [<span data-ttu-id="34cdb-122">Node</span><span class="sxs-lookup"><span data-stu-id="34cdb-122">Node</span></span>](https://www.npmjs.com/package/azure-eventgrid)
* [<span data-ttu-id="34cdb-123">Python</span><span class="sxs-lookup"><span data-stu-id="34cdb-123">Python</span></span>](https://pypi.python.org/pypi/azure-eventgrid)
* [<span data-ttu-id="34cdb-124">Ruby</span><span class="sxs-lookup"><span data-stu-id="34cdb-124">Ruby</span></span>](https://rubygems.org/gems/azure_event_grid)

## <a name="next-steps"></a><span data-ttu-id="34cdb-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="34cdb-125">Next steps</span></span>

* <span data-ttu-id="34cdb-126">For example applications, see [Event Grid code samples](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid).</span><span class="sxs-lookup"><span data-stu-id="34cdb-126">For example applications, see [Event Grid code samples](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid).</span></span>
* <span data-ttu-id="34cdb-127">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="34cdb-127">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="34cdb-128">For Event Grid commands in Azure CLI, see [Azure CLI](/cli/azure/eventgrid).</span><span class="sxs-lookup"><span data-stu-id="34cdb-128">For Event Grid commands in Azure CLI, see [Azure CLI](/cli/azure/eventgrid).</span></span>
* <span data-ttu-id="34cdb-129">For Event Grid commands in PowerShell, see [PowerShell](/powershell/module/azurerm.eventgrid).</span><span class="sxs-lookup"><span data-stu-id="34cdb-129">For Event Grid commands in PowerShell, see [PowerShell](/powershell/module/azurerm.eventgrid).</span></span>
