---
title: Azure CLI Script Sample - Running a job with Batch | Microsoft Docs
description: Azure CLI Script Sample - Running a job with Batch
services: batch
documentationcenter: ''
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/20/2017
ms.author: antisch
ms.openlocfilehash: a14f678cce6affdf000ac16be0e20faa654d42d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669674"
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="6f09e-103">Running jobs on Azure Batch with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6f09e-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="6f09e-104">This script creates a Batch job and adds a series of tasks to the job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="6f09e-105">It also demonstrates how to monitor a job and its tasks.</span><span class="sxs-lookup"><span data-stu-id="6f09e-105">It also demonstrates how to monitor a job and its tasks.</span></span>
<span data-ttu-id="6f09e-106">Running this script assumes that a Batch account has already been set up, and both a pool and an application have been configured.</span><span class="sxs-lookup"><span data-stu-id="6f09e-106">Running this script assumes that a Batch account has already been set up, and both a pool and an application have been configured.</span></span> <span data-ttu-id="6f09e-107">For more information, please see the [sample scripts](../batch-cli-samples.md) covering each of these topics.</span><span class="sxs-lookup"><span data-stu-id="6f09e-107">For more information, please see the [sample scripts](../batch-cli-samples.md) covering each of these topics.</span></span>

<span data-ttu-id="6f09e-108">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span><span class="sxs-lookup"><span data-stu-id="6f09e-108">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6f09e-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="6f09e-109">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="6f09e-110">Clean up job</span><span class="sxs-lookup"><span data-stu-id="6f09e-110">Clean up job</span></span>

<span data-ttu-id="6f09e-111">After you run the above sample script, run the following command to remove the job and all of its tasks.</span><span class="sxs-lookup"><span data-stu-id="6f09e-111">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="6f09e-112">Note that the pool will need to be deleted separately; please see the [tutorial on managing pools](./batch-cli-sample-manage-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6f09e-112">Note that the pool will need to be deleted separately; please see the [tutorial on managing pools](./batch-cli-sample-manage-pool.md).</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="6f09e-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6f09e-113">Script explanation</span></span>

<span data-ttu-id="6f09e-114">This script uses the following commands to create a Batch job and tasks.</span><span class="sxs-lookup"><span data-stu-id="6f09e-114">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="6f09e-115">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6f09e-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="6f09e-116">Command</span><span class="sxs-lookup"><span data-stu-id="6f09e-116">Command</span></span> | <span data-ttu-id="6f09e-117">Notes</span><span class="sxs-lookup"><span data-stu-id="6f09e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6f09e-118">az batch account login</span><span class="sxs-lookup"><span data-stu-id="6f09e-118">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="6f09e-119">Authenticate against a Batch account.</span><span class="sxs-lookup"><span data-stu-id="6f09e-119">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="6f09e-120">az batch job create</span><span class="sxs-lookup"><span data-stu-id="6f09e-120">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="6f09e-121">Creates a Batch job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-121">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="6f09e-122">az batch job set</span><span class="sxs-lookup"><span data-stu-id="6f09e-122">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="6f09e-123">Updates properties of a Batch job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-123">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="6f09e-124">az batch job show</span><span class="sxs-lookup"><span data-stu-id="6f09e-124">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="6f09e-125">Retrieves details of a specified Batch job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-125">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="6f09e-126">az batch task create</span><span class="sxs-lookup"><span data-stu-id="6f09e-126">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="6f09e-127">Adds a task to the specified Batch job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-127">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="6f09e-128">az batch task show</span><span class="sxs-lookup"><span data-stu-id="6f09e-128">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="6f09e-129">Retrieves the details of a task from the specified Batch job.</span><span class="sxs-lookup"><span data-stu-id="6f09e-129">Retrieves the details of a task from the specified Batch job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="6f09e-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f09e-130">Next steps</span></span>

<span data-ttu-id="6f09e-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f09e-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6f09e-132">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f09e-132">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
