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
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Running jobs on Azure Batch with Azure CLI

This script creates a Batch job and adds a series of tasks to the job. It also demonstrates how to monitor a job and its tasks.
Running this script assumes that a Batch account has already been set up, and both a pool and an application have been configured. For more information, please see the [sample scripts](../batch-cli-samples.md) covering each of these topics.

If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Clean up job

After you run the above sample script, run the following command to remove the job and all of its tasks. Note that the pool will need to be deleted separately; please see the [tutorial on managing pools](./batch-cli-sample-manage-pool.md).

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create a Batch job and tasks. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Authenticate against a Batch account.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Creates a Batch job.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Updates properties of a Batch job.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Retrieves details of a specified Batch job.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Adds a task to the specified Batch job.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Retrieves the details of a task from the specified Batch job.  |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).
