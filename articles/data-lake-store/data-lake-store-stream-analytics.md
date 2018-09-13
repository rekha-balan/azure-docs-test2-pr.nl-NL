---
title: Stream data from Stream Analytics into Data Lake Store | Microsoft Docs
description: Use Azure Stream Analytics to stream data into Azure Data Lake Store
services: data-lake-store,stream-analytics
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 67d840d64d4fcfdce62df3d940ce633abe681b3e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553453"
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="a97d8-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a97d8-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="a97d8-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="a97d8-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="a97d8-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span><span class="sxs-lookup"><span data-stu-id="a97d8-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="a97d8-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a97d8-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a97d8-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="a97d8-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a97d8-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a97d8-108">Prerequisites</span></span>
<span data-ttu-id="a97d8-109">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="a97d8-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="a97d8-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-110">**An Azure subscription**.</span></span> <span data-ttu-id="a97d8-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a97d8-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a97d8-112">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-112">**Azure Storage account**.</span></span> <span data-ttu-id="a97d8-113">You will use a blob container from this account to input data for a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="a97d8-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="a97d8-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="a97d8-115">Once you have created the container, upload a sample data file to it.</span><span class="sxs-lookup"><span data-stu-id="a97d8-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="a97d8-116">**Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="a97d8-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a97d8-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="a97d8-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="a97d8-119">Create a Stream Analytics Job</span><span class="sxs-lookup"><span data-stu-id="a97d8-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="a97d8-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span><span class="sxs-lookup"><span data-stu-id="a97d8-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="a97d8-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a97d8-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="a97d8-122">Sign on to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a97d8-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a97d8-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="a97d8-124">![Create a Stream Analytics Job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-124">![Create a Stream Analytics Job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="a97d8-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span><span class="sxs-lookup"><span data-stu-id="a97d8-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="a97d8-126">Create a Blob input for the job</span><span class="sxs-lookup"><span data-stu-id="a97d8-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="a97d8-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="a97d8-128">![Add an input to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-128">![Add an input to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="a97d8-129">On the **New input** blade, provide the following values.</span><span class="sxs-lookup"><span data-stu-id="a97d8-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="a97d8-130">![Add an input to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-130">![Add an input to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="a97d8-131">For **Input alias**, enter a unique name for the job input.</span><span class="sxs-lookup"><span data-stu-id="a97d8-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="a97d8-132">For **Source type**, select **Data stream**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="a97d8-133">For **Source**, select **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="a97d8-134">For **Subscription**, select **Use blob storage from current subscription**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="a97d8-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="a97d8-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="a97d8-136">For **Container**, select the container that you created in the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="a97d8-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="a97d8-137">For **Event serialization format**, select **CSV**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="a97d8-138">For **Delimiter**, select **tab**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="a97d8-139">For **Encoding**, select **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="a97d8-140">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-140">Click **Create**.</span></span> <span data-ttu-id="a97d8-141">The portal now adds the input and tests the connection to it.</span><span class="sxs-lookup"><span data-stu-id="a97d8-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="a97d8-142">Create a Data Lake Store output for the job</span><span class="sxs-lookup"><span data-stu-id="a97d8-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="a97d8-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="a97d8-144">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-144">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="a97d8-145">On the **New output** blade, provide the following values.</span><span class="sxs-lookup"><span data-stu-id="a97d8-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="a97d8-146">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-146">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="a97d8-147">For **Output alias**, enter a a unique name for the job output.</span><span class="sxs-lookup"><span data-stu-id="a97d8-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="a97d8-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a97d8-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="a97d8-149">For **Sink**, select **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="a97d8-150">You will be prompted to authorize access to Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a97d8-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="a97d8-151">Click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="a97d8-152">On the **New output** blade, continue to provide the following values.</span><span class="sxs-lookup"><span data-stu-id="a97d8-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="a97d8-153">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-153">![Add an output to your job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="a97d8-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span><span class="sxs-lookup"><span data-stu-id="a97d8-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="a97d8-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a97d8-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="a97d8-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span><span class="sxs-lookup"><span data-stu-id="a97d8-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="a97d8-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span><span class="sxs-lookup"><span data-stu-id="a97d8-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="a97d8-158">For **Event serialization format**, select **CSV**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="a97d8-159">For **Delimiter**, select **tab**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="a97d8-160">For **Encoding**, select **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="a97d8-161">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-161">Click **Create**.</span></span> <span data-ttu-id="a97d8-162">The portal now adds the output and tests the connection to it.</span><span class="sxs-lookup"><span data-stu-id="a97d8-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="a97d8-163">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="a97d8-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="a97d8-164">To run a Stream Analytics job, you must run a query from the **Query** tab. For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span><span class="sxs-lookup"><span data-stu-id="a97d8-164">To run a Stream Analytics job, you must run a query from the **Query** tab. For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="a97d8-165">![Run query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.png "Run query")</span><span class="sxs-lookup"><span data-stu-id="a97d8-165">![Run query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="a97d8-166">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-166">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="a97d8-167">From the dialog box, select **Custom Time**, and then set the current date and time.</span><span class="sxs-lookup"><span data-stu-id="a97d8-167">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="a97d8-168">![Set job time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span><span class="sxs-lookup"><span data-stu-id="a97d8-168">![Set job time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="a97d8-169">Click **Start** to start the job.</span><span class="sxs-lookup"><span data-stu-id="a97d8-169">Click **Start** to start the job.</span></span> <span data-ttu-id="a97d8-170">It can take up to a couple minutes to start the job.</span><span class="sxs-lookup"><span data-stu-id="a97d8-170">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="a97d8-171">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span><span class="sxs-lookup"><span data-stu-id="a97d8-171">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="a97d8-172">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="a97d8-172">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="a97d8-173">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="a97d8-173">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="a97d8-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span><span class="sxs-lookup"><span data-stu-id="a97d8-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="a97d8-175">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span><span class="sxs-lookup"><span data-stu-id="a97d8-175">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="a97d8-176">![Monitor job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span><span class="sxs-lookup"><span data-stu-id="a97d8-176">![Monitor job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="a97d8-177">Finally, you can verify that the job output data is available in the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="a97d8-177">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="a97d8-178">![Verify output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span><span class="sxs-lookup"><span data-stu-id="a97d8-178">![Verify output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="a97d8-179">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="a97d8-179">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="a97d8-180">See also</span><span class="sxs-lookup"><span data-stu-id="a97d8-180">See also</span></span>
* [<span data-ttu-id="a97d8-181">Create an HDInsight cluster to use Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a97d8-181">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)










