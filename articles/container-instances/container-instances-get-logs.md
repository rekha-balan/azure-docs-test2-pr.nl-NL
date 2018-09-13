---
title: Get container logs and events with Azure Container Instances
description: Learn how to debug with container logs and events with Azure Container Instances
services: container-instances
author: jluk
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 05/30/18
ms.author: juluk
ms.custom: mvc
ms.openlocfilehash: 4c8197e570c429893084fc1c2f8e4b36fd43a721
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868326"
---
# <a name="retrieve-container-logs-and-events-in-azure-container-instances"></a><span data-ttu-id="b5c01-103">Retrieve container logs and events in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b5c01-103">Retrieve container logs and events in Azure Container Instances</span></span>

<span data-ttu-id="b5c01-104">When you have a misbehaving container, start by viewing its logs with [az container logs][az-container-logs], and streaming its standard out and standard error with [az container attach][az-container-attach].</span><span class="sxs-lookup"><span data-stu-id="b5c01-104">When you have a misbehaving container, start by viewing its logs with [az container logs][az-container-logs], and streaming its standard out and standard error with [az container attach][az-container-attach].</span></span>

## <a name="view-logs"></a><span data-ttu-id="b5c01-105">View logs</span><span class="sxs-lookup"><span data-stu-id="b5c01-105">View logs</span></span>

<span data-ttu-id="b5c01-106">To view logs from your application code within a container, you can use the [az container logs][az-container-logs] command.</span><span class="sxs-lookup"><span data-stu-id="b5c01-106">To view logs from your application code within a container, you can use the [az container logs][az-container-logs] command.</span></span>

<span data-ttu-id="b5c01-107">The following is log output from the example task-based container in [Run a containerized task in ACI](container-instances-restart-policy.md), after having fed it an invalid URL to process:</span><span class="sxs-lookup"><span data-stu-id="b5c01-107">The following is log output from the example task-based container in [Run a containerized task in ACI](container-instances-restart-policy.md), after having fed it an invalid URL to process:</span></span>

```console
$ az container logs --resource-group myResourceGroup --name mycontainer
Traceback (most recent call last):
  File "wordcount.py", line 11, in <module>
    urllib.request.urlretrieve (sys.argv[1], "foo.txt")
  File "/usr/local/lib/python3.6/urllib/request.py", line 248, in urlretrieve
    with contextlib.closing(urlopen(url, data)) as fp:
  File "/usr/local/lib/python3.6/urllib/request.py", line 223, in urlopen
    return opener.open(url, data, timeout)
  File "/usr/local/lib/python3.6/urllib/request.py", line 532, in open
    response = meth(req, response)
  File "/usr/local/lib/python3.6/urllib/request.py", line 642, in http_response
    'http', request, response, code, msg, hdrs)
  File "/usr/local/lib/python3.6/urllib/request.py", line 570, in error
    return self._call_chain(*args)
  File "/usr/local/lib/python3.6/urllib/request.py", line 504, in _call_chain
    result = func(*args)
  File "/usr/local/lib/python3.6/urllib/request.py", line 650, in http_error_default
    raise HTTPError(req.full_url, code, msg, hdrs, fp)
urllib.error.HTTPError: HTTP Error 404: Not Found
```

## <a name="attach-output-streams"></a><span data-ttu-id="b5c01-108">Attach output streams</span><span class="sxs-lookup"><span data-stu-id="b5c01-108">Attach output streams</span></span>

<span data-ttu-id="b5c01-109">The [az container attach][az-container-attach] command provides diagnostic information during container startup.</span><span class="sxs-lookup"><span data-stu-id="b5c01-109">The [az container attach][az-container-attach] command provides diagnostic information during container startup.</span></span> <span data-ttu-id="b5c01-110">Once the container has started, it streams STDOUT and STDERR to your local console.</span><span class="sxs-lookup"><span data-stu-id="b5c01-110">Once the container has started, it streams STDOUT and STDERR to your local console.</span></span>

<span data-ttu-id="b5c01-111">For example, here is output from the task-based container in [Run a containerized task in ACI](container-instances-restart-policy.md), after having supplied a valid URL of a large text file to process:</span><span class="sxs-lookup"><span data-stu-id="b5c01-111">For example, here is output from the task-based container in [Run a containerized task in ACI](container-instances-restart-policy.md), after having supplied a valid URL of a large text file to process:</span></span>

```console
$ az container attach --resource-group myResourceGroup --name mycontainer
Container 'mycontainer' is in state 'Unknown'...
Container 'mycontainer' is in state 'Waiting'...
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-03-09 23:21:33+00:00) pulling image "microsoft/aci-wordcount:latest"
(count: 1) (last timestamp: 2018-03-09 23:21:49+00:00) Successfully pulled image "microsoft/aci-wordcount:latest"
(count: 1) (last timestamp: 2018-03-09 23:21:49+00:00) Created container with id e495ad3e411f0570e1fd37c1e73b0e0962f185aa8a7c982ebd410ad63d238618
(count: 1) (last timestamp: 2018-03-09 23:21:49+00:00) Started container with id e495ad3e411f0570e1fd37c1e73b0e0962f185aa8a7c982ebd410ad63d238618

Start streaming logs:
[('the', 22979),
 ('I', 20003),
 ('and', 18373),
 ('to', 15651),
 ('of', 15558),
 ('a', 12500),
 ('you', 11818),
 ('my', 10651),
 ('in', 9707),
 ('is', 8195)]
```

## <a name="get-diagnostic-events"></a><span data-ttu-id="b5c01-112">Get diagnostic events</span><span class="sxs-lookup"><span data-stu-id="b5c01-112">Get diagnostic events</span></span>

<span data-ttu-id="b5c01-113">If your container fails to deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span><span class="sxs-lookup"><span data-stu-id="b5c01-113">If your container fails to deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="b5c01-114">To view the events for your container, run the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="b5c01-114">To view the events for your container, run the [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="b5c01-115">The output includes the core properties of your container, along with deployment events (shown here truncated):</span><span class="sxs-lookup"><span data-stu-id="b5c01-115">The output includes the core properties of your container, along with deployment events (shown here truncated):</span></span>

```JSON
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...
        "events": [
          {
            "count": 1,
            "firstTimestamp": "2017-12-21T22:50:49+00:00",
            "lastTimestamp": "2017-12-21T22:50:49+00:00",
            "message": "pulling image \"microsoft/aci-helloworld\"",
            "name": "Pulling",
            "type": "Normal"
          },
          {
            "count": 1,
            "firstTimestamp": "2017-12-21T22:50:59+00:00",
            "lastTimestamp": "2017-12-21T22:50:59+00:00",
            "message": "Successfully pulled image \"microsoft/aci-helloworld\"",
            "name": "Pulled",
            "type": "Normal"
          },
          {
            "count": 1,
            "firstTimestamp": "2017-12-21T22:50:59+00:00",
            "lastTimestamp": "2017-12-21T22:50:59+00:00",
            "message": "Created container with id 2677c7fd54478e5adf6f07e48fb71357d9d18bccebd4a91486113da7b863f91f",
            "name": "Created",
            "type": "Normal"
          },
          {
            "count": 1,
            "firstTimestamp": "2017-12-21T22:50:59+00:00",
            "lastTimestamp": "2017-12-21T22:50:59+00:00",
            "message": "Started container with id 2677c7fd54478e5adf6f07e48fb71357d9d18bccebd4a91486113da7b863f91f",
            "name": "Started",
            "type": "Normal"
          }
        ],
        "previousState": null,
        "restartCount": 0
      },
      "name": "mycontainer",
      "ports": [
        {
          "port": 80,
          "protocol": null
        }
      ],
      ...
    }
  ],
  ...
}
```
## <a name="next-steps"></a><span data-ttu-id="b5c01-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5c01-116">Next steps</span></span>
<span data-ttu-id="b5c01-117">Learn how to [troubleshoot common container and deployment issues](container-instances-troubleshooting.md) for Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="b5c01-117">Learn how to [troubleshoot common container and deployment issues](container-instances-troubleshooting.md) for Azure Container Instances.</span></span>

<!-- LINKS - Internal -->
[az-container-attach]: /cli/azure/container#az-container-attach
[az-container-logs]: /cli/azure/container#az-container-logs