---
title: Understand and resolve WebHCat errors on HDInsight
description: Learn how to about common errors returned by WebHCat on HDInsight and how to resolve them.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: larryfr
ms.openlocfilehash: e322547872b9b8f9604053d6d05408b2369750d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661619"
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="ee3a2-103">Understand and resolve errors received from WebHCat on HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee3a2-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="ee3a2-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="ee3a2-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="ee3a2-106">What is WebHCat</span><span class="sxs-lookup"><span data-stu-id="ee3a2-106">What is WebHCat</span></span>

<span data-ttu-id="ee3a2-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="ee3a2-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="ee3a2-109">Modifying configuration</span><span class="sxs-lookup"><span data-stu-id="ee3a2-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee3a2-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="ee3a2-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span><span class="sxs-lookup"><span data-stu-id="ee3a2-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="ee3a2-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="ee3a2-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a2-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="ee3a2-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="ee3a2-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee3a2-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee3a2-117">For more information, see [HDInsight version 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="ee3a2-117">For more information, see [HDInsight version 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="ee3a2-118">Default configuration</span><span class="sxs-lookup"><span data-stu-id="ee3a2-118">Default configuration</span></span>

<span data-ttu-id="ee3a2-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span><span class="sxs-lookup"><span data-stu-id="ee3a2-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="ee3a2-120">Setting</span><span class="sxs-lookup"><span data-stu-id="ee3a2-120">Setting</span></span> | <span data-ttu-id="ee3a2-121">What it does</span><span class="sxs-lookup"><span data-stu-id="ee3a2-121">What it does</span></span> | <span data-ttu-id="ee3a2-122">Default value</span><span class="sxs-lookup"><span data-stu-id="ee3a2-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee3a2-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="ee3a2-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="ee3a2-124">The maximum number of jobs that can be active concurrently (pending or running)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="ee3a2-125">10,000</span><span class="sxs-lookup"><span data-stu-id="ee3a2-125">10,000</span></span> |
| <span data-ttu-id="ee3a2-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="ee3a2-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="ee3a2-127">The maximum number of requests that can be served concurrently</span><span class="sxs-lookup"><span data-stu-id="ee3a2-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="ee3a2-128">20</span><span class="sxs-lookup"><span data-stu-id="ee3a2-128">20</span></span> |
| <span data-ttu-id="ee3a2-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="ee3a2-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="ee3a2-130">The number of days that job history are retained</span><span class="sxs-lookup"><span data-stu-id="ee3a2-130">The number of days that job history are retained</span></span> |<span data-ttu-id="ee3a2-131">7 days</span><span class="sxs-lookup"><span data-stu-id="ee3a2-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="ee3a2-132">Too many requests</span><span class="sxs-lookup"><span data-stu-id="ee3a2-132">Too many requests</span></span>

<span data-ttu-id="ee3a2-133">**HTTP Status code**: 429</span><span class="sxs-lookup"><span data-stu-id="ee3a2-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="ee3a2-134">Cause</span><span class="sxs-lookup"><span data-stu-id="ee3a2-134">Cause</span></span> | <span data-ttu-id="ee3a2-135">Resolution</span><span class="sxs-lookup"><span data-stu-id="ee3a2-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="ee3a2-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="ee3a2-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="ee3a2-138">For more information, see [Modifying configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="ee3a2-139">Server unavailable</span><span class="sxs-lookup"><span data-stu-id="ee3a2-139">Server unavailable</span></span>

<span data-ttu-id="ee3a2-140">**HTTP Status code**: 503</span><span class="sxs-lookup"><span data-stu-id="ee3a2-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="ee3a2-141">Cause</span><span class="sxs-lookup"><span data-stu-id="ee3a2-141">Cause</span></span> | <span data-ttu-id="ee3a2-142">Resolution</span><span class="sxs-lookup"><span data-stu-id="ee3a2-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="ee3a2-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span><span class="sxs-lookup"><span data-stu-id="ee3a2-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="ee3a2-144">Wait two minutes, then retry the operation</span><span class="sxs-lookup"><span data-stu-id="ee3a2-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="ee3a2-145">Bad request Content: Could not find job</span><span class="sxs-lookup"><span data-stu-id="ee3a2-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="ee3a2-146">**HTTP Status code**: 400</span><span class="sxs-lookup"><span data-stu-id="ee3a2-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="ee3a2-147">Cause</span><span class="sxs-lookup"><span data-stu-id="ee3a2-147">Cause</span></span> | <span data-ttu-id="ee3a2-148">Resolution</span><span class="sxs-lookup"><span data-stu-id="ee3a2-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="ee3a2-149">Job details have been cleaned up by the job history cleaner</span><span class="sxs-lookup"><span data-stu-id="ee3a2-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="ee3a2-150">The default retention period for job history is 7 days.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="ee3a2-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="ee3a2-152">For more information, see [Modifying configuration](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="ee3a2-153">Job has been killed due to a failover</span><span class="sxs-lookup"><span data-stu-id="ee3a2-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="ee3a2-154">Retry job submission for up to two minutes</span><span class="sxs-lookup"><span data-stu-id="ee3a2-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="ee3a2-155">An Invalid job id was used</span><span class="sxs-lookup"><span data-stu-id="ee3a2-155">An Invalid job id was used</span></span> |<span data-ttu-id="ee3a2-156">Check if the job id is correct</span><span class="sxs-lookup"><span data-stu-id="ee3a2-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="ee3a2-157">Bad gateway</span><span class="sxs-lookup"><span data-stu-id="ee3a2-157">Bad gateway</span></span>

<span data-ttu-id="ee3a2-158">**HTTP Status code**: 502</span><span class="sxs-lookup"><span data-stu-id="ee3a2-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="ee3a2-159">Cause</span><span class="sxs-lookup"><span data-stu-id="ee3a2-159">Cause</span></span> | <span data-ttu-id="ee3a2-160">Resolution</span><span class="sxs-lookup"><span data-stu-id="ee3a2-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="ee3a2-161">Internal garbage collection is occurring within the WebHCat process</span><span class="sxs-lookup"><span data-stu-id="ee3a2-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="ee3a2-162">Wait for garbage collection to finish or restart the WebHCat service</span><span class="sxs-lookup"><span data-stu-id="ee3a2-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="ee3a2-163">Time out waiting on a response from the ResourceManager service.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="ee3a2-164">This can occur when the number of active applications goes the configured maximum (default 10,000)</span><span class="sxs-lookup"><span data-stu-id="ee3a2-164">This can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="ee3a2-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="ee3a2-166">See [Modifying configuration](#modifying-configuration) for more information</span><span class="sxs-lookup"><span data-stu-id="ee3a2-166">See [Modifying configuration](#modifying-configuration) for more information</span></span> |
| <span data-ttu-id="ee3a2-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span><span class="sxs-lookup"><span data-stu-id="ee3a2-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="ee3a2-168">Do not retrieve *all* job details.</span><span class="sxs-lookup"><span data-stu-id="ee3a2-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="ee3a2-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span><span class="sxs-lookup"><span data-stu-id="ee3a2-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="ee3a2-170">The WebHCat service is down during HeadNode failover</span><span class="sxs-lookup"><span data-stu-id="ee3a2-170">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="ee3a2-171">Wait for two minutes and retry the operation</span><span class="sxs-lookup"><span data-stu-id="ee3a2-171">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="ee3a2-172">There are more than 500 pending jobs submitted through WebHCat</span><span class="sxs-lookup"><span data-stu-id="ee3a2-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="ee3a2-173">Wait until currently pending jobs have completed before submitting more jobs</span><span class="sxs-lookup"><span data-stu-id="ee3a2-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
