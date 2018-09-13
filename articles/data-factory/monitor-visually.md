---
title: Visually monitor Azure data factories | Microsoft Docs
description: Learn how to visually monitor Azure Data factories
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/12/2018
ms.author: shlo
ms.openlocfilehash: 4b3828e1857d17a128de346449d5cf2041709e50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857666"
---
# <a name="visually-monitor-azure-data-factories"></a><span data-ttu-id="5eb04-103">Visually monitor Azure data factories</span><span class="sxs-lookup"><span data-stu-id="5eb04-103">Visually monitor Azure data factories</span></span>
<span data-ttu-id="5eb04-104">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span><span class="sxs-lookup"><span data-stu-id="5eb04-104">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span></span> <span data-ttu-id="5eb04-105">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span><span class="sxs-lookup"><span data-stu-id="5eb04-105">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span></span>
<span data-ttu-id="5eb04-106">In this quick start, you will learn how to visually monitor data factory v2 pipelines without writing a single line of code.</span><span class="sxs-lookup"><span data-stu-id="5eb04-106">In this quick start, you will learn how to visually monitor data factory v2 pipelines without writing a single line of code.</span></span>
<span data-ttu-id="5eb04-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="5eb04-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="monitor-data-factory-v2-pipelines"></a><span data-ttu-id="5eb04-108">Monitor data factory v2 pipelines</span><span class="sxs-lookup"><span data-stu-id="5eb04-108">Monitor data factory v2 pipelines</span></span>

1. <span data-ttu-id="5eb04-109">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="5eb04-109">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="5eb04-110">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="5eb04-110">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
2. <span data-ttu-id="5eb04-111">Log in to the  [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5eb04-111">Log in to the  [Azure portal](https://portal.azure.com/).</span></span>
3. <span data-ttu-id="5eb04-112">Navigate to the created data factory blade in Azure portal and click the 'Monitor & Manage' tile.</span><span class="sxs-lookup"><span data-stu-id="5eb04-112">Navigate to the created data factory blade in Azure portal and click the 'Monitor & Manage' tile.</span></span> <span data-ttu-id="5eb04-113">This will launch the ADF v2 visual monitoring experience.</span><span class="sxs-lookup"><span data-stu-id="5eb04-113">This will launch the ADF v2 visual monitoring experience.</span></span>

## <a name="list-view-monitoring"></a><span data-ttu-id="5eb04-114">List-View Monitoring</span><span class="sxs-lookup"><span data-stu-id="5eb04-114">List-View Monitoring</span></span>

<span data-ttu-id="5eb04-115">Monitor pipeline and activity runs with a simple list view interface.</span><span class="sxs-lookup"><span data-stu-id="5eb04-115">Monitor pipeline and activity runs with a simple list view interface.</span></span> <span data-ttu-id="5eb04-116">All the runs are displayed in local browser time zone.</span><span class="sxs-lookup"><span data-stu-id="5eb04-116">All the runs are displayed in local browser time zone.</span></span> <span data-ttu-id="5eb04-117">You can change the time zone and all the date time fields will snap to the selected time zone.</span><span class="sxs-lookup"><span data-stu-id="5eb04-117">You can change the time zone and all the date time fields will snap to the selected time zone.</span></span>  

#### <a name="monitoring-pipeline-runs"></a><span data-ttu-id="5eb04-118">Monitoring Pipeline Runs</span><span class="sxs-lookup"><span data-stu-id="5eb04-118">Monitoring Pipeline Runs</span></span>
<span data-ttu-id="5eb04-119">List view showcasing each pipeline run for your data factory v2 pipelines.</span><span class="sxs-lookup"><span data-stu-id="5eb04-119">List view showcasing each pipeline run for your data factory v2 pipelines.</span></span> <span data-ttu-id="5eb04-120">Included columns:</span><span class="sxs-lookup"><span data-stu-id="5eb04-120">Included columns:</span></span>

| <span data-ttu-id="5eb04-121">**Column Name**</span><span class="sxs-lookup"><span data-stu-id="5eb04-121">**Column Name**</span></span> | <span data-ttu-id="5eb04-122">**Description**</span><span class="sxs-lookup"><span data-stu-id="5eb04-122">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5eb04-123">Pipeline Name</span><span class="sxs-lookup"><span data-stu-id="5eb04-123">Pipeline Name</span></span> | <span data-ttu-id="5eb04-124">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="5eb04-124">Name of the pipeline.</span></span> |
| <span data-ttu-id="5eb04-125">Actions</span><span class="sxs-lookup"><span data-stu-id="5eb04-125">Actions</span></span> | <span data-ttu-id="5eb04-126">Single action available to view activity runs.</span><span class="sxs-lookup"><span data-stu-id="5eb04-126">Single action available to view activity runs.</span></span> |
| <span data-ttu-id="5eb04-127">Run Start</span><span class="sxs-lookup"><span data-stu-id="5eb04-127">Run Start</span></span> | <span data-ttu-id="5eb04-128">Pipeline run start date time (MM/DD/YYYY, HH:MM:SS AM/PM)</span><span class="sxs-lookup"><span data-stu-id="5eb04-128">Pipeline run start date time (MM/DD/YYYY, HH:MM:SS AM/PM)</span></span> |
| <span data-ttu-id="5eb04-129">Duration</span><span class="sxs-lookup"><span data-stu-id="5eb04-129">Duration</span></span> | <span data-ttu-id="5eb04-130">Run duration (HH:MM:SS)</span><span class="sxs-lookup"><span data-stu-id="5eb04-130">Run duration (HH:MM:SS)</span></span> |
| <span data-ttu-id="5eb04-131">Triggered By</span><span class="sxs-lookup"><span data-stu-id="5eb04-131">Triggered By</span></span> | <span data-ttu-id="5eb04-132">Manual trigger, Schedule trigger</span><span class="sxs-lookup"><span data-stu-id="5eb04-132">Manual trigger, Schedule trigger</span></span> |
| <span data-ttu-id="5eb04-133">Status</span><span class="sxs-lookup"><span data-stu-id="5eb04-133">Status</span></span> | <span data-ttu-id="5eb04-134">Failed, Succeeded, In Progress</span><span class="sxs-lookup"><span data-stu-id="5eb04-134">Failed, Succeeded, In Progress</span></span> |
| <span data-ttu-id="5eb04-135">Parameters</span><span class="sxs-lookup"><span data-stu-id="5eb04-135">Parameters</span></span> | <span data-ttu-id="5eb04-136">Pipeline run parameters (name, value pairs)</span><span class="sxs-lookup"><span data-stu-id="5eb04-136">Pipeline run parameters (name, value pairs)</span></span> |
| <span data-ttu-id="5eb04-137">Error</span><span class="sxs-lookup"><span data-stu-id="5eb04-137">Error</span></span> | <span data-ttu-id="5eb04-138">Pipeline run error (if/any)</span><span class="sxs-lookup"><span data-stu-id="5eb04-138">Pipeline run error (if/any)</span></span> |
| <span data-ttu-id="5eb04-139">Run ID</span><span class="sxs-lookup"><span data-stu-id="5eb04-139">Run ID</span></span> | <span data-ttu-id="5eb04-140">Id of the pipeline run</span><span class="sxs-lookup"><span data-stu-id="5eb04-140">Id of the pipeline run</span></span> |

![Monitor pipeline runs](media/monitor-visually/pipeline-runs.png)

#### <a name="monitoring-activity-runs"></a><span data-ttu-id="5eb04-142">Monitoring Activity Runs</span><span class="sxs-lookup"><span data-stu-id="5eb04-142">Monitoring Activity Runs</span></span>
<span data-ttu-id="5eb04-143">List view showcasing activity runs corresponding to each pipeline run.</span><span class="sxs-lookup"><span data-stu-id="5eb04-143">List view showcasing activity runs corresponding to each pipeline run.</span></span> <span data-ttu-id="5eb04-144">Click **'Activity Runs'** icon under the **'Actions'** column to view activity runs for each pipeline run.</span><span class="sxs-lookup"><span data-stu-id="5eb04-144">Click **'Activity Runs'** icon under the **'Actions'** column to view activity runs for each pipeline run.</span></span> <span data-ttu-id="5eb04-145">Included columns:</span><span class="sxs-lookup"><span data-stu-id="5eb04-145">Included columns:</span></span>

| <span data-ttu-id="5eb04-146">**Column Name**</span><span class="sxs-lookup"><span data-stu-id="5eb04-146">**Column Name**</span></span> | <span data-ttu-id="5eb04-147">**Description**</span><span class="sxs-lookup"><span data-stu-id="5eb04-147">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5eb04-148">Activity Name</span><span class="sxs-lookup"><span data-stu-id="5eb04-148">Activity Name</span></span> | <span data-ttu-id="5eb04-149">Name of the activity inside the pipeline.</span><span class="sxs-lookup"><span data-stu-id="5eb04-149">Name of the activity inside the pipeline.</span></span> |
| <span data-ttu-id="5eb04-150">Activity Type</span><span class="sxs-lookup"><span data-stu-id="5eb04-150">Activity Type</span></span> | <span data-ttu-id="5eb04-151">Type of the activity i.e. Copy, HDInsightSpark, HDInsightHive etc.</span><span class="sxs-lookup"><span data-stu-id="5eb04-151">Type of the activity i.e. Copy, HDInsightSpark, HDInsightHive etc.</span></span> |
| <span data-ttu-id="5eb04-152">Run Start</span><span class="sxs-lookup"><span data-stu-id="5eb04-152">Run Start</span></span> | <span data-ttu-id="5eb04-153">Activity run start date time (MM/DD/YYYY, HH:MM:SS AM/PM)</span><span class="sxs-lookup"><span data-stu-id="5eb04-153">Activity run start date time (MM/DD/YYYY, HH:MM:SS AM/PM)</span></span> |
| <span data-ttu-id="5eb04-154">Duration</span><span class="sxs-lookup"><span data-stu-id="5eb04-154">Duration</span></span> | <span data-ttu-id="5eb04-155">Run duration (HH:MM:SS)</span><span class="sxs-lookup"><span data-stu-id="5eb04-155">Run duration (HH:MM:SS)</span></span> |
| <span data-ttu-id="5eb04-156">Status</span><span class="sxs-lookup"><span data-stu-id="5eb04-156">Status</span></span> | <span data-ttu-id="5eb04-157">Failed, Succeeded, In Progress</span><span class="sxs-lookup"><span data-stu-id="5eb04-157">Failed, Succeeded, In Progress</span></span> |
| <span data-ttu-id="5eb04-158">Input</span><span class="sxs-lookup"><span data-stu-id="5eb04-158">Input</span></span> | <span data-ttu-id="5eb04-159">JSON array describing the activity inputs</span><span class="sxs-lookup"><span data-stu-id="5eb04-159">JSON array describing the activity inputs</span></span> |
| <span data-ttu-id="5eb04-160">Output</span><span class="sxs-lookup"><span data-stu-id="5eb04-160">Output</span></span> | <span data-ttu-id="5eb04-161">JSON array describing the activity outputs</span><span class="sxs-lookup"><span data-stu-id="5eb04-161">JSON array describing the activity outputs</span></span> |
| <span data-ttu-id="5eb04-162">Error</span><span class="sxs-lookup"><span data-stu-id="5eb04-162">Error</span></span> | <span data-ttu-id="5eb04-163">Activity run error (if/any)</span><span class="sxs-lookup"><span data-stu-id="5eb04-163">Activity run error (if/any)</span></span> |

![Monitor activity runs](media/monitor-visually/activity-runs.png)

> [!IMPORTANT]
> <span data-ttu-id="5eb04-165">You need to click **'Refresh'** icon on top to refresh the list of pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="5eb04-165">You need to click **'Refresh'** icon on top to refresh the list of pipeline and activity runs.</span></span> <span data-ttu-id="5eb04-166">Auto-refresh is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="5eb04-166">Auto-refresh is currently not supported.</span></span>
>

![Refresh](media/monitor-visually/refresh.png)

## <a name="features"></a><span data-ttu-id="5eb04-168">Features</span><span class="sxs-lookup"><span data-stu-id="5eb04-168">Features</span></span>

#### <a name="select-a-data-factory-to-monitor"></a><span data-ttu-id="5eb04-169">Select a data factory to monitor</span><span class="sxs-lookup"><span data-stu-id="5eb04-169">Select a data factory to monitor</span></span>
<span data-ttu-id="5eb04-170">Hover on the **Data Factory** icon on the top left.</span><span class="sxs-lookup"><span data-stu-id="5eb04-170">Hover on the **Data Factory** icon on the top left.</span></span> <span data-ttu-id="5eb04-171">Click on the 'Arrow' icon to see a list of azure subscriptions and data factories that you can monitor.</span><span class="sxs-lookup"><span data-stu-id="5eb04-171">Click on the 'Arrow' icon to see a list of azure subscriptions and data factories that you can monitor.</span></span>

![Select data factory](media/monitor-visually/select-datafactory.png)

#### <a name="rich-ordering-and-filtering"></a><span data-ttu-id="5eb04-173">Rich ordering and filtering</span><span class="sxs-lookup"><span data-stu-id="5eb04-173">Rich ordering and filtering</span></span>

<span data-ttu-id="5eb04-174">Order pipeline runs in desc/asc by Run Start and filter pipeline runs by following columns:</span><span class="sxs-lookup"><span data-stu-id="5eb04-174">Order pipeline runs in desc/asc by Run Start and filter pipeline runs by following columns:</span></span>

| <span data-ttu-id="5eb04-175">**Column Name**</span><span class="sxs-lookup"><span data-stu-id="5eb04-175">**Column Name**</span></span> | <span data-ttu-id="5eb04-176">**Description**</span><span class="sxs-lookup"><span data-stu-id="5eb04-176">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5eb04-177">Pipeline Name</span><span class="sxs-lookup"><span data-stu-id="5eb04-177">Pipeline Name</span></span> | <span data-ttu-id="5eb04-178">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="5eb04-178">Name of the pipeline.</span></span> <span data-ttu-id="5eb04-179">Options include quick filters for 'Last 24 hours', 'Last week',  'Last 30 days' or select a custom date time.</span><span class="sxs-lookup"><span data-stu-id="5eb04-179">Options include quick filters for 'Last 24 hours', 'Last week',  'Last 30 days' or select a custom date time.</span></span> |
| <span data-ttu-id="5eb04-180">Run Start</span><span class="sxs-lookup"><span data-stu-id="5eb04-180">Run Start</span></span> | <span data-ttu-id="5eb04-181">Pipeline run start date time</span><span class="sxs-lookup"><span data-stu-id="5eb04-181">Pipeline run start date time</span></span> |
| <span data-ttu-id="5eb04-182">Run Status</span><span class="sxs-lookup"><span data-stu-id="5eb04-182">Run Status</span></span> | <span data-ttu-id="5eb04-183">Filter runs by status i.e. Succeeded, Failed, In Progress</span><span class="sxs-lookup"><span data-stu-id="5eb04-183">Filter runs by status i.e. Succeeded, Failed, In Progress</span></span> |

![Filter](media/monitor-visually/filter.png)

#### <a name="addremove-columns-in-list-view"></a><span data-ttu-id="5eb04-185">Add/Remove columns in list view</span><span class="sxs-lookup"><span data-stu-id="5eb04-185">Add/Remove columns in list view</span></span>
<span data-ttu-id="5eb04-186">Right click the list view header and choose columns that you want to appear in the list view</span><span class="sxs-lookup"><span data-stu-id="5eb04-186">Right click the list view header and choose columns that you want to appear in the list view</span></span>

![Columns](media/monitor-visually/columns.png)

#### <a name="reorder-column-widths-in-list-view"></a><span data-ttu-id="5eb04-188">Reorder column widths in list view</span><span class="sxs-lookup"><span data-stu-id="5eb04-188">Reorder column widths in list view</span></span>
<span data-ttu-id="5eb04-189">Increase and decrease the column widths in list view by simply hovering over the column header</span><span class="sxs-lookup"><span data-stu-id="5eb04-189">Increase and decrease the column widths in list view by simply hovering over the column header</span></span>

#### <a name="user-properties"></a><span data-ttu-id="5eb04-190">User properties</span><span class="sxs-lookup"><span data-stu-id="5eb04-190">User properties</span></span>

<span data-ttu-id="5eb04-191">You can promote any pipeline activity property as a user property so that it becomes an entity that you can monitor.</span><span class="sxs-lookup"><span data-stu-id="5eb04-191">You can promote any pipeline activity property as a user property so that it becomes an entity that you can monitor.</span></span> <span data-ttu-id="5eb04-192">For example, you can promote the **Source** and **Destination** properties of the Copy activity in your pipeline as user properties.</span><span class="sxs-lookup"><span data-stu-id="5eb04-192">For example, you can promote the **Source** and **Destination** properties of the Copy activity in your pipeline as user properties.</span></span> <span data-ttu-id="5eb04-193">You can also select **Auto Generate** to generate the **Source** and **Destination** user properties for a Copy activity.</span><span class="sxs-lookup"><span data-stu-id="5eb04-193">You can also select **Auto Generate** to generate the **Source** and **Destination** user properties for a Copy activity.</span></span>

![Create user properties](media/monitor-visually/monitor-user-properties-image1.png)

> [!NOTE]
> <span data-ttu-id="5eb04-195">You can only promote up to 5 pipeline activity properties as user properties.</span><span class="sxs-lookup"><span data-stu-id="5eb04-195">You can only promote up to 5 pipeline activity properties as user properties.</span></span>

<span data-ttu-id="5eb04-196">After you create the user properties, you can then monitor them in the monitoring list views.</span><span class="sxs-lookup"><span data-stu-id="5eb04-196">After you create the user properties, you can then monitor them in the monitoring list views.</span></span> <span data-ttu-id="5eb04-197">If the source for the Copy activity is a table name, you can monitor the source table name as a column in the activity runs list view.</span><span class="sxs-lookup"><span data-stu-id="5eb04-197">If the source for the Copy activity is a table name, you can monitor the source table name as a column in the activity runs list view.</span></span>

![Activity runs list without user properties](media/monitor-visually/monitor-user-properties-image2.png)

![Add columns for user properties to activity runs list](media/monitor-visually/monitor-user-properties-image3.png)

![Activity runs list with columns for user properties](media/monitor-visually/monitor-user-properties-image4.png)

#### <a name="guided-tours"></a><span data-ttu-id="5eb04-201">Guided Tours</span><span class="sxs-lookup"><span data-stu-id="5eb04-201">Guided Tours</span></span>
<span data-ttu-id="5eb04-202">Click on the 'Information Icon' in lower left and click 'Guided Tours' to get step-by-step instructions on how to monitor your pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="5eb04-202">Click on the 'Information Icon' in lower left and click 'Guided Tours' to get step-by-step instructions on how to monitor your pipeline and activity runs.</span></span>

![Guided tours](media/monitor-visually/guided-tours.png)

#### <a name="feedback"></a><span data-ttu-id="5eb04-204">Feedback</span><span class="sxs-lookup"><span data-stu-id="5eb04-204">Feedback</span></span>
<span data-ttu-id="5eb04-205">Click on the 'Feedback' icon to give us feedback on various features or any issues that you might be facing.</span><span class="sxs-lookup"><span data-stu-id="5eb04-205">Click on the 'Feedback' icon to give us feedback on various features or any issues that you might be facing.</span></span>

![Feedback](media/monitor-visually/feedback.png)

## <a name="next-steps"></a><span data-ttu-id="5eb04-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="5eb04-207">Next steps</span></span>

<span data-ttu-id="5eb04-208">See  [Monitor and manage pipelines programmatically](https://docs.microsoft.com/azure/data-factory/monitor-programmatically) article to learn about monitoring and managing pipelines</span><span class="sxs-lookup"><span data-stu-id="5eb04-208">See  [Monitor and manage pipelines programmatically](https://docs.microsoft.com/azure/data-factory/monitor-programmatically) article to learn about monitoring and managing pipelines</span></span>
