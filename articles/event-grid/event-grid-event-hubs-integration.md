---
title: Azure Event Grid and Event Hubs integration
description: Describes how to use Azure Event Grid and Event Hubs to migrate data to a SQL Data Warehouse
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: tutorial
ms.date: 08/22/2018
ms.author: tomfitz
ms.openlocfilehash: aad7a24d8b0e0bc74815cad3604db1cc21a6db96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966449"
---
# <a name="stream-big-data-into-a-data-warehouse"></a><span data-ttu-id="7b624-103">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="7b624-103">Stream big data into a data warehouse</span></span>

<span data-ttu-id="7b624-104">Azure [Event Grid](overview.md) is an intelligent event routing service that enables you to react to notifications from apps and services.</span><span class="sxs-lookup"><span data-stu-id="7b624-104">Azure [Event Grid](overview.md) is an intelligent event routing service that enables you to react to notifications from apps and services.</span></span> <span data-ttu-id="7b624-105">For example, it can trigger an Azure Function to process Event Hubs data that has been captured to an Azure Blob storage or Data Lake Store, and migrate the data to other data repositories.</span><span class="sxs-lookup"><span data-stu-id="7b624-105">For example, it can trigger an Azure Function to process Event Hubs data that has been captured to an Azure Blob storage or Data Lake Store, and migrate the data to other data repositories.</span></span> <span data-ttu-id="7b624-106">This [Event Hubs Capture and Event Grid sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) shows how to use Event Hubs Capture with Event Grid to seamlessly migrate Event Hubs data from blob storage to a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b624-106">This [Event Hubs Capture and Event Grid sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) shows how to use Event Hubs Capture with Event Grid to seamlessly migrate Event Hubs data from blob storage to a SQL Data Warehouse.</span></span>

![Application overview](media/event-grid-event-hubs-integration/overview.png)

<span data-ttu-id="7b624-108">As data is sent to the event hub, Capture pulls data from the stream and generates storage blobs with the data in Avro format.</span><span class="sxs-lookup"><span data-stu-id="7b624-108">As data is sent to the event hub, Capture pulls data from the stream and generates storage blobs with the data in Avro format.</span></span> <span data-ttu-id="7b624-109">When Capture generates the blob, it triggers an event.</span><span class="sxs-lookup"><span data-stu-id="7b624-109">When Capture generates the blob, it triggers an event.</span></span> <span data-ttu-id="7b624-110">Event Grid distributes data about the event to subscribers.</span><span class="sxs-lookup"><span data-stu-id="7b624-110">Event Grid distributes data about the event to subscribers.</span></span> <span data-ttu-id="7b624-111">In this case, the event data is sent to the Azure Functions endpoint.</span><span class="sxs-lookup"><span data-stu-id="7b624-111">In this case, the event data is sent to the Azure Functions endpoint.</span></span> <span data-ttu-id="7b624-112">The event data includes the path of the generated blob.</span><span class="sxs-lookup"><span data-stu-id="7b624-112">The event data includes the path of the generated blob.</span></span> <span data-ttu-id="7b624-113">The function uses that URL to retrieve the file, and send it to the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b624-113">The function uses that URL to retrieve the file, and send it to the data warehouse.</span></span>

<span data-ttu-id="7b624-114">In this article, you:</span><span class="sxs-lookup"><span data-stu-id="7b624-114">In this article, you:</span></span>

* <span data-ttu-id="7b624-115">Deploy the following infrastructure:</span><span class="sxs-lookup"><span data-stu-id="7b624-115">Deploy the following infrastructure:</span></span>
  * <span data-ttu-id="7b624-116">Event hub with Capture enabled</span><span class="sxs-lookup"><span data-stu-id="7b624-116">Event hub with Capture enabled</span></span>
  * <span data-ttu-id="7b624-117">Storage account for the files from Capture</span><span class="sxs-lookup"><span data-stu-id="7b624-117">Storage account for the files from Capture</span></span>
  * <span data-ttu-id="7b624-118">Azure app service plan for hosting the function app</span><span class="sxs-lookup"><span data-stu-id="7b624-118">Azure app service plan for hosting the function app</span></span>
  * <span data-ttu-id="7b624-119">Function app for processing the event</span><span class="sxs-lookup"><span data-stu-id="7b624-119">Function app for processing the event</span></span>
  * <span data-ttu-id="7b624-120">SQL Server for hosting the data warehouse</span><span class="sxs-lookup"><span data-stu-id="7b624-120">SQL Server for hosting the data warehouse</span></span>
  * <span data-ttu-id="7b624-121">SQL Data Warehouse for storing the migrated data</span><span class="sxs-lookup"><span data-stu-id="7b624-121">SQL Data Warehouse for storing the migrated data</span></span>
* <span data-ttu-id="7b624-122">Create a table in the data warehouse</span><span class="sxs-lookup"><span data-stu-id="7b624-122">Create a table in the data warehouse</span></span>
* <span data-ttu-id="7b624-123">Add code to the function app</span><span class="sxs-lookup"><span data-stu-id="7b624-123">Add code to the function app</span></span>
* <span data-ttu-id="7b624-124">Subscribe to the event</span><span class="sxs-lookup"><span data-stu-id="7b624-124">Subscribe to the event</span></span>
* <span data-ttu-id="7b624-125">Run app that sends data to the event hub</span><span class="sxs-lookup"><span data-stu-id="7b624-125">Run app that sends data to the event hub</span></span>
* <span data-ttu-id="7b624-126">View migrated data in data warehouse</span><span class="sxs-lookup"><span data-stu-id="7b624-126">View migrated data in data warehouse</span></span>

## <a name="about-the-event-data"></a><span data-ttu-id="7b624-127">About the event data</span><span class="sxs-lookup"><span data-stu-id="7b624-127">About the event data</span></span>

<span data-ttu-id="7b624-128">Event Grid distributes event data to the subscribers.</span><span class="sxs-lookup"><span data-stu-id="7b624-128">Event Grid distributes event data to the subscribers.</span></span> <span data-ttu-id="7b624-129">The following example shows event data for creating a Capture file.</span><span class="sxs-lookup"><span data-stu-id="7b624-129">The following example shows event data for creating a Capture file.</span></span> <span data-ttu-id="7b624-130">In particular, notice the `fileUrl` property in the `data` object.</span><span class="sxs-lookup"><span data-stu-id="7b624-130">In particular, notice the `fileUrl` property in the `data` object.</span></span> <span data-ttu-id="7b624-131">The function app gets this value and uses it to retrieve the Capture file.</span><span class="sxs-lookup"><span data-stu-id="7b624-131">The function app gets this value and uses it to retrieve the Capture file.</span></span>

```json
[
    {
        "topic": "/subscriptions/<guid>/resourcegroups/rgDataMigrationSample/providers/Microsoft.EventHub/namespaces/tfdatamigratens",
        "subject": "eventhubs/hubdatamigration",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-08-31T19:12:46.0498024Z",
        "id": "14e87d03-6fbf-4bb2-9a21-92bd1281f247",
        "data": {
            "fileUrl": "https://tf0831datamigrate.blob.core.windows.net/windturbinecapture/tfdatamigratens/hubdatamigration/1/2017/08/31/19/11/45.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 249168,
            "eventCount": 1500,
            "firstSequenceNumber": 2400,
            "lastSequenceNumber": 3899,
            "firstEnqueueTime": "2017-08-31T19:12:14.674Z",
            "lastEnqueueTime": "2017-08-31T19:12:44.309Z"
        }
    }
]
```

## <a name="prerequisites"></a><span data-ttu-id="7b624-132">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7b624-132">Prerequisites</span></span>

<span data-ttu-id="7b624-133">To complete this tutorial, you must have:</span><span class="sxs-lookup"><span data-stu-id="7b624-133">To complete this tutorial, you must have:</span></span>

* <span data-ttu-id="7b624-134">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b624-134">An Azure subscription.</span></span> <span data-ttu-id="7b624-135">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="7b624-135">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
* <span data-ttu-id="7b624-136">[Visual studio 2017 Version 15.3.2 or greater](https://www.visualstudio.com/vs/) with workloads for: .NET desktop development, Azure development, ASP.NET and web development, Node.js development, and Python development.</span><span class="sxs-lookup"><span data-stu-id="7b624-136">[Visual studio 2017 Version 15.3.2 or greater](https://www.visualstudio.com/vs/) with workloads for: .NET desktop development, Azure development, ASP.NET and web development, Node.js development, and Python development.</span></span>
* <span data-ttu-id="7b624-137">The [EventHubsCaptureEventGridDemo sample project](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) downloaded to your computer.</span><span class="sxs-lookup"><span data-stu-id="7b624-137">The [EventHubsCaptureEventGridDemo sample project](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) downloaded to your computer.</span></span>

## <a name="deploy-the-infrastructure"></a><span data-ttu-id="7b624-138">Deploy the infrastructure</span><span class="sxs-lookup"><span data-stu-id="7b624-138">Deploy the infrastructure</span></span>

<span data-ttu-id="7b624-139">To simplify this article, you deploy the required infrastructure with a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="7b624-139">To simplify this article, you deploy the required infrastructure with a Resource Manager template.</span></span> <span data-ttu-id="7b624-140">To see the resources that are deployed, view the [template](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/EventHubsDataMigration.json).</span><span class="sxs-lookup"><span data-stu-id="7b624-140">To see the resources that are deployed, view the [template](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/EventHubsDataMigration.json).</span></span>

<span data-ttu-id="7b624-141">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="7b624-141">For Azure CLI, use:</span></span>

```azurecli-interactive
az group create -l westcentralus -n rgDataMigrationSample

az group deployment create \
  --resource-group rgDataMigrationSample \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/EventHubsDataMigration.json \
  --parameters eventHubNamespaceName=<event-hub-namespace> eventHubName=hubdatamigration sqlServerName=<sql-server-name> sqlServerUserName=<user-name> sqlServerPassword=<password> sqlServerDatabaseName=<database-name> storageName=<unique-storage-name> functionAppName=<app-name>
```

<span data-ttu-id="7b624-142">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="7b624-142">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroup -Name rgDataMigration -Location westcentralus

New-AzureRmResourceGroupDeployment -ResourceGroupName rgDataMigration -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/EventHubsDataMigration.json -eventHubNamespaceName <event-hub-namespace> -eventHubName hubdatamigration -sqlServerName <sql-server-name> -sqlServerUserName <user-name> -sqlServerDatabaseName <database-name> -storageName <unique-storage-name> -functionAppName <app-name>
```

<span data-ttu-id="7b624-143">Provide a password value when prompted.</span><span class="sxs-lookup"><span data-stu-id="7b624-143">Provide a password value when prompted.</span></span>

## <a name="create-a-table-in-sql-data-warehouse"></a><span data-ttu-id="7b624-144">Create a table in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7b624-144">Create a table in SQL Data Warehouse</span></span>

<span data-ttu-id="7b624-145">Add a table to your data warehouse by running the [CreateDataWarehouseTable.sql](https://github.com/Azure/azure-event-hubs/blob/master/samples/e2e/EventHubsCaptureEventGridDemo/scripts/CreateDataWarehouseTable.sql) script.</span><span class="sxs-lookup"><span data-stu-id="7b624-145">Add a table to your data warehouse by running the [CreateDataWarehouseTable.sql](https://github.com/Azure/azure-event-hubs/blob/master/samples/e2e/EventHubsCaptureEventGridDemo/scripts/CreateDataWarehouseTable.sql) script.</span></span> <span data-ttu-id="7b624-146">To run the script, use Visual Studio or the Query Editor in the portal.</span><span class="sxs-lookup"><span data-stu-id="7b624-146">To run the script, use Visual Studio or the Query Editor in the portal.</span></span>

<span data-ttu-id="7b624-147">The script to run is:</span><span class="sxs-lookup"><span data-stu-id="7b624-147">The script to run is:</span></span>

```sql
CREATE TABLE [dbo].[Fact_WindTurbineMetrics] (
    [DeviceId] nvarchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [MeasureTime] datetime NULL, 
    [GeneratedPower] float NULL, 
    [WindSpeed] float NULL, 
    [TurbineSpeed] float NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
```

## <a name="publish-the-azure-functions-app"></a><span data-ttu-id="7b624-148">Publish the Azure Functions app</span><span class="sxs-lookup"><span data-stu-id="7b624-148">Publish the Azure Functions app</span></span>

1. <span data-ttu-id="7b624-149">Open the [EventHubsCaptureEventGridDemo sample project](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) in Visual Studio 2017 (15.3.2 or greater).</span><span class="sxs-lookup"><span data-stu-id="7b624-149">Open the [EventHubsCaptureEventGridDemo sample project](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo) in Visual Studio 2017 (15.3.2 or greater).</span></span>

1. <span data-ttu-id="7b624-150">In Solution Explorer, right-click **FunctionEGDWDumper**, and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7b624-150">In Solution Explorer, right-click **FunctionEGDWDumper**, and select **Publish**.</span></span>

   ![Publish function app](media/event-grid-event-hubs-integration/publish-function-app.png)

1. <span data-ttu-id="7b624-152">Select **Azure Function App** and **Select Existing**.</span><span class="sxs-lookup"><span data-stu-id="7b624-152">Select **Azure Function App** and **Select Existing**.</span></span> <span data-ttu-id="7b624-153">Select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7b624-153">Select **Publish**.</span></span>

   ![Target function app](media/event-grid-event-hubs-integration/pick-target.png)

1. <span data-ttu-id="7b624-155">Select the function app that you deployed through the template.</span><span class="sxs-lookup"><span data-stu-id="7b624-155">Select the function app that you deployed through the template.</span></span> <span data-ttu-id="7b624-156">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b624-156">Select **OK**.</span></span>

   ![Select function app](media/event-grid-event-hubs-integration/select-function-app.png)

1. <span data-ttu-id="7b624-158">When Visual Studio has configured the profile, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7b624-158">When Visual Studio has configured the profile, select **Publish**.</span></span>

   ![Select publish](media/event-grid-event-hubs-integration/select-publish.png)

<span data-ttu-id="7b624-160">After publishing the function, you're ready to subscribe to the event.</span><span class="sxs-lookup"><span data-stu-id="7b624-160">After publishing the function, you're ready to subscribe to the event.</span></span>

## <a name="subscribe-to-the-event"></a><span data-ttu-id="7b624-161">Subscribe to the event</span><span class="sxs-lookup"><span data-stu-id="7b624-161">Subscribe to the event</span></span>

1. <span data-ttu-id="7b624-162">Go to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b624-162">Go to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7b624-163">Select your resource group and function app.</span><span class="sxs-lookup"><span data-stu-id="7b624-163">Select your resource group and function app.</span></span>

   ![View function app](media/event-grid-event-hubs-integration/view-function-app.png)

1. <span data-ttu-id="7b624-165">Select the function.</span><span class="sxs-lookup"><span data-stu-id="7b624-165">Select the function.</span></span>

   ![Select function](media/event-grid-event-hubs-integration/select-function.png)

1. <span data-ttu-id="7b624-167">Select **Add Event Grid subscription**.</span><span class="sxs-lookup"><span data-stu-id="7b624-167">Select **Add Event Grid subscription**.</span></span>

   ![Add subscription](media/event-grid-event-hubs-integration/add-event-grid-subscription.png)

9. <span data-ttu-id="7b624-169">Give the event grid subscription a name.</span><span class="sxs-lookup"><span data-stu-id="7b624-169">Give the event grid subscription a name.</span></span> <span data-ttu-id="7b624-170">Use **Event Hubs Namespaces** as the event type.</span><span class="sxs-lookup"><span data-stu-id="7b624-170">Use **Event Hubs Namespaces** as the event type.</span></span> <span data-ttu-id="7b624-171">Provide values to select your instance of the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="7b624-171">Provide values to select your instance of the Event Hubs namespace.</span></span> <span data-ttu-id="7b624-172">Leave the subscriber endpoint as the provided value.</span><span class="sxs-lookup"><span data-stu-id="7b624-172">Leave the subscriber endpoint as the provided value.</span></span> <span data-ttu-id="7b624-173">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b624-173">Select **Create**.</span></span>

   ![Create subscription](media/event-grid-event-hubs-integration/set-subscription-values.png)

## <a name="run-the-app-to-generate-data"></a><span data-ttu-id="7b624-175">Run the app to generate data</span><span class="sxs-lookup"><span data-stu-id="7b624-175">Run the app to generate data</span></span>

<span data-ttu-id="7b624-176">You've finished setting up your event hub, SQL data warehouse, Azure function app, and event subscription.</span><span class="sxs-lookup"><span data-stu-id="7b624-176">You've finished setting up your event hub, SQL data warehouse, Azure function app, and event subscription.</span></span> <span data-ttu-id="7b624-177">The solution is ready to migrate data from the event hub to the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b624-177">The solution is ready to migrate data from the event hub to the data warehouse.</span></span> <span data-ttu-id="7b624-178">Before running an application that generates data for event hub, you need to configure a few values.</span><span class="sxs-lookup"><span data-stu-id="7b624-178">Before running an application that generates data for event hub, you need to configure a few values.</span></span>

1. <span data-ttu-id="7b624-179">In the portal, select your event hub namespace.</span><span class="sxs-lookup"><span data-stu-id="7b624-179">In the portal, select your event hub namespace.</span></span> <span data-ttu-id="7b624-180">Select **Connection Strings**.</span><span class="sxs-lookup"><span data-stu-id="7b624-180">Select **Connection Strings**.</span></span>

   ![Select connection strings](media/event-grid-event-hubs-integration/event-hub-connection.png)

2. <span data-ttu-id="7b624-182">Select **RootManageSharedAccessKey**</span><span class="sxs-lookup"><span data-stu-id="7b624-182">Select **RootManageSharedAccessKey**</span></span>

   ![Select key](media/event-grid-event-hubs-integration/show-root-key.png)

3. <span data-ttu-id="7b624-184">Copy **Connection string - primary Key**</span><span class="sxs-lookup"><span data-stu-id="7b624-184">Copy **Connection string - primary Key**</span></span>

   ![Copy key](media/event-grid-event-hubs-integration/copy-key.png)

4. <span data-ttu-id="7b624-186">Go back to your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="7b624-186">Go back to your Visual Studio project.</span></span> <span data-ttu-id="7b624-187">In the WindTurbineDataGenerator project, open **program.cs**.</span><span class="sxs-lookup"><span data-stu-id="7b624-187">In the WindTurbineDataGenerator project, open **program.cs**.</span></span>

5. <span data-ttu-id="7b624-188">Replace the two constant values.</span><span class="sxs-lookup"><span data-stu-id="7b624-188">Replace the two constant values.</span></span> <span data-ttu-id="7b624-189">Use the copied value for **EventHubConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="7b624-189">Use the copied value for **EventHubConnectionString**.</span></span> <span data-ttu-id="7b624-190">Use **hubdatamigration** the event hub name.</span><span class="sxs-lookup"><span data-stu-id="7b624-190">Use **hubdatamigration** the event hub name.</span></span>

   ```cs
   private const string EventHubConnectionString = "Endpoint=sb://demomigrationnamespace.servicebus.windows.net/...";
   private const string EventHubName = "hubdatamigration";
   ```

6. <span data-ttu-id="7b624-191">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="7b624-191">Build the solution.</span></span> <span data-ttu-id="7b624-192">Run the WindTurbineGenerator.exe application.</span><span class="sxs-lookup"><span data-stu-id="7b624-192">Run the WindTurbineGenerator.exe application.</span></span> <span data-ttu-id="7b624-193">After a couple of minutes, query the table in your data warehouse for the migrated data.</span><span class="sxs-lookup"><span data-stu-id="7b624-193">After a couple of minutes, query the table in your data warehouse for the migrated data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b624-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b624-194">Next steps</span></span>

* <span data-ttu-id="7b624-195">To learn about differences in the Azure messaging services, see [Choose between Azure services that deliver messages](compare-messaging-services.md).</span><span class="sxs-lookup"><span data-stu-id="7b624-195">To learn about differences in the Azure messaging services, see [Choose between Azure services that deliver messages](compare-messaging-services.md).</span></span>
* <span data-ttu-id="7b624-196">For an introduction to Event Grid, see [About Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b624-196">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="7b624-197">For an introduction to Event Hubs Capture, see [Enable Event Hubs Capture using the Azure portal](../event-hubs/event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b624-197">For an introduction to Event Hubs Capture, see [Enable Event Hubs Capture using the Azure portal](../event-hubs/event-hubs-capture-enable-through-portal.md).</span></span>
* <span data-ttu-id="7b624-198">For more information about setting up and running the sample, see [Event Hubs Capture and Event Grid sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo).</span><span class="sxs-lookup"><span data-stu-id="7b624-198">For more information about setting up and running the sample, see [Event Hubs Capture and Event Grid sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/e2e/EventHubsCaptureEventGridDemo).</span></span>