---
title: 'Tutorial: Stream data into Azure Databricks using Event Hubs | Microsoft Docs'
description: Learn to use Azure Databricks with Event Hubs to ingest streaming data from Twitter and read the data in near real time.
services: azure-databricks
documentationcenter: ''
author: lenadroid
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.custom: mvc
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: Active
ms.date: 06/21/2018
ms.author: alehall
ms.openlocfilehash: a06ee5b03521fa2e0a711f5194cf01b32e7cea37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868438"
---
# <a name="tutorial-stream-data-into-azure-databricks-using-event-hubs"></a><span data-ttu-id="d0be8-103">Tutorial: Stream data into Azure Databricks using Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-103">Tutorial: Stream data into Azure Databricks using Event Hubs</span></span>

<span data-ttu-id="d0be8-104">In this tutorial, you connect a data ingestion system with Azure Databricks to stream data into an Apache Spark cluster in near real-time.</span><span class="sxs-lookup"><span data-stu-id="d0be8-104">In this tutorial, you connect a data ingestion system with Azure Databricks to stream data into an Apache Spark cluster in near real-time.</span></span> <span data-ttu-id="d0be8-105">You set up data ingestion system using Azure Event Hubs and then connect it to Azure Databricks to process the messages coming through.</span><span class="sxs-lookup"><span data-stu-id="d0be8-105">You set up data ingestion system using Azure Event Hubs and then connect it to Azure Databricks to process the messages coming through.</span></span> <span data-ttu-id="d0be8-106">To access a stream of data, you use Twitter APIs to ingest tweets into Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-106">To access a stream of data, you use Twitter APIs to ingest tweets into Event Hubs.</span></span> <span data-ttu-id="d0be8-107">Once you have the data in Azure Databricks, you can run analytical jobs to further analyze the data.</span><span class="sxs-lookup"><span data-stu-id="d0be8-107">Once you have the data in Azure Databricks, you can run analytical jobs to further analyze the data.</span></span> 

<span data-ttu-id="d0be8-108">By the end of this tutorial, you would have streamed tweets from Twitter (that have the term "Azure" in them) and read the tweets in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="d0be8-108">By the end of this tutorial, you would have streamed tweets from Twitter (that have the term "Azure" in them) and read the tweets in Azure Databricks.</span></span>

<span data-ttu-id="d0be8-109">The following illustration shows the application flow:</span><span class="sxs-lookup"><span data-stu-id="d0be8-109">The following illustration shows the application flow:</span></span>

<span data-ttu-id="d0be8-110">![Azure Databricks with Event Hubs](./media/databricks-stream-from-eventhubs/databricks-eventhubs-tutorial.png "Azure Databricks with Event Hubs")</span><span class="sxs-lookup"><span data-stu-id="d0be8-110">![Azure Databricks with Event Hubs](./media/databricks-stream-from-eventhubs/databricks-eventhubs-tutorial.png "Azure Databricks with Event Hubs")</span></span>

<span data-ttu-id="d0be8-111">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d0be8-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0be8-112">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="d0be8-112">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="d0be8-113">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-113">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="d0be8-114">Create a Twitter app to access streaming data</span><span class="sxs-lookup"><span data-stu-id="d0be8-114">Create a Twitter app to access streaming data</span></span>
> * <span data-ttu-id="d0be8-115">Create notebooks in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-115">Create notebooks in Azure Databricks</span></span>
> * <span data-ttu-id="d0be8-116">Attach libraries for Event Hubs and Twitter API</span><span class="sxs-lookup"><span data-stu-id="d0be8-116">Attach libraries for Event Hubs and Twitter API</span></span>
> * <span data-ttu-id="d0be8-117">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-117">Send tweets to Event Hubs</span></span>
> * <span data-ttu-id="d0be8-118">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-118">Read tweets from Event Hubs</span></span>

<span data-ttu-id="d0be8-119">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d0be8-119">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0be8-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0be8-120">Prerequisites</span></span>

<span data-ttu-id="d0be8-121">Before you start with this tutorial, make sure to meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="d0be8-121">Before you start with this tutorial, make sure to meet the following requirements:</span></span>
- <span data-ttu-id="d0be8-122">An Azure Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="d0be8-122">An Azure Event Hubs namespace.</span></span>
- <span data-ttu-id="d0be8-123">An Event Hub within the namespace.</span><span class="sxs-lookup"><span data-stu-id="d0be8-123">An Event Hub within the namespace.</span></span>
- <span data-ttu-id="d0be8-124">Connection string to access the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="d0be8-124">Connection string to access the Event Hubs namespace.</span></span> <span data-ttu-id="d0be8-125">The connection string should have a format similar to `Endpoint=sb://<namespace>.servicebus.windows.net/;SharedAccessKeyName=<key name>;SharedAccessKey=<key value>`.</span><span class="sxs-lookup"><span data-stu-id="d0be8-125">The connection string should have a format similar to `Endpoint=sb://<namespace>.servicebus.windows.net/;SharedAccessKeyName=<key name>;SharedAccessKey=<key value>`.</span></span>
- <span data-ttu-id="d0be8-126">Shared access policy name and policy key for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-126">Shared access policy name and policy key for Event Hubs.</span></span>

<span data-ttu-id="d0be8-127">You can meet these requirements by completing the steps in the article, [Create an Azure Event Hubs namespace and event hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d0be8-127">You can meet these requirements by completing the steps in the article, [Create an Azure Event Hubs namespace and event hub](../event-hubs/event-hubs-create.md).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="d0be8-128">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0be8-128">Log in to the Azure portal</span></span>

<span data-ttu-id="d0be8-129">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0be8-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="d0be8-130">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="d0be8-130">Create an Azure Databricks workspace</span></span>

<span data-ttu-id="d0be8-131">In this section, you create an Azure Databricks workspace using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0be8-131">In this section, you create an Azure Databricks workspace using the Azure portal.</span></span>

1. <span data-ttu-id="d0be8-132">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-132">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span></span>

    <span data-ttu-id="d0be8-133">![Databricks on Azure portal](./media/databricks-stream-from-eventhubs/azure-databricks-on-portal.png "Databricks on Azure portal")</span><span class="sxs-lookup"><span data-stu-id="d0be8-133">![Databricks on Azure portal](./media/databricks-stream-from-eventhubs/azure-databricks-on-portal.png "Databricks on Azure portal")</span></span>

3. <span data-ttu-id="d0be8-134">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="d0be8-134">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span></span>

    <span data-ttu-id="d0be8-135">![Create an Azure Databricks workspace](./media/databricks-stream-from-eventhubs/create-databricks-workspace.png "Create an Azure Databricks workspace")</span><span class="sxs-lookup"><span data-stu-id="d0be8-135">![Create an Azure Databricks workspace](./media/databricks-stream-from-eventhubs/create-databricks-workspace.png "Create an Azure Databricks workspace")</span></span>

    <span data-ttu-id="d0be8-136">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="d0be8-136">Provide the following values:</span></span>

    |<span data-ttu-id="d0be8-137">Property</span><span class="sxs-lookup"><span data-stu-id="d0be8-137">Property</span></span>  |<span data-ttu-id="d0be8-138">Description</span><span class="sxs-lookup"><span data-stu-id="d0be8-138">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="d0be8-139">**Workspace name**</span><span class="sxs-lookup"><span data-stu-id="d0be8-139">**Workspace name**</span></span>     | <span data-ttu-id="d0be8-140">Provide a name for your Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="d0be8-140">Provide a name for your Databricks workspace</span></span>        |
    |<span data-ttu-id="d0be8-141">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="d0be8-141">**Subscription**</span></span>     | <span data-ttu-id="d0be8-142">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d0be8-142">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="d0be8-143">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="d0be8-143">**Resource group**</span></span>     | <span data-ttu-id="d0be8-144">Specify whether you want to create a new resource group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="d0be8-144">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="d0be8-145">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="d0be8-145">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="d0be8-146">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0be8-146">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span></span> |
    |<span data-ttu-id="d0be8-147">**Location**</span><span class="sxs-lookup"><span data-stu-id="d0be8-147">**Location**</span></span>     | <span data-ttu-id="d0be8-148">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-148">Select **East US 2**.</span></span> <span data-ttu-id="d0be8-149">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="d0be8-149">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="d0be8-150">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="d0be8-150">**Pricing Tier**</span></span>     |  <span data-ttu-id="d0be8-151">Choose between **Standard** or **Premium**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-151">Choose between **Standard** or **Premium**.</span></span> <span data-ttu-id="d0be8-152">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="d0be8-152">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |

    <span data-ttu-id="d0be8-153">Select **Pin to dashboard** and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-153">Select **Pin to dashboard** and then select **Create**.</span></span>

4. <span data-ttu-id="d0be8-154">The account creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="d0be8-154">The account creation takes a few minutes.</span></span> <span data-ttu-id="d0be8-155">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span><span class="sxs-lookup"><span data-stu-id="d0be8-155">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span></span> <span data-ttu-id="d0be8-156">You may need to scroll right on your dashboard to see the tile.</span><span class="sxs-lookup"><span data-stu-id="d0be8-156">You may need to scroll right on your dashboard to see the tile.</span></span> <span data-ttu-id="d0be8-157">There is also a progress bar displayed near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="d0be8-157">There is also a progress bar displayed near the top of the screen.</span></span> <span data-ttu-id="d0be8-158">You can watch either area for progress.</span><span class="sxs-lookup"><span data-stu-id="d0be8-158">You can watch either area for progress.</span></span>

    <span data-ttu-id="d0be8-159">![Databricks deployment tile](./media/databricks-stream-from-eventhubs/databricks-deployment-tile.png "Databricks deployment tile")</span><span class="sxs-lookup"><span data-stu-id="d0be8-159">![Databricks deployment tile](./media/databricks-stream-from-eventhubs/databricks-deployment-tile.png "Databricks deployment tile")</span></span>

## <a name="create-a-spark-cluster-in-databricks"></a><span data-ttu-id="d0be8-160">Create a Spark cluster in Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-160">Create a Spark cluster in Databricks</span></span>

1. <span data-ttu-id="d0be8-161">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-161">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span></span>

2. <span data-ttu-id="d0be8-162">You are redirected to the Azure Databricks portal.</span><span class="sxs-lookup"><span data-stu-id="d0be8-162">You are redirected to the Azure Databricks portal.</span></span> <span data-ttu-id="d0be8-163">From the portal, select **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-163">From the portal, select **Cluster**.</span></span>

    <span data-ttu-id="d0be8-164">![Databricks on Azure](./media/databricks-stream-from-eventhubs/databricks-on-azure.png "Databricks on Azure")</span><span class="sxs-lookup"><span data-stu-id="d0be8-164">![Databricks on Azure](./media/databricks-stream-from-eventhubs/databricks-on-azure.png "Databricks on Azure")</span></span>

3. <span data-ttu-id="d0be8-165">In the **New cluster** page, provide the values to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="d0be8-165">In the **New cluster** page, provide the values to create a cluster.</span></span>

    <span data-ttu-id="d0be8-166">![Create Databricks Spark cluster on Azure](./media/databricks-stream-from-eventhubs/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span><span class="sxs-lookup"><span data-stu-id="d0be8-166">![Create Databricks Spark cluster on Azure](./media/databricks-stream-from-eventhubs/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span></span>

    <span data-ttu-id="d0be8-167">Accept all other default values other than the following:</span><span class="sxs-lookup"><span data-stu-id="d0be8-167">Accept all other default values other than the following:</span></span>

    * <span data-ttu-id="d0be8-168">Enter a name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0be8-168">Enter a name for the cluster.</span></span>
    * <span data-ttu-id="d0be8-169">For this article, create a cluster with **4.0** runtime.</span><span class="sxs-lookup"><span data-stu-id="d0be8-169">For this article, create a cluster with **4.0** runtime.</span></span>
    * <span data-ttu-id="d0be8-170">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span><span class="sxs-lookup"><span data-stu-id="d0be8-170">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span></span> <span data-ttu-id="d0be8-171">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span><span class="sxs-lookup"><span data-stu-id="d0be8-171">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span></span>

    <span data-ttu-id="d0be8-172">Select **Create cluster**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-172">Select **Create cluster**.</span></span> <span data-ttu-id="d0be8-173">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-173">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span></span>

## <a name="create-a-twitter-application"></a><span data-ttu-id="d0be8-174">Create a Twitter application</span><span class="sxs-lookup"><span data-stu-id="d0be8-174">Create a Twitter application</span></span>

<span data-ttu-id="d0be8-175">To receive a stream of tweets, you create an application in Twitter.</span><span class="sxs-lookup"><span data-stu-id="d0be8-175">To receive a stream of tweets, you create an application in Twitter.</span></span> <span data-ttu-id="d0be8-176">Follow the instructions create a Twitter application and record the values that you need to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d0be8-176">Follow the instructions create a Twitter application and record the values that you need to complete this tutorial.</span></span>

1. <span data-ttu-id="d0be8-177">From a web browser, go to [Twitter Application Management](https://apps.twitter.com/), and select **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-177">From a web browser, go to [Twitter Application Management](https://apps.twitter.com/), and select **Create New App**.</span></span>

    <span data-ttu-id="d0be8-178">![Create Twitter application](./media/databricks-stream-from-eventhubs/databricks-create-twitter-app.png "Create Twitter application")</span><span class="sxs-lookup"><span data-stu-id="d0be8-178">![Create Twitter application](./media/databricks-stream-from-eventhubs/databricks-create-twitter-app.png "Create Twitter application")</span></span>

2. <span data-ttu-id="d0be8-179">In the **Create an application** page, provide the details for the new app, and then select **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-179">In the **Create an application** page, provide the details for the new app, and then select **Create your Twitter application**.</span></span>

    <span data-ttu-id="d0be8-180">![Twitter application details](./media/databricks-stream-from-eventhubs/databricks-provide-twitter-app-details.png "Twitter application details")</span><span class="sxs-lookup"><span data-stu-id="d0be8-180">![Twitter application details](./media/databricks-stream-from-eventhubs/databricks-provide-twitter-app-details.png "Twitter application details")</span></span>

3. <span data-ttu-id="d0be8-181">In the application page, select the **Keys and Access Tokens** tab and copy the values for **Consume Key** and **Consumer Secret**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-181">In the application page, select the **Keys and Access Tokens** tab and copy the values for **Consume Key** and **Consumer Secret**.</span></span> <span data-ttu-id="d0be8-182">Also, select **Create my access token** to generate the access tokens.</span><span class="sxs-lookup"><span data-stu-id="d0be8-182">Also, select **Create my access token** to generate the access tokens.</span></span> <span data-ttu-id="d0be8-183">Copy the values for **Access Token** and **Access Token Secret**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-183">Copy the values for **Access Token** and **Access Token Secret**.</span></span>

    <span data-ttu-id="d0be8-184">![Twitter application details](./media/databricks-stream-from-eventhubs/twitter-app-key-secret.png "Twitter application details")</span><span class="sxs-lookup"><span data-stu-id="d0be8-184">![Twitter application details](./media/databricks-stream-from-eventhubs/twitter-app-key-secret.png "Twitter application details")</span></span>

<span data-ttu-id="d0be8-185">Save the values that you retrieved for the Twitter application.</span><span class="sxs-lookup"><span data-stu-id="d0be8-185">Save the values that you retrieved for the Twitter application.</span></span> <span data-ttu-id="d0be8-186">You need the values later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="d0be8-186">You need the values later in the tutorial.</span></span>

## <a name="attach-libraries-to-spark-cluster"></a><span data-ttu-id="d0be8-187">Attach libraries to Spark cluster</span><span class="sxs-lookup"><span data-stu-id="d0be8-187">Attach libraries to Spark cluster</span></span>

<span data-ttu-id="d0be8-188">In this tutorial, you use the Twitter APIs to send tweets to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-188">In this tutorial, you use the Twitter APIs to send tweets to Event Hubs.</span></span> <span data-ttu-id="d0be8-189">You also use the [Apache Spark Event Hubs connector](https://github.com/Azure/azure-event-hubs-spark) to read and write data into Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-189">You also use the [Apache Spark Event Hubs connector](https://github.com/Azure/azure-event-hubs-spark) to read and write data into Azure Event Hubs.</span></span> <span data-ttu-id="d0be8-190">To use these APIs as part of your cluster, add them as libraries to Azure Databricks and then associate them with your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="d0be8-190">To use these APIs as part of your cluster, add them as libraries to Azure Databricks and then associate them with your Spark cluster.</span></span> <span data-ttu-id="d0be8-191">The following instructions show how to add the library to the **Shared** folder in your workspace.</span><span class="sxs-lookup"><span data-stu-id="d0be8-191">The following instructions show how to add the library to the **Shared** folder in your workspace.</span></span>

1.  <span data-ttu-id="d0be8-192">In the Azure Databricks workspace, select **Workspace**, and then right-click **Shared**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-192">In the Azure Databricks workspace, select **Workspace**, and then right-click **Shared**.</span></span> <span data-ttu-id="d0be8-193">From the context menu, select **Create** > **Library**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-193">From the context menu, select **Create** > **Library**.</span></span>

    <span data-ttu-id="d0be8-194">![Add library dialog box](./media/databricks-stream-from-eventhubs/databricks-add-library-option.png "Add library dialog box")</span><span class="sxs-lookup"><span data-stu-id="d0be8-194">![Add library dialog box](./media/databricks-stream-from-eventhubs/databricks-add-library-option.png "Add library dialog box")</span></span>

2. <span data-ttu-id="d0be8-195">In the New Library page, for **Source** select **Maven Coordinate**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-195">In the New Library page, for **Source** select **Maven Coordinate**.</span></span> <span data-ttu-id="d0be8-196">For **Coordinate**, enter the coordinate for the package you want to add.</span><span class="sxs-lookup"><span data-stu-id="d0be8-196">For **Coordinate**, enter the coordinate for the package you want to add.</span></span> <span data-ttu-id="d0be8-197">Here is the Maven coordinates for the libraries used in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="d0be8-197">Here is the Maven coordinates for the libraries used in this tutorial:</span></span>

    * <span data-ttu-id="d0be8-198">Spark Event Hubs connector - `com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1`</span><span class="sxs-lookup"><span data-stu-id="d0be8-198">Spark Event Hubs connector - `com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1`</span></span>
    * <span data-ttu-id="d0be8-199">Twitter API - `org.twitter4j:twitter4j-core:4.0.6`</span><span class="sxs-lookup"><span data-stu-id="d0be8-199">Twitter API - `org.twitter4j:twitter4j-core:4.0.6`</span></span>

    <span data-ttu-id="d0be8-200">![Provide Maven coordinates](./media/databricks-stream-from-eventhubs/databricks-eventhub-specify-maven-coordinate.png "Provide Maven coordinates")</span><span class="sxs-lookup"><span data-stu-id="d0be8-200">![Provide Maven coordinates](./media/databricks-stream-from-eventhubs/databricks-eventhub-specify-maven-coordinate.png "Provide Maven coordinates")</span></span>

3. <span data-ttu-id="d0be8-201">Select **Create Library**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-201">Select **Create Library**.</span></span>

4. <span data-ttu-id="d0be8-202">Select the folder where you added the library, and then select the library name.</span><span class="sxs-lookup"><span data-stu-id="d0be8-202">Select the folder where you added the library, and then select the library name.</span></span>

    <span data-ttu-id="d0be8-203">![Select library to add](./media/databricks-stream-from-eventhubs/select-library.png "Select library to add")</span><span class="sxs-lookup"><span data-stu-id="d0be8-203">![Select library to add](./media/databricks-stream-from-eventhubs/select-library.png "Select library to add")</span></span>

5. <span data-ttu-id="d0be8-204">On the library page, select the cluster where you want to use the library.</span><span class="sxs-lookup"><span data-stu-id="d0be8-204">On the library page, select the cluster where you want to use the library.</span></span> <span data-ttu-id="d0be8-205">Once the library is successfully associated with the cluster, the status immediately changes to **Attached**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-205">Once the library is successfully associated with the cluster, the status immediately changes to **Attached**.</span></span>

    <span data-ttu-id="d0be8-206">![Attach library to cluster](./media/databricks-stream-from-eventhubs/databricks-library-attached.png "Attach library to cluster")</span><span class="sxs-lookup"><span data-stu-id="d0be8-206">![Attach library to cluster](./media/databricks-stream-from-eventhubs/databricks-library-attached.png "Attach library to cluster")</span></span>

6. <span data-ttu-id="d0be8-207">Repeat these steps for the Twitter package, `twitter4j-core:4.0.6`.</span><span class="sxs-lookup"><span data-stu-id="d0be8-207">Repeat these steps for the Twitter package, `twitter4j-core:4.0.6`.</span></span>

## <a name="create-notebooks-in-databricks"></a><span data-ttu-id="d0be8-208">Create notebooks in Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-208">Create notebooks in Databricks</span></span>

<span data-ttu-id="d0be8-209">In this section, you create two notebooks in Databricks workspace with the following names:</span><span class="sxs-lookup"><span data-stu-id="d0be8-209">In this section, you create two notebooks in Databricks workspace with the following names:</span></span>

- <span data-ttu-id="d0be8-210">**SendTweetsToEventHub** - A producer notebook you use to get tweets from Twitter and stream them to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-210">**SendTweetsToEventHub** - A producer notebook you use to get tweets from Twitter and stream them to Event Hubs.</span></span>
- <span data-ttu-id="d0be8-211">**ReadTweetsFromEventHub** - A consumer notebook you use to read the tweets from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d0be8-211">**ReadTweetsFromEventHub** - A consumer notebook you use to read the tweets from Event Hubs.</span></span>

1. <span data-ttu-id="d0be8-212">In the left pane, select **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-212">In the left pane, select **Workspace**.</span></span> <span data-ttu-id="d0be8-213">From the **Workspace** drop-down, select **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-213">From the **Workspace** drop-down, select **Create** > **Notebook**.</span></span>

    <span data-ttu-id="d0be8-214">![Create notebook in Databricks](./media/databricks-stream-from-eventhubs/databricks-create-notebook.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="d0be8-214">![Create notebook in Databricks](./media/databricks-stream-from-eventhubs/databricks-create-notebook.png "Create notebook in Databricks")</span></span>

2. <span data-ttu-id="d0be8-215">In the **Create Notebook** dialog box, enter **SendTweetsToEventHub**, select **Scala** as the language, and select the Spark cluster that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d0be8-215">In the **Create Notebook** dialog box, enter **SendTweetsToEventHub**, select **Scala** as the language, and select the Spark cluster that you created earlier.</span></span>

    <span data-ttu-id="d0be8-216">![Create notebook in Databricks](./media/databricks-stream-from-eventhubs/databricks-notebook-details.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="d0be8-216">![Create notebook in Databricks](./media/databricks-stream-from-eventhubs/databricks-notebook-details.png "Create notebook in Databricks")</span></span>

    <span data-ttu-id="d0be8-217">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-217">Select **Create**.</span></span>

3. <span data-ttu-id="d0be8-218">Repeat the steps to create the **ReadTweetsFromEventHub** notebook.</span><span class="sxs-lookup"><span data-stu-id="d0be8-218">Repeat the steps to create the **ReadTweetsFromEventHub** notebook.</span></span>

## <a name="send-tweets-to-event-hubs"></a><span data-ttu-id="d0be8-219">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-219">Send tweets to Event Hubs</span></span>

<span data-ttu-id="d0be8-220">In the **SendTweetsToEventHub** notebook, paste the following code, and replace the placeholders with values for your Event Hubs namesapce and Twitter application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d0be8-220">In the **SendTweetsToEventHub** notebook, paste the following code, and replace the placeholders with values for your Event Hubs namesapce and Twitter application that you created earlier.</span></span> <span data-ttu-id="d0be8-221">This notebook streams tweets with the keyword "Azure" into Event Hubs in real time.</span><span class="sxs-lookup"><span data-stu-id="d0be8-221">This notebook streams tweets with the keyword "Azure" into Event Hubs in real time.</span></span>

```scala
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
```

<span data-ttu-id="d0be8-222">To run the notebook, press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-222">To run the notebook, press **SHIFT + ENTER**.</span></span> <span data-ttu-id="d0be8-223">You see an output like the snippet below.</span><span class="sxs-lookup"><span data-stu-id="d0be8-223">You see an output like the snippet below.</span></span> <span data-ttu-id="d0be8-224">Each event in the output is a tweet that is ingested into the Event Hubs containing the term "Azure".</span><span class="sxs-lookup"><span data-stu-id="d0be8-224">Each event in the output is a tweet that is ingested into the Event Hubs containing the term "Azure".</span></span>

    Sent event: @Microsoft and @Esri launch Geospatial AI on Azure https://t.co/VmLUCiPm6q via @geoworldmedia #geoai #azure #gis #ArtificialIntelligence

    Sent event: Public preview of Java on App Service, built-in support for Tomcat and OpenJDK
    https://t.co/7vs7cKtvah
    #cloudcomputing #Azure

    Sent event: 4 Killer #Azure Features for #Data #Performance https://t.co/kpIb7hFO2j by @RedPixie

    Sent event: Migrate your databases to a fully managed service with Azure SQL Database Managed Instance | #Azure | #Cloud https://t.co/sJHXN4trDk

    Sent event: Top 10 Tricks to #Save Money with #Azure Virtual Machines https://t.co/F2wshBXdoz #Cloud

    ...
    ...

## <a name="read-tweets-from-event-hubs"></a><span data-ttu-id="d0be8-225">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-225">Read tweets from Event Hubs</span></span>

<span data-ttu-id="d0be8-226">In the **ReadTweetsFromEventHub** notebook, paste the following code, and replace the placeholder with values for your Azure Event Hubs that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d0be8-226">In the **ReadTweetsFromEventHub** notebook, paste the following code, and replace the placeholder with values for your Azure Event Hubs that you created earlier.</span></span> <span data-ttu-id="d0be8-227">This notebook reads the tweets that you earlier streamed into Event Hubs using the **SendTweetsToEventHub** notebook.</span><span class="sxs-lookup"><span data-stu-id="d0be8-227">This notebook reads the tweets that you earlier streamed into Event Hubs using the **SendTweetsToEventHub** notebook.</span></span>

```scala
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
```

<span data-ttu-id="d0be8-228">You get the following output:</span><span class="sxs-lookup"><span data-stu-id="d0be8-228">You get the following output:</span></span>


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

<span data-ttu-id="d0be8-229">Because the output is in a binary mode, use the following snippet to convert it into string.</span><span class="sxs-lookup"><span data-stu-id="d0be8-229">Because the output is in a binary mode, use the following snippet to convert it into string.</span></span>

```scala
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
```

<span data-ttu-id="d0be8-230">The output now resembles the following snippet:</span><span class="sxs-lookup"><span data-stu-id="d0be8-230">The output now resembles the following snippet:</span></span>

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

<span data-ttu-id="d0be8-231">That's it!</span><span class="sxs-lookup"><span data-stu-id="d0be8-231">That's it!</span></span> <span data-ttu-id="d0be8-232">Using Azure Databricks, you have successfully streamed data into Azure Event Hubs in near real-time.</span><span class="sxs-lookup"><span data-stu-id="d0be8-232">Using Azure Databricks, you have successfully streamed data into Azure Event Hubs in near real-time.</span></span> <span data-ttu-id="d0be8-233">You then consumed the stream data using the Event Hubs connector for Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d0be8-233">You then consumed the stream data using the Event Hubs connector for Apache Spark.</span></span> <span data-ttu-id="d0be8-234">For more information on how to use the Event Hubs connector for Spark, see the [connector documentation](https://github.com/Azure/azure-event-hubs-spark/tree/master/docs).</span><span class="sxs-lookup"><span data-stu-id="d0be8-234">For more information on how to use the Event Hubs connector for Spark, see the [connector documentation](https://github.com/Azure/azure-event-hubs-spark/tree/master/docs).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d0be8-235">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d0be8-235">Clean up resources</span></span>

<span data-ttu-id="d0be8-236">After you have finished running the tutorial, you can terminate the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0be8-236">After you have finished running the tutorial, you can terminate the cluster.</span></span> <span data-ttu-id="d0be8-237">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span><span class="sxs-lookup"><span data-stu-id="d0be8-237">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span></span> <span data-ttu-id="d0be8-238">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span><span class="sxs-lookup"><span data-stu-id="d0be8-238">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span></span>

<span data-ttu-id="d0be8-239">![Stop a Databricks cluster](./media/databricks-stream-from-eventhubs/terminate-databricks-cluster.png "Stop a Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="d0be8-239">![Stop a Databricks cluster](./media/databricks-stream-from-eventhubs/terminate-databricks-cluster.png "Stop a Databricks cluster")</span></span>

<span data-ttu-id="d0be8-240">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="d0be8-240">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span></span> <span data-ttu-id="d0be8-241">In such a case, the cluster will automatically stop if it has been inactive for the specified time.</span><span class="sxs-lookup"><span data-stu-id="d0be8-241">In such a case, the cluster will automatically stop if it has been inactive for the specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0be8-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0be8-242">Next steps</span></span>
<span data-ttu-id="d0be8-243">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="d0be8-243">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0be8-244">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="d0be8-244">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="d0be8-245">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-245">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="d0be8-246">Create a Twitter app to generate streaming data</span><span class="sxs-lookup"><span data-stu-id="d0be8-246">Create a Twitter app to generate streaming data</span></span>
> * <span data-ttu-id="d0be8-247">Create notebooks in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="d0be8-247">Create notebooks in Azure Databricks</span></span>
> * <span data-ttu-id="d0be8-248">Add libraries for Event Hubs and Twitter API</span><span class="sxs-lookup"><span data-stu-id="d0be8-248">Add libraries for Event Hubs and Twitter API</span></span>
> * <span data-ttu-id="d0be8-249">Send tweets to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-249">Send tweets to Event Hubs</span></span>
> * <span data-ttu-id="d0be8-250">Read tweets from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d0be8-250">Read tweets from Event Hubs</span></span>

<span data-ttu-id="d0be8-251">Advance to the next tutorial to learn about performing sentiment analysis on the streamed data using Azure Databricks and [Microsoft Cognitive Services API](../cognitive-services/text-analytics/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0be8-251">Advance to the next tutorial to learn about performing sentiment analysis on the streamed data using Azure Databricks and [Microsoft Cognitive Services API](../cognitive-services/text-analytics/overview.md).</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="d0be8-252">Sentiment analyis on streaming data using Azure Databricks </span><span class="sxs-lookup"><span data-stu-id="d0be8-252">Sentiment analyis on streaming data using Azure Databricks </span></span>](databricks-sentiment-analysis-cognitive-services.md)
