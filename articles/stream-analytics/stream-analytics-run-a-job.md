---
title: How to start streaming jobs in Stream Analytics | Microsoft Docs
description: How run a streaming job in Azure Stream Analytics | learning path segment.
keywords: streaming jobs
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: cd2e14173176603302c8c44a67b812657341bd7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669159"
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="2c73e-104">How to run a streaming job in Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2c73e-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="2c73e-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="2c73e-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="2c73e-106">To start your job:</span><span class="sxs-lookup"><span data-stu-id="2c73e-106">To start your job:</span></span>

1. <span data-ttu-id="2c73e-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2c73e-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![Start job Button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="2c73e-109">In the Azure portal, click **Start** at the top of your job page.</span><span class="sxs-lookup"><span data-stu-id="2c73e-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Azure portal Start job Button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="2c73e-111">Specify a **Start Output** value to determine when this job will start producing output.</span><span class="sxs-lookup"><span data-stu-id="2c73e-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="2c73e-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span><span class="sxs-lookup"><span data-stu-id="2c73e-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="2c73e-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span><span class="sxs-lookup"><span data-stu-id="2c73e-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="2c73e-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span><span class="sxs-lookup"><span data-stu-id="2c73e-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![Start streaming job Time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portal Start streaming job Time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="2c73e-117">Confirm your selection.</span><span class="sxs-lookup"><span data-stu-id="2c73e-117">Confirm your selection.</span></span> <span data-ttu-id="2c73e-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span><span class="sxs-lookup"><span data-stu-id="2c73e-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="2c73e-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span><span class="sxs-lookup"><span data-stu-id="2c73e-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![streaming job progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure portal streaming job progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="2c73e-122">Get help</span><span class="sxs-lookup"><span data-stu-id="2c73e-122">Get help</span></span>
<span data-ttu-id="2c73e-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2c73e-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c73e-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c73e-124">Next steps</span></span>
* [<span data-ttu-id="2c73e-125">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2c73e-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2c73e-126">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2c73e-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="2c73e-127">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="2c73e-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2c73e-128">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="2c73e-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2c73e-129">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="2c73e-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)







