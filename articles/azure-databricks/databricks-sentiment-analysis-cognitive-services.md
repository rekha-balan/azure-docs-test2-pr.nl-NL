---
title: 'Tutorial: Sentiment analysis on streaming data using Azure Databricks'
description: Learn to use Azure Databricks with Event Hubs and Cognitive Services API to run sentiment analysis on streaming data in near real-time.
services: azure-databricks
author: lenadroid
manager: cgronlun
ms.service: azure-databricks
ms.custom: mvc
ms.topic: tutorial
ms.workload: Active
ms.date: 08/06/2018
ms.author: alehall
ms.openlocfilehash: edd78b9b54e39a25aa3349f6ad27e61991ea91d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866431"
---
# <a name="tutorial-sentiment-analysis-on-streaming-data-using-azure-databricks"></a><span data-ttu-id="75979-103">Tutorial: Sentiment analysis on streaming data using Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-103">Tutorial: Sentiment analysis on streaming data using Azure Databricks</span></span>

<span data-ttu-id="75979-104">In this tutorial, you learn how to run sentiment analysis on a stream of data using Azure Databricks in near real-time.</span><span class="sxs-lookup"><span data-stu-id="75979-104">In this tutorial, you learn how to run sentiment analysis on a stream of data using Azure Databricks in near real-time.</span></span> <span data-ttu-id="75979-105">You set up data ingestion system using Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-105">You set up data ingestion system using Azure Event Hubs.</span></span> <span data-ttu-id="75979-106">You consume the messages from Event Hubs into Azure Databricks using the Spark Event Hubs connector.</span><span class="sxs-lookup"><span data-stu-id="75979-106">You consume the messages from Event Hubs into Azure Databricks using the Spark Event Hubs connector.</span></span> <span data-ttu-id="75979-107">Finally, you use Microsoft Cognitive Service APIs to run sentiment analysis on the streamed data.</span><span class="sxs-lookup"><span data-stu-id="75979-107">Finally, you use Microsoft Cognitive Service APIs to run sentiment analysis on the streamed data.</span></span>

<span data-ttu-id="75979-108">By the end of this tutorial, you would have streamed tweets from Twitter that have the term "Azure" in them and ran sentiment analysis on the tweets.</span><span class="sxs-lookup"><span data-stu-id="75979-108">By the end of this tutorial, you would have streamed tweets from Twitter that have the term "Azure" in them and ran sentiment analysis on the tweets.</span></span>

<span data-ttu-id="75979-109">The following illustration shows the application flow:</span><span class="sxs-lookup"><span data-stu-id="75979-109">The following illustration shows the application flow:</span></span>

<span data-ttu-id="75979-110">![Azure Databricks with Event Hubs and Cognitive Services](./media/databricks-sentiment-analysis-cognitive-services/databricks-cognitive-services-tutorial.png "Azure Databricks with Event Hubs and Cognitive Services")</span><span class="sxs-lookup"><span data-stu-id="75979-110">![Azure Databricks with Event Hubs and Cognitive Services](./media/databricks-sentiment-analysis-cognitive-services/databricks-cognitive-services-tutorial.png "Azure Databricks with Event Hubs and Cognitive Services")</span></span>

<span data-ttu-id="75979-111">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="75979-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75979-112">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="75979-112">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="75979-113">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-113">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="75979-114">Create a Twitter app to access streaming data</span><span class="sxs-lookup"><span data-stu-id="75979-114">Create a Twitter app to access streaming data</span></span>
> * <span data-ttu-id="75979-115">Create notebooks in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-115">Create notebooks in Azure Databricks</span></span>
> * <span data-ttu-id="75979-116">Attach libraries for Event Hubs and Twitter API</span><span class="sxs-lookup"><span data-stu-id="75979-116">Attach libraries for Event Hubs and Twitter API</span></span>
> * <span data-ttu-id="75979-117">Create a Microsoft Cognitive Services account and retrieve the access key</span><span class="sxs-lookup"><span data-stu-id="75979-117">Create a Microsoft Cognitive Services account and retrieve the access key</span></span>
> * <span data-ttu-id="75979-118">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-118">Send tweets to Event Hubs</span></span>
> * <span data-ttu-id="75979-119">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-119">Read tweets from Event Hubs</span></span>
> * <span data-ttu-id="75979-120">Run sentiment analysis on tweets</span><span class="sxs-lookup"><span data-stu-id="75979-120">Run sentiment analysis on tweets</span></span>

<span data-ttu-id="75979-121">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="75979-121">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75979-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75979-122">Prerequisites</span></span>

<span data-ttu-id="75979-123">Before you start with this tutorial, make sure to meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="75979-123">Before you start with this tutorial, make sure to meet the following requirements:</span></span>
- <span data-ttu-id="75979-124">An Azure Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="75979-124">An Azure Event Hubs namespace.</span></span>
- <span data-ttu-id="75979-125">An Event Hub within the namespace.</span><span class="sxs-lookup"><span data-stu-id="75979-125">An Event Hub within the namespace.</span></span>
- <span data-ttu-id="75979-126">Connection string to access the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="75979-126">Connection string to access the Event Hubs namespace.</span></span> <span data-ttu-id="75979-127">The connection string should have a format similar to `Endpoint=sb://<namespace>.servicebus.windows.net/;SharedAccessKeyName=<key name>;SharedAccessKey=<key value>`.</span><span class="sxs-lookup"><span data-stu-id="75979-127">The connection string should have a format similar to `Endpoint=sb://<namespace>.servicebus.windows.net/;SharedAccessKeyName=<key name>;SharedAccessKey=<key value>`.</span></span>
- <span data-ttu-id="75979-128">Shared access policy name and policy key for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-128">Shared access policy name and policy key for Event Hubs.</span></span>

<span data-ttu-id="75979-129">You can meet these requirements by completing the steps in the article, [Create an Azure Event Hubs namespace and event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="75979-129">You can meet these requirements by completing the steps in the article, [Create an Azure Event Hubs namespace and event hub](../event-hubs/event-hubs-create.md).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="75979-130">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="75979-130">Log in to the Azure portal</span></span>

<span data-ttu-id="75979-131">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75979-131">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="75979-132">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="75979-132">Create an Azure Databricks workspace</span></span>

<span data-ttu-id="75979-133">In this section, you create an Azure Databricks workspace using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75979-133">In this section, you create an Azure Databricks workspace using the Azure portal.</span></span>

1. <span data-ttu-id="75979-134">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span><span class="sxs-lookup"><span data-stu-id="75979-134">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span></span>

    <span data-ttu-id="75979-135">![Databricks on Azure portal](./media/databricks-sentiment-analysis-cognitive-services/azure-databricks-on-portal.png "Databricks on Azure portal")</span><span class="sxs-lookup"><span data-stu-id="75979-135">![Databricks on Azure portal](./media/databricks-sentiment-analysis-cognitive-services/azure-databricks-on-portal.png "Databricks on Azure portal")</span></span>

3. <span data-ttu-id="75979-136">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="75979-136">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span></span>

    <span data-ttu-id="75979-137">![Create an Azure Databricks workspace](./media/databricks-sentiment-analysis-cognitive-services/create-databricks-workspace.png "Create an Azure Databricks workspace")</span><span class="sxs-lookup"><span data-stu-id="75979-137">![Create an Azure Databricks workspace](./media/databricks-sentiment-analysis-cognitive-services/create-databricks-workspace.png "Create an Azure Databricks workspace")</span></span>

    <span data-ttu-id="75979-138">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="75979-138">Provide the following values:</span></span>

    |<span data-ttu-id="75979-139">Property</span><span class="sxs-lookup"><span data-stu-id="75979-139">Property</span></span>  |<span data-ttu-id="75979-140">Description</span><span class="sxs-lookup"><span data-stu-id="75979-140">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="75979-141">**Workspace name**</span><span class="sxs-lookup"><span data-stu-id="75979-141">**Workspace name**</span></span>     | <span data-ttu-id="75979-142">Provide a name for your Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="75979-142">Provide a name for your Databricks workspace</span></span>        |
    |<span data-ttu-id="75979-143">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="75979-143">**Subscription**</span></span>     | <span data-ttu-id="75979-144">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="75979-144">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="75979-145">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="75979-145">**Resource group**</span></span>     | <span data-ttu-id="75979-146">Specify whether you want to create a new resource group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="75979-146">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="75979-147">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="75979-147">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="75979-148">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75979-148">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span></span> |
    |<span data-ttu-id="75979-149">**Location**</span><span class="sxs-lookup"><span data-stu-id="75979-149">**Location**</span></span>     | <span data-ttu-id="75979-150">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="75979-150">Select **East US 2**.</span></span> <span data-ttu-id="75979-151">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="75979-151">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="75979-152">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="75979-152">**Pricing Tier**</span></span>     |  <span data-ttu-id="75979-153">Choose between **Standard** or **Premium**.</span><span class="sxs-lookup"><span data-stu-id="75979-153">Choose between **Standard** or **Premium**.</span></span> <span data-ttu-id="75979-154">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="75979-154">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |

    <span data-ttu-id="75979-155">Select **Pin to dashboard** and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75979-155">Select **Pin to dashboard** and then select **Create**.</span></span>

4. <span data-ttu-id="75979-156">The account creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="75979-156">The account creation takes a few minutes.</span></span> <span data-ttu-id="75979-157">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span><span class="sxs-lookup"><span data-stu-id="75979-157">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span></span> <span data-ttu-id="75979-158">You may need to scroll right on your dashboard to see the tile.</span><span class="sxs-lookup"><span data-stu-id="75979-158">You may need to scroll right on your dashboard to see the tile.</span></span> <span data-ttu-id="75979-159">There is also a progress bar displayed near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="75979-159">There is also a progress bar displayed near the top of the screen.</span></span> <span data-ttu-id="75979-160">You can watch either area for progress.</span><span class="sxs-lookup"><span data-stu-id="75979-160">You can watch either area for progress.</span></span>

    <span data-ttu-id="75979-161">![Databricks deployment tile](./media/databricks-sentiment-analysis-cognitive-services/databricks-deployment-tile.png "Databricks deployment tile")</span><span class="sxs-lookup"><span data-stu-id="75979-161">![Databricks deployment tile](./media/databricks-sentiment-analysis-cognitive-services/databricks-deployment-tile.png "Databricks deployment tile")</span></span>

## <a name="create-a-spark-cluster-in-databricks"></a><span data-ttu-id="75979-162">Create a Spark cluster in Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-162">Create a Spark cluster in Databricks</span></span>

1. <span data-ttu-id="75979-163">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="75979-163">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span></span>

2. <span data-ttu-id="75979-164">You are redirected to the Azure Databricks portal.</span><span class="sxs-lookup"><span data-stu-id="75979-164">You are redirected to the Azure Databricks portal.</span></span> <span data-ttu-id="75979-165">From the portal, select **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="75979-165">From the portal, select **Cluster**.</span></span>

    <span data-ttu-id="75979-166">![Databricks on Azure](./media/databricks-sentiment-analysis-cognitive-services/databricks-on-azure.png "Databricks on Azure")</span><span class="sxs-lookup"><span data-stu-id="75979-166">![Databricks on Azure](./media/databricks-sentiment-analysis-cognitive-services/databricks-on-azure.png "Databricks on Azure")</span></span>

3. <span data-ttu-id="75979-167">In the **New cluster** page, provide the values to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="75979-167">In the **New cluster** page, provide the values to create a cluster.</span></span>

    <span data-ttu-id="75979-168">![Create Databricks Spark cluster on Azure](./media/databricks-sentiment-analysis-cognitive-services/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span><span class="sxs-lookup"><span data-stu-id="75979-168">![Create Databricks Spark cluster on Azure](./media/databricks-sentiment-analysis-cognitive-services/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span></span>

    <span data-ttu-id="75979-169">Accept all other default values other than the following:</span><span class="sxs-lookup"><span data-stu-id="75979-169">Accept all other default values other than the following:</span></span>

    * <span data-ttu-id="75979-170">Enter a name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="75979-170">Enter a name for the cluster.</span></span>
    * <span data-ttu-id="75979-171">For this article, create a cluster with **4.0 (beta)** runtime.</span><span class="sxs-lookup"><span data-stu-id="75979-171">For this article, create a cluster with **4.0 (beta)** runtime.</span></span>
    * <span data-ttu-id="75979-172">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span><span class="sxs-lookup"><span data-stu-id="75979-172">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span></span> <span data-ttu-id="75979-173">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span><span class="sxs-lookup"><span data-stu-id="75979-173">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span></span>

    <span data-ttu-id="75979-174">Select **Create cluster**.</span><span class="sxs-lookup"><span data-stu-id="75979-174">Select **Create cluster**.</span></span> <span data-ttu-id="75979-175">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="75979-175">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span></span>

## <a name="create-a-twitter-application"></a><span data-ttu-id="75979-176">Create a Twitter application</span><span class="sxs-lookup"><span data-stu-id="75979-176">Create a Twitter application</span></span>

<span data-ttu-id="75979-177">To receive a stream of tweets, you must create an application in Twitter.</span><span class="sxs-lookup"><span data-stu-id="75979-177">To receive a stream of tweets, you must create an application in Twitter.</span></span> <span data-ttu-id="75979-178">Follow the steps to create a Twitter application and record the values that you need to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="75979-178">Follow the steps to create a Twitter application and record the values that you need to complete this tutorial.</span></span>

1. <span data-ttu-id="75979-179">From a web browser, go to [Twitter Application Management](https://apps.twitter.com/), and select **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="75979-179">From a web browser, go to [Twitter Application Management](https://apps.twitter.com/), and select **Create New App**.</span></span>

    <span data-ttu-id="75979-180">![Create Twitter application](./media/databricks-sentiment-analysis-cognitive-services/databricks-create-twitter-app.png "Create Twitter application")</span><span class="sxs-lookup"><span data-stu-id="75979-180">![Create Twitter application](./media/databricks-sentiment-analysis-cognitive-services/databricks-create-twitter-app.png "Create Twitter application")</span></span>

2. <span data-ttu-id="75979-181">In the **Create an application** page, provide the details for the new app, and then select **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="75979-181">In the **Create an application** page, provide the details for the new app, and then select **Create your Twitter application**.</span></span>

    <span data-ttu-id="75979-182">![Twitter application details](./media/databricks-sentiment-analysis-cognitive-services/databricks-provide-twitter-app-details.png "Twitter application details")</span><span class="sxs-lookup"><span data-stu-id="75979-182">![Twitter application details](./media/databricks-sentiment-analysis-cognitive-services/databricks-provide-twitter-app-details.png "Twitter application details")</span></span>

3. <span data-ttu-id="75979-183">In the application page, select the **Keys and Access Tokens** tab and copy the values for **Consumer Key** and **Consumer Secret**.</span><span class="sxs-lookup"><span data-stu-id="75979-183">In the application page, select the **Keys and Access Tokens** tab and copy the values for **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="75979-184">Also, select **Create my access token** to generate the access tokens.</span><span class="sxs-lookup"><span data-stu-id="75979-184">Also, select **Create my access token** to generate the access tokens.</span></span> <span data-ttu-id="75979-185">Copy the values for **Access Token** and **Access Token Secret**.</span><span class="sxs-lookup"><span data-stu-id="75979-185">Copy the values for **Access Token** and **Access Token Secret**.</span></span>

    <span data-ttu-id="75979-186">![Twitter application details](./media/databricks-sentiment-analysis-cognitive-services/twitter-app-key-secret.png "Twitter application details")</span><span class="sxs-lookup"><span data-stu-id="75979-186">![Twitter application details](./media/databricks-sentiment-analysis-cognitive-services/twitter-app-key-secret.png "Twitter application details")</span></span>

<span data-ttu-id="75979-187">Save the values that you retrieved for the Twitter application.</span><span class="sxs-lookup"><span data-stu-id="75979-187">Save the values that you retrieved for the Twitter application.</span></span> <span data-ttu-id="75979-188">You need the values later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="75979-188">You need the values later in the tutorial.</span></span>

## <a name="attach-libraries-to-spark-cluster"></a><span data-ttu-id="75979-189">Attach libraries to Spark cluster</span><span class="sxs-lookup"><span data-stu-id="75979-189">Attach libraries to Spark cluster</span></span>

<span data-ttu-id="75979-190">In this tutorial, you use the Twitter APIs to send tweets to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-190">In this tutorial, you use the Twitter APIs to send tweets to Event Hubs.</span></span> <span data-ttu-id="75979-191">You also use the [Apache Spark Event Hubs connector](https://github.com/Azure/azure-event-hubs-spark) to read and write data into Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-191">You also use the [Apache Spark Event Hubs connector](https://github.com/Azure/azure-event-hubs-spark) to read and write data into Azure Event Hubs.</span></span> <span data-ttu-id="75979-192">To use these APIs as part of your cluster, add them as libraries to Azure Databricks and then associate them with your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="75979-192">To use these APIs as part of your cluster, add them as libraries to Azure Databricks and then associate them with your Spark cluster.</span></span> <span data-ttu-id="75979-193">The following instructions show how to add the library to the **Shared** folder in your workspace.</span><span class="sxs-lookup"><span data-stu-id="75979-193">The following instructions show how to add the library to the **Shared** folder in your workspace.</span></span>

1.  <span data-ttu-id="75979-194">In the Azure Databricks workspace, select **Workspace**, and then right-click **Shared**.</span><span class="sxs-lookup"><span data-stu-id="75979-194">In the Azure Databricks workspace, select **Workspace**, and then right-click **Shared**.</span></span> <span data-ttu-id="75979-195">From the context menu, select **Create** > **Library**.</span><span class="sxs-lookup"><span data-stu-id="75979-195">From the context menu, select **Create** > **Library**.</span></span>

    <span data-ttu-id="75979-196">![Add library dialog box](./media/databricks-sentiment-analysis-cognitive-services/databricks-add-library-option.png "Add library dialog box")</span><span class="sxs-lookup"><span data-stu-id="75979-196">![Add library dialog box](./media/databricks-sentiment-analysis-cognitive-services/databricks-add-library-option.png "Add library dialog box")</span></span>

2. <span data-ttu-id="75979-197">In the New Library page, for **Source** select **Maven Coordinate**.</span><span class="sxs-lookup"><span data-stu-id="75979-197">In the New Library page, for **Source** select **Maven Coordinate**.</span></span> <span data-ttu-id="75979-198">For **Coordinate**, enter the coordinate for the package you want to add.</span><span class="sxs-lookup"><span data-stu-id="75979-198">For **Coordinate**, enter the coordinate for the package you want to add.</span></span> <span data-ttu-id="75979-199">Here is the Maven coordinates for the libraries used in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="75979-199">Here is the Maven coordinates for the libraries used in this tutorial:</span></span>

    * <span data-ttu-id="75979-200">Spark Event Hubs connector - `com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1`</span><span class="sxs-lookup"><span data-stu-id="75979-200">Spark Event Hubs connector - `com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1`</span></span>
    * <span data-ttu-id="75979-201">Twitter API - `org.twitter4j:twitter4j-core:4.0.6`</span><span class="sxs-lookup"><span data-stu-id="75979-201">Twitter API - `org.twitter4j:twitter4j-core:4.0.6`</span></span>

    <span data-ttu-id="75979-202">![Provide Maven coordinates](./media/databricks-sentiment-analysis-cognitive-services/databricks-eventhub-specify-maven-coordinate.png "Provide Maven coordinates")</span><span class="sxs-lookup"><span data-stu-id="75979-202">![Provide Maven coordinates](./media/databricks-sentiment-analysis-cognitive-services/databricks-eventhub-specify-maven-coordinate.png "Provide Maven coordinates")</span></span>

3. <span data-ttu-id="75979-203">Select **Create Library**.</span><span class="sxs-lookup"><span data-stu-id="75979-203">Select **Create Library**.</span></span>

4. <span data-ttu-id="75979-204">Select the folder where you added the library, and then select the library name.</span><span class="sxs-lookup"><span data-stu-id="75979-204">Select the folder where you added the library, and then select the library name.</span></span>

    <span data-ttu-id="75979-205">![Select library to add](./media/databricks-sentiment-analysis-cognitive-services/select-library.png "Select library to add")</span><span class="sxs-lookup"><span data-stu-id="75979-205">![Select library to add](./media/databricks-sentiment-analysis-cognitive-services/select-library.png "Select library to add")</span></span>

5. <span data-ttu-id="75979-206">On the library page, select the cluster where you want to use the library.</span><span class="sxs-lookup"><span data-stu-id="75979-206">On the library page, select the cluster where you want to use the library.</span></span> <span data-ttu-id="75979-207">Once the library is successfully associated with the cluster, the status immediately changes to **Attached**.</span><span class="sxs-lookup"><span data-stu-id="75979-207">Once the library is successfully associated with the cluster, the status immediately changes to **Attached**.</span></span>

    <span data-ttu-id="75979-208">![Attach library to cluster](./media/databricks-sentiment-analysis-cognitive-services/databricks-library-attached.png "Attach library to cluster")</span><span class="sxs-lookup"><span data-stu-id="75979-208">![Attach library to cluster](./media/databricks-sentiment-analysis-cognitive-services/databricks-library-attached.png "Attach library to cluster")</span></span>

6. <span data-ttu-id="75979-209">Repeat these steps for the Twitter package, `twitter4j-core:4.0.6`.</span><span class="sxs-lookup"><span data-stu-id="75979-209">Repeat these steps for the Twitter package, `twitter4j-core:4.0.6`.</span></span>

## <a name="get-a-cognitive-services-access-key"></a><span data-ttu-id="75979-210">Get a Cognitive Services access key</span><span class="sxs-lookup"><span data-stu-id="75979-210">Get a Cognitive Services access key</span></span>

<span data-ttu-id="75979-211">In this tutorial, you use the [Microsoft Cognitive Services Text Analytics APIs](../cognitive-services/text-analytics/overview.md) to run sentiment analysis on a stream of tweets in near real-time.</span><span class="sxs-lookup"><span data-stu-id="75979-211">In this tutorial, you use the [Microsoft Cognitive Services Text Analytics APIs](../cognitive-services/text-analytics/overview.md) to run sentiment analysis on a stream of tweets in near real-time.</span></span> <span data-ttu-id="75979-212">Before you use the APIs, you must create an Microsoft Cognitive Services account on Azure and retrieve an access key to use the Text Analytics APIs.</span><span class="sxs-lookup"><span data-stu-id="75979-212">Before you use the APIs, you must create an Microsoft Cognitive Services account on Azure and retrieve an access key to use the Text Analytics APIs.</span></span>

1. <span data-ttu-id="75979-213">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75979-213">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="75979-214">Select **+ Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="75979-214">Select **+ Create a resource**.</span></span>

3. <span data-ttu-id="75979-215">Under Azure Marketplace, Select **AI + Cognitive Services** > **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="75979-215">Under Azure Marketplace, Select **AI + Cognitive Services** > **Text Analytics API**.</span></span>

    <span data-ttu-id="75979-216">![Create cognitive services account](./media/databricks-sentiment-analysis-cognitive-services/databricks-cognitive-services-text-api.png "Create cognitive services account")</span><span class="sxs-lookup"><span data-stu-id="75979-216">![Create cognitive services account](./media/databricks-sentiment-analysis-cognitive-services/databricks-cognitive-services-text-api.png "Create cognitive services account")</span></span>

4. <span data-ttu-id="75979-217">In the **Create** dialog box, provide the following values:</span><span class="sxs-lookup"><span data-stu-id="75979-217">In the **Create** dialog box, provide the following values:</span></span>

    <span data-ttu-id="75979-218">![Create cognitive services account](./media/databricks-sentiment-analysis-cognitive-services/create-cognitive-services-account.png "Create cognitive services account")</span><span class="sxs-lookup"><span data-stu-id="75979-218">![Create cognitive services account](./media/databricks-sentiment-analysis-cognitive-services/create-cognitive-services-account.png "Create cognitive services account")</span></span>

    - <span data-ttu-id="75979-219">Enter a name for the Cognitive Services account.</span><span class="sxs-lookup"><span data-stu-id="75979-219">Enter a name for the Cognitive Services account.</span></span>
    - <span data-ttu-id="75979-220">Select the Azure subscription under which the account is created.</span><span class="sxs-lookup"><span data-stu-id="75979-220">Select the Azure subscription under which the account is created.</span></span>
    - <span data-ttu-id="75979-221">Select an Azure location.</span><span class="sxs-lookup"><span data-stu-id="75979-221">Select an Azure location.</span></span>
    - <span data-ttu-id="75979-222">Select a pricing tier for the service.</span><span class="sxs-lookup"><span data-stu-id="75979-222">Select a pricing tier for the service.</span></span> <span data-ttu-id="75979-223">For more information about Cognitive Services pricing, see [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="75979-223">For more information about Cognitive Services pricing, see [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/).</span></span>
    - <span data-ttu-id="75979-224">Specifiy whether you want to create a new resource group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="75979-224">Specifiy whether you want to create a new resource group or select an existing one.</span></span>

    <span data-ttu-id="75979-225">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75979-225">Select **Create**.</span></span>

5. <span data-ttu-id="75979-226">After the accout is created, from the **Overview** tab, select **Show access keys**.</span><span class="sxs-lookup"><span data-stu-id="75979-226">After the accout is created, from the **Overview** tab, select **Show access keys**.</span></span>

    <span data-ttu-id="75979-227">![Show access keys](./media/databricks-sentiment-analysis-cognitive-services/cognitive-services-get-access-keys.png "Show access keys")</span><span class="sxs-lookup"><span data-stu-id="75979-227">![Show access keys](./media/databricks-sentiment-analysis-cognitive-services/cognitive-services-get-access-keys.png "Show access keys")</span></span>

    <span data-ttu-id="75979-228">Also, copy a part of the endpoint URL, as shown in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="75979-228">Also, copy a part of the endpoint URL, as shown in the screenshot.</span></span> <span data-ttu-id="75979-229">You need this URL in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="75979-229">You need this URL in the tutorial.</span></span>

6. <span data-ttu-id="75979-230">Under **Manage keys**, select the copy icon against the key you want to use.</span><span class="sxs-lookup"><span data-stu-id="75979-230">Under **Manage keys**, select the copy icon against the key you want to use.</span></span>

    <span data-ttu-id="75979-231">![Copy access keys](./media/databricks-sentiment-analysis-cognitive-services/cognitive-services-copy-access-keys.png "Copy access keys")</span><span class="sxs-lookup"><span data-stu-id="75979-231">![Copy access keys](./media/databricks-sentiment-analysis-cognitive-services/cognitive-services-copy-access-keys.png "Copy access keys")</span></span>

7. <span data-ttu-id="75979-232">Save the values for the endpoint URL and the access key, you retrieved in this step.</span><span class="sxs-lookup"><span data-stu-id="75979-232">Save the values for the endpoint URL and the access key, you retrieved in this step.</span></span> <span data-ttu-id="75979-233">You need it later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="75979-233">You need it later in this tutorial.</span></span>

## <a name="create-notebooks-in-databricks"></a><span data-ttu-id="75979-234">Create notebooks in Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-234">Create notebooks in Databricks</span></span>

<span data-ttu-id="75979-235">In this section, you create two notebooks in Databricks workspace with the following names</span><span class="sxs-lookup"><span data-stu-id="75979-235">In this section, you create two notebooks in Databricks workspace with the following names</span></span>

- <span data-ttu-id="75979-236">**SendTweetsToEventHub** - A producer notebook you use to get tweets from Twitter and stream them to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-236">**SendTweetsToEventHub** - A producer notebook you use to get tweets from Twitter and stream them to Event Hubs.</span></span>
- <span data-ttu-id="75979-237">**AnalyzeTweetsFromEventHub** - A consumer notebook you use to read the tweets from Event Hubs and run sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="75979-237">**AnalyzeTweetsFromEventHub** - A consumer notebook you use to read the tweets from Event Hubs and run sentiment analysis.</span></span>

1. <span data-ttu-id="75979-238">In the left pane, select **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="75979-238">In the left pane, select **Workspace**.</span></span> <span data-ttu-id="75979-239">From the **Workspace** drop-down, select **Create**, and then select **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="75979-239">From the **Workspace** drop-down, select **Create**, and then select **Notebook**.</span></span>

    <span data-ttu-id="75979-240">![Create notebook in Databricks](./media/databricks-sentiment-analysis-cognitive-services/databricks-create-notebook.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="75979-240">![Create notebook in Databricks](./media/databricks-sentiment-analysis-cognitive-services/databricks-create-notebook.png "Create notebook in Databricks")</span></span>

2. <span data-ttu-id="75979-241">In the **Create Notebook** dialog box, enter **SendTweetsToEventHub**, select **Scala** as the language, and select the Spark cluster that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="75979-241">In the **Create Notebook** dialog box, enter **SendTweetsToEventHub**, select **Scala** as the language, and select the Spark cluster that you created earlier.</span></span>

    <span data-ttu-id="75979-242">![Create notebook in Databricks](./media/databricks-sentiment-analysis-cognitive-services/databricks-notebook-details.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="75979-242">![Create notebook in Databricks](./media/databricks-sentiment-analysis-cognitive-services/databricks-notebook-details.png "Create notebook in Databricks")</span></span>

    <span data-ttu-id="75979-243">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75979-243">Select **Create**.</span></span>

3. <span data-ttu-id="75979-244">Repeat the steps to create the **AnalyzeTweetsFromEventHub** notebook.</span><span class="sxs-lookup"><span data-stu-id="75979-244">Repeat the steps to create the **AnalyzeTweetsFromEventHub** notebook.</span></span>

## <a name="send-tweets-to-event-hubs"></a><span data-ttu-id="75979-245">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-245">Send tweets to Event Hubs</span></span>

<span data-ttu-id="75979-246">In the **SendTweetsToEventHub** notebook, paste the following code, and replace the placeholder with values for your Event Hubs namesapce and Twitter application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="75979-246">In the **SendTweetsToEventHub** notebook, paste the following code, and replace the placeholder with values for your Event Hubs namesapce and Twitter application that you created earlier.</span></span> <span data-ttu-id="75979-247">This notebook streams tweets with the keyword "Azure" into Event Hubs in real time.</span><span class="sxs-lookup"><span data-stu-id="75979-247">This notebook streams tweets with the keyword "Azure" into Event Hubs in real time.</span></span>

    import java.util._
    import scala.collection.JavaConverters._
    import com.microsoft.azure.eventhubs._
    import java.util.concurrent._

    val namespaceName = "<EVENT HUBS NAMESPACE>"
    val eventHubName = "<EVENT HUB NAME>"
    val sasKeyName = "<POLICY NAME>"
    val sasKey = "<POLICY KEY>"
    val connStr = new ConnectionStringBuilder()
                .setNamespaceName(namespaceName)
                .setEventHubName(eventHubName)
                .setSasKeyName(sasKeyName)
                .setSasKey(sasKey)

    val pool = Executors.newFixedThreadPool(1)
    val eventHubClient = EventHubClient.create(connStr.toString(), pool)

    def sendEvent(message: String) = {
      val messageData = EventData.create(message.getBytes("UTF-8"))
      eventHubClient.get().send(messageData)
      System.out.println("Sent event: " + message + "\n")
    }

    import twitter4j._
    import twitter4j.TwitterFactory
    import twitter4j.Twitter
    import twitter4j.conf.ConfigurationBuilder

    // Twitter configuration!
    // Replace values below with yours

    val twitterConsumerKey = "<CONSUMER KEY>"
    val twitterConsumerSecret = "<CONSUMER SECRET>"
    val twitterOauthAccessToken = "<ACCESS TOKEN>"
    val twitterOauthTokenSecret = "<TOKEN SECRET>"

    val cb = new ConfigurationBuilder()
      cb.setDebugEnabled(true)
      .setOAuthConsumerKey(twitterConsumerKey)
      .setOAuthConsumerSecret(twitterConsumerSecret)
      .setOAuthAccessToken(twitterOauthAccessToken)
      .setOAuthAccessTokenSecret(twitterOauthTokenSecret)

    val twitterFactory = new TwitterFactory(cb.build())
    val twitter = twitterFactory.getInstance()

    // Getting tweets with keyword "Azure" and sending them to the Event Hub in realtime!

    val query = new Query(" #Azure ")
    query.setCount(100)
    query.lang("en")
    var finished = false
    while (!finished) {
      val result = twitter.search(query)
      val statuses = result.getTweets()
      var lowestStatusId = Long.MaxValue
      for (status <- statuses.asScala) {
        if(!status.isRetweet()){
          sendEvent(status.getText())
        }
        lowestStatusId = Math.min(status.getId(), lowestStatusId)
        Thread.sleep(2000)
      }
      query.setMaxId(lowestStatusId - 1)
    }

    // Closing connection to the Event Hub
    eventHubClient.get().close()

<span data-ttu-id="75979-248">To run the notebook, press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="75979-248">To run the notebook, press **SHIFT + ENTER**.</span></span> <span data-ttu-id="75979-249">You see an output as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="75979-249">You see an output as shown in the following snippet.</span></span> <span data-ttu-id="75979-250">Each event in the output is a tweet that is ingested into the Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="75979-250">Each event in the output is a tweet that is ingested into the Event Hubs.</span></span>

    Sent event: @Microsoft and @Esri launch Geospatial AI on Azure https://t.co/VmLUCiPm6q via @geoworldmedia #geoai #azure #gis #ArtificialIntelligence

    Sent event: Public preview of Java on App Service, built-in support for Tomcat and OpenJDK
    https://t.co/7vs7cKtvah
    #cloudcomputing #Azure

    Sent event: 4 Killer #Azure Features for #Data #Performance https://t.co/kpIb7hFO2j by @RedPixie

    Sent event: Migrate your databases to a fully managed service with Azure SQL Database Managed Instance | #Azure | #Cloud https://t.co/sJHXN4trDk

    Sent event: Top 10 Tricks to #Save Money with #Azure Virtual Machines https://t.co/F2wshBXdoz #Cloud

    ...
    ...

## <a name="read-tweets-from-event-hubs"></a><span data-ttu-id="75979-251">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-251">Read tweets from Event Hubs</span></span>

<span data-ttu-id="75979-252">In the **AnalyzeTweetsFromEventHub** notebook, paste the following code, and replace the placeholder with values for your Azure Event Hubs that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="75979-252">In the **AnalyzeTweetsFromEventHub** notebook, paste the following code, and replace the placeholder with values for your Azure Event Hubs that you created earlier.</span></span> <span data-ttu-id="75979-253">This notebook reads the tweets that you earlier streamed into Event Hubs using the **SendTweetsToEventHub** notebook.</span><span class="sxs-lookup"><span data-stu-id="75979-253">This notebook reads the tweets that you earlier streamed into Event Hubs using the **SendTweetsToEventHub** notebook.</span></span>

    import org.apache.spark.eventhubs._

    // Build connection string with the above information
    val connectionString = ConnectionStringBuilder("<EVENT HUBS CONNECTION STRING>")
      .setEventHubName("<EVENT HUB NAME>")
      .build

    val customEventhubParameters =
      EventHubsConf(connectionString)
      .setMaxEventsPerTrigger(5)

    val incomingStream = spark.readStream.format("eventhubs").options(customEventhubParameters.toMap).load()

    incomingStream.printSchema

    // Sending the incoming stream into the console.
    // Data comes in batches!
    incomingStream.writeStream.outputMode("append").format("console").option("truncate", false).start().awaitTermination()

<span data-ttu-id="75979-254">You get the following output:</span><span class="sxs-lookup"><span data-stu-id="75979-254">You get the following output:</span></span>


    root
     |-- body: binary (nullable = true)
     |-- offset: long (nullable = true)
     |-- seqNumber: long (nullable = true)
     |-- enqueuedTime: long (nullable = true)
     |-- publisher: string (nullable = true)
     |-- partitionKey: string (nullable = true)

    -------------------------------------------
    Batch: 0
    -------------------------------------------
    +------+------+--------------+---------------+---------+------------+
    |body  |offset|sequenceNumber|enqueuedTime   |publisher|partitionKey|
    +------+------+--------------+---------------+---------+------------+
    |[50 75 62 6C 69 63 20 70 72 65 76 69 65 77 20 6F 66 20 4A 61 76 61 20 6F 6E 20 41 70 70 20 53 65 72 76 69 63 65 2C 20 62 75 69 6C 74 2D 69 6E 20 73 75 70 70 6F 72 74 20 66 6F 72 20 54 6F 6D 63 61 74 20 61 6E 64 20 4F 70 65 6E 4A 44 4B 0A 68 74 74 70 73 3A 2F 2F 74 2E 63 6F 2F 37 76 73 37 63 4B 74 76 61 68 20 0A 23 63 6C 6F 75 64 63 6F 6D 70 75 74 69 6E 67 20 23 41 7A 75 72 65]                              |0     |0             |2018-03-09 05:49:08.86 |null     |null        |
    |[4D 69 67 72 61 74 65 20 79 6F 75 72 20 64 61 74 61 62 61 73 65 73 20 74 6F 20 61 20 66 75 6C 6C 79 20 6D 61 6E 61 67 65 64 20 73 65 72 76 69 63 65 20 77 69 74 68 20 41 7A 75 72 65 20 53 51 4C 20 44 61 74 61 62 61 73 65 20 4D 61 6E 61 67 65 64 20 49 6E 73 74 61 6E 63 65 20 7C 20 23 41 7A 75 72 65 20 7C 20 23 43 6C 6F 75 64 20 68 74 74 70 73 3A 2F 2F 74 2E 63 6F 2F 73 4A 48 58 4E 34 74 72 44 6B]            |168   |1             |2018-03-09 05:49:24.752|null     |null        |
    +------+------+--------------+---------------+---------+------------+

    -------------------------------------------
    Batch: 1
    -------------------------------------------
    ...
    ...

<span data-ttu-id="75979-255">Because the output is in a binary mode, use the following snippet to convert it into string.</span><span class="sxs-lookup"><span data-stu-id="75979-255">Because the output is in a binary mode, use the following snippet to convert it into string.</span></span>

    import org.apache.spark.sql.types._
    import org.apache.spark.sql.functions._

    // Event Hub message format is JSON and contains "body" field
    // Body is binary, so we cast it to string to see the actual content of the message
    val messages =
      incomingStream
      .withColumn("Offset", $"offset".cast(LongType))
      .withColumn("Time (readable)", $"enqueuedTime".cast(TimestampType))
      .withColumn("Timestamp", $"enqueuedTime".cast(LongType))
      .withColumn("Body", $"body".cast(StringType))
      .select("Offset", "Time (readable)", "Timestamp", "Body")

    messages.printSchema

    messages.writeStream.outputMode("append").format("console").option("truncate", false).start().awaitTermination()

<span data-ttu-id="75979-256">The output now resembles the following snippet:</span><span class="sxs-lookup"><span data-stu-id="75979-256">The output now resembles the following snippet:</span></span>

    root
     |-- Offset: long (nullable = true)
     |-- Time (readable): timestamp (nullable = true)
     |-- Timestamp: long (nullable = true)
     |-- Body: string (nullable = true)

    -------------------------------------------
    Batch: 0
    -------------------------------------------
    +------+-----------------+----------+-------+
    |Offset|Time (readable)  |Timestamp |Body
    +------+-----------------+----------+-------+
    |0     |2018-03-09 05:49:08.86 |1520574548|Public preview of Java on App Service, built-in support for Tomcat and OpenJDK
    https://t.co/7vs7cKtvah
    #cloudcomputing #Azure          |
    |168   |2018-03-09 05:49:24.752|1520574564|Migrate your databases to a fully managed service with Azure SQL Database Managed Instance | #Azure | #Cloud https://t.co/sJHXN4trDk    |
    |0     |2018-03-09 05:49:02.936|1520574542|@Microsoft and @Esri launch Geospatial AI on Azure https://t.co/VmLUCiPm6q via @geoworldmedia #geoai #azure #gis #ArtificialIntelligence|
    |176   |2018-03-09 05:49:20.801|1520574560|4 Killer #Azure Features for #Data #Performance https://t.co/kpIb7hFO2j by @RedPixie                                                    |
    +------+-----------------+----------+-------+
    -------------------------------------------
    Batch: 1
    -------------------------------------------
    ...
    ...

<span data-ttu-id="75979-257">You have now streamed data from Azure Event Hubs into Azure Databricks at near real-time using the Event Hubs connector for Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="75979-257">You have now streamed data from Azure Event Hubs into Azure Databricks at near real-time using the Event Hubs connector for Apache Spark.</span></span> <span data-ttu-id="75979-258">For more information on how to use the Event Hubs connector for Spark, see the [connector documentation](https://github.com/Azure/azure-event-hubs-spark/tree/master/docs).</span><span class="sxs-lookup"><span data-stu-id="75979-258">For more information on how to use the Event Hubs connector for Spark, see the [connector documentation](https://github.com/Azure/azure-event-hubs-spark/tree/master/docs).</span></span>

## <a name="run-sentiment-analysis-on-tweets"></a><span data-ttu-id="75979-259">Run sentiment analysis on tweets</span><span class="sxs-lookup"><span data-stu-id="75979-259">Run sentiment analysis on tweets</span></span>

<span data-ttu-id="75979-260">In this section, you run sentiment analysis on the tweets received using the Twitter API.</span><span class="sxs-lookup"><span data-stu-id="75979-260">In this section, you run sentiment analysis on the tweets received using the Twitter API.</span></span> <span data-ttu-id="75979-261">For this section, you add the code snippets to the same **AnalyzeTweetsFromEventHub** notebook.</span><span class="sxs-lookup"><span data-stu-id="75979-261">For this section, you add the code snippets to the same **AnalyzeTweetsFromEventHub** notebook.</span></span>

<span data-ttu-id="75979-262">Start by adding a new code cell in the notebook and paste the code snippet provided below.</span><span class="sxs-lookup"><span data-stu-id="75979-262">Start by adding a new code cell in the notebook and paste the code snippet provided below.</span></span> <span data-ttu-id="75979-263">This code snippet defines data types for working with the Language and Sentiment API.</span><span class="sxs-lookup"><span data-stu-id="75979-263">This code snippet defines data types for working with the Language and Sentiment API.</span></span>

    import java.io._
    import java.net._
    import java.util._

    class Document(var id: String, var text: String, var language: String = "", var sentiment: Double = 0.0) extends Serializable

    class Documents(var documents: List[Document] = new ArrayList[Document]()) extends Serializable {

        def add(id: String, text: String, language: String = "") {
            documents.add (new Document(id, text, language))
        }
        def add(doc: Document) {
            documents.add (doc)
        }
    }

<span data-ttu-id="75979-264">Add a new code cell and paste the code snippet provided below.</span><span class="sxs-lookup"><span data-stu-id="75979-264">Add a new code cell and paste the code snippet provided below.</span></span> <span data-ttu-id="75979-265">This code snippet is required for parsing JSON strings.</span><span class="sxs-lookup"><span data-stu-id="75979-265">This code snippet is required for parsing JSON strings.</span></span>

    class CC[T] extends Serializable { def unapply(a:Any):Option[T] = Some(a.asInstanceOf[T]) }
    object M extends CC[scala.collection.immutable.Map[String, Any]]
    object L extends CC[scala.collection.immutable.List[Any]]
    object S extends CC[String]
    object D extends CC[Double]

<span data-ttu-id="75979-266">Add a new code cell and paste the snippet provided below.</span><span class="sxs-lookup"><span data-stu-id="75979-266">Add a new code cell and paste the snippet provided below.</span></span> <span data-ttu-id="75979-267">This snippet defines an object that contains functions to call the Text Analysis API to run language detection and sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="75979-267">This snippet defines an object that contains functions to call the Text Analysis API to run language detection and sentiment analysis.</span></span> <span data-ttu-id="75979-268">Make sure you replace the placeholders, `<PROVIDE ACCESS KEY HERE>` and `<PROVIDE HOST HERE>`, with the values you retrieved for your Cognitive Services account.</span><span class="sxs-lookup"><span data-stu-id="75979-268">Make sure you replace the placeholders, `<PROVIDE ACCESS KEY HERE>` and `<PROVIDE HOST HERE>`, with the values you retrieved for your Cognitive Services account.</span></span>

    import javax.net.ssl.HttpsURLConnection
    import com.google.gson.Gson
    import com.google.gson.GsonBuilder
    import com.google.gson.JsonObject
    import com.google.gson.JsonParser
    import scala.util.parsing.json._

    object SentimentDetector extends Serializable {

      // Cognitive Services API connection settings
      val accessKey = "<PROVIDE ACCESS KEY HERE>"
      val host = "<PROVIDE HOST HERE>"
      val languagesPath = "/text/analytics/v2.0/languages"
      val sentimentPath = "/text/analytics/v2.0/sentiment"
      val languagesUrl = new URL(host+languagesPath)
      val sentimenUrl = new URL(host+sentimentPath)

      def getConnection(path: URL): HttpsURLConnection = {
        val connection = path.openConnection().asInstanceOf[HttpsURLConnection]
        connection.setRequestMethod("POST")
        connection.setRequestProperty("Content-Type", "text/json")
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", accessKey)
        connection.setDoOutput(true)
        return connection
      }

      def prettify (json_text: String): String = {
        val parser = new JsonParser()
        val json = parser.parse(json_text).getAsJsonObject()
        val gson = new GsonBuilder().setPrettyPrinting().create()
        return gson.toJson(json)
      }

      // Handles the call to Cognitive Services API.
      // Expects Documents as parameters and the address of the API to call.
      // Returns an instance of Documents in response.
      def processUsingApi(inputDocs: Documents, path: URL): String = {
        val docText = new Gson().toJson(inputDocs)
        val encoded_text = docText.getBytes("UTF-8")
        val connection = getConnection(path)
        val wr = new DataOutputStream(connection.getOutputStream())
        wr.write(encoded_text, 0, encoded_text.length)
        wr.flush()
        wr.close()

        val response = new StringBuilder()
        val in = new BufferedReader(new InputStreamReader(connection.getInputStream()))
        var line = in.readLine()
        while (line != null) {
            response.append(line)
            line = in.readLine()
        }
        in.close()
        return response.toString()
      }

      // Calls the language API for specified documents.
      // Returns a documents with language field set.
      def getLanguage (inputDocs: Documents): Documents = {
        try {
          val response = processUsingApi(inputDocs, languagesUrl)
          // In case we need to log the json response somewhere
          val niceResponse = prettify(response)
          val docs = new Documents()
          val result = for {
                // Deserializing the JSON response from the API into Scala types
                Some(M(map)) <- scala.collection.immutable.List(JSON.parseFull(niceResponse))
                L(documents) = map("documents")
                M(document) <- documents
                S(id) = document("id")
                L(detectedLanguages) = document("detectedLanguages")
                M(detectedLanguage) <- detectedLanguages
                S(language) = detectedLanguage("iso6391Name")
          } yield {
                docs.add(new Document(id = id, text = id, language = language))
          }
          return docs
        } catch {
              case e: Exception => return new Documents()
        }
      }

      // Calls the sentiment API for specified documents. Needs a language field to be set for each of them.
      // Returns documents with sentiment field set, taking a value in the range from 0 to 1.
      def getSentiment (inputDocs: Documents): Documents = {
        try {
          val response = processUsingApi(inputDocs, sentimenUrl)
          val niceResponse = prettify(response)
          val docs = new Documents()
          val result = for {
                // Deserializing the JSON response from the API into Scala types
                Some(M(map)) <- scala.collection.immutable.List(JSON.parseFull(niceResponse))
                L(documents) = map("documents")
                M(document) <- documents
                S(id) = document("id")
                D(sentiment) = document("score")
          } yield {
                docs.add(new Document(id = id, text = id, sentiment = sentiment))
          }
          return docs
        } catch {
            case e: Exception => return new Documents()
        }
      }
    }

    // User Defined Function for processing content of messages to return their sentiment.
    val toSentiment = udf((textContent: String) => {
      val inputDocs = new Documents()
      inputDocs.add (textContent, textContent)
      val docsWithLanguage = SentimentDetector.getLanguage(inputDocs)
      val docsWithSentiment = SentimentDetector.getSentiment(docsWithLanguage)
      if (docsWithLanguage.documents.isEmpty) {
        // Placeholder value to display when unable to perform sentiment request for text in unknown language
        (-1).toDouble
      } else {
        docsWithSentiment.documents.get(0).sentiment.toDouble
      }
    })

<span data-ttu-id="75979-269">Add a final code cell to prepare a dataframe with the content of the tweet and the sentiment associated with the tweet.</span><span class="sxs-lookup"><span data-stu-id="75979-269">Add a final code cell to prepare a dataframe with the content of the tweet and the sentiment associated with the tweet.</span></span>

    // Prepare a dataframe with Content and Sentiment columns
    val streamingDataFrame = incomingStream.selectExpr("cast (body as string) AS Content").withColumn("Sentiment", toSentiment($"Content"))

    // Display the streaming data with the sentiment
    streamingDataFrame.writeStream.outputMode("append").format("console").option("truncate", false).start().awaitTermination()

<span data-ttu-id="75979-270">You should see an output like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="75979-270">You should see an output like the following snippet:</span></span>

    -------------------------------------------
    Batch: 0
    -------------------------------------------
    +--------------------------------+------------------+
    |Content                         |Sentiment         |
    +--------------------------------+------------------+
    |Public preview of Java on App Service, built-in support for Tomcat and OpenJDK
    https://t.co/7vs7cKtvah   #cloudcomputing #Azure          |0.7761918306350708|
    |Migrate your databases to a fully managed service with Azure SQL Database Managed Instance | #Azure | #Cloud https://t.co/sJHXN4trDk    |0.8558163642883301|
    |@Microsoft and @Esri launch Geospatial AI on Azure https://t.co/VmLUCiPm6q via @geoworldmedia #geoai #azure #gis #ArtificialIntelligence|0.5               |
    |4 Killer #Azure Features for #Data #Performance https://t.co/kpIb7hFO2j by @RedPixie                                                    |0.5               |
    +--------------------------------+------------------+

<span data-ttu-id="75979-271">A value closer to **1** in the **Sentiment** column suggests a great experience with Azure.</span><span class="sxs-lookup"><span data-stu-id="75979-271">A value closer to **1** in the **Sentiment** column suggests a great experience with Azure.</span></span> <span data-ttu-id="75979-272">A value closer to **0** suggests issues that users faced while working with Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="75979-272">A value closer to **0** suggests issues that users faced while working with Microsoft Azure.</span></span>

<span data-ttu-id="75979-273">That's it!</span><span class="sxs-lookup"><span data-stu-id="75979-273">That's it!</span></span> <span data-ttu-id="75979-274">Using Azure Databricks, you have successfully streamed data into Azure Event Hubs, consumed the stream data using the Event Hubs connector, and then ran sentiment analysis on streaming data in near real-time.</span><span class="sxs-lookup"><span data-stu-id="75979-274">Using Azure Databricks, you have successfully streamed data into Azure Event Hubs, consumed the stream data using the Event Hubs connector, and then ran sentiment analysis on streaming data in near real-time.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="75979-275">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="75979-275">Clean up resources</span></span>

<span data-ttu-id="75979-276">After you have finished running the tutorial, you can terminate the cluster.</span><span class="sxs-lookup"><span data-stu-id="75979-276">After you have finished running the tutorial, you can terminate the cluster.</span></span> <span data-ttu-id="75979-277">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span><span class="sxs-lookup"><span data-stu-id="75979-277">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span></span> <span data-ttu-id="75979-278">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span><span class="sxs-lookup"><span data-stu-id="75979-278">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span></span>

<span data-ttu-id="75979-279">![Stop a Databricks cluster](./media/databricks-sentiment-analysis-cognitive-services/terminate-databricks-cluster.png "Stop a Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="75979-279">![Stop a Databricks cluster](./media/databricks-sentiment-analysis-cognitive-services/terminate-databricks-cluster.png "Stop a Databricks cluster")</span></span>

<span data-ttu-id="75979-280">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="75979-280">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span></span> <span data-ttu-id="75979-281">In such a case, the cluster will automatically stop if it has been inactive for the specified time.</span><span class="sxs-lookup"><span data-stu-id="75979-281">In such a case, the cluster will automatically stop if it has been inactive for the specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75979-282">Next steps</span><span class="sxs-lookup"><span data-stu-id="75979-282">Next steps</span></span>
<span data-ttu-id="75979-283">In this tutorial, you learned how to use Azure Databricks to stream data into Azure Event Hubs and then read the streaming data from Event Hubs in real time.</span><span class="sxs-lookup"><span data-stu-id="75979-283">In this tutorial, you learned how to use Azure Databricks to stream data into Azure Event Hubs and then read the streaming data from Event Hubs in real time.</span></span> <span data-ttu-id="75979-284">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="75979-284">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="75979-285">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="75979-285">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="75979-286">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-286">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="75979-287">Create a Twitter app to access streaming data</span><span class="sxs-lookup"><span data-stu-id="75979-287">Create a Twitter app to access streaming data</span></span>
> * <span data-ttu-id="75979-288">Create notebooks in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="75979-288">Create notebooks in Azure Databricks</span></span>
> * <span data-ttu-id="75979-289">Add and attach libraries for Event Hubs and Twitter API</span><span class="sxs-lookup"><span data-stu-id="75979-289">Add and attach libraries for Event Hubs and Twitter API</span></span>
> * <span data-ttu-id="75979-290">Create a Microsoft Cognitive Services account and retrieve the access key</span><span class="sxs-lookup"><span data-stu-id="75979-290">Create a Microsoft Cognitive Services account and retrieve the access key</span></span>
> * <span data-ttu-id="75979-291">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-291">Send tweets to Event Hubs</span></span>
> * <span data-ttu-id="75979-292">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="75979-292">Read tweets from Event Hubs</span></span>
> * <span data-ttu-id="75979-293">Run sentiment analysis on tweets</span><span class="sxs-lookup"><span data-stu-id="75979-293">Run sentiment analysis on tweets</span></span>

<span data-ttu-id="75979-294">Advance to the next tutorial to learn about performing machine learning tasks using Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="75979-294">Advance to the next tutorial to learn about performing machine learning tasks using Azure Databricks.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="75979-295">Machine Learning using Azure Databricks </span><span class="sxs-lookup"><span data-stu-id="75979-295">Machine Learning using Azure Databricks </span></span>](https://docs.azuredatabricks.net/spark/latest/mllib/decision-trees.html)
