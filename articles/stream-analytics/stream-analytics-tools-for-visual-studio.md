---
title: Use Azure Stream Analytics Tools for Visual Studio | Microsoft Docs
description: Getting-started tutorial for the Azure Stream Analytics Tools for Visual Studio
keywords: visual studio
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: sujie
ms.openlocfilehash: a5042bd4c6b0b30a0f6c52135ffcce90d038dabc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549117"
---
# <a name="use-azure-stream-analytics-tool-for-visual-studio"></a><span data-ttu-id="e504c-104">Use Azure Stream Analytics Tool for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e504c-104">Use Azure Stream Analytics Tool for Visual Studio</span></span>
<span data-ttu-id="e504c-105">Azure Stream Analytics tools for Visual Studio are now generally available.</span><span class="sxs-lookup"><span data-stu-id="e504c-105">Azure Stream Analytics tools for Visual Studio are now generally available.</span></span> <span data-ttu-id="e504c-106">These tools enable a richer experience for Stream Analytics user to troubleshoot as well as write complex queries and even write queries locally.</span><span class="sxs-lookup"><span data-stu-id="e504c-106">These tools enable a richer experience for Stream Analytics user to troubleshoot as well as write complex queries and even write queries locally.</span></span> <span data-ttu-id="e504c-107">You will also have the ability to export a Stream Analytics job into a Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="e504c-107">You will also have the ability to export a Stream Analytics job into a Visual Studio project.</span></span>

## <a name="introduction"></a><span data-ttu-id="e504c-108">Introduction</span><span class="sxs-lookup"><span data-stu-id="e504c-108">Introduction</span></span>
<span data-ttu-id="e504c-109">In this tutorial, you will learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage and debug your Azure Stream Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="e504c-109">In this tutorial, you will learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage and debug your Azure Stream Analytics jobs.</span></span> 

<span data-ttu-id="e504c-110">After completing this tutorial, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="e504c-110">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="e504c-111">Familiarize yourself with the Azure Stream Analytics Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e504c-111">Familiarize yourself with the Azure Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="e504c-112">Configure and deploy a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="e504c-112">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="e504c-113">Test your job locally with local sample data.</span><span class="sxs-lookup"><span data-stu-id="e504c-113">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="e504c-114">Use the monitoring to troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="e504c-114">Use the monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="e504c-115">Export existing jobs to projects.</span><span class="sxs-lookup"><span data-stu-id="e504c-115">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e504c-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e504c-116">Prerequisites</span></span>
<span data-ttu-id="e504c-117">You will need the following prerequisites to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="e504c-117">You will need the following prerequisites to complete this tutorial:</span></span>
* <span data-ttu-id="e504c-118">Finish the steps before **Create a Stream Analytics job** from the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="e504c-118">Finish the steps before **Create a Stream Analytics job** from the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="e504c-119">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="e504c-119">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="e504c-120">Enterprise (Ultimate/Premium), Professional, Community editions are supported; Express edition is not supported.</span><span class="sxs-lookup"><span data-stu-id="e504c-120">Enterprise (Ultimate/Premium), Professional, Community editions are supported; Express edition is not supported.</span></span> <span data-ttu-id="e504c-121">Visual Studio 2017 is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="e504c-121">Visual Studio 2017 is currently not supported.</span></span> 
* <span data-ttu-id="e504c-122">Microsoft Azure SDK for .NET version 2.7.1 or above.</span><span class="sxs-lookup"><span data-stu-id="e504c-122">Microsoft Azure SDK for .NET version 2.7.1 or above.</span></span>  <span data-ttu-id="e504c-123">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="e504c-123">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="e504c-124">Installation of [Azure Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="e504c-124">Installation of [Azure Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="e504c-125">Create a Stream Analytics Project</span><span class="sxs-lookup"><span data-stu-id="e504c-125">Create a Stream Analytics Project</span></span>
<span data-ttu-id="e504c-126">In Visual Studio, click the **File Menu** and choose **New Project**.</span><span class="sxs-lookup"><span data-stu-id="e504c-126">In Visual Studio, click the **File Menu** and choose **New Project**.</span></span> <span data-ttu-id="e504c-127">Choose **Stream Analytics** from the templates list on the left and then click **Azure Stream Analytics Application**.</span><span class="sxs-lookup"><span data-stu-id="e504c-127">Choose **Stream Analytics** from the templates list on the left and then click **Azure Stream Analytics Application**.</span></span>
<span data-ttu-id="e504c-128">Input the Project Name, Location and Solution name at the bottom as you do for other projects.</span><span class="sxs-lookup"><span data-stu-id="e504c-128">Input the Project Name, Location and Solution name at the bottom as you do for other projects.</span></span>

![Create an Azure Stream Analytics project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

<span data-ttu-id="e504c-130">You will see a project **Toll** generated in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e504c-130">You will see a project **Toll** generated in **Solution Explorer**.</span></span>

![Create an Azure Stream Analytics project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="e504c-132">Choose the correct Subscription</span><span class="sxs-lookup"><span data-stu-id="e504c-132">Choose the correct Subscription</span></span>
1. <span data-ttu-id="e504c-133">Open **Server Explorer** in Visual Studio from **View** menu.</span><span class="sxs-lookup"><span data-stu-id="e504c-133">Open **Server Explorer** in Visual Studio from **View** menu.</span></span>
2. <span data-ttu-id="e504c-134">Log in with your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="e504c-134">Log in with your Azure Account.</span></span> 

## <a name="define-input-sources"></a><span data-ttu-id="e504c-135">Define input sources</span><span class="sxs-lookup"><span data-stu-id="e504c-135">Define input sources</span></span>
1.  <span data-ttu-id="e504c-136">In **Solution Explorer**, expand **Inputs** node and rename **Input.json** to **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="e504c-136">In **Solution Explorer**, expand **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="e504c-137">Double-click **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="e504c-137">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="e504c-138">Your **INPUT ALIAS** now should be **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="e504c-138">Your **INPUT ALIAS** now should be **EntryStream**.</span></span> <span data-ttu-id="e504c-139">Please note that input alias is the one will be used in query script.</span><span class="sxs-lookup"><span data-stu-id="e504c-139">Please note that input alias is the one will be used in query script.</span></span> 
3.  <span data-ttu-id="e504c-140">Source Type is **Data Stream**.</span><span class="sxs-lookup"><span data-stu-id="e504c-140">Source Type is **Data Stream**.</span></span>
4.  <span data-ttu-id="e504c-141">Source is **Event hub**.</span><span class="sxs-lookup"><span data-stu-id="e504c-141">Source is **Event hub**.</span></span>
5.  <span data-ttu-id="e504c-142">Service Bus Namescape should be the **tollData** one in the drop-down.</span><span class="sxs-lookup"><span data-stu-id="e504c-142">Service Bus Namescape should be the **tollData** one in the drop-down.</span></span>
6.  <span data-ttu-id="e504c-143">Event hub name should be set to **entry**.</span><span class="sxs-lookup"><span data-stu-id="e504c-143">Event hub name should be set to **entry**.</span></span>
7.  <span data-ttu-id="e504c-144">Event hub policy name is **RootManageSharedAccessKey** (the default value).</span><span class="sxs-lookup"><span data-stu-id="e504c-144">Event hub policy name is **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="e504c-145">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span><span class="sxs-lookup"><span data-stu-id="e504c-145">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span></span>
   
   <span data-ttu-id="e504c-146">Your settings will look like:</span><span class="sxs-lookup"><span data-stu-id="e504c-146">Your settings will look like:</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
   
9.  <span data-ttu-id="e504c-148">Click **Save** at the bottom of the page to finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="e504c-148">Click **Save** at the bottom of the page to finish the wizard.</span></span> <span data-ttu-id="e504c-149">Now you can add another input source to create the exit stream.</span><span class="sxs-lookup"><span data-stu-id="e504c-149">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="e504c-150">Right-click the inputs node and click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="e504c-150">Right-click the inputs node and click **New Item**.</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
   
10. <span data-ttu-id="e504c-152">In the popped up window, choose **Azure Stream Analytics Input** and change the Name to **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="e504c-152">In the popped up window, choose **Azure Stream Analytics Input** and change the Name to **ExitStream.json**.</span></span> <span data-ttu-id="e504c-153">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="e504c-153">Click **Add**.</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
   
11. <span data-ttu-id="e504c-155">Double-click **ExitStream.json** in the project and follow the same steps as the entry stream to fill in.</span><span class="sxs-lookup"><span data-stu-id="e504c-155">Double-click **ExitStream.json** in the project and follow the same steps as the entry stream to fill in.</span></span> <span data-ttu-id="e504c-156">Be sure to enter values for Event Hub name as on the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="e504c-156">Be sure to enter values for Event Hub name as on the following screenshot.</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)
   
   <span data-ttu-id="e504c-158">Now you have defined two input streams.</span><span class="sxs-lookup"><span data-stu-id="e504c-158">Now you have defined two input streams.</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
   
   <span data-ttu-id="e504c-160">Next, you will add reference data input for the blob file that contains car registration data.</span><span class="sxs-lookup"><span data-stu-id="e504c-160">Next, you will add reference data input for the blob file that contains car registration data.</span></span>
   
12. <span data-ttu-id="e504c-161">Right-click the **Inputs** node in the project, and then follow the same process for the stream inputs but select **REFERENCE DATA** instead of Data Stream and the Input Alias is **Registration**.</span><span class="sxs-lookup"><span data-stu-id="e504c-161">Right-click the **Inputs** node in the project, and then follow the same process for the stream inputs but select **REFERENCE DATA** instead of Data Stream and the Input Alias is **Registration**.</span></span>
   
   ![Define input sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)
   
13. <span data-ttu-id="e504c-163">Select Storage account that contains with **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="e504c-163">Select Storage account that contains with **tolldata**.</span></span> <span data-ttu-id="e504c-164">The container name should be **tolldata**, and the **PATH PATTERN** should be **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="e504c-164">The container name should be **tolldata**, and the **PATH PATTERN** should be **registration.json**.</span></span> <span data-ttu-id="e504c-165">This file name is case-sensitive and should be lowercase.</span><span class="sxs-lookup"><span data-stu-id="e504c-165">This file name is case-sensitive and should be lowercase.</span></span>
14. <span data-ttu-id="e504c-166">Click **Save** to finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="e504c-166">Click **Save** to finish the wizard.</span></span>

<span data-ttu-id="e504c-167">Now all inputs are defined.</span><span class="sxs-lookup"><span data-stu-id="e504c-167">Now all inputs are defined.</span></span>

## <a name="define-output"></a><span data-ttu-id="e504c-168">Define output</span><span class="sxs-lookup"><span data-stu-id="e504c-168">Define output</span></span>
1.  <span data-ttu-id="e504c-169">In **Solution Explorer**, expand **Inputs** node and double-click **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="e504c-169">In **Solution Explorer**, expand **Inputs** node and double-click **Output.json**.</span></span>
2.  <span data-ttu-id="e504c-170">Set the Output alias to **output** and then Sink to SQL database.</span><span class="sxs-lookup"><span data-stu-id="e504c-170">Set the Output alias to **output** and then Sink to SQL database.</span></span>
2.  <span data-ttu-id="e504c-171">Enter the database name: **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="e504c-171">Enter the database name: **TollDataDB**.</span></span>
3.  <span data-ttu-id="e504c-172">Enter **tolladmin** in the **USERNAME** field, **123toll!**</span><span class="sxs-lookup"><span data-stu-id="e504c-172">Enter **tolladmin** in the **USERNAME** field, **123toll!**</span></span> <span data-ttu-id="e504c-173">in the **PASSWORD** field, and **TollDataRefJoin** in the **TABLE** field.</span><span class="sxs-lookup"><span data-stu-id="e504c-173">in the **PASSWORD** field, and **TollDataRefJoin** in the **TABLE** field.</span></span>
4.  <span data-ttu-id="e504c-174">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e504c-174">Click **Save**.</span></span>

![Define output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="azure-stream-analytics-query"></a><span data-ttu-id="e504c-176">Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="e504c-176">Azure Stream Analytics Query</span></span>
<span data-ttu-id="e504c-177">This tutorial attempts to answer several business questions that are related to toll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics to provide a relevant answer.</span><span class="sxs-lookup"><span data-stu-id="e504c-177">This tutorial attempts to answer several business questions that are related to toll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics to provide a relevant answer.</span></span>
<span data-ttu-id="e504c-178">Before you start your first Stream Analytics job, let’s explore a simple scenarios and the query syntax.</span><span class="sxs-lookup"><span data-stu-id="e504c-178">Before you start your first Stream Analytics job, let’s explore a simple scenarios and the query syntax.</span></span>

### <a name="introduction-to-azure-stream-analytics-query-language"></a><span data-ttu-id="e504c-179">Introduction to Azure Stream Analytics query language</span><span class="sxs-lookup"><span data-stu-id="e504c-179">Introduction to Azure Stream Analytics query language</span></span>
<span data-ttu-id="e504c-180">Let’s say that you need to count the number of vehicles that enter a toll booth.</span><span class="sxs-lookup"><span data-stu-id="e504c-180">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="e504c-181">Because this is a continuous stream of events, you have to define a “period of time.”</span><span class="sxs-lookup"><span data-stu-id="e504c-181">Because this is a continuous stream of events, you have to define a “period of time.”</span></span> <span data-ttu-id="e504c-182">Let's modify the question to be “How many vehicles enter a toll booth every three minutes?”.</span><span class="sxs-lookup"><span data-stu-id="e504c-182">Let's modify the question to be “How many vehicles enter a toll booth every three minutes?”.</span></span> <span data-ttu-id="e504c-183">This is commonly referred to as the tumbling count.</span><span class="sxs-lookup"><span data-stu-id="e504c-183">This is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="e504c-184">Let’s look at the Azure Stream Analytics query that answers this question:</span><span class="sxs-lookup"><span data-stu-id="e504c-184">Let’s look at the Azure Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="e504c-185">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span><span class="sxs-lookup"><span data-stu-id="e504c-185">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="e504c-186">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span><span class="sxs-lookup"><span data-stu-id="e504c-186">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="e504c-187">Now that you have written your first Azure Stream Analytics query, it is time to test it by using sample data files located in your TollApp folder in the following path:</span><span class="sxs-lookup"><span data-stu-id="e504c-187">Now that you have written your first Azure Stream Analytics query, it is time to test it by using sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="e504c-188">**..\TollApp\TollApp\Data**</span><span class="sxs-lookup"><span data-stu-id="e504c-188">**..\TollApp\TollApp\Data**</span></span>

<span data-ttu-id="e504c-189">This folder contains the following files: •   Entry.json •   Exit.json •   Registration.json</span><span class="sxs-lookup"><span data-stu-id="e504c-189">This folder contains the following files: •   Entry.json •   Exit.json •   Registration.json</span></span>

## <a name="question-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="e504c-190">Question: Number of vehicles entering a toll booth</span><span class="sxs-lookup"><span data-stu-id="e504c-190">Question: Number of vehicles entering a toll booth</span></span>
<span data-ttu-id="e504c-191">In the project, double-click Script.asaql to open the script in editor and paste the script in previous section into the editor.</span><span class="sxs-lookup"><span data-stu-id="e504c-191">In the project, double-click Script.asaql to open the script in editor and paste the script in previous section into the editor.</span></span> <span data-ttu-id="e504c-192">The query editor supports Intellisense, syntax coloring and Error marker.</span><span class="sxs-lookup"><span data-stu-id="e504c-192">The query editor supports Intellisense, syntax coloring and Error marker.</span></span>

![Edit query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="testing-azure-stream-analytics-queries-locally"></a><span data-ttu-id="e504c-194">Testing Azure Stream Analytics queries locally</span><span class="sxs-lookup"><span data-stu-id="e504c-194">Testing Azure Stream Analytics queries locally</span></span>

1. <span data-ttu-id="e504c-195">You can first compile the query to see if there is any syntax error.</span><span class="sxs-lookup"><span data-stu-id="e504c-195">You can first compile the query to see if there is any syntax error.</span></span> <span data-ttu-id="e504c-196">[TBD]</span><span class="sxs-lookup"><span data-stu-id="e504c-196">[TBD]</span></span>
2. <span data-ttu-id="e504c-197">To validate this query against sample data, you can use local sample data by right-clicking the input and select **Add local input** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="e504c-197">To validate this query against sample data, you can use local sample data by right-clicking the input and select **Add local input** from the context menu.</span></span>
   
   ![Add local input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
   
   <span data-ttu-id="e504c-199">In the pop-up window select the sample data from your local path.</span><span class="sxs-lookup"><span data-stu-id="e504c-199">In the pop-up window select the sample data from your local path.</span></span> <span data-ttu-id="e504c-200">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e504c-200">Click **Save**.</span></span>
   
   ![Add local input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
   
   <span data-ttu-id="e504c-202">A file named **local_EntryStream.json** will be added automatically to your inputs folder.</span><span class="sxs-lookup"><span data-stu-id="e504c-202">A file named **local_EntryStream.json** will be added automatically to your inputs folder.</span></span>
   
   ![Add local input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
   
3. <span data-ttu-id="e504c-204">Click Run Locally in query editor.</span><span class="sxs-lookup"><span data-stu-id="e504c-204">Click Run Locally in query editor.</span></span> <span data-ttu-id="e504c-205">Or you can press F5.</span><span class="sxs-lookup"><span data-stu-id="e504c-205">Or you can press F5.</span></span>
   
   ![Local run](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)
   
   <span data-ttu-id="e504c-207">You can find output path from console output and press any key to open the result folder.</span><span class="sxs-lookup"><span data-stu-id="e504c-207">You can find output path from console output and press any key to open the result folder.</span></span>
   
   ![Local run](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)
   
4. <span data-ttu-id="e504c-209">Check result in local folder.</span><span class="sxs-lookup"><span data-stu-id="e504c-209">Check result in local folder.</span></span>
   
   ![Local run](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-03.png)
   
   
### <a name="sample-input"></a><span data-ttu-id="e504c-211">Sample input</span><span class="sxs-lookup"><span data-stu-id="e504c-211">Sample input</span></span>
<span data-ttu-id="e504c-212">You can also sample input data from input sources to local file.</span><span class="sxs-lookup"><span data-stu-id="e504c-212">You can also sample input data from input sources to local file.</span></span> <span data-ttu-id="e504c-213">Right-click the input config file and select **Sample Data**.</span><span class="sxs-lookup"><span data-stu-id="e504c-213">Right-click the input config file and select **Sample Data**.</span></span> 

![Sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

<span data-ttu-id="e504c-215">Please note that you can only sample Event Hub or IoT Hub for now.</span><span class="sxs-lookup"><span data-stu-id="e504c-215">Please note that you can only sample Event Hub or IoT Hub for now.</span></span> <span data-ttu-id="e504c-216">Other input sources are not supported.</span><span class="sxs-lookup"><span data-stu-id="e504c-216">Other input sources are not supported.</span></span>  <span data-ttu-id="e504c-217">In the pop-up dialog window, please fill in the local path for saving the sample data.</span><span class="sxs-lookup"><span data-stu-id="e504c-217">In the pop-up dialog window, please fill in the local path for saving the sample data.</span></span> <span data-ttu-id="e504c-218">Click **Sample**.</span><span class="sxs-lookup"><span data-stu-id="e504c-218">Click **Sample**.</span></span>

![Sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
<span data-ttu-id="e504c-220">You can see the progress in the Output window.</span><span class="sxs-lookup"><span data-stu-id="e504c-220">You can see the progress in the Output window.</span></span> 

![Sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-azure-stream-analytics-query-to-azure"></a><span data-ttu-id="e504c-222">Submit Azure Stream Analytics query to Azure</span><span class="sxs-lookup"><span data-stu-id="e504c-222">Submit Azure Stream Analytics query to Azure</span></span>
<span data-ttu-id="e504c-223">In **Query Editor**, click **Submit To Azure in script editor**.</span><span class="sxs-lookup"><span data-stu-id="e504c-223">In **Query Editor**, click **Submit To Azure in script editor**.</span></span>

![Submit job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
<span data-ttu-id="e504c-225">Choose Create a New Azure Stream Analytics Job.</span><span class="sxs-lookup"><span data-stu-id="e504c-225">Choose Create a New Azure Stream Analytics Job.</span></span> <span data-ttu-id="e504c-226">Input Job Name as below.</span><span class="sxs-lookup"><span data-stu-id="e504c-226">Input Job Name as below.</span></span> <span data-ttu-id="e504c-227">Choose the correct Subscription.</span><span class="sxs-lookup"><span data-stu-id="e504c-227">Choose the correct Subscription.</span></span> <span data-ttu-id="e504c-228">Click Submit.</span><span class="sxs-lookup"><span data-stu-id="e504c-228">Click Submit.</span></span>

![Submit job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-job"></a><span data-ttu-id="e504c-230">Start Job</span><span class="sxs-lookup"><span data-stu-id="e504c-230">Start Job</span></span>
<span data-ttu-id="e504c-231">Now your job has been created and job view is automatically opened.</span><span class="sxs-lookup"><span data-stu-id="e504c-231">Now your job has been created and job view is automatically opened.</span></span> <span data-ttu-id="e504c-232">Click the **GREEN** button to start the job.</span><span class="sxs-lookup"><span data-stu-id="e504c-232">Click the **GREEN** button to start the job.</span></span>

![Start job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
<span data-ttu-id="e504c-234">Choose the default setting and click **Start**.</span><span class="sxs-lookup"><span data-stu-id="e504c-234">Choose the default setting and click **Start**.</span></span>
 
![Start job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

<span data-ttu-id="e504c-236">You can see the job status has changed to **Running** and there are input/output events.</span><span class="sxs-lookup"><span data-stu-id="e504c-236">You can see the job status has changed to **Running** and there are input/output events.</span></span>

![Start job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-results-in-visual-studio"></a><span data-ttu-id="e504c-238">Check results in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e504c-238">Check results in Visual Studio</span></span>
1. <span data-ttu-id="e504c-239">Open Visual Studio Server Explorer, and right-click the **TollDataRefJoin** table.</span><span class="sxs-lookup"><span data-stu-id="e504c-239">Open Visual Studio Server Explorer, and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="e504c-240">Click **Show Table Data** to see the output of your job.</span><span class="sxs-lookup"><span data-stu-id="e504c-240">Click **Show Table Data** to see the output of your job.</span></span>
   
   ![Selection of "Show Table Data" in Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)
   

### <a name="view-job-metrics"></a><span data-ttu-id="e504c-242">View job metrics</span><span class="sxs-lookup"><span data-stu-id="e504c-242">View job metrics</span></span>
<span data-ttu-id="e504c-243">Some basic job statistics can be found in **Job Metrics**.</span><span class="sxs-lookup"><span data-stu-id="e504c-243">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Job metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-job-in-server-explorer"></a><span data-ttu-id="e504c-245">List job in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="e504c-245">List job in Server Explorer</span></span>
<span data-ttu-id="e504c-246">Click **Stream Analytics Jobs** in **Server Explorer** and click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="e504c-246">Click **Stream Analytics Jobs** in **Server Explorer** and click **Refresh**.</span></span> <span data-ttu-id="e504c-247">You should be able to see your job appeared under **Stream Analytics Jobs**.</span><span class="sxs-lookup"><span data-stu-id="e504c-247">You should be able to see your job appeared under **Stream Analytics Jobs**.</span></span>

![List jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-job-view"></a><span data-ttu-id="e504c-249">Open job view</span><span class="sxs-lookup"><span data-stu-id="e504c-249">Open job view</span></span>
<span data-ttu-id="e504c-250">Expand your job node and double-click on the **Job View** node to open job view.</span><span class="sxs-lookup"><span data-stu-id="e504c-250">Expand your job node and double-click on the **Job View** node to open job view.</span></span>

![Job view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="e504c-252">Export an existing job to a project</span><span class="sxs-lookup"><span data-stu-id="e504c-252">Export an existing job to a project</span></span>
<span data-ttu-id="e504c-253">There are two ways you can export an existing job to a project.</span><span class="sxs-lookup"><span data-stu-id="e504c-253">There are two ways you can export an existing job to a project.</span></span>
1. <span data-ttu-id="e504c-254">Right-click the job node under **Stream Analytics Jobs** node in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e504c-254">Right-click the job node under **Stream Analytics Jobs** node in **Server Explorer**.</span></span> <span data-ttu-id="e504c-255">Click **Export to New Stream Analytics Project** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="e504c-255">Click **Export to New Stream Analytics Project** from the context menu.</span></span>
   
   ![Export job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)
   
   <span data-ttu-id="e504c-257">You will see the generated project in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e504c-257">You will see the generated project in **Solution Explorer**.</span></span>
   
   ![Export job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
   
2. <span data-ttu-id="e504c-259">In job view, click **Generate Project**.</span><span class="sxs-lookup"><span data-stu-id="e504c-259">In job view, click **Generate Project**.</span></span>
   
   ![Export job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)
   
## <a name="known-issues-and-limitations"></a><span data-ttu-id="e504c-261">Known Issues and Limitations</span><span class="sxs-lookup"><span data-stu-id="e504c-261">Known Issues and Limitations</span></span>
 
1. <span data-ttu-id="e504c-262">Local testing does not work if your query has Geo-Spatial functions.</span><span class="sxs-lookup"><span data-stu-id="e504c-262">Local testing does not work if your query has Geo-Spatial functions.</span></span> 
2. <span data-ttu-id="e504c-263">No editor support for adding or changing JavaScript UDF.</span><span class="sxs-lookup"><span data-stu-id="e504c-263">No editor support for adding or changing JavaScript UDF.</span></span>
3. <span data-ttu-id="e504c-264">Local testing does not support saving output in JSON format.</span><span class="sxs-lookup"><span data-stu-id="e504c-264">Local testing does not support saving output in JSON format.</span></span> 
4. <span data-ttu-id="e504c-265">No support for Power BI output and ADLS output.</span><span class="sxs-lookup"><span data-stu-id="e504c-265">No support for Power BI output and ADLS output.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e504c-266">Next steps</span><span class="sxs-lookup"><span data-stu-id="e504c-266">Next steps</span></span>
* [<span data-ttu-id="e504c-267">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e504c-267">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e504c-268">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e504c-268">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="e504c-269">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="e504c-269">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e504c-270">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="e504c-270">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e504c-271">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="e504c-271">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

































