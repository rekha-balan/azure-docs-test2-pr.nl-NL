---
title: Real-time Twitter sentiment analysis with Azure Stream Analytics | Microsoft Docs
description: Learn how to use Stream Analytics for real-time Twitter sentiment analysis. Step-by-step guidance from event generation to data on a live dashboard.
keywords: real-time twitter trend analysis, sentiment analysis, social media analysis, trend analysis example
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 1c288d981106e46e1227a10f95ea7f297629020c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661203"
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="00eaf-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00eaf-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="00eaf-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="00eaf-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="00eaf-107">In this scenario, you write an Azure Stream Analytics query to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="00eaf-107">In this scenario, you write an Azure Stream Analytics query to analyze the data.</span></span> <span data-ttu-id="00eaf-108">Then you either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span><span class="sxs-lookup"><span data-stu-id="00eaf-108">Then you either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span></span>

<span data-ttu-id="00eaf-109">Social media analytics tools help organizations understand trending topics.</span><span class="sxs-lookup"><span data-stu-id="00eaf-109">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="00eaf-110">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span><span class="sxs-lookup"><span data-stu-id="00eaf-110">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="00eaf-111">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span><span class="sxs-lookup"><span data-stu-id="00eaf-111">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span></span>

<span data-ttu-id="00eaf-112">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords and develop sentiment analysis of the feed.</span><span class="sxs-lookup"><span data-stu-id="00eaf-112">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords and develop sentiment analysis of the feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="00eaf-113">Scenario: Social media sentiment analysis in real time</span><span class="sxs-lookup"><span data-stu-id="00eaf-113">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="00eaf-114">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span><span class="sxs-lookup"><span data-stu-id="00eaf-114">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span></span> <span data-ttu-id="00eaf-115">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span><span class="sxs-lookup"><span data-stu-id="00eaf-115">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="00eaf-116">Specifically, to identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span><span class="sxs-lookup"><span data-stu-id="00eaf-116">Specifically, to identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="00eaf-117">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span><span class="sxs-lookup"><span data-stu-id="00eaf-117">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00eaf-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00eaf-118">Prerequisites</span></span>

* <span data-ttu-id="00eaf-119">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="00eaf-119">An Azure subscription</span></span>
* <span data-ttu-id="00eaf-120">A Twitter account and [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)</span><span class="sxs-lookup"><span data-stu-id="00eaf-120">A Twitter account and [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)</span></span>
* <span data-ttu-id="00eaf-121">The [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub</span><span class="sxs-lookup"><span data-stu-id="00eaf-121">The [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub</span></span>
* <span data-ttu-id="00eaf-122">Optional: The source code for the Twitter client from [GitHub](https://aka.ms/azure-stream-analytics-twitterclient)</span><span class="sxs-lookup"><span data-stu-id="00eaf-122">Optional: The source code for the Twitter client from [GitHub](https://aka.ms/azure-stream-analytics-twitterclient)</span></span>

## <a name="create-an-event-hub-input"></a><span data-ttu-id="00eaf-123">Create an event hub input</span><span class="sxs-lookup"><span data-stu-id="00eaf-123">Create an event hub input</span></span>

<span data-ttu-id="00eaf-124">The sample application generates events and pushes them to an Event Hubs instance (an event hub, for short).</span><span class="sxs-lookup"><span data-stu-id="00eaf-124">The sample application generates events and pushes them to an Event Hubs instance (an event hub, for short).</span></span> <span data-ttu-id="00eaf-125">Azure Service Bus event hubs are the preferred method of event ingestion for Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="00eaf-125">Azure Service Bus event hubs are the preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="00eaf-126">For more information, review the event hub documentation at [Azure Service Bus documentation](/azure/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="00eaf-126">For more information, review the event hub documentation at [Azure Service Bus documentation](/azure/service-bus/).</span></span>

### <a name="create-an-event-hub"></a><span data-ttu-id="00eaf-127">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="00eaf-127">Create an event hub</span></span>

<span data-ttu-id="00eaf-128">Take the following steps to create an event hub:</span><span class="sxs-lookup"><span data-stu-id="00eaf-128">Take the following steps to create an event hub:</span></span>

1. <span data-ttu-id="00eaf-129">In the [Azure portal](https://portal.azure.com), select **NEW**, type **Event Hubs**, and then select **Event Hubs** from the resulting search.</span><span class="sxs-lookup"><span data-stu-id="00eaf-129">In the [Azure portal](https://portal.azure.com), select **NEW**, type **Event Hubs**, and then select **Event Hubs** from the resulting search.</span></span> <span data-ttu-id="00eaf-130">Then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-130">Then select **Create**.</span></span>

2. <span data-ttu-id="00eaf-131">Provide a name for the event hub, and then create a resource group.</span><span class="sxs-lookup"><span data-stu-id="00eaf-131">Provide a name for the event hub, and then create a resource group.</span></span> <span data-ttu-id="00eaf-132">We've specified `socialtwitter-eh` and `socialtwitter-rg` respectively.</span><span class="sxs-lookup"><span data-stu-id="00eaf-132">We've specified `socialtwitter-eh` and `socialtwitter-rg` respectively.</span></span> <span data-ttu-id="00eaf-133">Select the option to pin the account to the dashboard, and then select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="00eaf-133">Select the option to pin the account to the dashboard, and then select the **Create** button.</span></span>

3. <span data-ttu-id="00eaf-134">After the deployment is complete, select the event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-134">After the deployment is complete, select the event hub.</span></span> <span data-ttu-id="00eaf-135">Then, under **Entities**, select **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-135">Then, under **Entities**, select **Event Hubs**.</span></span>

4. <span data-ttu-id="00eaf-136">To create the event hub, select the **+ Event Hub** button.</span><span class="sxs-lookup"><span data-stu-id="00eaf-136">To create the event hub, select the **+ Event Hub** button.</span></span> <span data-ttu-id="00eaf-137">Provide your name again (ours was `socialtwitter-eh`), and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-137">Provide your name again (ours was `socialtwitter-eh`), and then select **Create**.</span></span>

5. <span data-ttu-id="00eaf-138">To grant access to the event hub, we need to create a shared access policy.</span><span class="sxs-lookup"><span data-stu-id="00eaf-138">To grant access to the event hub, we need to create a shared access policy.</span></span> <span data-ttu-id="00eaf-139">Select the event hub, and then, under **Settings**, select **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-139">Select the event hub, and then, under **Settings**, select **Shared access policies**.</span></span>

6. <span data-ttu-id="00eaf-140">Under **Shared access policies**, create a policy with **MANAGE** permissions by selecting **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-140">Under **Shared access policies**, create a policy with **MANAGE** permissions by selecting **+ Add**.</span></span> <span data-ttu-id="00eaf-141">Give the policy a name, check **MANAGE**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-141">Give the policy a name, check **MANAGE**, and then select **Create**.</span></span>

7. <span data-ttu-id="00eaf-142">Select your new policy after it has been created, and then select the copy button for the **CONNECTION STRING - PRIMARY KEY** entity.</span><span class="sxs-lookup"><span data-stu-id="00eaf-142">Select your new policy after it has been created, and then select the copy button for the **CONNECTION STRING - PRIMARY KEY** entity.</span></span> <span data-ttu-id="00eaf-143">We need this later in the exercise.</span><span class="sxs-lookup"><span data-stu-id="00eaf-143">We need this later in the exercise.</span></span> <span data-ttu-id="00eaf-144">Then return to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="00eaf-144">Then return to the dashboard.</span></span>

![Shared access policy endpoints](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/keysandendpoints.png)

## <a name="configure-and-start-the-twitter-client-application"></a><span data-ttu-id="00eaf-146">Configure and start the Twitter client application</span><span class="sxs-lookup"><span data-stu-id="00eaf-146">Configure and start the Twitter client application</span></span>

<span data-ttu-id="00eaf-147">We have created a client application that connects to Twitter data via [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect Tweet events about a parameterized set of topics.</span><span class="sxs-lookup"><span data-stu-id="00eaf-147">We have created a client application that connects to Twitter data via [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect Tweet events about a parameterized set of topics.</span></span> <span data-ttu-id="00eaf-148">The [Sentiment140](http://help.sentiment140.com/) open source tool assigns a sentiment value to each tweet as follows:</span><span class="sxs-lookup"><span data-stu-id="00eaf-148">The [Sentiment140](http://help.sentiment140.com/) open source tool assigns a sentiment value to each tweet as follows:</span></span>

* <span data-ttu-id="00eaf-149">0 = negative</span><span class="sxs-lookup"><span data-stu-id="00eaf-149">0 = negative</span></span>
* <span data-ttu-id="00eaf-150">2 = neutral</span><span class="sxs-lookup"><span data-stu-id="00eaf-150">2 = neutral</span></span>
* <span data-ttu-id="00eaf-151">4 = positive</span><span class="sxs-lookup"><span data-stu-id="00eaf-151">4 = positive</span></span>

<span data-ttu-id="00eaf-152">Then Tweet events are pushed to the event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-152">Then Tweet events are pushed to the event hub.</span></span>  

### <a name="set-up-the-application"></a><span data-ttu-id="00eaf-153">Set up the application</span><span class="sxs-lookup"><span data-stu-id="00eaf-153">Set up the application</span></span>
 <span data-ttu-id="00eaf-154">Follow these steps to set up the application:</span><span class="sxs-lookup"><span data-stu-id="00eaf-154">Follow these steps to set up the application:</span></span>

1. <span data-ttu-id="00eaf-155">[Download the TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip), and then unzip it.</span><span class="sxs-lookup"><span data-stu-id="00eaf-155">[Download the TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip), and then unzip it.</span></span>

2. <span data-ttu-id="00eaf-156">Run the `TwitterWPFClient.exe` application.</span><span class="sxs-lookup"><span data-stu-id="00eaf-156">Run the `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="00eaf-157">Then enter your data for the Twitter API Key and Secret, Twitter Access Token and Secret, and also the event hub information.</span><span class="sxs-lookup"><span data-stu-id="00eaf-157">Then enter your data for the Twitter API Key and Secret, Twitter Access Token and Secret, and also the event hub information.</span></span> <span data-ttu-id="00eaf-158">Finally, define which keywords you want to determine sentiment for.</span><span class="sxs-lookup"><span data-stu-id="00eaf-158">Finally, define which keywords you want to determine sentiment for.</span></span>

### <a name="generate-an-oauth-access-token"></a><span data-ttu-id="00eaf-159">Generate an OAuth access token</span><span class="sxs-lookup"><span data-stu-id="00eaf-159">Generate an OAuth access token</span></span>
<span data-ttu-id="00eaf-160">For more information, see [Steps to generate an OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="00eaf-160">For more information, see [Steps to generate an OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens).</span></span>  

 <span data-ttu-id="00eaf-161">To generate a token, you need to make an empty application.</span><span class="sxs-lookup"><span data-stu-id="00eaf-161">To generate a token, you need to make an empty application.</span></span>  

1. <span data-ttu-id="00eaf-162">Replace the EventHubConnectionString and EventHubName values in TwitterWpfClient.exe.config with the connection string and name of your event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-162">Replace the EventHubConnectionString and EventHubName values in TwitterWpfClient.exe.config with the connection string and name of your event hub.</span></span> <span data-ttu-id="00eaf-163">The connection string that you copied earlier gives you both the connection string and the name of your event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-163">The connection string that you copied earlier gives you both the connection string and the name of your event hub.</span></span> <span data-ttu-id="00eaf-164">Be sure to separate them and put each in the correct field.</span><span class="sxs-lookup"><span data-stu-id="00eaf-164">Be sure to separate them and put each in the correct field.</span></span> <span data-ttu-id="00eaf-165">For example, consider the following connection string:</span><span class="sxs-lookup"><span data-stu-id="00eaf-165">For example, consider the following connection string:</span></span>

 ```
    Endpoint=sb://your.servicebus.windows.net/;SharedAccessKeyName=yourpolicy;SharedAccessKey=yoursharedaccesskey;EntityPath=yourhub
 ```  

   <span data-ttu-id="00eaf-166">The TwitterWpfClient.exe.config file should contain your settings as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="00eaf-166">The TwitterWpfClient.exe.config file should contain your settings as shown in the following example:</span></span>

 ```
      add key="EventHubConnectionString" value="Endpoint=sb://your.servicebus.windows.net/;SharedAccessKeyName=yourpolicy;SharedAccessKey=yoursharedaccesskey"
      add key="EventHubName" value="yourhub"
   ```
   > [!NOTE]
   > <span data-ttu-id="00eaf-167">The text "EntityPath=" does **not** appear in the EventHubName value.</span><span class="sxs-lookup"><span data-stu-id="00eaf-167">The text "EntityPath=" does **not** appear in the EventHubName value.</span></span>

    <span data-ttu-id="00eaf-168">You can also enter the values for your Twitter and Azure connection information directly into the client.</span><span class="sxs-lookup"><span data-stu-id="00eaf-168">You can also enter the values for your Twitter and Azure connection information directly into the client.</span></span> <span data-ttu-id="00eaf-169">The same logic applies    where "EntityPath=" is not used.</span><span class="sxs-lookup"><span data-stu-id="00eaf-169">The same logic applies    where "EntityPath=" is not used.</span></span>

   ![wpfclient](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

2. <span data-ttu-id="00eaf-171">**Optional:** Adjust the keywords to search for.</span><span class="sxs-lookup"><span data-stu-id="00eaf-171">**Optional:** Adjust the keywords to search for.</span></span> <span data-ttu-id="00eaf-172">By default, this application looks for some game keywords.</span><span class="sxs-lookup"><span data-stu-id="00eaf-172">By default, this application looks for some game keywords.</span></span>  <span data-ttu-id="00eaf-173">You can adjust the values for **twitter_keywords** in TwitterWpfClient.exe.config, if desired.</span><span class="sxs-lookup"><span data-stu-id="00eaf-173">You can adjust the values for **twitter_keywords** in TwitterWpfClient.exe.config, if desired.</span></span>

3. <span data-ttu-id="00eaf-174">Run TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="00eaf-174">Run TwitterWpfClient.exe.</span></span> <span data-ttu-id="00eaf-175">Then select the green start button to collect social sentiment.</span><span class="sxs-lookup"><span data-stu-id="00eaf-175">Then select the green start button to collect social sentiment.</span></span> <span data-ttu-id="00eaf-176">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-176">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="00eaf-177">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="00eaf-177">Create a Stream Analytics job</span></span>

<span data-ttu-id="00eaf-178">Now that Tweet events are streaming in real time from Twitter, we can set up a Stream Analytics job to analyze these events in real time.</span><span class="sxs-lookup"><span data-stu-id="00eaf-178">Now that Tweet events are streaming in real time from Twitter, we can set up a Stream Analytics job to analyze these events in real time.</span></span>

### <a name="provision-a-stream-analytics-job"></a><span data-ttu-id="00eaf-179">Provision a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="00eaf-179">Provision a Stream Analytics job</span></span>

<span data-ttu-id="00eaf-180">To provision a Stream Analytics job, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="00eaf-180">To provision a Stream Analytics job, take the following steps:</span></span>

1. <span data-ttu-id="00eaf-181">In the [Azure portal](https://portal.azure.com/), select **NEW**, type **STREAM ANALYTICS**, and then select the Stream Analytics tile result.</span><span class="sxs-lookup"><span data-stu-id="00eaf-181">In the [Azure portal](https://portal.azure.com/), select **NEW**, type **STREAM ANALYTICS**, and then select the Stream Analytics tile result.</span></span>

2. <span data-ttu-id="00eaf-182">Specify the following values, and then select **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-182">Specify the following values, and then select **CREATE**.</span></span>

   * <span data-ttu-id="00eaf-183">**JOB NAME**: Enter a job name.</span><span class="sxs-lookup"><span data-stu-id="00eaf-183">**JOB NAME**: Enter a job name.</span></span>

   * <span data-ttu-id="00eaf-184">**Resource group**: Select the resource group that you created earlier in this exercise from the "use existing" option.</span><span class="sxs-lookup"><span data-stu-id="00eaf-184">**Resource group**: Select the resource group that you created earlier in this exercise from the "use existing" option.</span></span>

   * <span data-ttu-id="00eaf-185">**STORAGE ACCOUNT**: Choose the Azure storage account that you want to use to store the monitoring data for all Stream Analytics jobs that run within this region.</span><span class="sxs-lookup"><span data-stu-id="00eaf-185">**STORAGE ACCOUNT**: Choose the Azure storage account that you want to use to store the monitoring data for all Stream Analytics jobs that run within this region.</span></span> <span data-ttu-id="00eaf-186">You have the option to choose an existing storage account or to create a new one.</span><span class="sxs-lookup"><span data-stu-id="00eaf-186">You have the option to choose an existing storage account or to create a new one.</span></span>   

![New job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

<span data-ttu-id="00eaf-188">After the job has been created, it opens in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="00eaf-188">After the job has been created, it opens in the Azure portal.</span></span>

## <a name="specify-the-job-input"></a><span data-ttu-id="00eaf-189">Specify the job input</span><span class="sxs-lookup"><span data-stu-id="00eaf-189">Specify the job input</span></span>
<span data-ttu-id="00eaf-190">To specify the job input, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="00eaf-190">To specify the job input, take the following steps:</span></span>

1. <span data-ttu-id="00eaf-191">In your Stream Analytics job, in **Job Topology** in the middle of the job pane, select **INPUTS**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-191">In your Stream Analytics job, in **Job Topology** in the middle of the job pane, select **INPUTS**.</span></span> <span data-ttu-id="00eaf-192">Then select **ADD**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-192">Then select **ADD**.</span></span>

    <span data-ttu-id="00eaf-193">Next, the portal prompts you for some of the following information.</span><span class="sxs-lookup"><span data-stu-id="00eaf-193">Next, the portal prompts you for some of the following information.</span></span> <span data-ttu-id="00eaf-194">Most of the default values work, and are defined here:</span><span class="sxs-lookup"><span data-stu-id="00eaf-194">Most of the default values work, and are defined here:</span></span>

   * <span data-ttu-id="00eaf-195">**INPUT ALIAS**: Enter a friendly name for this job input, such as `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="00eaf-195">**INPUT ALIAS**: Enter a friendly name for this job input, such as `TwitterStream`.</span></span> <span data-ttu-id="00eaf-196">You use this name in the query later.</span><span class="sxs-lookup"><span data-stu-id="00eaf-196">You use this name in the query later.</span></span>  

   * <span data-ttu-id="00eaf-197">**EVENT HUB NAME**: Select the name of the event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-197">**EVENT HUB NAME**: Select the name of the event hub.</span></span>

   * <span data-ttu-id="00eaf-198">**EVENT HUB POLICY NAME**: Select the event hub policy that you created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="00eaf-198">**EVENT HUB POLICY NAME**: Select the event hub policy that you created earlier in this tutorial.</span></span>

2. <span data-ttu-id="00eaf-199">Select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="00eaf-199">Select the **Create** button.</span></span>

## <a name="specify-the-job-query"></a><span data-ttu-id="00eaf-200">Specify the job query</span><span class="sxs-lookup"><span data-stu-id="00eaf-200">Specify the job query</span></span>

<span data-ttu-id="00eaf-201">Stream Analytics supports a simple, declarative query model that describes transformations.</span><span class="sxs-lookup"><span data-stu-id="00eaf-201">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="00eaf-202">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="00eaf-202">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="00eaf-203">This tutorial helps you author and test several queries over Twitter data.</span><span class="sxs-lookup"><span data-stu-id="00eaf-203">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="00eaf-204">To compare the number of mentions among topics, we use a [Tumbling Window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span><span class="sxs-lookup"><span data-stu-id="00eaf-204">To compare the number of mentions among topics, we use a [Tumbling Window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span></span>

<span data-ttu-id="00eaf-205">Change the query in the code editor to the following, and then select **Save**:</span><span class="sxs-lookup"><span data-stu-id="00eaf-205">Change the query in the code editor to the following, and then select **Save**:</span></span>

```
SELECT System.Timestamp as Time, Topic, COUNT(*)
FROM TwitterStream TIMESTAMP BY CreatedAt
GROUP BY TUMBLINGWINDOW(s, 5), Topic
```   

<span data-ttu-id="00eaf-206">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span><span class="sxs-lookup"><span data-stu-id="00eaf-206">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span></span> <span data-ttu-id="00eaf-207">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span><span class="sxs-lookup"><span data-stu-id="00eaf-207">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span></span> <span data-ttu-id="00eaf-208">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="00eaf-208">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

<span data-ttu-id="00eaf-209">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span><span class="sxs-lookup"><span data-stu-id="00eaf-209">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span></span>

![Query box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/querybox.png)

## <a name="create-an-output-sink"></a><span data-ttu-id="00eaf-211">Create an output sink</span><span class="sxs-lookup"><span data-stu-id="00eaf-211">Create an output sink</span></span>

<span data-ttu-id="00eaf-212">Now that we have defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream, the last step is to define an output sink for the job.</span><span class="sxs-lookup"><span data-stu-id="00eaf-212">Now that we have defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream, the last step is to define an output sink for the job.</span></span>  

<span data-ttu-id="00eaf-213">We write the aggregated tweet events from our job query to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="00eaf-213">We write the aggregated tweet events from our job query to Azure Blob storage.</span></span>  <span data-ttu-id="00eaf-214">You can also push your results to Azure SQL Database, Azure Table storage, or Event Hubs, depending on your specific application needs.</span><span class="sxs-lookup"><span data-stu-id="00eaf-214">You can also push your results to Azure SQL Database, Azure Table storage, or Event Hubs, depending on your specific application needs.</span></span>

## <a name="specify-the-job-output"></a><span data-ttu-id="00eaf-215">Specify the job output</span><span class="sxs-lookup"><span data-stu-id="00eaf-215">Specify the job output</span></span>
<span data-ttu-id="00eaf-216">To specify the job output, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="00eaf-216">To specify the job output, take the following steps:</span></span>

1. <span data-ttu-id="00eaf-217">In your Stream Analytics job, select **OUTPUT** in **Job Topology**, and then select **ADD**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-217">In your Stream Analytics job, select **OUTPUT** in **Job Topology**, and then select **ADD**.</span></span>

2. <span data-ttu-id="00eaf-218">Type or select the following values in the pane:</span><span class="sxs-lookup"><span data-stu-id="00eaf-218">Type or select the following values in the pane:</span></span>

   * <span data-ttu-id="00eaf-219">**OUTPUT ALIAS**: Enter a friendly name for this job output.</span><span class="sxs-lookup"><span data-stu-id="00eaf-219">**OUTPUT ALIAS**: Enter a friendly name for this job output.</span></span> <span data-ttu-id="00eaf-220">This demonstration uses `Output`.</span><span class="sxs-lookup"><span data-stu-id="00eaf-220">This demonstration uses `Output`.</span></span>

   * <span data-ttu-id="00eaf-221">**Sink**: Select **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-221">**Sink**: Select **Blob storage**.</span></span>

   * <span data-ttu-id="00eaf-222">**STORAGE ACCOUNT**: Select **Create a new storage account**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-222">**STORAGE ACCOUNT**: Select **Create a new storage account**.</span></span>

    * <span data-ttu-id="00eaf-223">**STORAGE account**: Give the new storage account a name (`socialtwitter` in this example).</span><span class="sxs-lookup"><span data-stu-id="00eaf-223">**STORAGE account**: Give the new storage account a name (`socialtwitter` in this example).</span></span>

    * <span data-ttu-id="00eaf-224">**CONTAINER**: Give the new container a name (`socialtwitter` in this example).</span><span class="sxs-lookup"><span data-stu-id="00eaf-224">**CONTAINER**: Give the new container a name (`socialtwitter` in this example).</span></span>

3. <span data-ttu-id="00eaf-225">Leave the rest of the entries as default values.</span><span class="sxs-lookup"><span data-stu-id="00eaf-225">Leave the rest of the entries as default values.</span></span> <span data-ttu-id="00eaf-226">Finally, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-226">Finally, select **Create**.</span></span>

## <a name="start-the-job"></a><span data-ttu-id="00eaf-227">Start the job</span><span class="sxs-lookup"><span data-stu-id="00eaf-227">Start the job</span></span>

<span data-ttu-id="00eaf-228">Because a job input, query, and output have all been specified, we are ready to start the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="00eaf-228">Because a job input, query, and output have all been specified, we are ready to start the Stream Analytics job.</span></span>

<span data-ttu-id="00eaf-229">To start the job, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="00eaf-229">To start the job, take the following steps:</span></span>

1. <span data-ttu-id="00eaf-230">In the job overview pane, at the top of the page, select **START**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-230">In the job overview pane, at the top of the page, select **START**.</span></span>

2. <span data-ttu-id="00eaf-231">In the dialog box that opens, select **JOB START TIME**, and then select the **CHECK** button on the bottom of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="00eaf-231">In the dialog box that opens, select **JOB START TIME**, and then select the **CHECK** button on the bottom of the dialog box.</span></span> <span data-ttu-id="00eaf-232">The job status changes first to **Starting** and then to **Running**.</span><span class="sxs-lookup"><span data-stu-id="00eaf-232">The job status changes first to **Starting** and then to **Running**.</span></span>

![Job running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="00eaf-234">View output for sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="00eaf-234">View output for sentiment analysis</span></span>

<span data-ttu-id="00eaf-235">After your job has started running and is processing the real-time Twitter stream, choose how you want to view the output for sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="00eaf-235">After your job has started running and is processing the real-time Twitter stream, choose how you want to view the output for sentiment analysis.</span></span>

<span data-ttu-id="00eaf-236">Use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span><span class="sxs-lookup"><span data-stu-id="00eaf-236">Use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span></span> <span data-ttu-id="00eaf-237">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="00eaf-237">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot.</span></span>

![Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)

## <a name="create-another-query-to-identify-trending-topics"></a><span data-ttu-id="00eaf-239">Create another query to identify trending topics</span><span class="sxs-lookup"><span data-stu-id="00eaf-239">Create another query to identify trending topics</span></span>

<span data-ttu-id="00eaf-240">Another sample query that we created for this scenario is based on [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="00eaf-240">Another sample query that we created for this scenario is based on [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="00eaf-241">To identify trending topics, we look for topics that cross a threshold value for mentions in a given amount of time.</span><span class="sxs-lookup"><span data-stu-id="00eaf-241">To identify trending topics, we look for topics that cross a threshold value for mentions in a given amount of time.</span></span>

<span data-ttu-id="00eaf-242">For the purposes of this tutorial, we check for topics that are mentioned more than 20 times in the last 5 seconds.</span><span class="sxs-lookup"><span data-stu-id="00eaf-242">For the purposes of this tutorial, we check for topics that are mentioned more than 20 times in the last 5 seconds.</span></span>

```
SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
FROM TwitterStream TIMESTAMP BY CreatedAt
GROUP BY SLIDINGWINDOW(s, 5), topic
HAVING COUNT(*) > 20
```

## <a name="use-field-headers"></a><span data-ttu-id="00eaf-243">Use field headers</span><span class="sxs-lookup"><span data-stu-id="00eaf-243">Use field headers</span></span>

<span data-ttu-id="00eaf-244">The field labels you can use in this exercise are listed in this table.</span><span class="sxs-lookup"><span data-stu-id="00eaf-244">The field labels you can use in this exercise are listed in this table.</span></span> <span data-ttu-id="00eaf-245">Feel free to experiment in the query editor.</span><span class="sxs-lookup"><span data-stu-id="00eaf-245">Feel free to experiment in the query editor.</span></span>

<span data-ttu-id="00eaf-246">JSON property</span><span class="sxs-lookup"><span data-stu-id="00eaf-246">JSON property</span></span> | <span data-ttu-id="00eaf-247">Definition</span><span class="sxs-lookup"><span data-stu-id="00eaf-247">Definition</span></span>
--- | ---
<span data-ttu-id="00eaf-248">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="00eaf-248">CreatedAt</span></span> | <span data-ttu-id="00eaf-249">The time that the tweet was created</span><span class="sxs-lookup"><span data-stu-id="00eaf-249">The time that the tweet was created</span></span>
<span data-ttu-id="00eaf-250">Topic</span><span class="sxs-lookup"><span data-stu-id="00eaf-250">Topic</span></span> | <span data-ttu-id="00eaf-251">The topic that matches the specified keyword</span><span class="sxs-lookup"><span data-stu-id="00eaf-251">The topic that matches the specified keyword</span></span>
<span data-ttu-id="00eaf-252">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="00eaf-252">SentimentScore</span></span> | <span data-ttu-id="00eaf-253">The sentiment score from Sentiment140</span><span class="sxs-lookup"><span data-stu-id="00eaf-253">The sentiment score from Sentiment140</span></span>
<span data-ttu-id="00eaf-254">Author</span><span class="sxs-lookup"><span data-stu-id="00eaf-254">Author</span></span> | <span data-ttu-id="00eaf-255">The Twitter handle that sent the tweet</span><span class="sxs-lookup"><span data-stu-id="00eaf-255">The Twitter handle that sent the tweet</span></span>
<span data-ttu-id="00eaf-256">Text</span><span class="sxs-lookup"><span data-stu-id="00eaf-256">Text</span></span> | <span data-ttu-id="00eaf-257">The full body of the tweet</span><span class="sxs-lookup"><span data-stu-id="00eaf-257">The full body of the tweet</span></span>


## <a name="get-support"></a><span data-ttu-id="00eaf-258">Get support</span><span class="sxs-lookup"><span data-stu-id="00eaf-258">Get support</span></span>
<span data-ttu-id="00eaf-259">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="00eaf-259">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00eaf-260">Next steps</span><span class="sxs-lookup"><span data-stu-id="00eaf-260">Next steps</span></span>
* [<span data-ttu-id="00eaf-261">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00eaf-261">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="00eaf-262">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00eaf-262">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="00eaf-263">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="00eaf-263">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="00eaf-264">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="00eaf-264">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="00eaf-265">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="00eaf-265">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)






