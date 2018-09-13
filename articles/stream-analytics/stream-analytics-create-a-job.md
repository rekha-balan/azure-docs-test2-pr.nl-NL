---
title: How to create a data analytics processing job for Stream Analytics | Microsoft Docs
description: Create a data analytics processing job for Stream Analytics | learning path segment.
keywords: data analytics processing
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8c3833847a72941dbb8f8798db18cc580e77a80d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555832"
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="05d59-104">How to create a data analytics processing job for Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="05d59-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="05d59-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span><span class="sxs-lookup"><span data-stu-id="05d59-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="05d59-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span><span class="sxs-lookup"><span data-stu-id="05d59-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="05d59-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span><span class="sxs-lookup"><span data-stu-id="05d59-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="05d59-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="05d59-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="05d59-109">Note that this action has no billing implications until the job is started.</span><span class="sxs-lookup"><span data-stu-id="05d59-109">Note that this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="05d59-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="05d59-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="05d59-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="05d59-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Data analytics processing job wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Create data analytics processing job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="05d59-114">Specify the desired configuration for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="05d59-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="05d59-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="05d59-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="05d59-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span><span class="sxs-lookup"><span data-stu-id="05d59-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="05d59-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span><span class="sxs-lookup"><span data-stu-id="05d59-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="05d59-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span><span class="sxs-lookup"><span data-stu-id="05d59-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="05d59-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="05d59-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="05d59-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span><span class="sxs-lookup"><span data-stu-id="05d59-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="05d59-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span><span class="sxs-lookup"><span data-stu-id="05d59-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="05d59-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span><span class="sxs-lookup"><span data-stu-id="05d59-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="05d59-123">It can take a few minutes for the Stream Analytics job to be created.</span><span class="sxs-lookup"><span data-stu-id="05d59-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="05d59-124">To check the status, you can monitor the progress in the Notifications hub.</span><span class="sxs-lookup"><span data-stu-id="05d59-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Data analytics processing job notfications hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal Data analytics processing job create Job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="05d59-127">The new job will be shown with a status of **Created**.</span><span class="sxs-lookup"><span data-stu-id="05d59-127">The new job will be shown with a status of **Created**.</span></span> <span data-ttu-id="05d59-128">Notice that the **Start** button is disabled.</span><span class="sxs-lookup"><span data-stu-id="05d59-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="05d59-129">You must configure the job input, query, and output before you can start the job.</span><span class="sxs-lookup"><span data-stu-id="05d59-129">You must configure the job input, query, and output before you can start the job.</span></span>
   
   ![Data analytics processing job job Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal Data analytics processing job job status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="05d59-132">Get help</span><span class="sxs-lookup"><span data-stu-id="05d59-132">Get help</span></span>
<span data-ttu-id="05d59-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="05d59-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="05d59-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="05d59-134">Next steps</span></span>
* [<span data-ttu-id="05d59-135">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="05d59-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="05d59-136">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="05d59-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="05d59-137">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="05d59-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="05d59-138">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="05d59-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="05d59-139">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="05d59-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)







