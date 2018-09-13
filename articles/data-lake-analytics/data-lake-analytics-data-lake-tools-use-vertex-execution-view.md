---
title: Use the Vertex Execution View in Data Lake Tools for Visual Studio | Microsoft Docs
description: Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.
services: data-lake-analytics
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: 4a637a1f3a50caa82b984864b61da8e18a131254
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564610"
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="eecd8-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eecd8-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="eecd8-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="eecd8-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eecd8-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eecd8-105">Prerequisites</span></span>
* <span data-ttu-id="eecd8-106">Some basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="eecd8-106">Some basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="eecd8-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="eecd8-108">Open the Vertex Execution View</span><span class="sxs-lookup"><span data-stu-id="eecd8-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="eecd8-109">For a certain job, you can click the “Vertex Execution View” link in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="eecd8-109">For a certain job, you can click the “Vertex Execution View” link in the bottom left corner.</span></span> <span data-ttu-id="eecd8-110">You might be prompted to load profiles first and it can take some time depending on your network connectivity.</span><span class="sxs-lookup"><span data-stu-id="eecd8-110">You might be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics Tools Vertex Execution View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="eecd8-112">Understand Vertex Execution View</span><span class="sxs-lookup"><span data-stu-id="eecd8-112">Understand Vertex Execution View</span></span>
<span data-ttu-id="eecd8-113">After entering the Vertex Execution View, there are three parts:</span><span class="sxs-lookup"><span data-stu-id="eecd8-113">After entering the Vertex Execution View, there are three parts:</span></span>

![Data Lake Analytics Tools Vertex Execution View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

* <span data-ttu-id="eecd8-115">Vertex selector: On the left is the Vertex selector.</span><span class="sxs-lookup"><span data-stu-id="eecd8-115">Vertex selector: On the left is the Vertex selector.</span></span>  <span data-ttu-id="eecd8-116">You can select the vertices by features (such as top 10 data read, or choose by stage).</span><span class="sxs-lookup"><span data-stu-id="eecd8-116">You can select the vertices by features (such as top 10 data read, or choose by stage).</span></span>
  
    <span data-ttu-id="eecd8-117">One of the most common used filters is the vertices on critical path.</span><span class="sxs-lookup"><span data-stu-id="eecd8-117">One of the most common used filters is the vertices on critical path.</span></span> <span data-ttu-id="eecd8-118">Critical path is the longest path of a U-SQL job.</span><span class="sxs-lookup"><span data-stu-id="eecd8-118">Critical path is the longest path of a U-SQL job.</span></span> <span data-ttu-id="eecd8-119">It is useful for optimizing your jobs by checking which vertex takes the longest time.</span><span class="sxs-lookup"><span data-stu-id="eecd8-119">It is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
* <span data-ttu-id="eecd8-120">The top center pane:</span><span class="sxs-lookup"><span data-stu-id="eecd8-120">The top center pane:</span></span>
  
    ![Data Lake Analytics Tools Vertex Execution View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)
  
    <span data-ttu-id="eecd8-122">This view also shows the running status of all the vertices.</span><span class="sxs-lookup"><span data-stu-id="eecd8-122">This view also shows the running status of all the vertices.</span></span> <span data-ttu-id="eecd8-123">It converts the time accordingly to your local machine, and shows different status in different colors.</span><span class="sxs-lookup"><span data-stu-id="eecd8-123">It converts the time accordingly to your local machine, and shows different status in different colors.</span></span>
* <span data-ttu-id="eecd8-124">The bottom center pane:</span><span class="sxs-lookup"><span data-stu-id="eecd8-124">The bottom center pane:</span></span>
  
    ![Data Lake Analytics Tools Vertex Execution View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)
  
  * <span data-ttu-id="eecd8-126">Process Name: The name of the vertex instance.</span><span class="sxs-lookup"><span data-stu-id="eecd8-126">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="eecd8-127">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="eecd8-127">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="eecd8-128">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="eecd8-128">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
  * <span data-ttu-id="eecd8-129">Total Data Read/Written: The data was read/written by this vertex.</span><span class="sxs-lookup"><span data-stu-id="eecd8-129">Total Data Read/Written: The data was read/written by this vertex.</span></span>
  * <span data-ttu-id="eecd8-130">State/Exit Status: The final status when the vertex is ended.</span><span class="sxs-lookup"><span data-stu-id="eecd8-130">State/Exit Status: The final status when the vertex is ended.</span></span>
  * <span data-ttu-id="eecd8-131">Exit Code/Failure Type: The error when the vertex failed.</span><span class="sxs-lookup"><span data-stu-id="eecd8-131">Exit Code/Failure Type: The error when the vertex failed.</span></span>
  * <span data-ttu-id="eecd8-132">Creation Reason: Why the vertex was created.</span><span class="sxs-lookup"><span data-stu-id="eecd8-132">Creation Reason: Why the vertex was created.</span></span>
  * <span data-ttu-id="eecd8-133">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span><span class="sxs-lookup"><span data-stu-id="eecd8-133">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
  * <span data-ttu-id="eecd8-134">Process/Creator GUID: GUID for the current running vertex or its creator.</span><span class="sxs-lookup"><span data-stu-id="eecd8-134">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
  * <span data-ttu-id="eecd8-135">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span><span class="sxs-lookup"><span data-stu-id="eecd8-135">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
  * <span data-ttu-id="eecd8-136">Version Created Time.</span><span class="sxs-lookup"><span data-stu-id="eecd8-136">Version Created Time.</span></span>
  * <span data-ttu-id="eecd8-137">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span><span class="sxs-lookup"><span data-stu-id="eecd8-137">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eecd8-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="eecd8-138">Next steps</span></span>
* <span data-ttu-id="eecd8-139">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-139">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="eecd8-140">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-140">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="eecd8-141">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-141">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="eecd8-142">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-142">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="eecd8-143">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="eecd8-143">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="eecd8-144">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-144">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="eecd8-145">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="eecd8-145">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
* <span data-ttu-id="eecd8-146">To learn Data Lake Tools for Visual Studio code, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="eecd8-146">To learn Data Lake Tools for Visual Studio code, see [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>




