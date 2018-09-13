---
title: Azure Stream Analytics integration with Azure Machine Learning
description: This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning, using a user defined function.
services: stream-analytics
author: jasonwhowell
ms.author: jasonh
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 04/16/2018
ms.openlocfilehash: 63648dfe02a0b5ed00d0a7206a6aabbe200f94c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781019"
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="c61aa-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c61aa-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="c61aa-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c61aa-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="c61aa-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span><span class="sxs-lookup"><span data-stu-id="c61aa-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="c61aa-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span><span class="sxs-lookup"><span data-stu-id="c61aa-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="c61aa-107">You can apply what you learn from this article to scenarios such as these:</span><span class="sxs-lookup"><span data-stu-id="c61aa-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="c61aa-108">Analyzing real-time sentiment on streaming Twitter data.</span><span class="sxs-lookup"><span data-stu-id="c61aa-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="c61aa-109">Analyzing records of customer chats with support staff.</span><span class="sxs-lookup"><span data-stu-id="c61aa-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="c61aa-110">Evaluating comments on forums, blogs, and videos.</span><span class="sxs-lookup"><span data-stu-id="c61aa-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="c61aa-111">Many other real-time, predictive scoring scenarios.</span><span class="sxs-lookup"><span data-stu-id="c61aa-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="c61aa-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span><span class="sxs-lookup"><span data-stu-id="c61aa-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="c61aa-113">To simplify the tutorial, it's written so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c61aa-113">To simplify the tutorial, it's written so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="c61aa-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="c61aa-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![sample tweets in a CSV file](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="c61aa-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span><span class="sxs-lookup"><span data-stu-id="c61aa-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="c61aa-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span><span class="sxs-lookup"><span data-stu-id="c61aa-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="c61aa-118">The following figure demonstrates this configuration.</span><span class="sxs-lookup"><span data-stu-id="c61aa-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="c61aa-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span><span class="sxs-lookup"><span data-stu-id="c61aa-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="c61aa-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span><span class="sxs-lookup"><span data-stu-id="c61aa-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning integration overview](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="c61aa-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c61aa-122">Prerequisites</span></span>
<span data-ttu-id="c61aa-123">Before you start, make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="c61aa-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="c61aa-124">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c61aa-124">An active Azure subscription.</span></span>
* <span data-ttu-id="c61aa-125">A CSV file with some data in it.</span><span class="sxs-lookup"><span data-stu-id="c61aa-125">A CSV file with some data in it.</span></span> <span data-ttu-id="c61aa-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span><span class="sxs-lookup"><span data-stu-id="c61aa-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="c61aa-127">For this article, it is assumed that you're using the file from GitHub.</span><span class="sxs-lookup"><span data-stu-id="c61aa-127">For this article, it is assumed that you're using the file from GitHub.</span></span>

<span data-ttu-id="c61aa-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span><span class="sxs-lookup"><span data-stu-id="c61aa-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="c61aa-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span><span class="sxs-lookup"><span data-stu-id="c61aa-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="c61aa-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="c61aa-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="c61aa-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span><span class="sxs-lookup"><span data-stu-id="c61aa-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="c61aa-132">Start the Stream Analytics job and check the output.</span><span class="sxs-lookup"><span data-stu-id="c61aa-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="c61aa-133">Create a storage container and upload the CSV input file</span><span class="sxs-lookup"><span data-stu-id="c61aa-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="c61aa-134">For this step, you can use any CSV file, such as the one available from GitHub.</span><span class="sxs-lookup"><span data-stu-id="c61aa-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="c61aa-135">In the Azure portal, click **Create a resource** > **Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-135">In the Azure portal, click **Create a resource** > **Storage** > **Storage account**.</span></span>

2. <span data-ttu-id="c61aa-136">Provide a name (`samldemo` in the example).</span><span class="sxs-lookup"><span data-stu-id="c61aa-136">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="c61aa-137">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span><span class="sxs-lookup"><span data-stu-id="c61aa-137">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="c61aa-138">Specify an existing resource group and specify a location.</span><span class="sxs-lookup"><span data-stu-id="c61aa-138">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="c61aa-139">For location, we recommend that all the resources created in this tutorial use the same location.</span><span class="sxs-lookup"><span data-stu-id="c61aa-139">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![provide storage account details](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="c61aa-141">In the Azure portal, select the storage account.</span><span class="sxs-lookup"><span data-stu-id="c61aa-141">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="c61aa-142">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span><span class="sxs-lookup"><span data-stu-id="c61aa-142">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![create blob container](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="c61aa-144">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-144">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="c61aa-145">When you're done, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-145">When you're done, click **OK**.</span></span>

    ![specify blob container details](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="c61aa-147">In the **Containers** blade, select the new container, which opens the blade for that container.</span><span class="sxs-lookup"><span data-stu-id="c61aa-147">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="c61aa-148">Click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-148">Click **Upload**.</span></span>

    !['Upload' button for a container](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="c61aa-150">In the **Upload blob** blade, upload the **sampleinput.csv** file that you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="c61aa-150">In the **Upload blob** blade, upload the **sampleinput.csv** file that you downloaded earlier.</span></span> <span data-ttu-id="c61aa-151">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c61aa-151">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

9. <span data-ttu-id="c61aa-152">Click the **Upload** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="c61aa-152">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="c61aa-153">Add the sentiment analytics model from the Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="c61aa-153">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="c61aa-154">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="c61aa-154">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="c61aa-155">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="c61aa-155">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="c61aa-156">Click **Open in Studio**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-156">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, open Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="c61aa-158">Sign in to go to the workspace.</span><span class="sxs-lookup"><span data-stu-id="c61aa-158">Sign in to go to the workspace.</span></span> <span data-ttu-id="c61aa-159">Select a location.</span><span class="sxs-lookup"><span data-stu-id="c61aa-159">Select a location.</span></span>

4. <span data-ttu-id="c61aa-160">Click **Run** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c61aa-160">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="c61aa-161">The process runs, which takes about a minute.</span><span class="sxs-lookup"><span data-stu-id="c61aa-161">The process runs, which takes about a minute.</span></span>

   ![run experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="c61aa-163">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c61aa-163">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![deploy experiment in Machine Learning Studio as a web service](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="c61aa-165">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span><span class="sxs-lookup"><span data-stu-id="c61aa-165">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="c61aa-166">Provide text input such as "I love Microsoft".</span><span class="sxs-lookup"><span data-stu-id="c61aa-166">Provide text input such as "I love Microsoft".</span></span> 

   ![test experiment in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="c61aa-168">If the test works, you see a result similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="c61aa-168">If the test works, you see a result similar to the following example:</span></span>

   ![test results in Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="c61aa-170">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="c61aa-170">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="c61aa-171">The workbook contains the API key and the URL that you need later to set up the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="c61aa-171">The workbook contains the API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, quick glance](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="c61aa-173">Create a Stream Analytics job that uses the Machine Learning model</span><span class="sxs-lookup"><span data-stu-id="c61aa-173">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="c61aa-174">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span><span class="sxs-lookup"><span data-stu-id="c61aa-174">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="c61aa-175">Create the job</span><span class="sxs-lookup"><span data-stu-id="c61aa-175">Create the job</span></span>

1. <span data-ttu-id="c61aa-176">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c61aa-176">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="c61aa-177">Click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-177">Click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span></span> 

3. <span data-ttu-id="c61aa-178">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span><span class="sxs-lookup"><span data-stu-id="c61aa-178">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![specify settings for new Stream Analytics job](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="c61aa-180">Configure the job input</span><span class="sxs-lookup"><span data-stu-id="c61aa-180">Configure the job input</span></span>
<span data-ttu-id="c61aa-181">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span><span class="sxs-lookup"><span data-stu-id="c61aa-181">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="c61aa-182">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** option.</span><span class="sxs-lookup"><span data-stu-id="c61aa-182">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** option.</span></span>    

2. <span data-ttu-id="c61aa-183">In the **Inputs** blade, click **Add Stream Input** >**Blob storage**</span><span class="sxs-lookup"><span data-stu-id="c61aa-183">In the **Inputs** blade, click **Add Stream Input** >**Blob storage**</span></span>

3. <span data-ttu-id="c61aa-184">Fill out the **Blob Storage** blade with these values:</span><span class="sxs-lookup"><span data-stu-id="c61aa-184">Fill out the **Blob Storage** blade with these values:</span></span>

   
   |<span data-ttu-id="c61aa-185">Field</span><span class="sxs-lookup"><span data-stu-id="c61aa-185">Field</span></span>  |<span data-ttu-id="c61aa-186">Value</span><span class="sxs-lookup"><span data-stu-id="c61aa-186">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="c61aa-187">**Input alias**</span><span class="sxs-lookup"><span data-stu-id="c61aa-187">**Input alias**</span></span> | <span data-ttu-id="c61aa-188">Use the name `datainput` and select **Select blob storage from your subscription**</span><span class="sxs-lookup"><span data-stu-id="c61aa-188">Use the name `datainput` and select **Select blob storage from your subscription**</span></span>       |
   |<span data-ttu-id="c61aa-189">**Storage account**</span><span class="sxs-lookup"><span data-stu-id="c61aa-189">**Storage account**</span></span>  |  <span data-ttu-id="c61aa-190">Select the storage account you created earlier.</span><span class="sxs-lookup"><span data-stu-id="c61aa-190">Select the storage account you created earlier.</span></span>  |
   |<span data-ttu-id="c61aa-191">**Container**</span><span class="sxs-lookup"><span data-stu-id="c61aa-191">**Container**</span></span>  | <span data-ttu-id="c61aa-192">Select the container you created earlier (`azuresamldemoblob`)</span><span class="sxs-lookup"><span data-stu-id="c61aa-192">Select the container you created earlier (`azuresamldemoblob`)</span></span>        |
   |<span data-ttu-id="c61aa-193">**Event serialization format**</span><span class="sxs-lookup"><span data-stu-id="c61aa-193">**Event serialization format**</span></span>  |  <span data-ttu-id="c61aa-194">Select **CSV**</span><span class="sxs-lookup"><span data-stu-id="c61aa-194">Select **CSV**</span></span>       |

   ![Settings for new job input](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="c61aa-196">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-196">Click **Save**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="c61aa-197">Configure the job output</span><span class="sxs-lookup"><span data-stu-id="c61aa-197">Configure the job output</span></span>
<span data-ttu-id="c61aa-198">The job sends results to the same blob storage where it gets input.</span><span class="sxs-lookup"><span data-stu-id="c61aa-198">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="c61aa-199">Under **Job Topology** in the job blade, click the **Outputs** option.</span><span class="sxs-lookup"><span data-stu-id="c61aa-199">Under **Job Topology** in the job blade, click the **Outputs** option.</span></span>  

2. <span data-ttu-id="c61aa-200">In the **Outputs** blade, click **Add** >**Blob storage**, and then add an output with the alias `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="c61aa-200">In the **Outputs** blade, click **Add** >**Blob storage**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="c61aa-201">Fill out the **Blob Storage** blade with these values:</span><span class="sxs-lookup"><span data-stu-id="c61aa-201">Fill out the **Blob Storage** blade with these values:</span></span>

   |<span data-ttu-id="c61aa-202">Field</span><span class="sxs-lookup"><span data-stu-id="c61aa-202">Field</span></span>  |<span data-ttu-id="c61aa-203">Value</span><span class="sxs-lookup"><span data-stu-id="c61aa-203">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="c61aa-204">**Output alias**</span><span class="sxs-lookup"><span data-stu-id="c61aa-204">**Output alias**</span></span> | <span data-ttu-id="c61aa-205">Use the name `datamloutput` and select **Select blob storage from your subscription**</span><span class="sxs-lookup"><span data-stu-id="c61aa-205">Use the name `datamloutput` and select **Select blob storage from your subscription**</span></span>       |
   |<span data-ttu-id="c61aa-206">**Storage account**</span><span class="sxs-lookup"><span data-stu-id="c61aa-206">**Storage account**</span></span>  |  <span data-ttu-id="c61aa-207">Select the storage account you created earlier.</span><span class="sxs-lookup"><span data-stu-id="c61aa-207">Select the storage account you created earlier.</span></span>  |
   |<span data-ttu-id="c61aa-208">**Container**</span><span class="sxs-lookup"><span data-stu-id="c61aa-208">**Container**</span></span>  | <span data-ttu-id="c61aa-209">Select the container you created earlier (`azuresamldemoblob`)</span><span class="sxs-lookup"><span data-stu-id="c61aa-209">Select the container you created earlier (`azuresamldemoblob`)</span></span>        |
   |<span data-ttu-id="c61aa-210">**Event serialization format**</span><span class="sxs-lookup"><span data-stu-id="c61aa-210">**Event serialization format**</span></span>  |  <span data-ttu-id="c61aa-211">Select **CSV**</span><span class="sxs-lookup"><span data-stu-id="c61aa-211">Select **CSV**</span></span>       |

   ![Settings for new job output](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="c61aa-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-213">Click **Save**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="c61aa-214">Add the Machine Learning function</span><span class="sxs-lookup"><span data-stu-id="c61aa-214">Add the Machine Learning function</span></span> 
<span data-ttu-id="c61aa-215">Earlier you published a Machine Learning model to a web service.</span><span class="sxs-lookup"><span data-stu-id="c61aa-215">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="c61aa-216">In this scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="c61aa-216">In this scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="c61aa-217">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span><span class="sxs-lookup"><span data-stu-id="c61aa-217">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="c61aa-218">In this section of the tutorial, you define a function in the Stream Analysis job.</span><span class="sxs-lookup"><span data-stu-id="c61aa-218">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="c61aa-219">The function can be invoked to send a tweet to the web service and get the response back.</span><span class="sxs-lookup"><span data-stu-id="c61aa-219">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="c61aa-220">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="c61aa-220">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="c61aa-221">Navigate to your job blade > **Functions** > **+ Add** > **AzureML**</span><span class="sxs-lookup"><span data-stu-id="c61aa-221">Navigate to your job blade > **Functions** > **+ Add** > **AzureML**</span></span>

3. <span data-ttu-id="c61aa-222">Fill out the **Azure Machine Learning function** blade with these values:</span><span class="sxs-lookup"><span data-stu-id="c61aa-222">Fill out the **Azure Machine Learning function** blade with these values:</span></span>

   |<span data-ttu-id="c61aa-223">Field</span><span class="sxs-lookup"><span data-stu-id="c61aa-223">Field</span></span>  |<span data-ttu-id="c61aa-224">Value</span><span class="sxs-lookup"><span data-stu-id="c61aa-224">Value</span></span>  |
   |---------|---------|
   | <span data-ttu-id="c61aa-225">**Function alias**</span><span class="sxs-lookup"><span data-stu-id="c61aa-225">**Function alias**</span></span> | <span data-ttu-id="c61aa-226">Use the name `sentiment` and select **Provide Azure Machine Learning function settings manually** which gives you an option to enter the URL and key.</span><span class="sxs-lookup"><span data-stu-id="c61aa-226">Use the name `sentiment` and select **Provide Azure Machine Learning function settings manually** which gives you an option to enter the URL and key.</span></span>      |
   | <span data-ttu-id="c61aa-227">**URL**</span><span class="sxs-lookup"><span data-stu-id="c61aa-227">**URL**</span></span>| <span data-ttu-id="c61aa-228">Paste the web service URL.</span><span class="sxs-lookup"><span data-stu-id="c61aa-228">Paste the web service URL.</span></span>|
   |<span data-ttu-id="c61aa-229">**Key**</span><span class="sxs-lookup"><span data-stu-id="c61aa-229">**Key**</span></span> | <span data-ttu-id="c61aa-230">Paste the API key.</span><span class="sxs-lookup"><span data-stu-id="c61aa-230">Paste the API key.</span></span> |
  
   ![Settings for adding a Machine Learning function to the Stream Analytics job](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
4. <span data-ttu-id="c61aa-232">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-232">Click **Save**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="c61aa-233">Create a query to transform the data</span><span class="sxs-lookup"><span data-stu-id="c61aa-233">Create a query to transform the data</span></span>

<span data-ttu-id="c61aa-234">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span><span class="sxs-lookup"><span data-stu-id="c61aa-234">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="c61aa-235">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="c61aa-235">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="c61aa-236">The query then sends the result to the output that you defined (blob storage).</span><span class="sxs-lookup"><span data-stu-id="c61aa-236">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="c61aa-237">Return to the job overview blade.</span><span class="sxs-lookup"><span data-stu-id="c61aa-237">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="c61aa-238">Under **Job Topology**, click the **Query** box.</span><span class="sxs-lookup"><span data-stu-id="c61aa-238">Under **Job Topology**, click the **Query** box.</span></span>

3. <span data-ttu-id="c61aa-239">Enter the following query:</span><span class="sxs-lookup"><span data-stu-id="c61aa-239">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result 
    FROM datainput  
    )  

    SELECT text, result.[Score]  
    INTO datamloutput
    FROM sentiment  
    ```    

    <span data-ttu-id="c61aa-240">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span><span class="sxs-lookup"><span data-stu-id="c61aa-240">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="c61aa-241">Click **Save** to save the query.</span><span class="sxs-lookup"><span data-stu-id="c61aa-241">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="c61aa-242">Start the Stream Analytics job and check the output</span><span class="sxs-lookup"><span data-stu-id="c61aa-242">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="c61aa-243">You can now start the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="c61aa-243">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="c61aa-244">Start the job</span><span class="sxs-lookup"><span data-stu-id="c61aa-244">Start the job</span></span>
1. <span data-ttu-id="c61aa-245">Return to the job overview blade.</span><span class="sxs-lookup"><span data-stu-id="c61aa-245">Return to the job overview blade.</span></span>

2. <span data-ttu-id="c61aa-246">Click **Start** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="c61aa-246">Click **Start** at the top of the blade.</span></span>

3. <span data-ttu-id="c61aa-247">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span><span class="sxs-lookup"><span data-stu-id="c61aa-247">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="c61aa-248">When you're done, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-248">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="c61aa-249">Check the output</span><span class="sxs-lookup"><span data-stu-id="c61aa-249">Check the output</span></span>
1. <span data-ttu-id="c61aa-250">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span><span class="sxs-lookup"><span data-stu-id="c61aa-250">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="c61aa-251">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span><span class="sxs-lookup"><span data-stu-id="c61aa-251">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="c61aa-252">Alternatively, do the following steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c61aa-252">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="c61aa-253">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span><span class="sxs-lookup"><span data-stu-id="c61aa-253">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="c61aa-254">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="c61aa-254">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="c61aa-255">Right-click the generated file and then select **Download**.</span><span class="sxs-lookup"><span data-stu-id="c61aa-255">Right-click the generated file and then select **Download**.</span></span> 

   ![Download CSV job output from Blob storage](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="c61aa-257">Open the generated CSV file.</span><span class="sxs-lookup"><span data-stu-id="c61aa-257">Open the generated CSV file.</span></span> <span data-ttu-id="c61aa-258">You see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="c61aa-258">You see something like the following example:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV view](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="c61aa-260">View metrics</span><span class="sxs-lookup"><span data-stu-id="c61aa-260">View metrics</span></span>
<span data-ttu-id="c61aa-261">You also can view Azure Machine Learning function-related metrics.</span><span class="sxs-lookup"><span data-stu-id="c61aa-261">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="c61aa-262">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span><span class="sxs-lookup"><span data-stu-id="c61aa-262">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="c61aa-263">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="c61aa-263">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="c61aa-264">**Function Events** indicates the number of events in the request.</span><span class="sxs-lookup"><span data-stu-id="c61aa-264">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="c61aa-265">By default, each request to a Machine Learning web service contains up to 1,000 events.</span><span class="sxs-lookup"><span data-stu-id="c61aa-265">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="c61aa-266">Next steps</span><span class="sxs-lookup"><span data-stu-id="c61aa-266">Next steps</span></span>

* [<span data-ttu-id="c61aa-267">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c61aa-267">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c61aa-268">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="c61aa-268">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c61aa-269">Integrate REST API and Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c61aa-269">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="c61aa-270">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="c61aa-270">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



