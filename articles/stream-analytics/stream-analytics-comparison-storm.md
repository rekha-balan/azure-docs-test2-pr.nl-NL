---
title: 'Analytics platforms: Apache Storm comparison to Stream Analytics | Microsoft Docs'
description: Get guidance choosing a cloud analytics platform by using an Apache Storm comparison to Stream Analytics. Understand features and differences.
keywords: analytics platform, analytics platforms, cloud analytics platform, storm comparison
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: 9dcac84fdc33515ef12ab5b8154f700bb8618290
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563929"
---
# <a name="help-choosing-a-streaming-analytics-platform-apache-storm-comparison-to-azure-stream-analytics"></a><span data-ttu-id="ca6ff-105">Help choosing a streaming analytics platform: Apache Storm comparison to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ca6ff-105">Help choosing a streaming analytics platform: Apache Storm comparison to Azure Stream Analytics</span></span>
<span data-ttu-id="ca6ff-106">Get guidance choosing a cloud analytics platform by using this Apache Storm comparison to Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-106">Get guidance choosing a cloud analytics platform by using this Apache Storm comparison to Azure Stream Analytics.</span></span> <span data-ttu-id="ca6ff-107">Understand the value propositions of Stream Analytics versus Apache Storm as a managed service on Azure HDInsight, so you can choose the right solution for your business use cases.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-107">Understand the value propositions of Stream Analytics versus Apache Storm as a managed service on Azure HDInsight, so you can choose the right solution for your business use cases.</span></span>

<span data-ttu-id="ca6ff-108">Both analytics platforms provide benefits of a PaaS solution, there are a few major distinguishing capabilities that differentiate them.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-108">Both analytics platforms provide benefits of a PaaS solution, there are a few major distinguishing capabilities that differentiate them.</span></span> <span data-ttu-id="ca6ff-109">Capabilities as well as the limitations of these services are listed below to help you land on the solution you need to achieve your goals.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-109">Capabilities as well as the limitations of these services are listed below to help you land on the solution you need to achieve your goals.</span></span>

## <a name="storm-comparison-to-stream-analytics-general-features"></a><span data-ttu-id="ca6ff-110">Storm comparison to Stream Analytics: General features</span><span class="sxs-lookup"><span data-stu-id="ca6ff-110">Storm comparison to Stream Analytics: General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="ca6ff-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-114">
                    <strong>Open Source</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-114">
                    <strong>Open Source</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-115">No, Azure Stream Analytics is a Microsoft proprietary offering.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-115">No, Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-116">Yes, Apache Storm is an Apache licensed technology.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-116">Yes, Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-117">
                    <strong>Microsoft Supported</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-117">
                    <strong>Microsoft Supported</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-118">Yes</span><span class="sxs-lookup"><span data-stu-id="ca6ff-118">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-119">Yes</span><span class="sxs-lookup"><span data-stu-id="ca6ff-119">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-120">
                    <strong>Hardware requirements</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-120">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-121">There are no hardware requirements.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-121">There are no hardware requirements.</span></span> <span data-ttu-id="ca6ff-122">Azure Stream Analytics is an Azure Service.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-122">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-123">There are no hardware requirements.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-123">There are no hardware requirements.</span></span> <span data-ttu-id="ca6ff-124">Apache Storm is an Azure Service.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-124">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-125">
                    <strong>Top Level Unit</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-125">
                    <strong>Top Level Unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-126">With Azure Stream Analytics customers deploy and monitor streaming jobs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-126">With Azure Stream Analytics customers deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-127">With Apache Storm on HDInsight customers deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other  workloads (incl. batch).</span><span class="sxs-lookup"><span data-stu-id="ca6ff-127">With Apache Storm on HDInsight customers deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other  workloads (incl. batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-128">
                    <strong>Price</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-128">
                    <strong>Price</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-129">Stream Analytics is priced by volume of data processed and the number of streaming units (per hour the job is running) required.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-129">Stream Analytics is priced by volume of data processed and the number of streaming units (per hour the job is running) required.</span></span>
                </p>
                <p><span data-ttu-id="ca6ff-130">
                    <a href="http://azure.microsoft.com/en-us/pricing/details/stream-analytics/">Further pricing information can be found here.</a>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-130">
                    <a href="http://azure.microsoft.com/en-us/pricing/details/stream-analytics/">Further pricing information can be found here.</a>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-131">For Apache Storm on HDInsight, the unit of purchase is cluster-based, and is charged based on the time the cluster is running, independent of jobs deployed.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-131">For Apache Storm on HDInsight, the unit of purchase is cluster-based, and is charged based on the time the cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p><span data-ttu-id="ca6ff-132">
                    <a href="http://azure.microsoft.com/en-us/pricing/details/hdinsight/">Further pricing information can be found here.</a>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-132">
                    <a href="http://azure.microsoft.com/en-us/pricing/details/hdinsight/">Further pricing information can be found here.</a>
                </span></span></p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring-on-each-analytics-platform"></a><span data-ttu-id="ca6ff-133">Authoring on each analytics platform</span><span class="sxs-lookup"><span data-stu-id="ca6ff-133">Authoring on each analytics platform</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-134">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-134">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-135">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-135">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="ca6ff-136">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-136">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-137">
                    <strong>Capabilities: SQL DSL</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-137">
                    <strong>Capabilities: SQL DSL</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-138">Yes, an easy to use SQL language support is available.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-138">Yes, an easy to use SQL language support is available.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-139">No, users must write code in Java C# or use Trident APIs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-139">No, users must write code in Java C# or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-140">
                    <strong>Capabilities: Temporal operators</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-140">
                    <strong>Capabilities: Temporal operators</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-141">Windowed aggregates, and temporal joins are supported out of the box.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-141">Windowed aggregates, and temporal joins are supported out of the box.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-142">Temporal operators must to be implemented by the user.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-142">Temporal operators must to be implemented by the user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-143">
                    <strong>Development Experience</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-143">
                    <strong>Development Experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-144">Interactive authoring and debugging experience through Azure Portal on sample data.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-144">Interactive authoring and debugging experience through Azure Portal on sample data.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-145">Development, debugging and monitoring experience is provided through the Visual Studio experience for .NET users, while for Java and other languages developers may use the IDE of their choice.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-145">Development, debugging and monitoring experience is provided through the Visual Studio experience for .NET users, while for Java and other languages developers may use the IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-146">
                    <strong>Debugging support</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-146">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-147">Stream Analytics offers basic job status and Operations logs as a way of debugging, but currently does not offer flexibility in what/how much is included in the logs ie: verbose mode.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-147">Stream Analytics offers basic job status and Operations logs as a way of debugging, but currently does not offer flexibility in what/how much is included in the logs ie: verbose mode.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-148">Detailed logs are available for debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-148">Detailed logs are available for debugging purposes.</span></span> <span data-ttu-id="ca6ff-149">There are two ways to surface logs to user, via visual Studio or user can RDP into the cluster to access logs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-149">There are two ways to surface logs to user, via visual Studio or user can RDP into the cluster to access logs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-150">
                    <strong>Support for UDF (User Defined Functions)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-150">
                    <strong>Support for UDF (User Defined Functions)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-151">Currently there is no support for UDFs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-151">Currently there is no support for UDFs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-152">UDFs can be written in C#, Java or the language of your choice.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-152">UDFs can be written in C#, Java or the language of your choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-153">
                    <strong>Extensible - custom code </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-153">
                    <strong>Extensible - custom code </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-154">There is no support for extensible code in Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-154">There is no support for extensible code in Stream Analytics.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-155">Yes, there is availability to write custom code in C#, Java or other supported languages on Storm.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-155">Yes, there is availability to write custom code in C#, Java or other supported languages on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-and-outputs"></a><span data-ttu-id="ca6ff-156">Data sources and outputs</span><span class="sxs-lookup"><span data-stu-id="ca6ff-156">Data sources and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-157">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-157">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-158">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-158">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="ca6ff-159">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-159">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-160">
                 <strong>Input Data Sources</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-160">
                 <strong>Input Data Sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-161">The supported input sources are Azure Event Hubs and Azure Blobs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-161">The supported input sources are Azure Event Hubs and Azure Blobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-162">There are connectors available for Event Hubs, Service Bus, Kafka, etc. Unsupported connectors may be implemented via custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-162">There are connectors available for Event Hubs, Service Bus, Kafka, etc. Unsupported connectors may be implemented via custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-163">
                    <strong>Input Data formats</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-163">
                    <strong>Input Data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-164">Supported input formats are Avro, JSON, CSV.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-164">Supported input formats are Avro, JSON, CSV.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-165">Any format may be implemented via custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-165">Any format may be implemented via custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-166">
                    <strong>Outputs</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-166">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-167">A streaming job may have multiple outputs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-167">A streaming job may have multiple outputs.</span></span> <span data-ttu-id="ca6ff-168">Supported Outputs: Azure Event Hubs, Azure Blob Storage, Azure Tables, Azure SQL DB, and PowerBI.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-168">Supported Outputs: Azure Event Hubs, Azure Blob Storage, Azure Tables, Azure SQL DB, and PowerBI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-169">Support for many outputs in a topology, each output may have custom logic for downstream processing.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-169">Support for many outputs in a topology, each output may have custom logic for downstream processing.</span></span> <span data-ttu-id="ca6ff-170">Out of the box Storm includes connectors for PowerBI, Azure Event Hubs, Azure Blob Store, Azure DocumentDB, SQL and HBase.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-170">Out of the box Storm includes connectors for PowerBI, Azure Event Hubs, Azure Blob Store, Azure DocumentDB, SQL and HBase.</span></span> <span data-ttu-id="ca6ff-171">Unsupported connectors may be implemented via custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-171">Unsupported connectors may be implemented via custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-172">
                    <strong>Data Encoding formats</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-172">
                    <strong>Data Encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-173">Stream Analytics requires UTF-8 data format to be utilized.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-173">Stream Analytics requires UTF-8 data format to be utilized.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-174">Any data encoding format may be implemented via custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-174">Any data encoding format may be implemented via custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="ca6ff-175">Management and operations</span><span class="sxs-lookup"><span data-stu-id="ca6ff-175">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-176">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-176">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-177">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-177">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="ca6ff-178">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-178">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-179">
                    <strong>Job Deployment model</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-179">
                    <strong>Job Deployment model</strong>
                </span></span></p>
                <p><span data-ttu-id="ca6ff-180">
                    - <strong>Azure Portal</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-180">
                    - <strong>Azure Portal</strong>
                </span></span></p>
                <p><span data-ttu-id="ca6ff-181">
                    - <strong>Visual Studio</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-181">
                    - <strong>Visual Studio</strong>
                </span></span></p>
                <p><span data-ttu-id="ca6ff-182">
                    - <strong>PowerShell</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-182">
                    - <strong>PowerShell</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-183">Deployment is implemented via Azure Portal, PowerShell and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-183">Deployment is implemented via Azure Portal, PowerShell and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-184">Depolyment is implemented via Azure Portal, PowerShell, Visual Studio and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-184">Depolyment is implemented via Azure Portal, PowerShell, Visual Studio and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-185">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-185">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-186">Monitoring is implemented via Azure Portal and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-186">Monitoring is implemented via Azure Portal and REST APIs.</span></span>
                </p>
                <p>
<span data-ttu-id="ca6ff-187">The user may also configure Azure alerts.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-187">The user may also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-188">Monitoring is implemented via Storm UI and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-188">Monitoring is implemented via Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-189">
                    <strong>Scalability</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-189">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-190">Number of Streaming Units for each job.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-190">Number of Streaming Units for each job.</span></span> <span data-ttu-id="ca6ff-191">Each Streaming Unit processes up to 1MB/s.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-191">Each Streaming Unit processes up to 1MB/s.</span></span> <span data-ttu-id="ca6ff-192">Max of 50 units by default.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-192">Max of 50 units by default.</span></span> <span data-ttu-id="ca6ff-193">Call to increase limit.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-193">Call to increase limit.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-194">Number of nodes in the HDI Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-194">Number of nodes in the HDI Storm cluster.</span></span> <span data-ttu-id="ca6ff-195">No limit on number of nodes (Top limit defined by your Azure quota).</span><span class="sxs-lookup"><span data-stu-id="ca6ff-195">No limit on number of nodes (Top limit defined by your Azure quota).</span></span> <span data-ttu-id="ca6ff-196">Call to increase limit.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-196">Call to increase limit.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-197">
                    <strong>Data processing limits</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-197">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-198">Users can scale up or down number of Streaming Units to increase data processing or optimize costs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-198">Users can scale up or down number of Streaming Units to increase data processing or optimize costs.</span></span>
                </p>
                <p>
<span data-ttu-id="ca6ff-199">Scale up to 1 GB/s</span><span class="sxs-lookup"><span data-stu-id="ca6ff-199">Scale up to 1 GB/s</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-200">User can scale up or down cluster size to meet needs.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-200">User can scale up or down cluster size to meet needs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-201">
                    <strong>Stop/Resume</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-202">Stop and resume from last place stopped.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-203">Stop and resume from last place stopped based on the watermark.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-203">Stop and resume from last place stopped based on the watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-204">
                    <strong>Service and framework update</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-205">Automatic patching with no downtime.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-206">Automatic patching with no downtime.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLA’s</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLA’s</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-208">SLA of 99.9% uptime</span><span class="sxs-lookup"><span data-stu-id="ca6ff-208">SLA of 99.9% uptime</span></span> </p>
                <p>
<span data-ttu-id="ca6ff-209">Auto-recovery from failures</span><span class="sxs-lookup"><span data-stu-id="ca6ff-209">Auto-recovery from failures</span></span> </p>
                <p>
<span data-ttu-id="ca6ff-210">Recovery of stateful temporal operators is built-in.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-210">Recovery of stateful temporal operators is built-in.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-211">SLA of 99.9% uptime of the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-211">SLA of 99.9% uptime of the Storm cluster.</span></span> <span data-ttu-id="ca6ff-212">Apache Storm is a fault tolerant streaming platform however it is the customers' responsibility to ensure their streaming jobs run uninterrupted.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-212">Apache Storm is a fault tolerant streaming platform however it is the customers' responsibility to ensure their streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="ca6ff-213">Advanced Features</span><span class="sxs-lookup"><span data-stu-id="ca6ff-213">Advanced Features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-214">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-214">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="ca6ff-215">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-215">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="ca6ff-216">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-216">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-217">
                    <strong>Late arrival and out of order event handling</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-217">
                    <strong>Late arrival and out of order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-218">Built-in configurable policies to reorder, drop events or adjust event time.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-218">Built-in configurable policies to reorder, drop events or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-219">User must implement logic to handle this scenario.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-219">User must implement logic to handle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-220">
                    <strong>Reference data</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-220">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-221">Reference data available from Azure Blobs with max size of 100 MB of in-memory lookup cache.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-221">Reference data available from Azure Blobs with max size of 100 MB of in-memory lookup cache.</span></span> <span data-ttu-id="ca6ff-222">Refreshing of reference data is managed by the service.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-222">Refreshing of reference data is managed by the service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-223">No limits on data size.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-223">No limits on data size.</span></span> <span data-ttu-id="ca6ff-224">Connectors available for HBase, DocumentDB, SQL Server and Azure.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-224">Connectors available for HBase, DocumentDB, SQL Server and Azure.</span></span> <span data-ttu-id="ca6ff-225">Unsupported connectors may be implemented via custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-225">Unsupported connectors may be implemented via custom code.</span></span>
                </p>
                <p>
<span data-ttu-id="ca6ff-226">Refreshing of reference data must be handled by custom code.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-226">Refreshing of reference data must be handled by custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="ca6ff-227">
                    <strong>Integration with Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="ca6ff-227">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="ca6ff-228">By configuring published Azure Machine Learning models as functions during ASA job creation <a href="http://blogs.msdn.com/b/streamanalytics/archive/2015/05/24/real-time-scoring-of-streaming-data-using-machine-learning-models.aspx">(private preview)</a>.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-228">By configuring published Azure Machine Learning models as functions during ASA job creation <a href="http://blogs.msdn.com/b/streamanalytics/archive/2015/05/24/real-time-scoring-of-streaming-data-using-machine-learning-models.aspx">(private preview)</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="ca6ff-229">Available through Storm Bolts.</span><span class="sxs-lookup"><span data-stu-id="ca6ff-229">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
