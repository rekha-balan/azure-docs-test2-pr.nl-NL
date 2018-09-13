---
title: Azure Stream Analytics and Machine Learning integration | Microsoft Docs
description: How to use a user-defined function and Machine Learning in a Stream Analytics job
keywords: ''
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 17d47adbeb32940f0e9e6b0e5705be9107f34bdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549752"
---
# <a name="sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="728d0-103">Sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="728d0-103">Sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="728d0-104">This article is designed to help you quickly set up a simple Azure Stream Analytics job, with Azure Machine Learning integration.</span><span class="sxs-lookup"><span data-stu-id="728d0-104">This article is designed to help you quickly set up a simple Azure Stream Analytics job, with Azure Machine Learning integration.</span></span> <span data-ttu-id="728d0-105">We will use a sentiment analytics Machine Learning model from the Cortana Intelligence Gallery to analyze streaming text data, and determine the sentiment score in real time.</span><span class="sxs-lookup"><span data-stu-id="728d0-105">We will use a sentiment analytics Machine Learning model from the Cortana Intelligence Gallery to analyze streaming text data, and determine the sentiment score in real time.</span></span> <span data-ttu-id="728d0-106">The information in this article can help you understand scenarios such as real-time sentiment analytics on streaming Twitter data, analyze records of customer chats with support staff, and evaluate comments on forums, blogs, and videos, in addition to many other real-time, predictive scoring scenarios.</span><span class="sxs-lookup"><span data-stu-id="728d0-106">The information in this article can help you understand scenarios such as real-time sentiment analytics on streaming Twitter data, analyze records of customer chats with support staff, and evaluate comments on forums, blogs, and videos, in addition to many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="728d0-107">This article offers a sample CSV file with text as input in Azure Blob storage, shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="728d0-107">This article offers a sample CSV file with text as input in Azure Blob storage, shown in the following image.</span></span> <span data-ttu-id="728d0-108">The job applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span><span class="sxs-lookup"><span data-stu-id="728d0-108">The job applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="728d0-109">The end result is placed in the same blob store in another CSV file.</span><span class="sxs-lookup"><span data-stu-id="728d0-109">The end result is placed in the same blob store in another CSV file.</span></span> 

![Stream Analytics Machine Learning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="728d0-111">The following image demonstrates this configuration.</span><span class="sxs-lookup"><span data-stu-id="728d0-111">The following image demonstrates this configuration.</span></span> <span data-ttu-id="728d0-112">For a more realistic scenario, you can replace Blob storage with streaming Twitter data from an Azure Event Hubs input.</span><span class="sxs-lookup"><span data-stu-id="728d0-112">For a more realistic scenario, you can replace Blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="728d0-113">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span><span class="sxs-lookup"><span data-stu-id="728d0-113">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="728d0-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="728d0-115">Prerequisites</span></span>
<span data-ttu-id="728d0-116">The prerequisites for completing the tasks that are demonstrated in this article are as follows:</span><span class="sxs-lookup"><span data-stu-id="728d0-116">The prerequisites for completing the tasks that are demonstrated in this article are as follows:</span></span>

* <span data-ttu-id="728d0-117">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="728d0-117">An active Azure subscription.</span></span>
* <span data-ttu-id="728d0-118">A CSV file with some data in it.</span><span class="sxs-lookup"><span data-stu-id="728d0-118">A CSV file with some data in it.</span></span> <span data-ttu-id="728d0-119">You can download the file shown in Figure 1 from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample Data/sampleinput.csv), or you can create your own file.</span><span class="sxs-lookup"><span data-stu-id="728d0-119">You can download the file shown in Figure 1 from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="728d0-120">For this article, we assume that you use the one provided for download on GitHub.</span><span class="sxs-lookup"><span data-stu-id="728d0-120">For this article, we assume that you use the one provided for download on GitHub.</span></span>

<span data-ttu-id="728d0-121">At a high level, to complete the tasks demonstrated in this article, you'll do the following:</span><span class="sxs-lookup"><span data-stu-id="728d0-121">At a high level, to complete the tasks demonstrated in this article, you'll do the following:</span></span>

1. <span data-ttu-id="728d0-122">Upload the CSV input file to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="728d0-122">Upload the CSV input file to Azure Blob storage.</span></span>
2. <span data-ttu-id="728d0-123">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="728d0-123">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace.</span></span>
3. <span data-ttu-id="728d0-124">Deploy this model as a web service in the Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="728d0-124">Deploy this model as a web service in the Machine Learning workspace.</span></span>
4. <span data-ttu-id="728d0-125">Create a Stream Analytics job that calls this web service as a function, to determine sentiment for the text input.</span><span class="sxs-lookup"><span data-stu-id="728d0-125">Create a Stream Analytics job that calls this web service as a function, to determine sentiment for the text input.</span></span>
5. <span data-ttu-id="728d0-126">Start the Stream Analytics job and observe the output.</span><span class="sxs-lookup"><span data-stu-id="728d0-126">Start the Stream Analytics job and observe the output.</span></span>

## <a name="create-a-storage-blob-and-upload-the-csv-input-file"></a><span data-ttu-id="728d0-127">Create a storage blob and upload the CSV input file</span><span class="sxs-lookup"><span data-stu-id="728d0-127">Create a storage blob and upload the CSV input file</span></span>
<span data-ttu-id="728d0-128">For this step, you can use any CSV file, such as the one already specified as available for download on GitHub.</span><span class="sxs-lookup"><span data-stu-id="728d0-128">For this step, you can use any CSV file, such as the one already specified as available for download on GitHub.</span></span> <span data-ttu-id="728d0-129">Uploading the csv file is simple as it is an option included in creating a storage blob.</span><span class="sxs-lookup"><span data-stu-id="728d0-129">Uploading the csv file is simple as it is an option included in creating a storage blob.</span></span>

<span data-ttu-id="728d0-130">For our tutorial, create a new storage account by clicking **New** and then searching for 'storage account' and then selecting the resulting icon for storage account and providing details for the creation of the account.</span><span class="sxs-lookup"><span data-stu-id="728d0-130">For our tutorial, create a new storage account by clicking **New** and then searching for 'storage account' and then selecting the resulting icon for storage account and providing details for the creation of the account.</span></span> <span data-ttu-id="728d0-131">Provide a **Name** (azuresamldemosa in my example), create or use an existing **Resource group** and specify a **Location** (for location, it is important that all the resources created in this demo all use the same location if possible).</span><span class="sxs-lookup"><span data-stu-id="728d0-131">Provide a **Name** (azuresamldemosa in my example), create or use an existing **Resource group** and specify a **Location** (for location, it is important that all the resources created in this demo all use the same location if possible).</span></span>

![create storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-sa.png)

<span data-ttu-id="728d0-133">Once that is completed you can click on Blob service and create a blob container.</span><span class="sxs-lookup"><span data-stu-id="728d0-133">Once that is completed you can click on Blob service and create a blob container.</span></span>

![create blob container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

<span data-ttu-id="728d0-135">Then provide a **Name** for the container (azuresamldemoblob in my example) and verify the **Access type** is set to 'blob'.</span><span class="sxs-lookup"><span data-stu-id="728d0-135">Then provide a **Name** for the container (azuresamldemoblob in my example) and verify the **Access type** is set to 'blob'.</span></span>

![create blob access type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

<span data-ttu-id="728d0-137">Now we can populate the blob with our data.</span><span class="sxs-lookup"><span data-stu-id="728d0-137">Now we can populate the blob with our data.</span></span> <span data-ttu-id="728d0-138">Select **Files** and then select the file on your local drive that you downloaded from GitHub.</span><span class="sxs-lookup"><span data-stu-id="728d0-138">Select **Files** and then select the file on your local drive that you downloaded from GitHub.</span></span> <span data-ttu-id="728d0-139">I selected Block blob and 4 MB as a size these should be fine for this demonstration.</span><span class="sxs-lookup"><span data-stu-id="728d0-139">I selected Block blob and 4 MB as a size these should be fine for this demonstration.</span></span> <span data-ttu-id="728d0-140">Then select **Upload** and the portal will create a blob with the text sample for you.</span><span class="sxs-lookup"><span data-stu-id="728d0-140">Then select **Upload** and the portal will create a blob with the text sample for you.</span></span>

![create blob upload file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

<span data-ttu-id="728d0-142">Now that the sample data is in a blob it is time to enable the sentiment analysis model in Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="728d0-142">Now that the sample data is in a blob it is time to enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="728d0-143">Add the sentiment analytics model from the Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="728d0-143">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>
1. <span data-ttu-id="728d0-144">Download the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) from the Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="728d0-144">Download the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) from the Cortana Intelligence Gallery.</span></span>  
2. <span data-ttu-id="728d0-145">In Machine Learning Studio, select **Open in Studio**.</span><span class="sxs-lookup"><span data-stu-id="728d0-145">In Machine Learning Studio, select **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, open Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="728d0-147">Sign in to go to the workspace.</span><span class="sxs-lookup"><span data-stu-id="728d0-147">Sign in to go to the workspace.</span></span> <span data-ttu-id="728d0-148">Select the location that best suits your own location.</span><span class="sxs-lookup"><span data-stu-id="728d0-148">Select the location that best suits your own location.</span></span>
4. <span data-ttu-id="728d0-149">Click **Run** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="728d0-149">Click **Run** at the bottom of the page.</span></span>  
5. <span data-ttu-id="728d0-150">After the process runs successfully, select **Deploy Web Service**.</span><span class="sxs-lookup"><span data-stu-id="728d0-150">After the process runs successfully, select **Deploy Web Service**.</span></span>
6. <span data-ttu-id="728d0-151">The sentiment analytics model is ready to use.</span><span class="sxs-lookup"><span data-stu-id="728d0-151">The sentiment analytics model is ready to use.</span></span> <span data-ttu-id="728d0-152">To validate, select the **Test** button and provide text input, such as, “I love Microsoft.”</span><span class="sxs-lookup"><span data-stu-id="728d0-152">To validate, select the **Test** button and provide text input, such as, “I love Microsoft.”</span></span> <span data-ttu-id="728d0-153">The test should return a result similar to the following:</span><span class="sxs-lookup"><span data-stu-id="728d0-153">The test should return a result similar to the following:</span></span>

`'Predictive Mini Twitter sentiment analysis Experiment' test returned ["4","0.715057671070099"]...`  

![Stream Analytics Machine Learning, analysis data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-analysis-data.png)  

<span data-ttu-id="728d0-155">In the **Apps** column, select the link for **Excel 2010 or earlier workbook** to get your API key and the URL that you’ll need later to set up the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="728d0-155">In the **Apps** column, select the link for **Excel 2010 or earlier workbook** to get your API key and the URL that you’ll need later to set up the Stream Analytics job.</span></span> <span data-ttu-id="728d0-156">(This step is required only to use a Machine Learning model from another Azure account workspace.</span><span class="sxs-lookup"><span data-stu-id="728d0-156">(This step is required only to use a Machine Learning model from another Azure account workspace.</span></span> <span data-ttu-id="728d0-157">This article assumes this is the case, to address that scenario.)</span><span class="sxs-lookup"><span data-stu-id="728d0-157">This article assumes this is the case, to address that scenario.)</span></span>  

<span data-ttu-id="728d0-158">Note the web service URL and access key from the downloaded Excel file, as shown below:</span><span class="sxs-lookup"><span data-stu-id="728d0-158">Note the web service URL and access key from the downloaded Excel file, as shown below:</span></span>  

![Stream Analytics Machine Learning, quick glance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  

## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="728d0-160">Create a Stream Analytics job that uses the Machine Learning model</span><span class="sxs-lookup"><span data-stu-id="728d0-160">Create a Stream Analytics job that uses the Machine Learning model</span></span>
1. <span data-ttu-id="728d0-161">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="728d0-161">Go to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="728d0-162">Click **New** > **Intelligence + analytics** > **Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="728d0-162">Click **New** > **Intelligence + analytics** > **Stream Analytics**.</span></span> <span data-ttu-id="728d0-163">Enter a name for your job in **Job name**, specify an existing resource group or create a new one as required, and enter the appropriate location for the job in the **Location** field.</span><span class="sxs-lookup"><span data-stu-id="728d0-163">Enter a name for your job in **Job name**, specify an existing resource group or create a new one as required, and enter the appropriate location for the job in the **Location** field.</span></span>    
   
   ![create job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   
3. <span data-ttu-id="728d0-165">After the job is created, on the **Inputs** tab, select **Add an Input**.</span><span class="sxs-lookup"><span data-stu-id="728d0-165">After the job is created, on the **Inputs** tab, select **Add an Input**.</span></span>  
   
   ![Stream Analytics Machine Learning, add Machine Learning input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

4. <span data-ttu-id="728d0-167">Select **Add** and then specify an **Input alias**, select **Data stream**, **Blob Storage** as the input, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="728d0-167">Select **Add** and then specify an **Input alias**, select **Data stream**, **Blob Storage** as the input, and then select **Next**.</span></span>  
5. <span data-ttu-id="728d0-168">On the **Blob Storage Settings** page of the wizard, provide the storage account blob container name you defined earlier when you uploaded the data.</span><span class="sxs-lookup"><span data-stu-id="728d0-168">On the **Blob Storage Settings** page of the wizard, provide the storage account blob container name you defined earlier when you uploaded the data.</span></span> <span data-ttu-id="728d0-169">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="728d0-169">Click **Next**.</span></span> <span data-ttu-id="728d0-170">For **Event Serialization Format**, select **CSV**.</span><span class="sxs-lookup"><span data-stu-id="728d0-170">For **Event Serialization Format**, select **CSV**.</span></span> <span data-ttu-id="728d0-171">Accept the default values for the rest of the **Serialization settings** page.</span><span class="sxs-lookup"><span data-stu-id="728d0-171">Accept the default values for the rest of the **Serialization settings** page.</span></span> <span data-ttu-id="728d0-172">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="728d0-172">Click **OK**.</span></span>  
   
   ![add input blob container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-blob.png)

6. <span data-ttu-id="728d0-174">On the **Outputs** tab, select **Add an Output**.</span><span class="sxs-lookup"><span data-stu-id="728d0-174">On the **Outputs** tab, select **Add an Output**.</span></span>  
   
   ![Stream Analytics Machine Learning, add output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

7. <span data-ttu-id="728d0-176">Click **Blob Storage**, and then enter the same parameters, except for the container.</span><span class="sxs-lookup"><span data-stu-id="728d0-176">Click **Blob Storage**, and then enter the same parameters, except for the container.</span></span> <span data-ttu-id="728d0-177">The value for **Input** was configured to read from the container named “test” where the **CSV** file was uploaded.</span><span class="sxs-lookup"><span data-stu-id="728d0-177">The value for **Input** was configured to read from the container named “test” where the **CSV** file was uploaded.</span></span> <span data-ttu-id="728d0-178">For **Output**, enter “testoutput”.</span><span class="sxs-lookup"><span data-stu-id="728d0-178">For **Output**, enter “testoutput”.</span></span>
8. <span data-ttu-id="728d0-179">Validate that the output’s **Serialization settings** are set to **CSV**, and then select the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="728d0-179">Validate that the output’s **Serialization settings** are set to **CSV**, and then select the **OK** button.</span></span>
   
   ![Stream Analytics Machine Learning, add output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

9. <span data-ttu-id="728d0-181">On the **Functions** tab, select **Add a Machine Learning Function**.</span><span class="sxs-lookup"><span data-stu-id="728d0-181">On the **Functions** tab, select **Add a Machine Learning Function**.</span></span>  
   
   ![Stream Analytics Machine Learning, add Machine Learning function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  

10. <span data-ttu-id="728d0-183">On the **Machine Learning Web Service Settings** page, locate the Machine Learning workspace, web service, and default endpoint.</span><span class="sxs-lookup"><span data-stu-id="728d0-183">On the **Machine Learning Web Service Settings** page, locate the Machine Learning workspace, web service, and default endpoint.</span></span> <span data-ttu-id="728d0-184">For this article, apply the settings manually to gain familiarity with configuring a web service for any workspace, as long as you know the URL and have the API key.</span><span class="sxs-lookup"><span data-stu-id="728d0-184">For this article, apply the settings manually to gain familiarity with configuring a web service for any workspace, as long as you know the URL and have the API key.</span></span> <span data-ttu-id="728d0-185">Enter the endpoint **URL** and **API key**.</span><span class="sxs-lookup"><span data-stu-id="728d0-185">Enter the endpoint **URL** and **API key**.</span></span> <span data-ttu-id="728d0-186">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="728d0-186">Click **OK**.</span></span> <span data-ttu-id="728d0-187">Note that the **Function Alias** is 'sentiment'.</span><span class="sxs-lookup"><span data-stu-id="728d0-187">Note that the **Function Alias** is 'sentiment'.</span></span>  
    
    ![Stream Analytics Machine Learning, Machine Learning web service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/add-function-endpoints.png)    

11. <span data-ttu-id="728d0-189">On the **Query** tab, modify the query as follows:</span><span class="sxs-lookup"><span data-stu-id="728d0-189">On the **Query** tab, modify the query as follows:</span></span>    
    
    ```
    WITH sentiment AS (  
      SELECT text, sentiment(text) as result from datainput  
    )  
    
    Select text, result.[Scored Labels]  
    Into testoutput  
    From sentiment  
    ```    

12. <span data-ttu-id="728d0-190">Click **Save** to save the query.</span><span class="sxs-lookup"><span data-stu-id="728d0-190">Click **Save** to save the query.</span></span>

## <a name="start-the-stream-analytics-job-and-observe-the-output"></a><span data-ttu-id="728d0-191">Start the Stream Analytics job and observe the output</span><span class="sxs-lookup"><span data-stu-id="728d0-191">Start the Stream Analytics job and observe the output</span></span>
1. <span data-ttu-id="728d0-192">Click **Start** at the top of the job page.</span><span class="sxs-lookup"><span data-stu-id="728d0-192">Click **Start** at the top of the job page.</span></span>
2. <span data-ttu-id="728d0-193">On the **Start Query Dialog**, select **Custom Time**, and then select one day prior to when you uploaded the CSV to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="728d0-193">On the **Start Query Dialog**, select **Custom Time**, and then select one day prior to when you uploaded the CSV to Blob storage.</span></span> <span data-ttu-id="728d0-194">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="728d0-194">Click **OK**.</span></span>  
3. <span data-ttu-id="728d0-195">Go to the Blob storage by using the tool you used to upload the CSV file, for example, Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="728d0-195">Go to the Blob storage by using the tool you used to upload the CSV file, for example, Visual Studio.</span></span>
4. <span data-ttu-id="728d0-196">A few minutes after the job is started, the output container is created and a CSV file is uploaded to it.</span><span class="sxs-lookup"><span data-stu-id="728d0-196">A few minutes after the job is started, the output container is created and a CSV file is uploaded to it.</span></span>  
5. <span data-ttu-id="728d0-197">Open the file in the default CSV editor.</span><span class="sxs-lookup"><span data-stu-id="728d0-197">Open the file in the default CSV editor.</span></span> <span data-ttu-id="728d0-198">Something similar to the following should be displayed:</span><span class="sxs-lookup"><span data-stu-id="728d0-198">Something similar to the following should be displayed:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  

## <a name="conclusion"></a><span data-ttu-id="728d0-200">Conclusion</span><span class="sxs-lookup"><span data-stu-id="728d0-200">Conclusion</span></span>
<span data-ttu-id="728d0-201">This article demonstrates how to create a Stream Analytics job that reads streaming text data and applies sentiment analytics to the data in real time.</span><span class="sxs-lookup"><span data-stu-id="728d0-201">This article demonstrates how to create a Stream Analytics job that reads streaming text data and applies sentiment analytics to the data in real time.</span></span> <span data-ttu-id="728d0-202">You can accomplish all of this without needing to worry about the intricacies of building a sentiment analytics model.</span><span class="sxs-lookup"><span data-stu-id="728d0-202">You can accomplish all of this without needing to worry about the intricacies of building a sentiment analytics model.</span></span> <span data-ttu-id="728d0-203">This is one of the advantages of the Cortana Intelligence Suite.</span><span class="sxs-lookup"><span data-stu-id="728d0-203">This is one of the advantages of the Cortana Intelligence Suite.</span></span>

<span data-ttu-id="728d0-204">You also can view Azure Machine Learning function-related metrics.</span><span class="sxs-lookup"><span data-stu-id="728d0-204">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="728d0-205">To do this, select the **Monitor** tab. Three function-related metrics are displayed.</span><span class="sxs-lookup"><span data-stu-id="728d0-205">To do this, select the **Monitor** tab. Three function-related metrics are displayed.</span></span>  

* <span data-ttu-id="728d0-206">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="728d0-206">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="728d0-207">**Function Events** indicates the number of events in the request.</span><span class="sxs-lookup"><span data-stu-id="728d0-207">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="728d0-208">By default, each request to a Machine Learning web service contains up to 1,000 events.</span><span class="sxs-lookup"><span data-stu-id="728d0-208">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  
  
    ![Stream Analytics Machine Learning, Machine Learning monitor view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-machine-learning-integration-tutorial/job-monitor.png)  



















