---
title: Azure Machine Learning deployment troubleshooting guide | Microsoft Docs
description: Troubleshooting guide for deployment and service creation
services: machine-learning
author: aashishb
ms.author: aashishb
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 11/16/2017
ms.openlocfilehash: 4cf86466d5fca4f5095c67a8400643bff29bb56c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868964"
---
# <a name="troubleshooting-service-deployment-and-environment-setup"></a><span data-ttu-id="c9bea-103">Troubleshooting service deployment and environment setup</span><span class="sxs-lookup"><span data-stu-id="c9bea-103">Troubleshooting service deployment and environment setup</span></span>
<span data-ttu-id="c9bea-104">The following information can help determine the cause of errors when setting up the model management environment.</span><span class="sxs-lookup"><span data-stu-id="c9bea-104">The following information can help determine the cause of errors when setting up the model management environment.</span></span>

## <a name="model-management-environment"></a><span data-ttu-id="c9bea-105">Model management environment</span><span class="sxs-lookup"><span data-stu-id="c9bea-105">Model management environment</span></span>
### <a name="contributor-permission-required"></a><span data-ttu-id="c9bea-106">Contributor permission required</span><span class="sxs-lookup"><span data-stu-id="c9bea-106">Contributor permission required</span></span>
<span data-ttu-id="c9bea-107">You need contributor access to the subscription or the resource group to set up a cluster for deployment of your web services.</span><span class="sxs-lookup"><span data-stu-id="c9bea-107">You need contributor access to the subscription or the resource group to set up a cluster for deployment of your web services.</span></span>

### <a name="resource-availability"></a><span data-ttu-id="c9bea-108">Resource availability</span><span class="sxs-lookup"><span data-stu-id="c9bea-108">Resource availability</span></span>
<span data-ttu-id="c9bea-109">You need to have enough resources available in your subscription so you can provision the environment resources.</span><span class="sxs-lookup"><span data-stu-id="c9bea-109">You need to have enough resources available in your subscription so you can provision the environment resources.</span></span>

### <a name="subscription-caps"></a><span data-ttu-id="c9bea-110">Subscription Caps</span><span class="sxs-lookup"><span data-stu-id="c9bea-110">Subscription Caps</span></span>
<span data-ttu-id="c9bea-111">Your subscription may have a cap on billing which could prevent you from provisioning the environment resources.</span><span class="sxs-lookup"><span data-stu-id="c9bea-111">Your subscription may have a cap on billing which could prevent you from provisioning the environment resources.</span></span> <span data-ttu-id="c9bea-112">Remove that cap to enable provisioning.</span><span class="sxs-lookup"><span data-stu-id="c9bea-112">Remove that cap to enable provisioning.</span></span>

### <a name="enable-debug-and-verbose-options"></a><span data-ttu-id="c9bea-113">Enable debug and verbose options</span><span class="sxs-lookup"><span data-stu-id="c9bea-113">Enable debug and verbose options</span></span>
<span data-ttu-id="c9bea-114">Use the `--debug` and  `--verbose` flags in the setup command to show debug and trace information as the environment is being provisioned.</span><span class="sxs-lookup"><span data-stu-id="c9bea-114">Use the `--debug` and  `--verbose` flags in the setup command to show debug and trace information as the environment is being provisioned.</span></span>

```
az ml env setup -l <location> -n <name> -c --debug --verbose 
```

## <a name="service-deployment"></a><span data-ttu-id="c9bea-115">Service deployment</span><span class="sxs-lookup"><span data-stu-id="c9bea-115">Service deployment</span></span>
<span data-ttu-id="c9bea-116">The following information can help determine the cause of errors during deployment or when calling the web service.</span><span class="sxs-lookup"><span data-stu-id="c9bea-116">The following information can help determine the cause of errors during deployment or when calling the web service.</span></span>

### <a name="service-logs"></a><span data-ttu-id="c9bea-117">Service logs</span><span class="sxs-lookup"><span data-stu-id="c9bea-117">Service logs</span></span>
<span data-ttu-id="c9bea-118">The `logs` option of the service CLI provides log data from Docker and Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c9bea-118">The `logs` option of the service CLI provides log data from Docker and Kubernetes.</span></span>

```
az ml service logs realtime -i <web service id>
```

<span data-ttu-id="c9bea-119">For additional log settings, use the `--help` (or `-h`) option.</span><span class="sxs-lookup"><span data-stu-id="c9bea-119">For additional log settings, use the `--help` (or `-h`) option.</span></span>

```
az ml service logs realtime -h
```

### <a name="debug-and-verbose-options"></a><span data-ttu-id="c9bea-120">Debug and Verbose options</span><span class="sxs-lookup"><span data-stu-id="c9bea-120">Debug and Verbose options</span></span>
<span data-ttu-id="c9bea-121">Use the `--debug` flag to show debug logs as the service is being deployed.</span><span class="sxs-lookup"><span data-stu-id="c9bea-121">Use the `--debug` flag to show debug logs as the service is being deployed.</span></span>

```
az ml service create realtime -m <modelfile>.pkl -f score.py -n <service name> -r python --debug
```

<span data-ttu-id="c9bea-122">Use the `--verbose` flag to see additional details as the service is being deployed.</span><span class="sxs-lookup"><span data-stu-id="c9bea-122">Use the `--verbose` flag to see additional details as the service is being deployed.</span></span>

```
az ml service create realtime -m <modelfile>.pkl -f score.py -n <service name> -r python --verbose
```

### <a name="enable-request-logging-in-app-insights"></a><span data-ttu-id="c9bea-123">Enable request logging in App Insights</span><span class="sxs-lookup"><span data-stu-id="c9bea-123">Enable request logging in App Insights</span></span>
<span data-ttu-id="c9bea-124">Set the `-l` flag to true when creating a web service to enable request level logging.</span><span class="sxs-lookup"><span data-stu-id="c9bea-124">Set the `-l` flag to true when creating a web service to enable request level logging.</span></span> <span data-ttu-id="c9bea-125">The request logs are written to the App Insights instance for your environment in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9bea-125">The request logs are written to the App Insights instance for your environment in Azure.</span></span> <span data-ttu-id="c9bea-126">Search for this instance using the environment name you used when using the `az ml env setup` command.</span><span class="sxs-lookup"><span data-stu-id="c9bea-126">Search for this instance using the environment name you used when using the `az ml env setup` command.</span></span>

- <span data-ttu-id="c9bea-127">Set `-l` to true when creating the service.</span><span class="sxs-lookup"><span data-stu-id="c9bea-127">Set `-l` to true when creating the service.</span></span>
- <span data-ttu-id="c9bea-128">Open App Insights in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c9bea-128">Open App Insights in Azure portal.</span></span> <span data-ttu-id="c9bea-129">Use your environment name to find the App Insights instance.</span><span class="sxs-lookup"><span data-stu-id="c9bea-129">Use your environment name to find the App Insights instance.</span></span>
- <span data-ttu-id="c9bea-130">Once in App Insights, click on Search in the top menu to view the results.</span><span class="sxs-lookup"><span data-stu-id="c9bea-130">Once in App Insights, click on Search in the top menu to view the results.</span></span>
- <span data-ttu-id="c9bea-131">Or go to `Analytics` > `Exceptions` > `exceptions take | 10`.</span><span class="sxs-lookup"><span data-stu-id="c9bea-131">Or go to `Analytics` > `Exceptions` > `exceptions take | 10`.</span></span>


### <a name="add-error-handling-in-scoring-script"></a><span data-ttu-id="c9bea-132">Add error handling in scoring script</span><span class="sxs-lookup"><span data-stu-id="c9bea-132">Add error handling in scoring script</span></span>
<span data-ttu-id="c9bea-133">Use exception handling in your `scoring.py` script's **run** function to return the error message as part of your web service output.</span><span class="sxs-lookup"><span data-stu-id="c9bea-133">Use exception handling in your `scoring.py` script's **run** function to return the error message as part of your web service output.</span></span>

<span data-ttu-id="c9bea-134">Python example:</span><span class="sxs-lookup"><span data-stu-id="c9bea-134">Python example:</span></span>
```
    try:
        <code to load model and score>
   except Exception as e:
        return(str(e))
```

## <a name="other-common-problems"></a><span data-ttu-id="c9bea-135">Other common problems</span><span class="sxs-lookup"><span data-stu-id="c9bea-135">Other common problems</span></span>
- <span data-ttu-id="c9bea-136">If pip install of azure-cli-ml fails with the error `cannot find the path specified` on a Windows machine, you need to enable long path support.</span><span class="sxs-lookup"><span data-stu-id="c9bea-136">If pip install of azure-cli-ml fails with the error `cannot find the path specified` on a Windows machine, you need to enable long path support.</span></span> <span data-ttu-id="c9bea-137">See https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/.</span><span class="sxs-lookup"><span data-stu-id="c9bea-137">See https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/.</span></span> 
- <span data-ttu-id="c9bea-138">If the `env setup` command fails with `LocationNotAvailableForResourceType`, you are probably using the wrong location (region) for the machine learning resources.</span><span class="sxs-lookup"><span data-stu-id="c9bea-138">If the `env setup` command fails with `LocationNotAvailableForResourceType`, you are probably using the wrong location (region) for the machine learning resources.</span></span> <span data-ttu-id="c9bea-139">Make sure your location specified with the `-l` parameter is `eastus2`, `westcentralus`, or `australiaeast`.</span><span class="sxs-lookup"><span data-stu-id="c9bea-139">Make sure your location specified with the `-l` parameter is `eastus2`, `westcentralus`, or `australiaeast`.</span></span>
- <span data-ttu-id="c9bea-140">If the `env setup` command fails with `Resource quota limit exceeded`, make sure you have enough cores available in your subscription and that your resources are not being used up in other processes.</span><span class="sxs-lookup"><span data-stu-id="c9bea-140">If the `env setup` command fails with `Resource quota limit exceeded`, make sure you have enough cores available in your subscription and that your resources are not being used up in other processes.</span></span>
- <span data-ttu-id="c9bea-141">If the `env setup` command fails with `Invalid environment name. Name must only contain lowercase alphanumeric characters`, make sure the service name does not contain upper-case letters, symbols, or the underscore ( _ ) (as in *my_environment*).</span><span class="sxs-lookup"><span data-stu-id="c9bea-141">If the `env setup` command fails with `Invalid environment name. Name must only contain lowercase alphanumeric characters`, make sure the service name does not contain upper-case letters, symbols, or the underscore ( _ ) (as in *my_environment*).</span></span>
- <span data-ttu-id="c9bea-142">If the `service create` command fails with `Service Name: [service_name] is invalid. The name of a service must consist of lower case alphanumeric characters (etc.)`, make sure the service name is between 3 and 32 characters in length; starts and ends with lower-case alphanumeric characters; and does not contain upper-case letters, symbols other than hyphen ( - ) and period ( .</span><span class="sxs-lookup"><span data-stu-id="c9bea-142">If the `service create` command fails with `Service Name: [service_name] is invalid. The name of a service must consist of lower case alphanumeric characters (etc.)`, make sure the service name is between 3 and 32 characters in length; starts and ends with lower-case alphanumeric characters; and does not contain upper-case letters, symbols other than hyphen ( - ) and period ( .</span></span> <span data-ttu-id="c9bea-143">), or the underscore ( _ ) (as in *my_webservice*).</span><span class="sxs-lookup"><span data-stu-id="c9bea-143">), or the underscore ( _ ) (as in *my_webservice*).</span></span>
- <span data-ttu-id="c9bea-144">Retry if you get a `502 Bad Gateway` error when calling the web service.</span><span class="sxs-lookup"><span data-stu-id="c9bea-144">Retry if you get a `502 Bad Gateway` error when calling the web service.</span></span> <span data-ttu-id="c9bea-145">It normally means the container hasn't been deployed to the cluster yet.</span><span class="sxs-lookup"><span data-stu-id="c9bea-145">It normally means the container hasn't been deployed to the cluster yet.</span></span>
- <span data-ttu-id="c9bea-146">If you get `CrashLoopBackOff` error when creating a service, check your logs.</span><span class="sxs-lookup"><span data-stu-id="c9bea-146">If you get `CrashLoopBackOff` error when creating a service, check your logs.</span></span> <span data-ttu-id="c9bea-147">It typically is the result of missing dependencies in the **init** function.</span><span class="sxs-lookup"><span data-stu-id="c9bea-147">It typically is the result of missing dependencies in the **init** function.</span></span>
