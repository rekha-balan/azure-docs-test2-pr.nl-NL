---
title: Azure ML Logging API reference | Microsoft Docs
description: Logging API reference.
services: machine-learning
author: akshaya-a
ms.author: akannava
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/25/2017
ms.openlocfilehash: 101c47f4916ca3fab56800eaf012c55150769302
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870505"
---
# <a name="logging-api-reference"></a><span data-ttu-id="901a4-103">Logging API reference</span><span class="sxs-lookup"><span data-stu-id="901a4-103">Logging API reference</span></span>

<span data-ttu-id="901a4-104">Azure ML's logging library allows the program to emit metrics and files that are tracked by the history service for later analysis.</span><span class="sxs-lookup"><span data-stu-id="901a4-104">Azure ML's logging library allows the program to emit metrics and files that are tracked by the history service for later analysis.</span></span> <span data-ttu-id="901a4-105">Currently, a few basic types of metrics and files are supported, and the set of supported types will grow with future releases of the Python package.</span><span class="sxs-lookup"><span data-stu-id="901a4-105">Currently, a few basic types of metrics and files are supported, and the set of supported types will grow with future releases of the Python package.</span></span>

## <a name="uploading-metrics"></a><span data-ttu-id="901a4-106">Uploading metrics</span><span class="sxs-lookup"><span data-stu-id="901a4-106">Uploading metrics</span></span>

```python
# import logging API package
from azureml.logging import get_azureml_logger

# initialize a logger object
logger = get_azureml_logger()

# log "scalar" metrics
logger.log("simple integer value", 7)
logger.log("simple float value", 3.141592)
logger.log("simple string value", "this is a string metric")

# log a list of numerical values. 
# this automatically creates a chart in the Run History details page
logger.log("chart data points", [1, 3, 5, 10, 6, 4])
```

<span data-ttu-id="901a4-107">By default, all metrics are submitted asynchronously so that the submission doesn't impede program execution.</span><span class="sxs-lookup"><span data-stu-id="901a4-107">By default, all metrics are submitted asynchronously so that the submission doesn't impede program execution.</span></span> <span data-ttu-id="901a4-108">This can cause ordering issues when multiple metrics are sent in edge cases.</span><span class="sxs-lookup"><span data-stu-id="901a4-108">This can cause ordering issues when multiple metrics are sent in edge cases.</span></span> <span data-ttu-id="901a4-109">An example of this would be two metrics logged at the same time, but for some reason the user would prefer their exact ordering be preserved.</span><span class="sxs-lookup"><span data-stu-id="901a4-109">An example of this would be two metrics logged at the same time, but for some reason the user would prefer their exact ordering be preserved.</span></span> <span data-ttu-id="901a4-110">Another case is when the metric must be tracked before running some code that is known to potentially fail fast.</span><span class="sxs-lookup"><span data-stu-id="901a4-110">Another case is when the metric must be tracked before running some code that is known to potentially fail fast.</span></span> <span data-ttu-id="901a4-111">In both cases, the solution is to _wait_ until the metric is fully logged before proceeding:</span><span class="sxs-lookup"><span data-stu-id="901a4-111">In both cases, the solution is to _wait_ until the metric is fully logged before proceeding:</span></span>

```python
# blocking call
logger.log("my metric 1", 1).wait()
logger.log("my metric 2", 2).wait()
```

## <a name="consuming-metrics"></a><span data-ttu-id="901a4-112">Consuming metrics</span><span class="sxs-lookup"><span data-stu-id="901a4-112">Consuming metrics</span></span>

<span data-ttu-id="901a4-113">The metrics are stored by the history service and tied to the Run that produced them.</span><span class="sxs-lookup"><span data-stu-id="901a4-113">The metrics are stored by the history service and tied to the Run that produced them.</span></span> <span data-ttu-id="901a4-114">Both the Run History tab and CLI command below allow you to retrieve them (and artifacts below) after a run has completed.</span><span class="sxs-lookup"><span data-stu-id="901a4-114">Both the Run History tab and CLI command below allow you to retrieve them (and artifacts below) after a run has completed.</span></span>

```azurecli
# show the last run
$ az ml history last

# list all past runs
$ az ml history list 

# show a paritcular run
$ az ml history info -r <runid>
```

## <a name="artifacts-files"></a><span data-ttu-id="901a4-115">Artifacts (files)</span><span class="sxs-lookup"><span data-stu-id="901a4-115">Artifacts (files)</span></span>

<span data-ttu-id="901a4-116">In addition to metrics, AzureML allows the user to track files as well.</span><span class="sxs-lookup"><span data-stu-id="901a4-116">In addition to metrics, AzureML allows the user to track files as well.</span></span> <span data-ttu-id="901a4-117">By default, all files written into the `outputs` folder relative to the program's working directory (the project folder in the compute context) are uploaded to the history service and tracked for later analysis.</span><span class="sxs-lookup"><span data-stu-id="901a4-117">By default, all files written into the `outputs` folder relative to the program's working directory (the project folder in the compute context) are uploaded to the history service and tracked for later analysis.</span></span> <span data-ttu-id="901a4-118">The caveat is that the individual file size must be smaller than 512 MB.</span><span class="sxs-lookup"><span data-stu-id="901a4-118">The caveat is that the individual file size must be smaller than 512 MB.</span></span>


```Python
# Log content as an artifact
logger.upload("artifact/path", "This should be the contents of artifact/path in the service")
```

## <a name="consuming-artifacts"></a><span data-ttu-id="901a4-119">Consuming artifacts</span><span class="sxs-lookup"><span data-stu-id="901a4-119">Consuming artifacts</span></span>

<span data-ttu-id="901a4-120">To print the contents of an artifact that has been tracked, user can use the Run History tab for the given run to **Download** or **Promote** the Artifact, or use the below CLI commands to achieve the same effect.</span><span class="sxs-lookup"><span data-stu-id="901a4-120">To print the contents of an artifact that has been tracked, user can use the Run History tab for the given run to **Download** or **Promote** the Artifact, or use the below CLI commands to achieve the same effect.</span></span>

```azurecli
# show all artifacts generated by a run
$ az ml history info -r <runid> -a <artifact/path>

# promote a particular artifact
$ az ml history promote -r <runid> -ap <artifact/prefix> -n <name of asset to create>
```
## <a name="next-steps"></a><span data-ttu-id="901a4-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="901a4-121">Next steps</span></span>
- <span data-ttu-id="901a4-122">Walk through the [Classifying iris tutoria, part 2](tutorial-classifying-iris-part-2.md) to see logging API in action.</span><span class="sxs-lookup"><span data-stu-id="901a4-122">Walk through the [Classifying iris tutoria, part 2](tutorial-classifying-iris-part-2.md) to see logging API in action.</span></span>
- <span data-ttu-id="901a4-123">Review [How to Use Run History and Model Metrics in Azure Machine Learning Workbench](how-to-use-run-history-model-metrics.md) to understand deeper how logging APIs can be used in Run History.</span><span class="sxs-lookup"><span data-stu-id="901a4-123">Review [How to Use Run History and Model Metrics in Azure Machine Learning Workbench](how-to-use-run-history-model-metrics.md) to understand deeper how logging APIs can be used in Run History.</span></span>
