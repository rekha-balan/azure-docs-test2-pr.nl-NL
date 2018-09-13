---
title: Use Azure Cosmos DB change feed to visualize real-time data analytics | Microsoft Docs
description: This article describes how change feed can be used by a retail company to understand user patterns, perform real-time data analysis and visualization.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: java
ms.topic: conceptual
ms.date: 08/12/2018
ms.author: sngun
ms.openlocfilehash: d2c4c890e1a1599e68fba1a0728061ec244f382f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856873"
---
# <a name="use-azure-cosmos-db-change-feed-to-visualize-real-time-data-analytics"></a><span data-ttu-id="001fa-103">Use Azure Cosmos DB change feed to visualize real-time data analytics</span><span class="sxs-lookup"><span data-stu-id="001fa-103">Use Azure Cosmos DB change feed to visualize real-time data analytics</span></span>

<span data-ttu-id="001fa-104">The Azure Cosmos DB change feed is a mechanism to get a continuous and incremental feed of records from an Azure Cosmos DB container as those records are being created or modified.</span><span class="sxs-lookup"><span data-stu-id="001fa-104">The Azure Cosmos DB change feed is a mechanism to get a continuous and incremental feed of records from an Azure Cosmos DB container as those records are being created or modified.</span></span> <span data-ttu-id="001fa-105">Change feed support works by listening to container for any changes.</span><span class="sxs-lookup"><span data-stu-id="001fa-105">Change feed support works by listening to container for any changes.</span></span> <span data-ttu-id="001fa-106">It then outputs the sorted list of documents that were changed in the order in which they were modified.</span><span class="sxs-lookup"><span data-stu-id="001fa-106">It then outputs the sorted list of documents that were changed in the order in which they were modified.</span></span> <span data-ttu-id="001fa-107">To learn more about change feed, see [working with change feed](change-feed.md) article.</span><span class="sxs-lookup"><span data-stu-id="001fa-107">To learn more about change feed, see [working with change feed](change-feed.md) article.</span></span> 

<span data-ttu-id="001fa-108">This article describes how change feed can be used by an e-commerce company to understand user patterns, perform real-time data analysis and visualization.</span><span class="sxs-lookup"><span data-stu-id="001fa-108">This article describes how change feed can be used by an e-commerce company to understand user patterns, perform real-time data analysis and visualization.</span></span> <span data-ttu-id="001fa-109">You will analyze events such as a user viewing an item, adding an item to their cart, or purchasing an item.</span><span class="sxs-lookup"><span data-stu-id="001fa-109">You will analyze events such as a user viewing an item, adding an item to their cart, or purchasing an item.</span></span> <span data-ttu-id="001fa-110">When one of these events occurs, a new record is created, and the change feed logs that record.</span><span class="sxs-lookup"><span data-stu-id="001fa-110">When one of these events occurs, a new record is created, and the change feed logs that record.</span></span> <span data-ttu-id="001fa-111">Change feed then triggers a series of steps resulting in visualization of metrics that analyze the company performance and activity.</span><span class="sxs-lookup"><span data-stu-id="001fa-111">Change feed then triggers a series of steps resulting in visualization of metrics that analyze the company performance and activity.</span></span> <span data-ttu-id="001fa-112">Sample metrics that you can visualize include revenue, unique site visitors, most popular items, and average price of the items that are viewed versus added to a cart versus purchased.</span><span class="sxs-lookup"><span data-stu-id="001fa-112">Sample metrics that you can visualize include revenue, unique site visitors, most popular items, and average price of the items that are viewed versus added to a cart versus purchased.</span></span> <span data-ttu-id="001fa-113">These sample metrics can help an e-commerce company evaluate its site popularity, develop its advertising and pricing strategies, and make decisions regarding what inventory to invest in.</span><span class="sxs-lookup"><span data-stu-id="001fa-113">These sample metrics can help an e-commerce company evaluate its site popularity, develop its advertising and pricing strategies, and make decisions regarding what inventory to invest in.</span></span>

<span data-ttu-id="001fa-114">Interested in watching a video about the solution before getting started, see the following video:</span><span class="sxs-lookup"><span data-stu-id="001fa-114">Interested in watching a video about the solution before getting started, see the following video:</span></span>

> [!VIDEO https://www.youtube.com/embed/AYOiMkvxlzo]
>

## <a name="solution-components"></a><span data-ttu-id="001fa-115">Solution components</span><span class="sxs-lookup"><span data-stu-id="001fa-115">Solution components</span></span>
<span data-ttu-id="001fa-116">The following diagram represents the data flow and components involved in the solution:</span><span class="sxs-lookup"><span data-stu-id="001fa-116">The following diagram represents the data flow and components involved in the solution:</span></span>

![Project visual](./media/changefeed-ecommerce-solution/project-visual.png)
 
1. <span data-ttu-id="001fa-118">**Data Generation:** Data simulator is used to generate retail data that represents events such as a user viewing an item, adding an item to their cart, and purchasing an item.</span><span class="sxs-lookup"><span data-stu-id="001fa-118">**Data Generation:** Data simulator is used to generate retail data that represents events such as a user viewing an item, adding an item to their cart, and purchasing an item.</span></span> <span data-ttu-id="001fa-119">You can generate large set of sample data by using the data generator.</span><span class="sxs-lookup"><span data-stu-id="001fa-119">You can generate large set of sample data by using the data generator.</span></span> <span data-ttu-id="001fa-120">The generated sample data contains documents in the following format:</span><span class="sxs-lookup"><span data-stu-id="001fa-120">The generated sample data contains documents in the following format:</span></span>
   
   ```json
   {      
     "CartID": 2486,
     "Action": "Viewed",
     "Item": "Women's Denim Jacket",
     "Price": 31.99
   }
   ```

2. <span data-ttu-id="001fa-121">**Cosmos DB:** The generated data is stores in an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="001fa-121">**Cosmos DB:** The generated data is stores in an Azure Cosmos DB collection.</span></span>  

3. <span data-ttu-id="001fa-122">**Change Feed:** The change feed will listen for changes to the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="001fa-122">**Change Feed:** The change feed will listen for changes to the Azure Cosmos DB collection.</span></span> <span data-ttu-id="001fa-123">Each time a new document is added into the collection (that is when an event occurs such a user viewing an item, adding an item to their cart, or purchasing an item), the change feed will trigger an [Azure Function](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="001fa-123">Each time a new document is added into the collection (that is when an event occurs such a user viewing an item, adding an item to their cart, or purchasing an item), the change feed will trigger an [Azure Function](../azure-functions/functions-overview.md).</span></span>  

4. <span data-ttu-id="001fa-124">**Azure Function:** The Azure Function processes the new data and sends it to an [Azure Event Hub](../event-hubs/event-hubs-about.md).</span><span class="sxs-lookup"><span data-stu-id="001fa-124">**Azure Function:** The Azure Function processes the new data and sends it to an [Azure Event Hub](../event-hubs/event-hubs-about.md).</span></span>  

5. <span data-ttu-id="001fa-125">**Event Hub:** The Azure Event Hub stores these events and sends them to [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) to perform further analysis.</span><span class="sxs-lookup"><span data-stu-id="001fa-125">**Event Hub:** The Azure Event Hub stores these events and sends them to [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) to perform further analysis.</span></span>  

6. <span data-ttu-id="001fa-126">**Azure Stream Analytics:** Azure Stream Analytics defines queries to process the events and perform real-time data analysis.</span><span class="sxs-lookup"><span data-stu-id="001fa-126">**Azure Stream Analytics:** Azure Stream Analytics defines queries to process the events and perform real-time data analysis.</span></span> <span data-ttu-id="001fa-127">This data is then sent to [Microsoft Power BI](https://docs.microsoft.com/power-bi/desktop-what-is-desktop).</span><span class="sxs-lookup"><span data-stu-id="001fa-127">This data is then sent to [Microsoft Power BI](https://docs.microsoft.com/power-bi/desktop-what-is-desktop).</span></span>  

7. <span data-ttu-id="001fa-128">**Power BI:** Power BI is used to visualize the data sent by Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="001fa-128">**Power BI:** Power BI is used to visualize the data sent by Azure Stream Analytics.</span></span> <span data-ttu-id="001fa-129">You can build a dashboard to see how the metrics change in real time.</span><span class="sxs-lookup"><span data-stu-id="001fa-129">You can build a dashboard to see how the metrics change in real time.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="001fa-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="001fa-130">Prerequisites</span></span>

* <span data-ttu-id="001fa-131">Microsoft .NET Framework 4.7.1 or higher</span><span class="sxs-lookup"><span data-stu-id="001fa-131">Microsoft .NET Framework 4.7.1 or higher</span></span>

* <span data-ttu-id="001fa-132">Microsoft .NET Core 2.1 (or higher)</span><span class="sxs-lookup"><span data-stu-id="001fa-132">Microsoft .NET Core 2.1 (or higher)</span></span>

* <span data-ttu-id="001fa-133">Visual Studio with Universal Windows Platform development, .NET desktop development, and ASP.NET and web development workloads</span><span class="sxs-lookup"><span data-stu-id="001fa-133">Visual Studio with Universal Windows Platform development, .NET desktop development, and ASP.NET and web development workloads</span></span>

* <span data-ttu-id="001fa-134">Microsoft Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="001fa-134">Microsoft Azure Subscription</span></span>

* <span data-ttu-id="001fa-135">Microsoft Power BI Account</span><span class="sxs-lookup"><span data-stu-id="001fa-135">Microsoft Power BI Account</span></span>

* <span data-ttu-id="001fa-136">Download the [Azure Cosmos DB change feed lab](https://github.com/Azure-Samples/azure-cosmos-db-change-feed-dotnet-retail-sample) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="001fa-136">Download the [Azure Cosmos DB change feed lab](https://github.com/Azure-Samples/azure-cosmos-db-change-feed-dotnet-retail-sample) from GitHub.</span></span> 

## <a name="create-azure-resources"></a><span data-ttu-id="001fa-137">Create Azure resources</span><span class="sxs-lookup"><span data-stu-id="001fa-137">Create Azure resources</span></span> 

<span data-ttu-id="001fa-138">Create the Azure resources - Azure Cosmos DB, Storage account, Event Hub, Stream Analytics required by the solution.</span><span class="sxs-lookup"><span data-stu-id="001fa-138">Create the Azure resources - Azure Cosmos DB, Storage account, Event Hub, Stream Analytics required by the solution.</span></span> <span data-ttu-id="001fa-139">You will deploy these resources through an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="001fa-139">You will deploy these resources through an Azure Resource Manager template.</span></span> <span data-ttu-id="001fa-140">Use the following steps to deploy these resources:</span><span class="sxs-lookup"><span data-stu-id="001fa-140">Use the following steps to deploy these resources:</span></span> 

1. <span data-ttu-id="001fa-141">Set the Windows PowerShell execution policy to **Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="001fa-141">Set the Windows PowerShell execution policy to **Unrestricted**.</span></span> <span data-ttu-id="001fa-142">To do so, open **Windows PowerShell as an Administrator** and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="001fa-142">To do so, open **Windows PowerShell as an Administrator** and run the following commands:</span></span>

   ```powershell
   Get-ExecutionPolicy
   Set-ExecutionPolicy Unrestricted 
   ```

2. <span data-ttu-id="001fa-143">From the GitHub repository you downloaded in the previous step, navigate to the **Azure Resource Manager** folder, and open the file called **parameters.json** file.</span><span class="sxs-lookup"><span data-stu-id="001fa-143">From the GitHub repository you downloaded in the previous step, navigate to the **Azure Resource Manager** folder, and open the file called **parameters.json** file.</span></span>  

3. <span data-ttu-id="001fa-144">Provide values for cosmosdbaccount_name, eventhubnamespace_name, storageaccount_name, parameters as indicated in **parameters.json** file.</span><span class="sxs-lookup"><span data-stu-id="001fa-144">Provide values for cosmosdbaccount_name, eventhubnamespace_name, storageaccount_name, parameters as indicated in **parameters.json** file.</span></span> <span data-ttu-id="001fa-145">You'll need to use the names that you give to each of your resources later.</span><span class="sxs-lookup"><span data-stu-id="001fa-145">You'll need to use the names that you give to each of your resources later.</span></span>  

4. <span data-ttu-id="001fa-146">From **Windows PowerShell**, navigate to the **Azure Resource Manager** folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="001fa-146">From **Windows PowerShell**, navigate to the **Azure Resource Manager** folder and run the following command:</span></span>

   ```powershell
   .\deploy.ps1
   ```
5. <span data-ttu-id="001fa-147">When prompted, enter your Azure **Subcription ID**, **changefeedlab** for the resource group name, and **run1** for the deployment name.</span><span class="sxs-lookup"><span data-stu-id="001fa-147">When prompted, enter your Azure **Subcription ID**, **changefeedlab** for the resource group name, and **run1** for the deployment name.</span></span> <span data-ttu-id="001fa-148">Once the resources begin to deploy, it may take up to 10 minutes for it to complete.</span><span class="sxs-lookup"><span data-stu-id="001fa-148">Once the resources begin to deploy, it may take up to 10 minutes for it to complete.</span></span>

## <a name="create-a-database-and-the-collection"></a><span data-ttu-id="001fa-149">Create a database and the collection</span><span class="sxs-lookup"><span data-stu-id="001fa-149">Create a database and the collection</span></span>

<span data-ttu-id="001fa-150">You will now create a collection to hold e-commerce site events.</span><span class="sxs-lookup"><span data-stu-id="001fa-150">You will now create a collection to hold e-commerce site events.</span></span> <span data-ttu-id="001fa-151">When a user views an item, adds an item to their cart, or purchases an item, the collection will receive a record that includes the action ("viewed", "added", or "purchased"), the name of the item involved, the price of the item involved, and the ID number of the user cart involved.</span><span class="sxs-lookup"><span data-stu-id="001fa-151">When a user views an item, adds an item to their cart, or purchases an item, the collection will receive a record that includes the action ("viewed", "added", or "purchased"), the name of the item involved, the price of the item involved, and the ID number of the user cart involved.</span></span>

1. <span data-ttu-id="001fa-152">Go to [Azure Portal](http://portal.azure.com/) and find the **Azure Cosmos DB Account** that’s created by the template deployment.</span><span class="sxs-lookup"><span data-stu-id="001fa-152">Go to [Azure Portal](http://portal.azure.com/) and find the **Azure Cosmos DB Account** that’s created by the template deployment.</span></span>  

2. <span data-ttu-id="001fa-153">From the **Data Explorer** pane, select **New Collection** and fill the form with the following details:</span><span class="sxs-lookup"><span data-stu-id="001fa-153">From the **Data Explorer** pane, select **New Collection** and fill the form with the following details:</span></span>  

   * <span data-ttu-id="001fa-154">For the **Database id** field, select **Create new**, then enter **changefeedlabdatabase**.</span><span class="sxs-lookup"><span data-stu-id="001fa-154">For the **Database id** field, select **Create new**, then enter **changefeedlabdatabase**.</span></span> <span data-ttu-id="001fa-155">Leave the **Provision database throughput** box unchecked.</span><span class="sxs-lookup"><span data-stu-id="001fa-155">Leave the **Provision database throughput** box unchecked.</span></span>  
   * <span data-ttu-id="001fa-156">For the **Collection** id field, enter **changefeedlabcollection**.</span><span class="sxs-lookup"><span data-stu-id="001fa-156">For the **Collection** id field, enter **changefeedlabcollection**.</span></span>  
   * <span data-ttu-id="001fa-157">For **Storage capacity**, select **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="001fa-157">For **Storage capacity**, select **Unlimited**.</span></span>  
   * <span data-ttu-id="001fa-158">For the **Partition key** field, enter **/Item**.</span><span class="sxs-lookup"><span data-stu-id="001fa-158">For the **Partition key** field, enter **/Item**.</span></span> <span data-ttu-id="001fa-159">This is case-sensitive, so make sure you enter it correctly.</span><span class="sxs-lookup"><span data-stu-id="001fa-159">This is case-sensitive, so make sure you enter it correctly.</span></span>  
   * <span data-ttu-id="001fa-160">For the **Throughput** field, enter **10000**.</span><span class="sxs-lookup"><span data-stu-id="001fa-160">For the **Throughput** field, enter **10000**.</span></span>  
   * <span data-ttu-id="001fa-161">Click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="001fa-161">Click the **OK** button.</span></span>  

3. <span data-ttu-id="001fa-162">Next create another collection named **leases** for change feed processing.</span><span class="sxs-lookup"><span data-stu-id="001fa-162">Next create another collection named **leases** for change feed processing.</span></span> <span data-ttu-id="001fa-163">The leases collection coordinates processing the change feed across multiple workers.</span><span class="sxs-lookup"><span data-stu-id="001fa-163">The leases collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="001fa-164">A separate collection is used to store the leases with one lease per partition.</span><span class="sxs-lookup"><span data-stu-id="001fa-164">A separate collection is used to store the leases with one lease per partition.</span></span>  

4.  <span data-ttu-id="001fa-165">Return to the **Data Explorer** pane and select **New Collection** and fill the form with the following details:</span><span class="sxs-lookup"><span data-stu-id="001fa-165">Return to the **Data Explorer** pane and select **New Collection** and fill the form with the following details:</span></span>

   * <span data-ttu-id="001fa-166">For the **Database id** field, select **Use existing**, then enter **changefeedlabdatabase**.</span><span class="sxs-lookup"><span data-stu-id="001fa-166">For the **Database id** field, select **Use existing**, then enter **changefeedlabdatabase**.</span></span>  
   * <span data-ttu-id="001fa-167">For the **Collection id** field, enter **leases**.</span><span class="sxs-lookup"><span data-stu-id="001fa-167">For the **Collection id** field, enter **leases**.</span></span>  
   * <span data-ttu-id="001fa-168">For **Storage capacity**, select **Fixed**.</span><span class="sxs-lookup"><span data-stu-id="001fa-168">For **Storage capacity**, select **Fixed**.</span></span>  
   * <span data-ttu-id="001fa-169">Leave the **Throughput** field set to its default value.</span><span class="sxs-lookup"><span data-stu-id="001fa-169">Leave the **Throughput** field set to its default value.</span></span>  
   * <span data-ttu-id="001fa-170">Click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="001fa-170">Click the **OK** button.</span></span>

## <a name="get-the-connection-string-and-keys"></a><span data-ttu-id="001fa-171">Get the connection string and keys</span><span class="sxs-lookup"><span data-stu-id="001fa-171">Get the connection string and keys</span></span>

### <a name="get-the-azure-cosmos-db-connection-string"></a><span data-ttu-id="001fa-172">Get the Azure Cosmos DB connection string</span><span class="sxs-lookup"><span data-stu-id="001fa-172">Get the Azure Cosmos DB connection string</span></span>

1. <span data-ttu-id="001fa-173">Go to [Azure Portal](http://portal.azure.com/) and find the **Azure Cosmos DB Account** that’s created by the template deployment.</span><span class="sxs-lookup"><span data-stu-id="001fa-173">Go to [Azure Portal](http://portal.azure.com/) and find the **Azure Cosmos DB Account** that’s created by the template deployment.</span></span>  

2. <span data-ttu-id="001fa-174">Navigate to the **Keys** pane, copy the PRIMARY CONNECTION STRING and copy it to a notepad or another document that you will have access to throughout the lab.</span><span class="sxs-lookup"><span data-stu-id="001fa-174">Navigate to the **Keys** pane, copy the PRIMARY CONNECTION STRING and copy it to a notepad or another document that you will have access to throughout the lab.</span></span> <span data-ttu-id="001fa-175">You should label it **Cosmos DB Connection String**.</span><span class="sxs-lookup"><span data-stu-id="001fa-175">You should label it **Cosmos DB Connection String**.</span></span> <span data-ttu-id="001fa-176">You'll need to copy the string into your code later, so take a note and remember where you are storing it.</span><span class="sxs-lookup"><span data-stu-id="001fa-176">You'll need to copy the string into your code later, so take a note and remember where you are storing it.</span></span>

### <a name="get-the-storage-account-key-and-connection-string"></a><span data-ttu-id="001fa-177">Get the storage account key and connection string</span><span class="sxs-lookup"><span data-stu-id="001fa-177">Get the storage account key and connection string</span></span>

<span data-ttu-id="001fa-178">Azure Storage Accounts allow users to store data.</span><span class="sxs-lookup"><span data-stu-id="001fa-178">Azure Storage Accounts allow users to store data.</span></span> <span data-ttu-id="001fa-179">In this lab, you will use a storage account to store data that is used by the Azure Function.</span><span class="sxs-lookup"><span data-stu-id="001fa-179">In this lab, you will use a storage account to store data that is used by the Azure Function.</span></span> <span data-ttu-id="001fa-180">The Azure Function is triggered when any modification is made to the collection.</span><span class="sxs-lookup"><span data-stu-id="001fa-180">The Azure Function is triggered when any modification is made to the collection.</span></span>

1. <span data-ttu-id="001fa-181">Return to your resource group and open the storage account that you created earlier</span><span class="sxs-lookup"><span data-stu-id="001fa-181">Return to your resource group and open the storage account that you created earlier</span></span>  

2. <span data-ttu-id="001fa-182">Select **Access keys** from the menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="001fa-182">Select **Access keys** from the menu on the left-hand side.</span></span>  

3. <span data-ttu-id="001fa-183">Copy the values under **key 1** to a notepad or another document that you will have access to throughout the lab.</span><span class="sxs-lookup"><span data-stu-id="001fa-183">Copy the values under **key 1** to a notepad or another document that you will have access to throughout the lab.</span></span> <span data-ttu-id="001fa-184">You should label the **Key** as **Storage Key** and the **Connection string** as **Storage Connection String**.</span><span class="sxs-lookup"><span data-stu-id="001fa-184">You should label the **Key** as **Storage Key** and the **Connection string** as **Storage Connection String**.</span></span> <span data-ttu-id="001fa-185">You'll need to copy these strings into your code later, so take a note and remember where you are storing them.</span><span class="sxs-lookup"><span data-stu-id="001fa-185">You'll need to copy these strings into your code later, so take a note and remember where you are storing them.</span></span>  

### <a name="get-the-event-hub-namespace-connection-string"></a><span data-ttu-id="001fa-186">Get the event hub namespace connection string</span><span class="sxs-lookup"><span data-stu-id="001fa-186">Get the event hub namespace connection string</span></span>

<span data-ttu-id="001fa-187">An Azure Event Hub receives the event data, stores, processes, and forwards the data.</span><span class="sxs-lookup"><span data-stu-id="001fa-187">An Azure Event Hub receives the event data, stores, processes, and forwards the data.</span></span> <span data-ttu-id="001fa-188">In this lab, the Azure Event Hub will receive a document every time a new event occurs (i.e. an item is viewed by a user, added to a user's cart, or purchased by a user) and then will forward that document to Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="001fa-188">In this lab, the Azure Event Hub will receive a document every time a new event occurs (i.e. an item is viewed by a user, added to a user's cart, or purchased by a user) and then will forward that document to Azure Stream Analytics.</span></span>

1. <span data-ttu-id="001fa-189">Return to your resource group and open the **Event Hub Namespace** that you created and named in the prelab.</span><span class="sxs-lookup"><span data-stu-id="001fa-189">Return to your resource group and open the **Event Hub Namespace** that you created and named in the prelab.</span></span>  

2. <span data-ttu-id="001fa-190">Select **Shared access policies** from the menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="001fa-190">Select **Shared access policies** from the menu on the left-hand side.</span></span>  

3. <span data-ttu-id="001fa-191">Select **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="001fa-191">Select **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="001fa-192">Copy the **Connection string-primary key** to a notepad or another document that you will have access to throughout the lab.</span><span class="sxs-lookup"><span data-stu-id="001fa-192">Copy the **Connection string-primary key** to a notepad or another document that you will have access to throughout the lab.</span></span> <span data-ttu-id="001fa-193">You should label it **Event Hub Namespace** connection string.</span><span class="sxs-lookup"><span data-stu-id="001fa-193">You should label it **Event Hub Namespace** connection string.</span></span> <span data-ttu-id="001fa-194">You'll need to copy the string into your code later, so take a note and remember where you are storing it.</span><span class="sxs-lookup"><span data-stu-id="001fa-194">You'll need to copy the string into your code later, so take a note and remember where you are storing it.</span></span>

## <a name="set-up-azure-function-to-read-the-change-feed"></a><span data-ttu-id="001fa-195">Set up Azure Function to read the change feed</span><span class="sxs-lookup"><span data-stu-id="001fa-195">Set up Azure Function to read the change feed</span></span>

<span data-ttu-id="001fa-196">When a new document is created, or a current document is modified in a Cosmos DB collection, the change feed automatically adds that modified document to its history of collection changes.</span><span class="sxs-lookup"><span data-stu-id="001fa-196">When a new document is created, or a current document is modified in a Cosmos DB collection, the change feed automatically adds that modified document to its history of collection changes.</span></span> <span data-ttu-id="001fa-197">You will now build and run an Azure Function that processes the change feed.</span><span class="sxs-lookup"><span data-stu-id="001fa-197">You will now build and run an Azure Function that processes the change feed.</span></span> <span data-ttu-id="001fa-198">When a document is created or modified in the collection you created, the Azure Function will be triggered by the change feed.</span><span class="sxs-lookup"><span data-stu-id="001fa-198">When a document is created or modified in the collection you created, the Azure Function will be triggered by the change feed.</span></span> <span data-ttu-id="001fa-199">Then the Azure Function will send the modified document to the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="001fa-199">Then the Azure Function will send the modified document to the Event Hub.</span></span>

1. <span data-ttu-id="001fa-200">Return to the repository that you cloned on your device.</span><span class="sxs-lookup"><span data-stu-id="001fa-200">Return to the repository that you cloned on your device.</span></span>  

2. <span data-ttu-id="001fa-201">Right-click the file named **ChangeFeedLabSolution.sln** and select **Open With Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="001fa-201">Right-click the file named **ChangeFeedLabSolution.sln** and select **Open With Visual Studio**.</span></span>  

3. <span data-ttu-id="001fa-202">Navigate to **local.settings.json** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="001fa-202">Navigate to **local.settings.json** in Visual Studio.</span></span> <span data-ttu-id="001fa-203">Then use the values you recorded earlier to fill in the blanks.</span><span class="sxs-lookup"><span data-stu-id="001fa-203">Then use the values you recorded earlier to fill in the blanks.</span></span>  

4. <span data-ttu-id="001fa-204">Navigate to **ChangeFeedProcessor.cs**.</span><span class="sxs-lookup"><span data-stu-id="001fa-204">Navigate to **ChangeFeedProcessor.cs**.</span></span> <span data-ttu-id="001fa-205">In the parameters for the **Run** function, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="001fa-205">In the parameters for the **Run** function, perform the following actions:</span></span>  

   * <span data-ttu-id="001fa-206">Replace the text **YOUR COLLECTION NAME HERE** with the name of your collection.</span><span class="sxs-lookup"><span data-stu-id="001fa-206">Replace the text **YOUR COLLECTION NAME HERE** with the name of your collection.</span></span> <span data-ttu-id="001fa-207">If you followed earlier instructions, the name of your collection is changefeedlabcollection.</span><span class="sxs-lookup"><span data-stu-id="001fa-207">If you followed earlier instructions, the name of your collection is changefeedlabcollection.</span></span>  
   * <span data-ttu-id="001fa-208">Replace the text **YOUR LEASES COLLECTION NAME HERE** with the name of your leases collection.</span><span class="sxs-lookup"><span data-stu-id="001fa-208">Replace the text **YOUR LEASES COLLECTION NAME HERE** with the name of your leases collection.</span></span> <span data-ttu-id="001fa-209">If you followed earlier instructions, the name of your leases collection is **leases**.</span><span class="sxs-lookup"><span data-stu-id="001fa-209">If you followed earlier instructions, the name of your leases collection is **leases**.</span></span>  
   * <span data-ttu-id="001fa-210">At the top of Visual Studio, make sure that the Startup Project box on the left of the green arrow says **ChangeFeedFunction**.</span><span class="sxs-lookup"><span data-stu-id="001fa-210">At the top of Visual Studio, make sure that the Startup Project box on the left of the green arrow says **ChangeFeedFunction**.</span></span>  
   * <span data-ttu-id="001fa-211">Select **Start**  at the top of the page to run the program</span><span class="sxs-lookup"><span data-stu-id="001fa-211">Select **Start**  at the top of the page to run the program</span></span>  
   * <span data-ttu-id="001fa-212">You can confirm that the function is running when the console app says "Job host started".</span><span class="sxs-lookup"><span data-stu-id="001fa-212">You can confirm that the function is running when the console app says "Job host started".</span></span>

## <a name="insert-data-into-azure-cosmos-db"></a><span data-ttu-id="001fa-213">Insert data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="001fa-213">Insert data into Azure Cosmos DB</span></span> 

<span data-ttu-id="001fa-214">To see how change feed processes new actions on an e-commerce site, have to simulate data that represents users viewing items from the product catalog, adding those items to their carts, and purchasing the items in their carts.</span><span class="sxs-lookup"><span data-stu-id="001fa-214">To see how change feed processes new actions on an e-commerce site, have to simulate data that represents users viewing items from the product catalog, adding those items to their carts, and purchasing the items in their carts.</span></span> <span data-ttu-id="001fa-215">This data is arbitrary and for the purpose of replicating what data on an Ecommerce site would look like.</span><span class="sxs-lookup"><span data-stu-id="001fa-215">This data is arbitrary and for the purpose of replicating what data on an Ecommerce site would look like.</span></span>

1. <span data-ttu-id="001fa-216">Navigate back to the repository in File Explorer, and right-click **ChangeFeedFunction.sln** to open it again in a new Visual Studio window.</span><span class="sxs-lookup"><span data-stu-id="001fa-216">Navigate back to the repository in File Explorer, and right-click **ChangeFeedFunction.sln** to open it again in a new Visual Studio window.</span></span>  

2. <span data-ttu-id="001fa-217">Navigate to the **App.config** file.Within the <appSettings> block, add the URI and unique **PRIMARY KEY** that of your Azure Cosmos DB account that you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="001fa-217">Navigate to the **App.config** file.Within the <appSettings> block, add the URI and unique **PRIMARY KEY** that of your Azure Cosmos DB account that you retrieved earlier.</span></span>  

3. <span data-ttu-id="001fa-218">Add in the **collection** and **database** names.</span><span class="sxs-lookup"><span data-stu-id="001fa-218">Add in the **collection** and **database** names.</span></span> <span data-ttu-id="001fa-219">(These names should be **changefeedlabcollection** and **changefeedlabdatabase** unless you choose to name yours differently.)</span><span class="sxs-lookup"><span data-stu-id="001fa-219">(These names should be **changefeedlabcollection** and **changefeedlabdatabase** unless you choose to name yours differently.)</span></span>

   ![Update connection strings](./media/changefeed-ecommerce-solution/update-connection-string.png)
 
4. <span data-ttu-id="001fa-221">Save the changes on all the files edited.</span><span class="sxs-lookup"><span data-stu-id="001fa-221">Save the changes on all the files edited.</span></span>  

5. <span data-ttu-id="001fa-222">At the top of Visual Studio, make sure that the **Startup Project** box on the left of the green arrow says **DataGenerator**.</span><span class="sxs-lookup"><span data-stu-id="001fa-222">At the top of Visual Studio, make sure that the **Startup Project** box on the left of the green arrow says **DataGenerator**.</span></span> <span data-ttu-id="001fa-223">Then select **Start** at the top of the page to run the program.</span><span class="sxs-lookup"><span data-stu-id="001fa-223">Then select **Start** at the top of the page to run the program.</span></span>  
 
6. <span data-ttu-id="001fa-224">Wait for the program to run.</span><span class="sxs-lookup"><span data-stu-id="001fa-224">Wait for the program to run.</span></span> <span data-ttu-id="001fa-225">The stars mean that data is coming in!</span><span class="sxs-lookup"><span data-stu-id="001fa-225">The stars mean that data is coming in!</span></span> <span data-ttu-id="001fa-226">Keep the program running - it is important that lots of data is collected.</span><span class="sxs-lookup"><span data-stu-id="001fa-226">Keep the program running - it is important that lots of data is collected.</span></span>  

7. <span data-ttu-id="001fa-227">If you navigate to [Azure Portal](http://portal.azure.com/) , then to the Cosmos DB account within your resource group, then to **Data Explorer**, you will see the randomized data imported in your **changefeedlabcollection** .</span><span class="sxs-lookup"><span data-stu-id="001fa-227">If you navigate to [Azure Portal](http://portal.azure.com/) , then to the Cosmos DB account within your resource group, then to **Data Explorer**, you will see the randomized data imported in your **changefeedlabcollection** .</span></span>
 
   ![Data generated in portal](./media/changefeed-ecommerce-solution/data-generated-in-portal.png)

## <a name="set-up-a-stream-analytics-job"></a><span data-ttu-id="001fa-229">Set up a stream analytics job</span><span class="sxs-lookup"><span data-stu-id="001fa-229">Set up a stream analytics job</span></span>

<span data-ttu-id="001fa-230">Azure Stream Analytics is a fully managed cloud service for real-time processing of streaming data.</span><span class="sxs-lookup"><span data-stu-id="001fa-230">Azure Stream Analytics is a fully managed cloud service for real-time processing of streaming data.</span></span> <span data-ttu-id="001fa-231">In this lab, you will use stream analytics to process new events from the Event Hub (i.e. when an item is viewed, added to a cart, or purchased), incorporate those events into real-time data analysis, and send them into Power BI for visualization.</span><span class="sxs-lookup"><span data-stu-id="001fa-231">In this lab, you will use stream analytics to process new events from the Event Hub (i.e. when an item is viewed, added to a cart, or purchased), incorporate those events into real-time data analysis, and send them into Power BI for visualization.</span></span>

1. <span data-ttu-id="001fa-232">From the [Azure Portal](http://portal.azure.com/), navigate to your resource group, then to **streamjob1** (the stream analytics job that you created in the prelab).</span><span class="sxs-lookup"><span data-stu-id="001fa-232">From the [Azure Portal](http://portal.azure.com/), navigate to your resource group, then to **streamjob1** (the stream analytics job that you created in the prelab).</span></span>  

2. <span data-ttu-id="001fa-233">Select **Inputs** as demonstrated below.</span><span class="sxs-lookup"><span data-stu-id="001fa-233">Select **Inputs** as demonstrated below.</span></span>  

   ![Create input](./media/changefeed-ecommerce-solution/create-input.png)

3. <span data-ttu-id="001fa-235">Select **+ Add stream input**.</span><span class="sxs-lookup"><span data-stu-id="001fa-235">Select **+ Add stream input**.</span></span> <span data-ttu-id="001fa-236">Then select **Event Hub** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="001fa-236">Then select **Event Hub** from the drop-down menu.</span></span>  

4. <span data-ttu-id="001fa-237">Fill the new input form with the following details:</span><span class="sxs-lookup"><span data-stu-id="001fa-237">Fill the new input form with the following details:</span></span>

   * <span data-ttu-id="001fa-238">In the **Input** alias field, enter **input**.</span><span class="sxs-lookup"><span data-stu-id="001fa-238">In the **Input** alias field, enter **input**.</span></span>  
   * <span data-ttu-id="001fa-239">Select the option for **Select Event Hub from your subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="001fa-239">Select the option for **Select Event Hub from your subscriptions**.</span></span>  
   * <span data-ttu-id="001fa-240">Set the **Subscription** field to your subscription.</span><span class="sxs-lookup"><span data-stu-id="001fa-240">Set the **Subscription** field to your subscription.</span></span>  
   * <span data-ttu-id="001fa-241">In the **Event Hub namespace** field, enter the name of your Event Hub Namespace that you created during the prelab.</span><span class="sxs-lookup"><span data-stu-id="001fa-241">In the **Event Hub namespace** field, enter the name of your Event Hub Namespace that you created during the prelab.</span></span>  
   * <span data-ttu-id="001fa-242">In the **Event Hub name** field, select the option for **Use existing** and choose **event-hub1** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="001fa-242">In the **Event Hub name** field, select the option for **Use existing** and choose **event-hub1** from the drop-down menu.</span></span>  
   * <span data-ttu-id="001fa-243">Leave **Event Hub policy** name field set to its default value.</span><span class="sxs-lookup"><span data-stu-id="001fa-243">Leave **Event Hub policy** name field set to its default value.</span></span>  
   * <span data-ttu-id="001fa-244">Leave **Event serialization format** as **JSON**.</span><span class="sxs-lookup"><span data-stu-id="001fa-244">Leave **Event serialization format** as **JSON**.</span></span>  
   * <span data-ttu-id="001fa-245">Leave **Encoding field** set to **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="001fa-245">Leave **Encoding field** set to **UTF-8**.</span></span>  
   * <span data-ttu-id="001fa-246">Leave **Event compression type** field set to **None**.</span><span class="sxs-lookup"><span data-stu-id="001fa-246">Leave **Event compression type** field set to **None**.</span></span>  
   * <span data-ttu-id="001fa-247">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="001fa-247">Click the **Save** button.</span></span>

5. <span data-ttu-id="001fa-248">Navigate back to the stream analytics job page, and select **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="001fa-248">Navigate back to the stream analytics job page, and select **Outputs**.</span></span>  

6. <span data-ttu-id="001fa-249">Select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="001fa-249">Select **+ Add**.</span></span> <span data-ttu-id="001fa-250">Then select **Power BI** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="001fa-250">Then select **Power BI** from the drop-down menu.</span></span>  

7. <span data-ttu-id="001fa-251">To create a new Power BI output to visualize average price, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="001fa-251">To create a new Power BI output to visualize average price, perform the following actions:</span></span>

   * <span data-ttu-id="001fa-252">In the **Output alias** field, enter **averagePriceOutput**.</span><span class="sxs-lookup"><span data-stu-id="001fa-252">In the **Output alias** field, enter **averagePriceOutput**.</span></span>  
   * <span data-ttu-id="001fa-253">Leave the **Group workspace** field set to **Authorize connection to load workspaces**.</span><span class="sxs-lookup"><span data-stu-id="001fa-253">Leave the **Group workspace** field set to **Authorize connection to load workspaces**.</span></span>  
   * <span data-ttu-id="001fa-254">In the **Dataset name** field, enter **averagePrice**.</span><span class="sxs-lookup"><span data-stu-id="001fa-254">In the **Dataset name** field, enter **averagePrice**.</span></span>  
   * <span data-ttu-id="001fa-255">In the **Table name** field, enter **averagePrice**.</span><span class="sxs-lookup"><span data-stu-id="001fa-255">In the **Table name** field, enter **averagePrice**.</span></span>  
   * <span data-ttu-id="001fa-256">Click the **Authorize** button, then follow the instructions to authorize the connection to Power BI.</span><span class="sxs-lookup"><span data-stu-id="001fa-256">Click the **Authorize** button, then follow the instructions to authorize the connection to Power BI.</span></span>  
   * <span data-ttu-id="001fa-257">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="001fa-257">Click the **Save** button.</span></span>  

8. <span data-ttu-id="001fa-258">Then go back to **streamjob1** and click **Edit query**.</span><span class="sxs-lookup"><span data-stu-id="001fa-258">Then go back to **streamjob1** and click **Edit query**.</span></span>

   ![Edit query](./media/changefeed-ecommerce-solution/edit-query.png)
 
9. <span data-ttu-id="001fa-260">Paste the following query into the query window.</span><span class="sxs-lookup"><span data-stu-id="001fa-260">Paste the following query into the query window.</span></span> <span data-ttu-id="001fa-261">The **AVERAGE PRICE** query calculates the average price of all items that are viewed by users, the average price of all items that are added to users' carts, and the average price of all items that are purchased by users.</span><span class="sxs-lookup"><span data-stu-id="001fa-261">The **AVERAGE PRICE** query calculates the average price of all items that are viewed by users, the average price of all items that are added to users' carts, and the average price of all items that are purchased by users.</span></span> <span data-ttu-id="001fa-262">This metric can help e-commerce companies decide what prices to sell items at and what inventory to invest in.</span><span class="sxs-lookup"><span data-stu-id="001fa-262">This metric can help e-commerce companies decide what prices to sell items at and what inventory to invest in.</span></span> <span data-ttu-id="001fa-263">For example, if the average price of items viewed is much higher than the average price of items purchased, then a company might choose to add less expensive items to its inventory.</span><span class="sxs-lookup"><span data-stu-id="001fa-263">For example, if the average price of items viewed is much higher than the average price of items purchased, then a company might choose to add less expensive items to its inventory.</span></span>

   ```sql
   /*AVERAGE PRICE*/      
   SELECT System.TimeStamp AS Time, Action, AVG(Price)  
    INTO averagePriceOutput  
    FROM input  
    GROUP BY Action, TumblingWindow(second,5) 
   ```
10. <span data-ttu-id="001fa-264">Then click **Save** in the upper left-hand corner.</span><span class="sxs-lookup"><span data-stu-id="001fa-264">Then click **Save** in the upper left-hand corner.</span></span>  

11. <span data-ttu-id="001fa-265">Now return to **streamjob1** and click the **Start** button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="001fa-265">Now return to **streamjob1** and click the **Start** button at the top of the page.</span></span> <span data-ttu-id="001fa-266">Azure Stream Analytics can take a few minutes to start up, but eventually you will see it change from "Starting" to "Running".</span><span class="sxs-lookup"><span data-stu-id="001fa-266">Azure Stream Analytics can take a few minutes to start up, but eventually you will see it change from "Starting" to "Running".</span></span>

## <a name="connect-to-power-bi"></a><span data-ttu-id="001fa-267">Connect to Power BI</span><span class="sxs-lookup"><span data-stu-id="001fa-267">Connect to Power BI</span></span>

<span data-ttu-id="001fa-268">Power BI is a suite of business analytics tools to analyze data and share insights.</span><span class="sxs-lookup"><span data-stu-id="001fa-268">Power BI is a suite of business analytics tools to analyze data and share insights.</span></span> <span data-ttu-id="001fa-269">It's a great example of how you can strategically visualize the analyzed data.</span><span class="sxs-lookup"><span data-stu-id="001fa-269">It's a great example of how you can strategically visualize the analyzed data.</span></span>

1. <span data-ttu-id="001fa-270">Sign in to Power BI and navigate to **My Workspace** by opening the menu on the left-hand side of the page.</span><span class="sxs-lookup"><span data-stu-id="001fa-270">Sign in to Power BI and navigate to **My Workspace** by opening the menu on the left-hand side of the page.</span></span>  

2. <span data-ttu-id="001fa-271">Select **+ Create** in the top right-hand corner and then select **Dashboard** to create a dashboard.</span><span class="sxs-lookup"><span data-stu-id="001fa-271">Select **+ Create** in the top right-hand corner and then select **Dashboard** to create a dashboard.</span></span>  

3. <span data-ttu-id="001fa-272">Select **+ Add tile** in the top right-hand corner.</span><span class="sxs-lookup"><span data-stu-id="001fa-272">Select **+ Add tile** in the top right-hand corner.</span></span>  

4. <span data-ttu-id="001fa-273">Select **Custom Streaming Data**, then click the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="001fa-273">Select **Custom Streaming Data**, then click the **Next** button.</span></span>  
 
5. <span data-ttu-id="001fa-274">Select **averagePrice** from **YOUR DATASETS**, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="001fa-274">Select **averagePrice** from **YOUR DATASETS**, then click **Next**.</span></span>  

6. <span data-ttu-id="001fa-275">In the **Visualization Type** field, choose **Clustered bar chart** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="001fa-275">In the **Visualization Type** field, choose **Clustered bar chart** from the drop-down menu.</span></span> <span data-ttu-id="001fa-276">Under **Axis**, add action.</span><span class="sxs-lookup"><span data-stu-id="001fa-276">Under **Axis**, add action.</span></span> <span data-ttu-id="001fa-277">Skip **Legend** without adding anything.</span><span class="sxs-lookup"><span data-stu-id="001fa-277">Skip **Legend** without adding anything.</span></span> <span data-ttu-id="001fa-278">Then, under the next section called **Value**, add **avg**. Select **Next**, then title your chart, and select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="001fa-278">Then, under the next section called **Value**, add **avg**. Select **Next**, then title your chart, and select **Apply**.</span></span> <span data-ttu-id="001fa-279">You should see a new chart on your dashboard!</span><span class="sxs-lookup"><span data-stu-id="001fa-279">You should see a new chart on your dashboard!</span></span>  

7. <span data-ttu-id="001fa-280">Now, if you want to visualize more metrics, you can go back to **streamjob1** and create three more outputs with the following fields.</span><span class="sxs-lookup"><span data-stu-id="001fa-280">Now, if you want to visualize more metrics, you can go back to **streamjob1** and create three more outputs with the following fields.</span></span>

   <span data-ttu-id="001fa-281">a.</span><span class="sxs-lookup"><span data-stu-id="001fa-281">a.</span></span> <span data-ttu-id="001fa-282">**Output alias:** incomingRevenueOutput, Dataset name: incomingRevenue, Table name: incomingRevenue</span><span class="sxs-lookup"><span data-stu-id="001fa-282">**Output alias:** incomingRevenueOutput, Dataset name: incomingRevenue, Table name: incomingRevenue</span></span>  
   <span data-ttu-id="001fa-283">b.</span><span class="sxs-lookup"><span data-stu-id="001fa-283">b.</span></span> <span data-ttu-id="001fa-284">**Output alias:** top5Output, Dataset name: top5, Table name: top5</span><span class="sxs-lookup"><span data-stu-id="001fa-284">**Output alias:** top5Output, Dataset name: top5, Table name: top5</span></span>  
   <span data-ttu-id="001fa-285">c.</span><span class="sxs-lookup"><span data-stu-id="001fa-285">c.</span></span> <span data-ttu-id="001fa-286">**Output alias:** uniqueVisitorCountOutput, Dataset name: uniqueVisitorCount, Table name: uniqueVisitorCount</span><span class="sxs-lookup"><span data-stu-id="001fa-286">**Output alias:** uniqueVisitorCountOutput, Dataset name: uniqueVisitorCount, Table name: uniqueVisitorCount</span></span>

   <span data-ttu-id="001fa-287">Then click **Edit query** and paste the following queries **above** the one you already wrote.</span><span class="sxs-lookup"><span data-stu-id="001fa-287">Then click **Edit query** and paste the following queries **above** the one you already wrote.</span></span>

   ```sql
    /*TOP 5*/
    WITH Counter AS
    (
    SELECT Item, Price, Action, COUNT(*) AS countEvents
    FROM input
    WHERE Action = 'Purchased'
    GROUP BY Item, Price, Action, TumblingWindow(second,30)
    ), 
    top5 AS
    (
    SELECT DISTINCT
    CollectTop(5)  OVER (ORDER BY countEvents) AS topEvent
    FROM Counter
    GROUP BY TumblingWindow(second,30)
    ), 
    arrayselect AS 
    (
    SELECT arrayElement.ArrayValue
    FROM top5
    CROSS APPLY GetArrayElements(top5.topevent) AS arrayElement
    ) 
    SELECT arrayvalue.value.item, arrayvalue.value.price,   arrayvalue.value.countEvents
    INTO top5Output
    FROM arrayselect

    /*REVENUE*/
    SELECT System.TimeStamp AS Time, SUM(Price)
    INTO incomingRevenueOutput
    FROM input
    WHERE Action = 'Purchased'
    GROUP BY TumblingWindow(hour, 1)

    /*UNIQUE VISITORS*/
    SELECT System.TimeStamp AS Time, COUNT(DISTINCT CartID) as uniqueVisitors
    INTO uniqueVisitorCountOutput
    FROM input
    GROUP BY TumblingWindow(second, 5)
   ```
   
   <span data-ttu-id="001fa-288">The TOP 5 query calculates the top 5 items, ranked by the number of times that they have been purchased.</span><span class="sxs-lookup"><span data-stu-id="001fa-288">The TOP 5 query calculates the top 5 items, ranked by the number of times that they have been purchased.</span></span> <span data-ttu-id="001fa-289">This metric can help e-commerce companies evaluate which items are most popular and can influence the company's advertising, pricing, and inventory decisions.</span><span class="sxs-lookup"><span data-stu-id="001fa-289">This metric can help e-commerce companies evaluate which items are most popular and can influence the company's advertising, pricing, and inventory decisions.</span></span>

   <span data-ttu-id="001fa-290">The REVENUE query calculates revenue by summing up the prices of all items purchased each minute.</span><span class="sxs-lookup"><span data-stu-id="001fa-290">The REVENUE query calculates revenue by summing up the prices of all items purchased each minute.</span></span> <span data-ttu-id="001fa-291">This metric can help e-commerce companies evaluate its financial performance and also understand what times of day contribute to most revenue.</span><span class="sxs-lookup"><span data-stu-id="001fa-291">This metric can help e-commerce companies evaluate its financial performance and also understand what times of day contribute to most revenue.</span></span> <span data-ttu-id="001fa-292">This can impact the overall company strategy, marketing in particular.</span><span class="sxs-lookup"><span data-stu-id="001fa-292">This can impact the overall company strategy, marketing in particular.</span></span>

   <span data-ttu-id="001fa-293">The UNIQUE VISITORS query calculates how many unique visitors are on the site every 5 seconds by detecting unique cart ID's.</span><span class="sxs-lookup"><span data-stu-id="001fa-293">The UNIQUE VISITORS query calculates how many unique visitors are on the site every 5 seconds by detecting unique cart ID's.</span></span> <span data-ttu-id="001fa-294">This metric can help e-commerce companies evaluate their site activity and strategize how to acquire more customers.</span><span class="sxs-lookup"><span data-stu-id="001fa-294">This metric can help e-commerce companies evaluate their site activity and strategize how to acquire more customers.</span></span>

8. <span data-ttu-id="001fa-295">You can now add tiles for these datasets as well.</span><span class="sxs-lookup"><span data-stu-id="001fa-295">You can now add tiles for these datasets as well.</span></span>

   * <span data-ttu-id="001fa-296">For Top 5, it would make sense to do a clustered column chart with the items as the axis and the count as the value.</span><span class="sxs-lookup"><span data-stu-id="001fa-296">For Top 5, it would make sense to do a clustered column chart with the items as the axis and the count as the value.</span></span>  
   * <span data-ttu-id="001fa-297">For Revenue, it would make sense to do a line chart with time as the axis and the sum of the prices as the value.</span><span class="sxs-lookup"><span data-stu-id="001fa-297">For Revenue, it would make sense to do a line chart with time as the axis and the sum of the prices as the value.</span></span> <span data-ttu-id="001fa-298">The time window to display should be the largest possible in order to deliver as much information as possible.</span><span class="sxs-lookup"><span data-stu-id="001fa-298">The time window to display should be the largest possible in order to deliver as much information as possible.</span></span>  
   * <span data-ttu-id="001fa-299">For Unique Visitors, it would make sense to do a card visualization with the number of unique visitors as the value.</span><span class="sxs-lookup"><span data-stu-id="001fa-299">For Unique Visitors, it would make sense to do a card visualization with the number of unique visitors as the value.</span></span>

   <span data-ttu-id="001fa-300">This is how a sample dashboard looks with these charts:</span><span class="sxs-lookup"><span data-stu-id="001fa-300">This is how a sample dashboard looks with these charts:</span></span>

   ![visualizations](./media/changefeed-ecommerce-solution/visualizations.png)

## <a name="optional-visualize-with-an-e-commerce-site"></a><span data-ttu-id="001fa-302">Optional: Visualize with an E-commerce site</span><span class="sxs-lookup"><span data-stu-id="001fa-302">Optional: Visualize with an E-commerce site</span></span>

<span data-ttu-id="001fa-303">You will now observe how you can use your new data analysis tool to connect with a real e-commerce site.</span><span class="sxs-lookup"><span data-stu-id="001fa-303">You will now observe how you can use your new data analysis tool to connect with a real e-commerce site.</span></span> <span data-ttu-id="001fa-304">In order to build the e-commerce site, use an Azure Cosmos DB database to store the list of product categories (Women's, Men's, Unisex), the product catalog, and a list of the most popular items.</span><span class="sxs-lookup"><span data-stu-id="001fa-304">In order to build the e-commerce site, use an Azure Cosmos DB database to store the list of product categories (Women's, Men's, Unisex), the product catalog, and a list of the most popular items.</span></span>

1. <span data-ttu-id="001fa-305">Navigate back to the [Azure Portal](http://portal.azure.com/), then to your **Cosmos DB account**, then to **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="001fa-305">Navigate back to the [Azure Portal](http://portal.azure.com/), then to your **Cosmos DB account**, then to **Data Explorer**.</span></span>  

   <span data-ttu-id="001fa-306">Add two collections under **changefeedlabdatabase** - **products** and **categories** with Fixed storage capacity.</span><span class="sxs-lookup"><span data-stu-id="001fa-306">Add two collections under **changefeedlabdatabase** - **products** and **categories** with Fixed storage capacity.</span></span>

   <span data-ttu-id="001fa-307">Add another collection under **changefeedlabdatabase** named **topItems** with **Unlimited** storage capacity.</span><span class="sxs-lookup"><span data-stu-id="001fa-307">Add another collection under **changefeedlabdatabase** named **topItems** with **Unlimited** storage capacity.</span></span> <span data-ttu-id="001fa-308">Write **/Item** as the partition key.</span><span class="sxs-lookup"><span data-stu-id="001fa-308">Write **/Item** as the partition key.</span></span>

2. <span data-ttu-id="001fa-309">Click on the **topItems** collection, and under **Scale and Settings** set the **Time to Live** to be **30 seconds** so that topItems updates every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="001fa-309">Click on the **topItems** collection, and under **Scale and Settings** set the **Time to Live** to be **30 seconds** so that topItems updates every 30 seconds.</span></span>

   ![Time to live](./media/changefeed-ecommerce-solution/time-to-live.png)

3. <span data-ttu-id="001fa-311">In order to populate the **topItems** collection with the most frequently purchased items, navigate back to **streamjob1** and add a new **Output**.</span><span class="sxs-lookup"><span data-stu-id="001fa-311">In order to populate the **topItems** collection with the most frequently purchased items, navigate back to **streamjob1** and add a new **Output**.</span></span> <span data-ttu-id="001fa-312">Select **Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="001fa-312">Select **Cosmos DB**.</span></span>

4. <span data-ttu-id="001fa-313">Fill in the required fields as pictured below.</span><span class="sxs-lookup"><span data-stu-id="001fa-313">Fill in the required fields as pictured below.</span></span>

   ![Cosmos output](./media/changefeed-ecommerce-solution/cosmos-output.png)
 
5. <span data-ttu-id="001fa-315">If you added the optional TOP 5 query in the previous part of the lab, proceed to part 5a.</span><span class="sxs-lookup"><span data-stu-id="001fa-315">If you added the optional TOP 5 query in the previous part of the lab, proceed to part 5a.</span></span> <span data-ttu-id="001fa-316">If not, proceed to part 5b.</span><span class="sxs-lookup"><span data-stu-id="001fa-316">If not, proceed to part 5b.</span></span>

   <span data-ttu-id="001fa-317">5a.</span><span class="sxs-lookup"><span data-stu-id="001fa-317">5a.</span></span> <span data-ttu-id="001fa-318">In **streamjob1**, select **Edit query** and paste the following query in your Azure Stream Analytics query editor below the TOP 5 query but above the rest of the queries.</span><span class="sxs-lookup"><span data-stu-id="001fa-318">In **streamjob1**, select **Edit query** and paste the following query in your Azure Stream Analytics query editor below the TOP 5 query but above the rest of the queries.</span></span>

   ```sql
   SELECT arrayvalue.value.item AS Item, arrayvalue.value.price, arrayvalue.value.countEvents
   INTO topItems
   FROM arrayselect
   ```
   <span data-ttu-id="001fa-319">5b.</span><span class="sxs-lookup"><span data-stu-id="001fa-319">5b.</span></span> <span data-ttu-id="001fa-320">In **streamjob1**, select **Edit query** and paste the following query in your Azure Stream Analytics query editor above all other queries.</span><span class="sxs-lookup"><span data-stu-id="001fa-320">In **streamjob1**, select **Edit query** and paste the following query in your Azure Stream Analytics query editor above all other queries.</span></span>

   ```sql
   /*TOP 5*/
   WITH Counter AS
   (
   SELECT Item, Price, Action, COUNT(*) AS countEvents
   FROM input
   WHERE Action = 'Purchased'
   GROUP BY Item, Price, Action, TumblingWindow(second,30)
   ), 
   top5 AS
   (
   SELECT DISTINCT
   CollectTop(5)  OVER (ORDER BY countEvents) AS topEvent
   FROM Counter
   GROUP BY TumblingWindow(second,30)
   ), 
   arrayselect AS 
   (
   SELECT arrayElement.ArrayValue
   FROM top5
   CROSS APPLY GetArrayElements(top5.topevent) AS arrayElement
   ) 
   SELECT arrayvalue.value.item AS Item, arrayvalue.value.price, arrayvalue.value.countEvents
   INTO topItems
   FROM arrayselect
   ```

6. <span data-ttu-id="001fa-321">Open **EcommerceWebApp.sln** and navigate to the **Web.config** file in the **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="001fa-321">Open **EcommerceWebApp.sln** and navigate to the **Web.config** file in the **Solution Explorer**.</span></span>  

7. <span data-ttu-id="001fa-322">Within the `<appSettings>` block, add the **URI** and **PRIMARY KEY** that you saved earlier where it says **your URI here** and **your primary key here**.</span><span class="sxs-lookup"><span data-stu-id="001fa-322">Within the `<appSettings>` block, add the **URI** and **PRIMARY KEY** that you saved earlier where it says **your URI here** and **your primary key here**.</span></span> <span data-ttu-id="001fa-323">Then add in your **database name** and **collection name** as indicated.</span><span class="sxs-lookup"><span data-stu-id="001fa-323">Then add in your **database name** and **collection name** as indicated.</span></span> <span data-ttu-id="001fa-324">(These names should be **changefeedlabdatabase** and **changefeedlabcollection** unless you chose to name yours differently.)</span><span class="sxs-lookup"><span data-stu-id="001fa-324">(These names should be **changefeedlabdatabase** and **changefeedlabcollection** unless you chose to name yours differently.)</span></span>

   <span data-ttu-id="001fa-325">Fill in your **products collection name**, **categories collection name**, and **top items collection name** as indicated.</span><span class="sxs-lookup"><span data-stu-id="001fa-325">Fill in your **products collection name**, **categories collection name**, and **top items collection name** as indicated.</span></span> <span data-ttu-id="001fa-326">(These names should be **products, categories, and topItems** unless you chose to name yours differently.)</span><span class="sxs-lookup"><span data-stu-id="001fa-326">(These names should be **products, categories, and topItems** unless you chose to name yours differently.)</span></span>  

8. <span data-ttu-id="001fa-327">Navigate to and open the **Checkout folder** within **EcommerceWebApp.sln.**</span><span class="sxs-lookup"><span data-stu-id="001fa-327">Navigate to and open the **Checkout folder** within **EcommerceWebApp.sln.**</span></span> <span data-ttu-id="001fa-328">Then open the **Web.config** file within that folder.</span><span class="sxs-lookup"><span data-stu-id="001fa-328">Then open the **Web.config** file within that folder.</span></span>  

9. <span data-ttu-id="001fa-329">Within the `<appSettings>` block, add the **URI** and **PRIMARY KEY** that you saved earlier where indicated.</span><span class="sxs-lookup"><span data-stu-id="001fa-329">Within the `<appSettings>` block, add the **URI** and **PRIMARY KEY** that you saved earlier where indicated.</span></span> <span data-ttu-id="001fa-330">Then add in your **databse name** and **collection name** as indicated.</span><span class="sxs-lookup"><span data-stu-id="001fa-330">Then add in your **databse name** and **collection name** as indicated.</span></span> <span data-ttu-id="001fa-331">(These names should be **changefeedlabdatabase** and **changefeedlabcollection** unless you chose to name yours differently.)</span><span class="sxs-lookup"><span data-stu-id="001fa-331">(These names should be **changefeedlabdatabase** and **changefeedlabcollection** unless you chose to name yours differently.)</span></span>  

10. <span data-ttu-id="001fa-332">Press **Start** at the top of the page to run the program.</span><span class="sxs-lookup"><span data-stu-id="001fa-332">Press **Start** at the top of the page to run the program.</span></span>  

11. <span data-ttu-id="001fa-333">Now you can play around on the e-commerce site.</span><span class="sxs-lookup"><span data-stu-id="001fa-333">Now you can play around on the e-commerce site.</span></span> <span data-ttu-id="001fa-334">When you view an item, add an item to your cart, change the quantity of an item in your cart, or purchase an item, these events will be passed through the Cosmos DB change feed to Event Hub, ASA, and then Power BI.</span><span class="sxs-lookup"><span data-stu-id="001fa-334">When you view an item, add an item to your cart, change the quantity of an item in your cart, or purchase an item, these events will be passed through the Cosmos DB change feed to Event Hub, ASA, and then Power BI.</span></span> <span data-ttu-id="001fa-335">We recommend continuing to run DataGenerator to generate significant web traffic data and provide a realistic set of "Hot Products" on the e-commerce site.</span><span class="sxs-lookup"><span data-stu-id="001fa-335">We recommend continuing to run DataGenerator to generate significant web traffic data and provide a realistic set of "Hot Products" on the e-commerce site.</span></span>

## <a name="delete-the-resources"></a><span data-ttu-id="001fa-336">Delete the resources</span><span class="sxs-lookup"><span data-stu-id="001fa-336">Delete the resources</span></span>

<span data-ttu-id="001fa-337">To delete the resources that you created during this lab, navigate to the resource group on [Azure Portal](http://portal.azure.com/), then select **Delete resource group** from the menu at the top of the page and follow the instructions provided.</span><span class="sxs-lookup"><span data-stu-id="001fa-337">To delete the resources that you created during this lab, navigate to the resource group on [Azure Portal](http://portal.azure.com/), then select **Delete resource group** from the menu at the top of the page and follow the instructions provided.</span></span>

## <a name="next-steps"></a><span data-ttu-id="001fa-338">Next steps</span><span class="sxs-lookup"><span data-stu-id="001fa-338">Next steps</span></span> 
  
* <span data-ttu-id="001fa-339">To learn more about change feed, see [working with change feed support in Azure Cosmos DB](change-feed.md)</span><span class="sxs-lookup"><span data-stu-id="001fa-339">To learn more about change feed, see [working with change feed support in Azure Cosmos DB](change-feed.md)</span></span> 
* <span data-ttu-id="001fa-340">[Change feed notification solution](change-feed-hl7-fhir-logic-apps.md) for healthcare organization using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="001fa-340">[Change feed notification solution](change-feed-hl7-fhir-logic-apps.md) for healthcare organization using Azure Cosmos DB.</span></span>
