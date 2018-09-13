---
title: How to configure data outputs for Stream Analytics jobs | Microsoft Docs
description: Configure Outputs for Stream Analytics jobs | learning path segment.
keywords: data output, data movement
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2ddbc4d12e227afc37b3670c2c2f92270d9a9a43
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563277"
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="6f2fc-104">How to configure data outputs for Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6f2fc-104">How to configure data outputs for Stream Analytics jobs</span></span>
<span data-ttu-id="6f2fc-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="6f2fc-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="6f2fc-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="6f2fc-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="6f2fc-109">To add an output to your Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="6f2fc-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="6f2fc-110">In the Azure Classic Portal, click **Outputs** and then click **Add Output** in your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-110">In the Azure Classic Portal, click **Outputs** and then click **Add Output** in your Stream Analytics job.</span></span>
   
    ![Add Outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
    <span data-ttu-id="6f2fc-112">In the Azure portal click the **Outputs** tile in your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-112">In the Azure portal click the **Outputs** tile in your Stream Analytics job.</span></span>
   
    ![Azure Porta Add Outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/5-stream-analytics-add-outputs.png)
2. <span data-ttu-id="6f2fc-114">Specify the type of the output:</span><span class="sxs-lookup"><span data-stu-id="6f2fc-114">Specify the type of the output:</span></span>
   
    ![Choose data movement type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
    ![Azure portal choose data movement type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/6-stream-analytics-add-outputs.png)
3. <span data-ttu-id="6f2fc-117">Provide a friendly name for this output in the **Output Alias** box.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-117">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="6f2fc-118">This name can be used in your job's query later on to refer to the output.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-118">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="6f2fc-119">Fill in the rest of the required connection properties to connect to your output.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-119">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="6f2fc-120">These fields vary by output type and are defined in detail here.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-120">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Add data output properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/3-stream-analytics-add-outputs.png)  
4. <span data-ttu-id="6f2fc-122">Depending on the output type, you may need to specify how the data is serialized or formatted.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-122">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="6f2fc-123">The specific serialization settings for each output type are documented here.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-123">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="6f2fc-124">Fill in the rest of the required connection properties to connect to your data source.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-124">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="6f2fc-125">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="6f2fc-125">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Add data output to event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/4-stream-analytics-add-outputs.png)  
   
    ![Azure portal data output to event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-outputs/7-stream-analytics-add-outputs.png)  

> [!Note]
> <span data-ttu-id="6f2fc-128">Any output element added to the job, must exist before the job is started and events start flowing.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-128">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="6f2fc-129">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-129">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="6f2fc-130">It needs to be created by the user before the ASA job is started.</span><span class="sxs-lookup"><span data-stu-id="6f2fc-130">It needs to be created by the user before the ASA job is started.</span></span>
> 
> 

## <a name="get-help"></a><span data-ttu-id="6f2fc-131">Get help</span><span class="sxs-lookup"><span data-stu-id="6f2fc-131">Get help</span></span>
<span data-ttu-id="6f2fc-132">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6f2fc-132">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f2fc-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f2fc-133">Next steps</span></span>
* [<span data-ttu-id="6f2fc-134">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6f2fc-134">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6f2fc-135">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6f2fc-135">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="6f2fc-136">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6f2fc-136">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6f2fc-137">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="6f2fc-137">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6f2fc-138">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="6f2fc-138">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)








