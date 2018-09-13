---
title: Troubleshooting Azure Container Instances
description: Learn how to troubleshoot issues with Azure Container Instances
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 07/19/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 6f57bc41cddc997a69f92ba4e8ca66faaeb29738
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966652"
---
# <a name="troubleshoot-common-issues-in-azure-container-instances"></a><span data-ttu-id="ef38e-103">Troubleshoot common issues in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="ef38e-103">Troubleshoot common issues in Azure Container Instances</span></span>

<span data-ttu-id="ef38e-104">This article shows how to troubleshoot common issues for managing or deploying containers to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="ef38e-104">This article shows how to troubleshoot common issues for managing or deploying containers to Azure Container Instances.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="ef38e-105">Naming conventions</span><span class="sxs-lookup"><span data-stu-id="ef38e-105">Naming conventions</span></span>

<span data-ttu-id="ef38e-106">When defining your container specification, certain parameters require adherence to naming restrictions.</span><span class="sxs-lookup"><span data-stu-id="ef38e-106">When defining your container specification, certain parameters require adherence to naming restrictions.</span></span> <span data-ttu-id="ef38e-107">Below is a table with specific requirements for container group properties.</span><span class="sxs-lookup"><span data-stu-id="ef38e-107">Below is a table with specific requirements for container group properties.</span></span> <span data-ttu-id="ef38e-108">For more information on Azure naming conventions, see [Naming conventions][azure-name-restrictions] in the Azure Architecture Center.</span><span class="sxs-lookup"><span data-stu-id="ef38e-108">For more information on Azure naming conventions, see [Naming conventions][azure-name-restrictions] in the Azure Architecture Center.</span></span>

| <span data-ttu-id="ef38e-109">Scope</span><span class="sxs-lookup"><span data-stu-id="ef38e-109">Scope</span></span> | <span data-ttu-id="ef38e-110">Length</span><span class="sxs-lookup"><span data-stu-id="ef38e-110">Length</span></span> | <span data-ttu-id="ef38e-111">Casing</span><span class="sxs-lookup"><span data-stu-id="ef38e-111">Casing</span></span> | <span data-ttu-id="ef38e-112">Valid characters</span><span class="sxs-lookup"><span data-stu-id="ef38e-112">Valid characters</span></span> | <span data-ttu-id="ef38e-113">Suggested pattern</span><span class="sxs-lookup"><span data-stu-id="ef38e-113">Suggested pattern</span></span> | <span data-ttu-id="ef38e-114">Example</span><span class="sxs-lookup"><span data-stu-id="ef38e-114">Example</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="ef38e-115">Container group name</span><span class="sxs-lookup"><span data-stu-id="ef38e-115">Container group name</span></span> | <span data-ttu-id="ef38e-116">1-64</span><span class="sxs-lookup"><span data-stu-id="ef38e-116">1-64</span></span> |<span data-ttu-id="ef38e-117">Case insensitive</span><span class="sxs-lookup"><span data-stu-id="ef38e-117">Case insensitive</span></span> |<span data-ttu-id="ef38e-118">Alphanumeric, and hyphen anywhere except the first or last character</span><span class="sxs-lookup"><span data-stu-id="ef38e-118">Alphanumeric, and hyphen anywhere except the first or last character</span></span> |`<name>-<role>-CG<number>` |`web-batch-CG1` |
| <span data-ttu-id="ef38e-119">Container name</span><span class="sxs-lookup"><span data-stu-id="ef38e-119">Container name</span></span> | <span data-ttu-id="ef38e-120">1-64</span><span class="sxs-lookup"><span data-stu-id="ef38e-120">1-64</span></span> |<span data-ttu-id="ef38e-121">Case insensitive</span><span class="sxs-lookup"><span data-stu-id="ef38e-121">Case insensitive</span></span> |<span data-ttu-id="ef38e-122">Alphanumeric, and hyphen anywhere except the first or last character</span><span class="sxs-lookup"><span data-stu-id="ef38e-122">Alphanumeric, and hyphen anywhere except the first or last character</span></span> |`<name>-<role>-CG<number>` |`web-batch-CG1` |
| <span data-ttu-id="ef38e-123">Container ports</span><span class="sxs-lookup"><span data-stu-id="ef38e-123">Container ports</span></span> | <span data-ttu-id="ef38e-124">Between 1 and 65535</span><span class="sxs-lookup"><span data-stu-id="ef38e-124">Between 1 and 65535</span></span> |<span data-ttu-id="ef38e-125">Integer</span><span class="sxs-lookup"><span data-stu-id="ef38e-125">Integer</span></span> |<span data-ttu-id="ef38e-126">Integer between 1 and 65535</span><span class="sxs-lookup"><span data-stu-id="ef38e-126">Integer between 1 and 65535</span></span> |`<port-number>` |`443` |
| <span data-ttu-id="ef38e-127">DNS name label</span><span class="sxs-lookup"><span data-stu-id="ef38e-127">DNS name label</span></span> | <span data-ttu-id="ef38e-128">5-63</span><span class="sxs-lookup"><span data-stu-id="ef38e-128">5-63</span></span> |<span data-ttu-id="ef38e-129">Case insensitive</span><span class="sxs-lookup"><span data-stu-id="ef38e-129">Case insensitive</span></span> |<span data-ttu-id="ef38e-130">Alphanumeric, and hyphen anywhere except the first or last character</span><span class="sxs-lookup"><span data-stu-id="ef38e-130">Alphanumeric, and hyphen anywhere except the first or last character</span></span> |`<name>` |`frontend-site1` |
| <span data-ttu-id="ef38e-131">Environment variable</span><span class="sxs-lookup"><span data-stu-id="ef38e-131">Environment variable</span></span> | <span data-ttu-id="ef38e-132">1-63</span><span class="sxs-lookup"><span data-stu-id="ef38e-132">1-63</span></span> |<span data-ttu-id="ef38e-133">Case insensitive</span><span class="sxs-lookup"><span data-stu-id="ef38e-133">Case insensitive</span></span> |<span data-ttu-id="ef38e-134">Alphanumeric, and underscore (_) anywhere except the first or last character</span><span class="sxs-lookup"><span data-stu-id="ef38e-134">Alphanumeric, and underscore (_) anywhere except the first or last character</span></span> |`<name>` |`MY_VARIABLE` |
| <span data-ttu-id="ef38e-135">Volume name</span><span class="sxs-lookup"><span data-stu-id="ef38e-135">Volume name</span></span> | <span data-ttu-id="ef38e-136">5-63</span><span class="sxs-lookup"><span data-stu-id="ef38e-136">5-63</span></span> |<span data-ttu-id="ef38e-137">Case insensitive</span><span class="sxs-lookup"><span data-stu-id="ef38e-137">Case insensitive</span></span> |<span data-ttu-id="ef38e-138">Lowercase letters and numbers, and hyphens anywhere except the first or last character.</span><span class="sxs-lookup"><span data-stu-id="ef38e-138">Lowercase letters and numbers, and hyphens anywhere except the first or last character.</span></span> <span data-ttu-id="ef38e-139">Cannot contain two consecutive hyphens.</span><span class="sxs-lookup"><span data-stu-id="ef38e-139">Cannot contain two consecutive hyphens.</span></span> |`<name>` |`batch-output-volume` |

## <a name="os-version-of-image-not-supported"></a><span data-ttu-id="ef38e-140">OS version of image not supported</span><span class="sxs-lookup"><span data-stu-id="ef38e-140">OS version of image not supported</span></span>

<span data-ttu-id="ef38e-141">If you specify an image that Azure Container Instances doesn't support, an `OsVersionNotSupported` error is returned.</span><span class="sxs-lookup"><span data-stu-id="ef38e-141">If you specify an image that Azure Container Instances doesn't support, an `OsVersionNotSupported` error is returned.</span></span> <span data-ttu-id="ef38e-142">The error is similar to following, where `{0}` is the name of the image you attempted to deploy:</span><span class="sxs-lookup"><span data-stu-id="ef38e-142">The error is similar to following, where `{0}` is the name of the image you attempted to deploy:</span></span>

```json
{
  "error": {
    "code": "OsVersionNotSupported",
    "message": "The OS version of image '{0}' is not supported."
  }
}
```

<span data-ttu-id="ef38e-143">This error is most often encountered when deploying Windows images that are based on a Semi-Annual Channel (SAC) release.</span><span class="sxs-lookup"><span data-stu-id="ef38e-143">This error is most often encountered when deploying Windows images that are based on a Semi-Annual Channel (SAC) release.</span></span> <span data-ttu-id="ef38e-144">For example, Windows versions 1709 and 1803 are SAC releases, and generate this error upon deployment.</span><span class="sxs-lookup"><span data-stu-id="ef38e-144">For example, Windows versions 1709 and 1803 are SAC releases, and generate this error upon deployment.</span></span>

<span data-ttu-id="ef38e-145">Azure Container Instances supports Windows images based only on Long-Term Servicing Channel (LTSC) versions.</span><span class="sxs-lookup"><span data-stu-id="ef38e-145">Azure Container Instances supports Windows images based only on Long-Term Servicing Channel (LTSC) versions.</span></span> <span data-ttu-id="ef38e-146">To mitigate this issue when deploying Windows containers, always deploy LTSC-based images.</span><span class="sxs-lookup"><span data-stu-id="ef38e-146">To mitigate this issue when deploying Windows containers, always deploy LTSC-based images.</span></span>

<span data-ttu-id="ef38e-147">For details about the LTSC and SAC versions of Windows, see [Windows Server Semi-Annual Channel overview][windows-sac-overview].</span><span class="sxs-lookup"><span data-stu-id="ef38e-147">For details about the LTSC and SAC versions of Windows, see [Windows Server Semi-Annual Channel overview][windows-sac-overview].</span></span>

## <a name="unable-to-pull-image"></a><span data-ttu-id="ef38e-148">Unable to pull image</span><span class="sxs-lookup"><span data-stu-id="ef38e-148">Unable to pull image</span></span>

<span data-ttu-id="ef38e-149">If Azure Container Instances is initially unable to pull your image, it retries for a period of time.</span><span class="sxs-lookup"><span data-stu-id="ef38e-149">If Azure Container Instances is initially unable to pull your image, it retries for a period of time.</span></span> <span data-ttu-id="ef38e-150">If the image pull operation continues to fail, ACI eventually fails the deployment, and you may see a `Failed to pull image` error.</span><span class="sxs-lookup"><span data-stu-id="ef38e-150">If the image pull operation continues to fail, ACI eventually fails the deployment, and you may see a `Failed to pull image` error.</span></span>

<span data-ttu-id="ef38e-151">To resolve this issue, delete the container instance and retry your deployment.</span><span class="sxs-lookup"><span data-stu-id="ef38e-151">To resolve this issue, delete the container instance and retry your deployment.</span></span> <span data-ttu-id="ef38e-152">Ensure that the image exists in the registry, and that you've typed the image name correctly.</span><span class="sxs-lookup"><span data-stu-id="ef38e-152">Ensure that the image exists in the registry, and that you've typed the image name correctly.</span></span>

<span data-ttu-id="ef38e-153">If the image can't be pulled, events like the following are shown in the output of [az container show][az-container-show]:</span><span class="sxs-lookup"><span data-stu-id="ef38e-153">If the image can't be pulled, events like the following are shown in the output of [az container show][az-container-show]:</span></span>

```bash
"events": [
  {
    "count": 3,
    "firstTimestamp": "2017-12-21T22:56:19+00:00",
    "lastTimestamp": "2017-12-21T22:57:00+00:00",
    "message": "pulling image \"microsoft/aci-hellowrld\"",
    "name": "Pulling",
    "type": "Normal"
  },
  {
    "count": 3,
    "firstTimestamp": "2017-12-21T22:56:19+00:00",
    "lastTimestamp": "2017-12-21T22:57:00+00:00",
    "message": "Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image t/aci-hellowrld:latest not found",
    "name": "Failed",
    "type": "Warning"
  },
  {
    "count": 3,
    "firstTimestamp": "2017-12-21T22:56:20+00:00",
    "lastTimestamp": "2017-12-21T22:57:16+00:00",
    "message": "Back-off pulling image \"microsoft/aci-hellowrld\"",
    "name": "BackOff",
    "type": "Normal"
  }
],
```

## <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="ef38e-154">Container continually exits and restarts</span><span class="sxs-lookup"><span data-stu-id="ef38e-154">Container continually exits and restarts</span></span>

<span data-ttu-id="ef38e-155">If your container runs to completion and automatically restarts, you might need to set a [restart policy](container-instances-restart-policy.md) of **OnFailure** or **Never**.</span><span class="sxs-lookup"><span data-stu-id="ef38e-155">If your container runs to completion and automatically restarts, you might need to set a [restart policy](container-instances-restart-policy.md) of **OnFailure** or **Never**.</span></span> <span data-ttu-id="ef38e-156">If you specify **OnFailure** and still see continual restarts, there might be an issue with the application or script executed in your container.</span><span class="sxs-lookup"><span data-stu-id="ef38e-156">If you specify **OnFailure** and still see continual restarts, there might be an issue with the application or script executed in your container.</span></span>

<span data-ttu-id="ef38e-157">The Container Instances API includes a `restartCount` property.</span><span class="sxs-lookup"><span data-stu-id="ef38e-157">The Container Instances API includes a `restartCount` property.</span></span> <span data-ttu-id="ef38e-158">To check the number of restarts for a container, you can use the [az container show][az-container-show] command in the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ef38e-158">To check the number of restarts for a container, you can use the [az container show][az-container-show] command in the Azure CLI.</span></span> <span data-ttu-id="ef38e-159">In following example output (which has been truncated for brevity), you can see the `restartCount` property at the end of the output.</span><span class="sxs-lookup"><span data-stu-id="ef38e-159">In following example output (which has been truncated for brevity), you can see the `restartCount` property at the end of the output.</span></span>

```json
...
 "events": [
   {
     "count": 1,
     "firstTimestamp": "2017-11-13T21:20:06+00:00",
     "lastTimestamp": "2017-11-13T21:20:06+00:00",
     "message": "Pulling: pulling image \"myregistry.azurecr.io/aci-tutorial-app:v1\"",
     "type": "Normal"
   },
   {
     "count": 1,
     "firstTimestamp": "2017-11-13T21:20:14+00:00",
     "lastTimestamp": "2017-11-13T21:20:14+00:00",
     "message": "Pulled: Successfully pulled image \"myregistry.azurecr.io/aci-tutorial-app:v1\"",
     "type": "Normal"
   },
   {
     "count": 1,
     "firstTimestamp": "2017-11-13T21:20:14+00:00",
     "lastTimestamp": "2017-11-13T21:20:14+00:00",
     "message": "Created: Created container with id bf25a6ac73a925687cafcec792c9e3723b0776f683d8d1402b20cc9fb5f66a10",
     "type": "Normal"
   },
   {
     "count": 1,
     "firstTimestamp": "2017-11-13T21:20:14+00:00",
     "lastTimestamp": "2017-11-13T21:20:14+00:00",
     "message": "Started: Started container with id bf25a6ac73a925687cafcec792c9e3723b0776f683d8d1402b20cc9fb5f66a10",
     "type": "Normal"
   }
 ],
 "previousState": null,
 "restartCount": 0
...
}
```

> [!NOTE]
> <span data-ttu-id="ef38e-160">Most container images for Linux distributions set a shell, such as bash, as the default command.</span><span class="sxs-lookup"><span data-stu-id="ef38e-160">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="ef38e-161">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop when configured with the default **Always** restart policy.</span><span class="sxs-lookup"><span data-stu-id="ef38e-161">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop when configured with the default **Always** restart policy.</span></span>

## <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="ef38e-162">Container takes a long time to start</span><span class="sxs-lookup"><span data-stu-id="ef38e-162">Container takes a long time to start</span></span>

<span data-ttu-id="ef38e-163">The two primary factors that contribute to container startup time in Azure Container Instances are:</span><span class="sxs-lookup"><span data-stu-id="ef38e-163">The two primary factors that contribute to container startup time in Azure Container Instances are:</span></span>

* [<span data-ttu-id="ef38e-164">Image size</span><span class="sxs-lookup"><span data-stu-id="ef38e-164">Image size</span></span>](#image-size)
* [<span data-ttu-id="ef38e-165">Image location</span><span class="sxs-lookup"><span data-stu-id="ef38e-165">Image location</span></span>](#image-location)

<span data-ttu-id="ef38e-166">Windows images have [additional considerations](#cached-windows-images).</span><span class="sxs-lookup"><span data-stu-id="ef38e-166">Windows images have [additional considerations](#cached-windows-images).</span></span>

### <a name="image-size"></a><span data-ttu-id="ef38e-167">Image size</span><span class="sxs-lookup"><span data-stu-id="ef38e-167">Image size</span></span>

<span data-ttu-id="ef38e-168">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span><span class="sxs-lookup"><span data-stu-id="ef38e-168">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="ef38e-169">Because Azure Container Instances pulls your container image on demand, the startup time you see is directly related to its size.</span><span class="sxs-lookup"><span data-stu-id="ef38e-169">Because Azure Container Instances pulls your container image on demand, the startup time you see is directly related to its size.</span></span>

<span data-ttu-id="ef38e-170">You can view the size of your container image by using the `docker images` command in the Docker CLI:</span><span class="sxs-lookup"><span data-stu-id="ef38e-170">You can view the size of your container image by using the `docker images` command in the Docker CLI:</span></span>

```console
$ docker images
REPOSITORY                  TAG       IMAGE ID        CREATED        SIZE
microsoft/aci-helloworld    latest    7f78509b568e    13 days ago    68.1MB
```

<span data-ttu-id="ef38e-171">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span><span class="sxs-lookup"><span data-stu-id="ef38e-171">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="ef38e-172">One way to do this is with [multi-stage builds][docker-multi-stage-builds].</span><span class="sxs-lookup"><span data-stu-id="ef38e-172">One way to do this is with [multi-stage builds][docker-multi-stage-builds].</span></span> <span data-ttu-id="ef38e-173">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span><span class="sxs-lookup"><span data-stu-id="ef38e-173">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

### <a name="image-location"></a><span data-ttu-id="ef38e-174">Image location</span><span class="sxs-lookup"><span data-stu-id="ef38e-174">Image location</span></span>

<span data-ttu-id="ef38e-175">Another way to reduce the impact of the image pull on your container's startup time is to host the container image in [Azure Container Registry](/azure/container-registry/) in the same region where you intend to deploy container instances.</span><span class="sxs-lookup"><span data-stu-id="ef38e-175">Another way to reduce the impact of the image pull on your container's startup time is to host the container image in [Azure Container Registry](/azure/container-registry/) in the same region where you intend to deploy container instances.</span></span> <span data-ttu-id="ef38e-176">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span><span class="sxs-lookup"><span data-stu-id="ef38e-176">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>

### <a name="cached-windows-images"></a><span data-ttu-id="ef38e-177">Cached Windows images</span><span class="sxs-lookup"><span data-stu-id="ef38e-177">Cached Windows images</span></span>

<span data-ttu-id="ef38e-178">Azure Container Instances uses a caching mechanism to help speed container startup time for images based on certain Windows images.</span><span class="sxs-lookup"><span data-stu-id="ef38e-178">Azure Container Instances uses a caching mechanism to help speed container startup time for images based on certain Windows images.</span></span>

<span data-ttu-id="ef38e-179">To ensure the fastest Windows container startup time, use one of the **three most recent** versions of the following **two images** as the base image:</span><span class="sxs-lookup"><span data-stu-id="ef38e-179">To ensure the fastest Windows container startup time, use one of the **three most recent** versions of the following **two images** as the base image:</span></span>

* <span data-ttu-id="ef38e-180">[Windows Server 2016][docker-hub-windows-core] (LTS only)</span><span class="sxs-lookup"><span data-stu-id="ef38e-180">[Windows Server 2016][docker-hub-windows-core] (LTS only)</span></span>
* <span data-ttu-id="ef38e-181">[Windows Server 2016 Nano Server][docker-hub-windows-nano]</span><span class="sxs-lookup"><span data-stu-id="ef38e-181">[Windows Server 2016 Nano Server][docker-hub-windows-nano]</span></span>

### <a name="windows-containers-slow-network-readiness"></a><span data-ttu-id="ef38e-182">Windows containers slow network readiness</span><span class="sxs-lookup"><span data-stu-id="ef38e-182">Windows containers slow network readiness</span></span>

<span data-ttu-id="ef38e-183">Windows containers may incur no inbound or outbound connectivity for up to 5 seconds on initial creation.</span><span class="sxs-lookup"><span data-stu-id="ef38e-183">Windows containers may incur no inbound or outbound connectivity for up to 5 seconds on initial creation.</span></span> <span data-ttu-id="ef38e-184">After initial setup, container networking should resume appropriately.</span><span class="sxs-lookup"><span data-stu-id="ef38e-184">After initial setup, container networking should resume appropriately.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="ef38e-185">Resource not available error</span><span class="sxs-lookup"><span data-stu-id="ef38e-185">Resource not available error</span></span>

<span data-ttu-id="ef38e-186">Due to varying regional resource load in Azure, you might receive the following error when attempting to deploy a container instance:</span><span class="sxs-lookup"><span data-stu-id="ef38e-186">Due to varying regional resource load in Azure, you might receive the following error when attempting to deploy a container instance:</span></span>

`The requested resource with 'x' CPU and 'y.z' GB memory is not available in the location 'example region' at this moment. Please retry with a different resource request or in another location.`

<span data-ttu-id="ef38e-187">This error indicates that due to heavy load in the region in which you are attempting to deploy, the resources specified for your container can't be allocated at that time.</span><span class="sxs-lookup"><span data-stu-id="ef38e-187">This error indicates that due to heavy load in the region in which you are attempting to deploy, the resources specified for your container can't be allocated at that time.</span></span> <span data-ttu-id="ef38e-188">Use one or more of the following mitigation steps to help resolve your issue.</span><span class="sxs-lookup"><span data-stu-id="ef38e-188">Use one or more of the following mitigation steps to help resolve your issue.</span></span>

* <span data-ttu-id="ef38e-189">Verify your container deployment settings fall within the parameters defined in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md#region-availability)</span><span class="sxs-lookup"><span data-stu-id="ef38e-189">Verify your container deployment settings fall within the parameters defined in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md#region-availability)</span></span>
* <span data-ttu-id="ef38e-190">Specify lower CPU and memory settings for the container</span><span class="sxs-lookup"><span data-stu-id="ef38e-190">Specify lower CPU and memory settings for the container</span></span>
* <span data-ttu-id="ef38e-191">Deploy to a different Azure region</span><span class="sxs-lookup"><span data-stu-id="ef38e-191">Deploy to a different Azure region</span></span>
* <span data-ttu-id="ef38e-192">Deploy at a later time</span><span class="sxs-lookup"><span data-stu-id="ef38e-192">Deploy at a later time</span></span>

## <a name="cannot-connect-to-underlying-docker-api-or-run-privileged-containers"></a><span data-ttu-id="ef38e-193">Cannot connect to underlying Docker API or run privileged containers</span><span class="sxs-lookup"><span data-stu-id="ef38e-193">Cannot connect to underlying Docker API or run privileged containers</span></span>

<span data-ttu-id="ef38e-194">Azure Container Instances does not expose direct access to the underlying infrastructure that hosts container groups.</span><span class="sxs-lookup"><span data-stu-id="ef38e-194">Azure Container Instances does not expose direct access to the underlying infrastructure that hosts container groups.</span></span> <span data-ttu-id="ef38e-195">This includes access to the Docker API running on the container's host and running privileged containers.</span><span class="sxs-lookup"><span data-stu-id="ef38e-195">This includes access to the Docker API running on the container's host and running privileged containers.</span></span> <span data-ttu-id="ef38e-196">If you require Docker interaction, check the [REST reference documentation](https://aka.ms/aci/rest) to see what the ACI API supports.</span><span class="sxs-lookup"><span data-stu-id="ef38e-196">If you require Docker interaction, check the [REST reference documentation](https://aka.ms/aci/rest) to see what the ACI API supports.</span></span> <span data-ttu-id="ef38e-197">If there is something missing, submit a request on the [ACI feedback forums](https://aka.ms/aci/feedback).</span><span class="sxs-lookup"><span data-stu-id="ef38e-197">If there is something missing, submit a request on the [ACI feedback forums](https://aka.ms/aci/feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef38e-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef38e-198">Next steps</span></span>
<span data-ttu-id="ef38e-199">Learn how to [retrieve container logs & events](container-instances-get-logs.md) to help debug your containers.</span><span class="sxs-lookup"><span data-stu-id="ef38e-199">Learn how to [retrieve container logs & events](container-instances-get-logs.md) to help debug your containers.</span></span>

<!-- LINKS - External -->
[azure-name-restrictions]: https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions
[windows-sac-overview]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[docker-multi-stage-builds]: https://docs.docker.com/engine/userguide/eng-image/multistage-build/
[docker-hub-windows-core]: https://hub.docker.com/r/microsoft/windowsservercore/
[docker-hub-windows-nano]: https://hub.docker.com/r/microsoft/nanoserver/

<!-- LINKS - Internal -->
[az-container-show]: /cli/azure/container#az-container-show
