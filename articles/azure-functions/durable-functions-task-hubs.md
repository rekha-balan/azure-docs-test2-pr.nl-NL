---
title: Task hubs in Durable Functions - Azure
description: Learn what a task hub is in the Durable Functions extension for Azure Functions. Learn how to configure configure task hubs.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 53c70d4407222a80a9bc948db51294cd3e4e1bb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857390"
---
# <a name="task-hubs-in-durable-functions-azure-functions"></a><span data-ttu-id="9e345-104">Task hubs in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="9e345-104">Task hubs in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="9e345-105">A *task hub* in [Durable Functions](durable-functions-overview.md) is a logical container for Azure Storage resources that are used for orchestrations.</span><span class="sxs-lookup"><span data-stu-id="9e345-105">A *task hub* in [Durable Functions](durable-functions-overview.md) is a logical container for Azure Storage resources that are used for orchestrations.</span></span> <span data-ttu-id="9e345-106">Orchestrator and activity functions can only interact with each other when they belong to the same task hub.</span><span class="sxs-lookup"><span data-stu-id="9e345-106">Orchestrator and activity functions can only interact with each other when they belong to the same task hub.</span></span>

<span data-ttu-id="9e345-107">Each function app has a separate task hub.</span><span class="sxs-lookup"><span data-stu-id="9e345-107">Each function app has a separate task hub.</span></span> <span data-ttu-id="9e345-108">If multiple function apps share a storage account, the storage account contains multiple task hubs.</span><span class="sxs-lookup"><span data-stu-id="9e345-108">If multiple function apps share a storage account, the storage account contains multiple task hubs.</span></span> <span data-ttu-id="9e345-109">The following diagram illustrates one task hub per function app in shared and dedicated storage accounts.</span><span class="sxs-lookup"><span data-stu-id="9e345-109">The following diagram illustrates one task hub per function app in shared and dedicated storage accounts.</span></span>

![Diagram showing shared and dedicated storage accounts.](media/durable-functions-task-hubs/task-hubs-storage.png)

## <a name="azure-storage-resources"></a><span data-ttu-id="9e345-111">Azure Storage resources</span><span class="sxs-lookup"><span data-stu-id="9e345-111">Azure Storage resources</span></span>

<span data-ttu-id="9e345-112">A task hub consists of the following storage resources:</span><span class="sxs-lookup"><span data-stu-id="9e345-112">A task hub consists of the following storage resources:</span></span> 

* <span data-ttu-id="9e345-113">One or more control queues.</span><span class="sxs-lookup"><span data-stu-id="9e345-113">One or more control queues.</span></span>
* <span data-ttu-id="9e345-114">One work-item queue.</span><span class="sxs-lookup"><span data-stu-id="9e345-114">One work-item queue.</span></span>
* <span data-ttu-id="9e345-115">One history table.</span><span class="sxs-lookup"><span data-stu-id="9e345-115">One history table.</span></span>
* <span data-ttu-id="9e345-116">One instances table.</span><span class="sxs-lookup"><span data-stu-id="9e345-116">One instances table.</span></span>
* <span data-ttu-id="9e345-117">One storage container containing one or more lease blobs.</span><span class="sxs-lookup"><span data-stu-id="9e345-117">One storage container containing one or more lease blobs.</span></span>

<span data-ttu-id="9e345-118">All of these resources are created automatically in the default Azure Storage account when orchestrator or activity functions run or are scheduled to run.</span><span class="sxs-lookup"><span data-stu-id="9e345-118">All of these resources are created automatically in the default Azure Storage account when orchestrator or activity functions run or are scheduled to run.</span></span> <span data-ttu-id="9e345-119">The [Performance and Scale](durable-functions-perf-and-scale.md) article explains how these resources are used.</span><span class="sxs-lookup"><span data-stu-id="9e345-119">The [Performance and Scale](durable-functions-perf-and-scale.md) article explains how these resources are used.</span></span>

## <a name="task-hub-names"></a><span data-ttu-id="9e345-120">Task hub names</span><span class="sxs-lookup"><span data-stu-id="9e345-120">Task hub names</span></span>

<span data-ttu-id="9e345-121">Task hubs are identified by a name that is declared in the *host.json* file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="9e345-121">Task hubs are identified by a name that is declared in the *host.json* file, as shown in the following example:</span></span>

```json
{
  "durableTask": {
    "HubName": "MyTaskHub"
  }
}
```

<span data-ttu-id="9e345-122">Task hub names must start with a letter and consist of only letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="9e345-122">Task hub names must start with a letter and consist of only letters and numbers.</span></span> <span data-ttu-id="9e345-123">If not specified, the default name is **DurableFunctionsHub**.</span><span class="sxs-lookup"><span data-stu-id="9e345-123">If not specified, the default name is **DurableFunctionsHub**.</span></span>

> [!NOTE]
> <span data-ttu-id="9e345-124">The name is what differentiates one task hub from another when there are multiple task hubs in a shared storage account.</span><span class="sxs-lookup"><span data-stu-id="9e345-124">The name is what differentiates one task hub from another when there are multiple task hubs in a shared storage account.</span></span> <span data-ttu-id="9e345-125">If you have multiple function apps sharing a shared storage account, you have to configure different names for each task hub in the *host.json* files.</span><span class="sxs-lookup"><span data-stu-id="9e345-125">If you have multiple function apps sharing a shared storage account, you have to configure different names for each task hub in the *host.json* files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e345-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e345-126">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e345-127">Learn how to handle versioning</span><span class="sxs-lookup"><span data-stu-id="9e345-127">Learn how to handle versioning</span></span>](durable-functions-versioning.md)
