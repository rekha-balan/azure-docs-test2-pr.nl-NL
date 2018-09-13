---
title: Find runs with the best accuracy and lowest duration in Azure Machine Learning Workbench | Microsoft Docs
description: An end-to-end use case to find best accuracy through CLI by using Azure Machine Learning Workbench
services: machine-learning
author: totekp
ms.author: kefzhou
manager: akannava
ms.reviewer: akannava, haining, mldocs, jmartens, jasonwhowell
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/29/2017
ms.openlocfilehash: 14925aa9171edac4a9ff976f2200f6dfc0ba0dae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871216"
---
# <a name="find-runs-with-the-best-accuracy-and-lowest-duration"></a><span data-ttu-id="ef018-103">Find runs with the best accuracy and lowest duration</span><span class="sxs-lookup"><span data-stu-id="ef018-103">Find runs with the best accuracy and lowest duration</span></span>
<span data-ttu-id="ef018-104">Given multiple runs, one use case is to find runs with the best accuracy.</span><span class="sxs-lookup"><span data-stu-id="ef018-104">Given multiple runs, one use case is to find runs with the best accuracy.</span></span> <span data-ttu-id="ef018-105">One approach is to use the command-line interface (CLI) with a [JMESPath](http://jmespath.org/) query.</span><span class="sxs-lookup"><span data-stu-id="ef018-105">One approach is to use the command-line interface (CLI) with a [JMESPath](http://jmespath.org/) query.</span></span> <span data-ttu-id="ef018-106">For more information on how to use JMESPath in the Azure CLI, see [Use JMESPath queries with Azure CLI](https://docs.microsoft.com/cli/azure/query-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="ef018-106">For more information on how to use JMESPath in the Azure CLI, see [Use JMESPath queries with Azure CLI](https://docs.microsoft.com/cli/azure/query-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="ef018-107">In the following example, four runs are created with accuracy values of 0, 0.98, 1, and 1.</span><span class="sxs-lookup"><span data-stu-id="ef018-107">In the following example, four runs are created with accuracy values of 0, 0.98, 1, and 1.</span></span> <span data-ttu-id="ef018-108">Runs are filtered if they are in the range `[MaxAccuracy-Threshold, MaxAccuracy]` where `Threshold = .03`.</span><span class="sxs-lookup"><span data-stu-id="ef018-108">Runs are filtered if they are in the range `[MaxAccuracy-Threshold, MaxAccuracy]` where `Threshold = .03`.</span></span>

## <a name="sample-data"></a><span data-ttu-id="ef018-109">Sample data</span><span class="sxs-lookup"><span data-stu-id="ef018-109">Sample data</span></span>
<span data-ttu-id="ef018-110">If you don't have existing runs with an `Accuracy` value, the following steps generate runs for querying.</span><span class="sxs-lookup"><span data-stu-id="ef018-110">If you don't have existing runs with an `Accuracy` value, the following steps generate runs for querying.</span></span>

<span data-ttu-id="ef018-111">First, create a Python file in the Azure Machine Learning Workbench, name it `log_accuracy.py`, and paste in the following code:</span><span class="sxs-lookup"><span data-stu-id="ef018-111">First, create a Python file in the Azure Machine Learning Workbench, name it `log_accuracy.py`, and paste in the following code:</span></span>
```python
from azureml.logging import get_azureml_logger

logger = get_azureml_logger()

accuracy_value = 0.5

if len(sys.argv) > 1:
     accuracy_value = float(sys.argv[1])

logger.log("Accuracy", accuracy_value)
```

<span data-ttu-id="ef018-112">Next, create a file `run.py`, and paste in the following code:</span><span class="sxs-lookup"><span data-stu-id="ef018-112">Next, create a file `run.py`, and paste in the following code:</span></span>
```python
import os

accuracy_values = [0, 0.98, 1.0, 1.0]
for value in accuracy_values:
    os.system('az ml experiment submit -c local ./log_accuracy.py {}'.format(value))
```

<span data-ttu-id="ef018-113">Lastly, open the CLI through Workbench and run the command `python run.py` to submit four experiments.</span><span class="sxs-lookup"><span data-stu-id="ef018-113">Lastly, open the CLI through Workbench and run the command `python run.py` to submit four experiments.</span></span> <span data-ttu-id="ef018-114">After the script finishes, you should see four more runs in the `Run History` tab.</span><span class="sxs-lookup"><span data-stu-id="ef018-114">After the script finishes, you should see four more runs in the `Run History` tab.</span></span>

## <a name="query-the-run-history"></a><span data-ttu-id="ef018-115">Query the run history</span><span class="sxs-lookup"><span data-stu-id="ef018-115">Query the run history</span></span>
<span data-ttu-id="ef018-116">The first command finds the max accuracy value.</span><span class="sxs-lookup"><span data-stu-id="ef018-116">The first command finds the max accuracy value.</span></span>
```powershell
az ml history list --query '@[?Accuracy != null] | max_by(@, &Accuracy).Accuracy'
```

<span data-ttu-id="ef018-117">Using this max accuracy value of `1` and a threshold value of `0.03`, the second command filters runs by using `Accuracy` and then sorts runs by `duration` ascending.</span><span class="sxs-lookup"><span data-stu-id="ef018-117">Using this max accuracy value of `1` and a threshold value of `0.03`, the second command filters runs by using `Accuracy` and then sorts runs by `duration` ascending.</span></span>
```powershell
az ml history list --query '@[?Accuracy >= sum(`[1, -0.03]`)] | sort_by(@, &duration)'
```
> [!NOTE]
> <span data-ttu-id="ef018-118">If you want a strict upper-bound check, the query format is ``@[?Accuracy >= sum(`[$max_accuracy_value, -$threshold]`) && Accuracy <= `$max_accuracy_value`]``</span><span class="sxs-lookup"><span data-stu-id="ef018-118">If you want a strict upper-bound check, the query format is ``@[?Accuracy >= sum(`[$max_accuracy_value, -$threshold]`) && Accuracy <= `$max_accuracy_value`]``</span></span>

<span data-ttu-id="ef018-119">If you use PowerShell, the following code uses local variables to store threshold and max accuracy:</span><span class="sxs-lookup"><span data-stu-id="ef018-119">If you use PowerShell, the following code uses local variables to store threshold and max accuracy:</span></span>
```powershell
$threshold = 0.03
$max_accuracy_value = az ml history list --query '@[?Accuracy != null] | max_by(@, &Accuracy).Accuracy'
$find_runs_query = '@[?Accuracy >= sum(`[{0}, -{1}]`)] | sort_by(@, &duration)' -f $max_accuracy_value, $threshold
az ml history list --query $find_runs_query
```

## <a name="next-steps"></a><span data-ttu-id="ef018-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef018-120">Next steps</span></span>
<span data-ttu-id="ef018-121">For more information on logging, see [How to use run history and model metrics in Azure Machine Learning Workbench](how-to-use-run-history-model-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ef018-121">For more information on logging, see [How to use run history and model metrics in Azure Machine Learning Workbench](how-to-use-run-history-model-metrics.md).</span></span>    
