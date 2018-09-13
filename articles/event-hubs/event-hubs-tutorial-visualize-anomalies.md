---
title: Visualize data anomalies in real-time events sent to Azure Event Hubs | Microsoft Docs
description: Tutorial - Visualize data anomalies in real-time events sent to Microsoft Azure Event Hubs
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
ms.author: shvija
ms.date: 08/08/2018
ms.topic: tutorial
ms.service: event-hubs
ms.custom: mvc
ms.openlocfilehash: 04a9a3b3df44814d680f01595d70ced08a946591
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968922"
---
# <a name="tutorial-visualize-data-anomalies-in-real-time-events-sent-to-azure-event-hubs"></a><span data-ttu-id="8fae1-103">Tutorial: Visualize data anomalies in real-time events sent to Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8fae1-103">Tutorial: Visualize data anomalies in real-time events sent to Azure Event Hubs</span></span>

<span data-ttu-id="8fae1-104">With Azure Event Hubs, you can use Azure Stream Analytics to check the incoming data and pull out the anomalies, which you can then visualize in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8fae1-104">With Azure Event Hubs, you can use Azure Stream Analytics to check the incoming data and pull out the anomalies, which you can then visualize in Power BI.</span></span> <span data-ttu-id="8fae1-105">Let's say you have thousands of devices constantly sending real-time data to an event hub, adding up to millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="8fae1-105">Let's say you have thousands of devices constantly sending real-time data to an event hub, adding up to millions of events per second.</span></span> <span data-ttu-id="8fae1-106">How do you check that much data for anomalies, or errors, in the data?</span><span class="sxs-lookup"><span data-stu-id="8fae1-106">How do you check that much data for anomalies, or errors, in the data?</span></span> <span data-ttu-id="8fae1-107">For example, what if the devices are sending credit card transactions, and you need to capture anywhere you have multiple transactions in multiple countries within a 5-second time interval?</span><span class="sxs-lookup"><span data-stu-id="8fae1-107">For example, what if the devices are sending credit card transactions, and you need to capture anywhere you have multiple transactions in multiple countries within a 5-second time interval?</span></span> <span data-ttu-id="8fae1-108">This could happen if someone steals credit cards and then uses them to purchase items around the globe at the same time.</span><span class="sxs-lookup"><span data-stu-id="8fae1-108">This could happen if someone steals credit cards and then uses them to purchase items around the globe at the same time.</span></span> 

<span data-ttu-id="8fae1-109">In this tutorial, you simulate this example.</span><span class="sxs-lookup"><span data-stu-id="8fae1-109">In this tutorial, you simulate this example.</span></span> <span data-ttu-id="8fae1-110">You run an application that creates and sends credit card transactions to an event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-110">You run an application that creates and sends credit card transactions to an event hub.</span></span> <span data-ttu-id="8fae1-111">Then you read the stream of data in real-time with Azure Stream Analytics, which separates the valid transactions from the invalid transactions, and then use Power BI to visually identify the transactions that are tagged as invalid.</span><span class="sxs-lookup"><span data-stu-id="8fae1-111">Then you read the stream of data in real-time with Azure Stream Analytics, which separates the valid transactions from the invalid transactions, and then use Power BI to visually identify the transactions that are tagged as invalid.</span></span>

<span data-ttu-id="8fae1-112">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="8fae1-112">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8fae1-113">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="8fae1-113">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="8fae1-114">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="8fae1-114">Create an event hub</span></span>
> * <span data-ttu-id="8fae1-115">Run the app that sends credit card transactions</span><span class="sxs-lookup"><span data-stu-id="8fae1-115">Run the app that sends credit card transactions</span></span>
> * <span data-ttu-id="8fae1-116">Configure a Stream Analytics job to process those transactions</span><span class="sxs-lookup"><span data-stu-id="8fae1-116">Configure a Stream Analytics job to process those transactions</span></span>
> * <span data-ttu-id="8fae1-117">Configure a Power BI visualization to show the results</span><span class="sxs-lookup"><span data-stu-id="8fae1-117">Configure a Power BI visualization to show the results</span></span>

<span data-ttu-id="8fae1-118">To complete this tutorial, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8fae1-118">To complete this tutorial, you need an Azure subscription.</span></span> <span data-ttu-id="8fae1-119">If you don't have one, [create a free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="8fae1-119">If you don't have one, [create a free account][] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fae1-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8fae1-120">Prerequisites</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

- <span data-ttu-id="8fae1-121">Install [Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8fae1-121">Install [Visual Studio](https://www.visualstudio.com/).</span></span> 
- <span data-ttu-id="8fae1-122">You need a Power BI account to analyze output from a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="8fae1-122">You need a Power BI account to analyze output from a Stream Analytics job.</span></span> <span data-ttu-id="8fae1-123">You can [try Power BI for free](https://app.powerbi.com/signupredirect?pbi_source=web).</span><span class="sxs-lookup"><span data-stu-id="8fae1-123">You can [try Power BI for free](https://app.powerbi.com/signupredirect?pbi_source=web).</span></span>

## <a name="set-up-resources"></a><span data-ttu-id="8fae1-124">Set up resources</span><span class="sxs-lookup"><span data-stu-id="8fae1-124">Set up resources</span></span>

<span data-ttu-id="8fae1-125">For this tutorial, you need an Event Hubs namespace and an event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-125">For this tutorial, you need an Event Hubs namespace and an event hub.</span></span> <span data-ttu-id="8fae1-126">You can create these resources using Azure CLI or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fae1-126">You can create these resources using Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="8fae1-127">Use the same resource group and location for all of the resources.</span><span class="sxs-lookup"><span data-stu-id="8fae1-127">Use the same resource group and location for all of the resources.</span></span> <span data-ttu-id="8fae1-128">Then at the end, you can remove everything in one step by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="8fae1-128">Then at the end, you can remove everything in one step by deleting the resource group.</span></span>

<span data-ttu-id="8fae1-129">The following sections describe how to perform these required steps.</span><span class="sxs-lookup"><span data-stu-id="8fae1-129">The following sections describe how to perform these required steps.</span></span> <span data-ttu-id="8fae1-130">Follow the CLI *or* the PowerShell instructions to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8fae1-130">Follow the CLI *or* the PowerShell instructions to perform the following steps:</span></span>

1. <span data-ttu-id="8fae1-131">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fae1-131">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span></span> 

2. <span data-ttu-id="8fae1-132">Create an Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="8fae1-132">Create an Event Hubs namespace.</span></span> 

3. <span data-ttu-id="8fae1-133">Create an event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-133">Create an event hub.</span></span>

> [!NOTE]
> <span data-ttu-id="8fae1-134">There are variables set in each script that you need later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="8fae1-134">There are variables set in each script that you need later in the tutorial.</span></span> <span data-ttu-id="8fae1-135">These include resource group name ($resourceGroup), event hub namespace (**$eventHubNamespace**), and event hub name (**$eventHubName**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-135">These include resource group name ($resourceGroup), event hub namespace (**$eventHubNamespace**), and event hub name (**$eventHubName**).</span></span> <span data-ttu-id="8fae1-136">These are referred to with their dollar sign ($) prefixes later in this article, so you know they were set in the script.</span><span class="sxs-lookup"><span data-stu-id="8fae1-136">These are referred to with their dollar sign ($) prefixes later in this article, so you know they were set in the script.</span></span>

<!-- some day they will approve the tab control; 
  When that happens, put CLI and PSH in tabs. -->

### <a name="set-up-your-resources-using-azure-cli"></a><span data-ttu-id="8fae1-137">Set up your resources using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fae1-137">Set up your resources using Azure CLI</span></span>

<span data-ttu-id="8fae1-138">Copy and paste this script into Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8fae1-138">Copy and paste this script into Cloud Shell.</span></span> <span data-ttu-id="8fae1-139">Assuming you are already logged in, it runs the script one line at a time.</span><span class="sxs-lookup"><span data-stu-id="8fae1-139">Assuming you are already logged in, it runs the script one line at a time.</span></span>

<span data-ttu-id="8fae1-140">The variables that must be globally unique have `$RANDOM` concatenated to them.</span><span class="sxs-lookup"><span data-stu-id="8fae1-140">The variables that must be globally unique have `$RANDOM` concatenated to them.</span></span> <span data-ttu-id="8fae1-141">When the script is run and the variables are set, a random numeric string is generated and concatenated to the end of the fixed string, making it unique.</span><span class="sxs-lookup"><span data-stu-id="8fae1-141">When the script is run and the variables are set, a random numeric string is generated and concatenated to the end of the fixed string, making it unique.</span></span>

```azurecli-interactive
# Set the values for location and resource group name.
location=westus
resourceGroup=ContosoResourcesEH

# Create the resource group to be used
#   for all the resources for this tutorial.
az group create --name $resourceGroup \
    --location $location

# The Event Hubs namespace name must be globally unique, so add a random number to the end.
eventHubNamespace=ContosoEHNamespace$RANDOM
echo "Event Hub Namespace = " $eventHubNamespace

# Create the Event Hubs namespace.
az eventhubs namespace create --resource-group $resourceGroup \
   --name $eventHubNamespace \
   --location $location \
   --sku Standard

# The event hub name must be globally unique, so add a random number to the end.
eventHubName=ContosoEHhub$RANDOM
echo "event hub name = " $eventHubName

# Create the event hub.
az eventhubs eventhub create --resource-group $resourceGroup \
    --namespace-name $eventHubNamespace \
    --name $eventHubName \
    --message-retention 3 \
    --partition-count 2

# Get the connection string that authenticates the app with the Event Hubs service.
connectionString=$(az eventhubs namespace authorization-rule keys list \
   --resource-group $resourceGroup \
   --namespace-name $eventHubNamespace \
   --name RootManageSharedAccessKey \
   --query primaryConnectionString \
   --output tsv)
echo "Connection string = " $connectionString 
```

### <a name="set-up-your-resources-using-azure-powershell"></a><span data-ttu-id="8fae1-142">Set up your resources using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fae1-142">Set up your resources using Azure PowerShell</span></span>

<span data-ttu-id="8fae1-143">Copy and paste this script into Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8fae1-143">Copy and paste this script into Cloud Shell.</span></span> <span data-ttu-id="8fae1-144">Assuming you are already logged in, it runs the script one line at a time.</span><span class="sxs-lookup"><span data-stu-id="8fae1-144">Assuming you are already logged in, it runs the script one line at a time.</span></span>

<span data-ttu-id="8fae1-145">The variables that must be globally unique have `$(Get-Random)` concatenated to them.</span><span class="sxs-lookup"><span data-stu-id="8fae1-145">The variables that must be globally unique have `$(Get-Random)` concatenated to them.</span></span> <span data-ttu-id="8fae1-146">When the script is run and the variables are set, a random numeric string is generated and concatenated to the end of the fixed string, making it unique.</span><span class="sxs-lookup"><span data-stu-id="8fae1-146">When the script is run and the variables are set, a random numeric string is generated and concatenated to the end of the fixed string, making it unique.</span></span>

```azurepowershell-interactive
# Log in to Azure account.
Login-AzureRMAccount

# Set the values for the location and resource group.
$location = "West US"
$resourceGroup = "ContosoResourcesEH"

# Create the resource group to be used  
#   for all resources for this tutorial.
New-AzureRmResourceGroup -Name $resourceGroup -Location $location

# The Event Hubs namespace name must be globally unique, so add a random number to the end.
$eventHubNamespace = "contosoEHNamespace$(Get-Random)"
Write-Host "Event Hub Namespace is " $eventHubNamespace

# The event hub name must be globally unique, so add a random number to the end.
$eventHubName = "contosoEHhub$(Get-Random)"
Write-Host "Event hub Name is " $eventHubName

# Create the Event Hubs namespace.
New-AzureRmEventHubNamespace -ResourceGroupName $resourceGroup `
     -NamespaceName $eventHubNamespace `
     -Location $location

# Create the event hub.
$yourEventHub = New-AzureRmEventHub -ResourceGroupName $resourceGroup `
    -NamespaceName $eventHubNamespace `
    -Name $eventHubName `
    -MessageRetentionInDays 3 `
    -PartitionCount 2

# Get the event hub key, and retrieve the connection string from that object.
# You need this to run the app that sends test messages to the event hub.
$eventHubKey = Get-AzureRmEventHubKey -ResourceGroupName $resourceGroup `
    -Namespace $eventHubNamespace `
    -AuthorizationRuleName RootManageSharedAccessKey

# Save this value somewhere local for later use.
Write-Host "Connection string is " $eventHubKey.PrimaryConnectionString
```

## <a name="run-app-to-produce-test-event-data"></a><span data-ttu-id="8fae1-147">Run app to produce test event data</span><span class="sxs-lookup"><span data-stu-id="8fae1-147">Run app to produce test event data</span></span>

<span data-ttu-id="8fae1-148">The Event Hubs [samples on GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet) include an [anomaly detector app](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/AnomalyDetector) that produces test data for you.</span><span class="sxs-lookup"><span data-stu-id="8fae1-148">The Event Hubs [samples on GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet) include an [anomaly detector app](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/AnomalyDetector) that produces test data for you.</span></span> <span data-ttu-id="8fae1-149">It simulates the use of credit cards by writing credit card transactions to the event hub, including occasionally writing several transactions for the same credit card in multiple locations so that they are tagged as anomalies.</span><span class="sxs-lookup"><span data-stu-id="8fae1-149">It simulates the use of credit cards by writing credit card transactions to the event hub, including occasionally writing several transactions for the same credit card in multiple locations so that they are tagged as anomalies.</span></span> <span data-ttu-id="8fae1-150">To run this app, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8fae1-150">To run this app, follow these steps:</span></span> 

1. <span data-ttu-id="8fae1-151">Download the [Azure Event Hubs samples](https://github.com/Azure/azure-event-hubs/archive/master.zip) from GitHub and unzip it locally.</span><span class="sxs-lookup"><span data-stu-id="8fae1-151">Download the [Azure Event Hubs samples](https://github.com/Azure/azure-event-hubs/archive/master.zip) from GitHub and unzip it locally.</span></span>

2. <span data-ttu-id="8fae1-152">Go to the folder \azure-event-hubs-master\samples\DotNet\AnomalyDetector\ and double-click on AnomalyDetector.sln to open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fae1-152">Go to the folder \azure-event-hubs-master\samples\DotNet\AnomalyDetector\ and double-click on AnomalyDetector.sln to open the solution in Visual Studio.</span></span> 

3. <span data-ttu-id="8fae1-153">Open Program.cs and replace **Event Hubs connection string** with the connection string you saved when running the script.</span><span class="sxs-lookup"><span data-stu-id="8fae1-153">Open Program.cs and replace **Event Hubs connection string** with the connection string you saved when running the script.</span></span> 

4. <span data-ttu-id="8fae1-154">Replace **Event Hub name** with your event hub name.</span><span class="sxs-lookup"><span data-stu-id="8fae1-154">Replace **Event Hub name** with your event hub name.</span></span> <span data-ttu-id="8fae1-155">Click F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="8fae1-155">Click F5 to run the application.</span></span> <span data-ttu-id="8fae1-156">It starts sending events to your event hub, and continues until it has sent 1000 events.</span><span class="sxs-lookup"><span data-stu-id="8fae1-156">It starts sending events to your event hub, and continues until it has sent 1000 events.</span></span> <span data-ttu-id="8fae1-157">There are a few instances where the app needs to be running for you to retrieve data.</span><span class="sxs-lookup"><span data-stu-id="8fae1-157">There are a few instances where the app needs to be running for you to retrieve data.</span></span> <span data-ttu-id="8fae1-158">These cases are pointed out in the following instructions, where needed.</span><span class="sxs-lookup"><span data-stu-id="8fae1-158">These cases are pointed out in the following instructions, where needed.</span></span>

## <a name="set-up-azure-stream-analytics"></a><span data-ttu-id="8fae1-159">Set up Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8fae1-159">Set up Azure Stream Analytics</span></span>

<span data-ttu-id="8fae1-160">Now you can stream data into your event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-160">Now you can stream data into your event hub.</span></span> <span data-ttu-id="8fae1-161">To use that data in a Power BI visualization, start by setting up a Stream Analytics job to retrieve the data that is then fed into the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="8fae1-161">To use that data in a Power BI visualization, start by setting up a Stream Analytics job to retrieve the data that is then fed into the Power BI visualization.</span></span>

### <a name="create-the-stream-analytics-job"></a><span data-ttu-id="8fae1-162">Create the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-162">Create the Stream Analytics job</span></span>

1. <span data-ttu-id="8fae1-163">In the Azure portal, click **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-163">In the Azure portal, click **Create a resource**.</span></span> <span data-ttu-id="8fae1-164">Type **stream analytics** into the search box and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-164">Type **stream analytics** into the search box and press **Enter**.</span></span> <span data-ttu-id="8fae1-165">Select **Stream Analytics Job**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-165">Select **Stream Analytics Job**.</span></span> <span data-ttu-id="8fae1-166">Click **Create** on the Stream Analytics job pane.</span><span class="sxs-lookup"><span data-stu-id="8fae1-166">Click **Create** on the Stream Analytics job pane.</span></span> 

2. <span data-ttu-id="8fae1-167">Enter the following information for the job:</span><span class="sxs-lookup"><span data-stu-id="8fae1-167">Enter the following information for the job:</span></span>

   <span data-ttu-id="8fae1-168">**Job name**: Use **contosoEHjob**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-168">**Job name**: Use **contosoEHjob**.</span></span> <span data-ttu-id="8fae1-169">This field is the name of the job and it must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="8fae1-169">This field is the name of the job and it must be globally unique.</span></span>

   <span data-ttu-id="8fae1-170">**Subscription**: Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8fae1-170">**Subscription**: Select your subscription.</span></span>

   <span data-ttu-id="8fae1-171">**Resource group**: Use the same resource group used by your event hub (**ContosoResourcesEH**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-171">**Resource group**: Use the same resource group used by your event hub (**ContosoResourcesEH**).</span></span>

   <span data-ttu-id="8fae1-172">**Location**: Use the same location used in the setup script (**West US**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-172">**Location**: Use the same location used in the setup script (**West US**).</span></span>

   ![Screenshot showing how to create a new Azure Stream Analytics job.](./media/event-hubs-tutorial-visualize-anomalies/stream-analytics-add-job.png)

    <span data-ttu-id="8fae1-174">Accept the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="8fae1-174">Accept the defaults for the rest of the fields.</span></span> <span data-ttu-id="8fae1-175">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-175">Click **Create**.</span></span> 

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="8fae1-176">Add an input to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-176">Add an input to the Stream Analytics job</span></span>

<span data-ttu-id="8fae1-177">If you're not in the portal at the **Stream Analytics Job** pane, you can get back to your Stream Analytics job by clicking **Resource Groups** in the portal, then selecting your resource group (**ContosoResourcesEH**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-177">If you're not in the portal at the **Stream Analytics Job** pane, you can get back to your Stream Analytics job by clicking **Resource Groups** in the portal, then selecting your resource group (**ContosoResourcesEH**).</span></span> <span data-ttu-id="8fae1-178">This action shows all of the resources in the group, and you can then select your stream analytics job.</span><span class="sxs-lookup"><span data-stu-id="8fae1-178">This action shows all of the resources in the group, and you can then select your stream analytics job.</span></span> 

<span data-ttu-id="8fae1-179">The inputs for the Steam Analytics job are the credit card transactions from the event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-179">The inputs for the Steam Analytics job are the credit card transactions from the event hub.</span></span>

> [!NOTE]
> <span data-ttu-id="8fae1-180">The values for variables starting with the dollar sign ($) are set in the startup scripts in the previous sections.</span><span class="sxs-lookup"><span data-stu-id="8fae1-180">The values for variables starting with the dollar sign ($) are set in the startup scripts in the previous sections.</span></span> <span data-ttu-id="8fae1-181">You must use the same values here when specifying those fields, which are the Event Hubs namespace and event hub name.</span><span class="sxs-lookup"><span data-stu-id="8fae1-181">You must use the same values here when specifying those fields, which are the Event Hubs namespace and event hub name.</span></span>

1. <span data-ttu-id="8fae1-182">Under **Job Topology**, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-182">Under **Job Topology**, click **Inputs**.</span></span>

2. <span data-ttu-id="8fae1-183">In the **Inputs** pane, click **Add stream input** and select Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8fae1-183">In the **Inputs** pane, click **Add stream input** and select Event Hubs.</span></span> <span data-ttu-id="8fae1-184">On the screen that appears, fill in the following fields:</span><span class="sxs-lookup"><span data-stu-id="8fae1-184">On the screen that appears, fill in the following fields:</span></span>

   <span data-ttu-id="8fae1-185">**Input alias**: Use **contosoinputs**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-185">**Input alias**: Use **contosoinputs**.</span></span> <span data-ttu-id="8fae1-186">This field is the name of the input stream, used when defining the query for the data.</span><span class="sxs-lookup"><span data-stu-id="8fae1-186">This field is the name of the input stream, used when defining the query for the data.</span></span>

   <span data-ttu-id="8fae1-187">**Subscription**: Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8fae1-187">**Subscription**: Select your subscription.</span></span>

   <span data-ttu-id="8fae1-188">**Event Hubs namespace**: Select your Event Hub namespace ($**eventHubNamespace**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-188">**Event Hubs namespace**: Select your Event Hub namespace ($**eventHubNamespace**).</span></span> 

   <span data-ttu-id="8fae1-189">**Event Hub name**: Click **Use existing** and select your event hub ($**eventHubName**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-189">**Event Hub name**: Click **Use existing** and select your event hub ($**eventHubName**).</span></span>

   <span data-ttu-id="8fae1-190">**Event Hubs policy name**: Select **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-190">**Event Hubs policy name**: Select **RootManageSharedAccessKey**.</span></span>

   <span data-ttu-id="8fae1-191">**Event Hubs consumer group**: Leave this field blank to use the default consumer group.</span><span class="sxs-lookup"><span data-stu-id="8fae1-191">**Event Hubs consumer group**: Leave this field blank to use the default consumer group.</span></span>

   <span data-ttu-id="8fae1-192">Accept the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="8fae1-192">Accept the defaults for the rest of the fields.</span></span>

   ![Screenshot showing how to add an input stream to the Stream Analytics job.](./media/event-hubs-tutorial-visualize-anomalies/stream-analytics-inputs.png)

5. <span data-ttu-id="8fae1-194">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-194">Click **Save**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="8fae1-195">Add an output to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-195">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="8fae1-196">Under **Job Topology**, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-196">Under **Job Topology**, click **Outputs**.</span></span> <span data-ttu-id="8fae1-197">This field is the name of the output stream, used when defining the query for the data.</span><span class="sxs-lookup"><span data-stu-id="8fae1-197">This field is the name of the output stream, used when defining the query for the data.</span></span>

2. <span data-ttu-id="8fae1-198">In the **Outputs** pane, click **Add**, and then select **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-198">In the **Outputs** pane, click **Add**, and then select **Power BI**.</span></span> <span data-ttu-id="8fae1-199">On the screen that appears, complete the following fields:</span><span class="sxs-lookup"><span data-stu-id="8fae1-199">On the screen that appears, complete the following fields:</span></span>

   <span data-ttu-id="8fae1-200">**Output alias**: Use **contosooutputs**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-200">**Output alias**: Use **contosooutputs**.</span></span> <span data-ttu-id="8fae1-201">This field is the unique alias for the output.</span><span class="sxs-lookup"><span data-stu-id="8fae1-201">This field is the unique alias for the output.</span></span> 

   <span data-ttu-id="8fae1-202">**Dataset name**: Use **contosoehdataset**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-202">**Dataset name**: Use **contosoehdataset**.</span></span> <span data-ttu-id="8fae1-203">This field is the name of the dataset to be used in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8fae1-203">This field is the name of the dataset to be used in Power BI.</span></span> 

   <span data-ttu-id="8fae1-204">**Table name**: Use **contosoehtable**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-204">**Table name**: Use **contosoehtable**.</span></span> <span data-ttu-id="8fae1-205">This field is the name of the table to be used in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8fae1-205">This field is the name of the table to be used in Power BI.</span></span> 

   <span data-ttu-id="8fae1-206">Accept the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="8fae1-206">Accept the defaults for the rest of the fields.</span></span>

   ![Screenshot showing how to set up the output for a Stream Analytics job.](./media/event-hubs-tutorial-visualize-anomalies/stream-analytics-outputs.png)

3. <span data-ttu-id="8fae1-208">Click **Authorize**, and sign in to your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="8fae1-208">Click **Authorize**, and sign in to your Power BI account.</span></span>

4. <span data-ttu-id="8fae1-209">Accept the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="8fae1-209">Accept the defaults for the rest of the fields.</span></span>

5. <span data-ttu-id="8fae1-210">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-210">Click **Save**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="8fae1-211">Configure the query of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-211">Configure the query of the Stream Analytics job</span></span>

<span data-ttu-id="8fae1-212">This query is used to retrieve the data that is ultimately sent to the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="8fae1-212">This query is used to retrieve the data that is ultimately sent to the Power BI visualization.</span></span> <span data-ttu-id="8fae1-213">It uses **contosoinputs** and **contosooutputs**, which you previously defined when setting up the job.</span><span class="sxs-lookup"><span data-stu-id="8fae1-213">It uses **contosoinputs** and **contosooutputs**, which you previously defined when setting up the job.</span></span> <span data-ttu-id="8fae1-214">This query retrieves the credit card transactions that it deems fraudulent, which are transactions in which the same credit card number has multiple transactions in different locations in the same five-second interval.</span><span class="sxs-lookup"><span data-stu-id="8fae1-214">This query retrieves the credit card transactions that it deems fraudulent, which are transactions in which the same credit card number has multiple transactions in different locations in the same five-second interval.</span></span>

1. <span data-ttu-id="8fae1-215">Under **Job Topology**, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-215">Under **Job Topology**, click **Query**.</span></span>

2. <span data-ttu-id="8fae1-216">Replace the query with the following one:</span><span class="sxs-lookup"><span data-stu-id="8fae1-216">Replace the query with the following one:</span></span> 

   ```SQL
   /* criteria for fraud:
      credit card purchases with the same card
      in different locations within 5 seconds
   */
   SELECT System.Timestamp AS WindowEnd, 
     COUNT(*) as FraudulentUses      
   INTO contosooutputs
   FROM contosoinputs CS1 TIMESTAMP BY [Timestamp]
       JOIN contosoinputs CS2 TIMESTAMP BY [Timestamp]
       /* where the credit card # is the same */
       ON CS1.CreditCardId = CS2.CreditCardId
       /* and time between the two is between 0 and 5 seconds */
       AND DATEDIFF(second, CS1, CS2) BETWEEN 0 AND 5
       /* where the location is different */
   WHERE CS1.Location != CS2.Location
   GROUP BY TumblingWindow(Duration(second, 1))
   ```

4. <span data-ttu-id="8fae1-217">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-217">Click **Save**.</span></span>

### <a name="test-the-query-for-the-stream-analytics-job"></a><span data-ttu-id="8fae1-218">Test the query for the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-218">Test the query for the Stream Analytics job</span></span> 

1. <span data-ttu-id="8fae1-219">Run the Anomaly Detector app to send data to the event hub while you're setting up and running the test.</span><span class="sxs-lookup"><span data-stu-id="8fae1-219">Run the Anomaly Detector app to send data to the event hub while you're setting up and running the test.</span></span> 

2. <span data-ttu-id="8fae1-220">In the Query pane, click the dots next to the **contosoinputs** input, and then select **Sample data from input**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-220">In the Query pane, click the dots next to the **contosoinputs** input, and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="8fae1-221">Specify that you want three minutes of data, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-221">Specify that you want three minutes of data, then click **OK**.</span></span> <span data-ttu-id="8fae1-222">Wait until you're notified that the data has been sampled.</span><span class="sxs-lookup"><span data-stu-id="8fae1-222">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="8fae1-223">Click **Test** and make sure you're getting results.</span><span class="sxs-lookup"><span data-stu-id="8fae1-223">Click **Test** and make sure you're getting results.</span></span> <span data-ttu-id="8fae1-224">Results are displayed in the **Results** section of the bottom pane on the right under the query.</span><span class="sxs-lookup"><span data-stu-id="8fae1-224">Results are displayed in the **Results** section of the bottom pane on the right under the query.</span></span>

5. <span data-ttu-id="8fae1-225">Close the Query pane.</span><span class="sxs-lookup"><span data-stu-id="8fae1-225">Close the Query pane.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="8fae1-226">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="8fae1-226">Run the Stream Analytics job</span></span>

<span data-ttu-id="8fae1-227">In the Stream Analytics job, click **Start**, then **Now**, then **Start**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-227">In the Stream Analytics job, click **Start**, then **Now**, then **Start**.</span></span> <span data-ttu-id="8fae1-228">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-228">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

## <a name="set-up-the-power-bi-visualizations"></a><span data-ttu-id="8fae1-229">Set up the Power BI visualizations</span><span class="sxs-lookup"><span data-stu-id="8fae1-229">Set up the Power BI visualizations</span></span>

1. <span data-ttu-id="8fae1-230">Run the Anomaly Detector app to send data to the event hub while you're setting up the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="8fae1-230">Run the Anomaly Detector app to send data to the event hub while you're setting up the Power BI visualization.</span></span> <span data-ttu-id="8fae1-231">You may need to run it multiple times, as it only generates 1000 transactions each time it runs.</span><span class="sxs-lookup"><span data-stu-id="8fae1-231">You may need to run it multiple times, as it only generates 1000 transactions each time it runs.</span></span>

2. <span data-ttu-id="8fae1-232">Sign in to your [Power BI](https://powerbi.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="8fae1-232">Sign in to your [Power BI](https://powerbi.microsoft.com/) account.</span></span>

3. <span data-ttu-id="8fae1-233">Go to **My Workspace**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-233">Go to **My Workspace**.</span></span>

4. <span data-ttu-id="8fae1-234">Click **Datasets**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-234">Click **Datasets**.</span></span>

   <span data-ttu-id="8fae1-235">You should see the dataset that you specified when you created the output for the Stream Analytics job (**contosoehdataset**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-235">You should see the dataset that you specified when you created the output for the Stream Analytics job (**contosoehdataset**).</span></span> <span data-ttu-id="8fae1-236">It may take 5-10 minutes for the dataset to appear for the first time.</span><span class="sxs-lookup"><span data-stu-id="8fae1-236">It may take 5-10 minutes for the dataset to appear for the first time.</span></span>

5. <span data-ttu-id="8fae1-237">Click **Dashboards**, then click **Create** and select **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-237">Click **Dashboards**, then click **Create** and select **Dashboard**.</span></span>

   ![Screenshot of the Dashboards and Create buttons.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-add-dashboard.png)

6. <span data-ttu-id="8fae1-239">Specify the name of the dashboard, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-239">Specify the name of the dashboard, then click **Create**.</span></span> <span data-ttu-id="8fae1-240">Use **Credit Card Anomalies**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-240">Use **Credit Card Anomalies**.</span></span>

   ![Screenshot of specifying dashboard name.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-dashboard-name.png)

7. <span data-ttu-id="8fae1-242">On the Dashboard page, click **Add tile**, select **Custom Streaming Data** in the **REAL - TIME DATA** section, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-242">On the Dashboard page, click **Add tile**, select **Custom Streaming Data** in the **REAL - TIME DATA** section, then click **Next**.</span></span>

   ![Screenshot specifying source for tile.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-add-card-real-time-data.png)

8. <span data-ttu-id="8fae1-244">Select your dataset (**contosoehdataset**) and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-244">Select your dataset (**contosoehdataset**) and click **Next**.</span></span>

   ![Screenshot specifying dataset.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-dashboard-select-dataset.png)

9. <span data-ttu-id="8fae1-246">Select **Card** for visualization type.</span><span class="sxs-lookup"><span data-stu-id="8fae1-246">Select **Card** for visualization type.</span></span> <span data-ttu-id="8fae1-247">Under **Fields**, click **Add value**, then select **fraudulentuses**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-247">Under **Fields**, click **Add value**, then select **fraudulentuses**.</span></span>

   ![Screenshot specifying visualization type and fields.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-add-card-tile.png)

   <span data-ttu-id="8fae1-249">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-249">Click **Next**.</span></span>

10. <span data-ttu-id="8fae1-250">Set the title to **Fraudulent uses** and the subtitle to **Sum in last few minutes**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-250">Set the title to **Fraudulent uses** and the subtitle to **Sum in last few minutes**.</span></span> <span data-ttu-id="8fae1-251">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-251">Click **Apply**.</span></span> <span data-ttu-id="8fae1-252">It saves the tile to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fae1-252">It saves the tile to your dashboard.</span></span>

    ![Screenshot specifying title and subtitle for dashboard tile.](./media/event-hubs-tutorial-visualize-anomalies/power-bi-tile-details.png)

11. <span data-ttu-id="8fae1-254">Add another visualization.</span><span class="sxs-lookup"><span data-stu-id="8fae1-254">Add another visualization.</span></span> <span data-ttu-id="8fae1-255">Repeat the first few steps again:</span><span class="sxs-lookup"><span data-stu-id="8fae1-255">Repeat the first few steps again:</span></span>

   * <span data-ttu-id="8fae1-256">Click **Add Tile**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-256">Click **Add Tile**.</span></span>
   * <span data-ttu-id="8fae1-257">Select **Custom Streaming Data**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-257">Select **Custom Streaming Data**.</span></span> 
   * <span data-ttu-id="8fae1-258">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-258">Click **Next**.</span></span>
   * <span data-ttu-id="8fae1-259">Select your dataset and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-259">Select your dataset and then click **Next**.</span></span> 

12. <span data-ttu-id="8fae1-260">Under **Visualization Type**, select **Line chart**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-260">Under **Visualization Type**, select **Line chart**.</span></span>

13. <span data-ttu-id="8fae1-261">Under **Axis**, click **Add Value**, and select **windowend**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-261">Under **Axis**, click **Add Value**, and select **windowend**.</span></span> 

14. <span data-ttu-id="8fae1-262">Under **Values**, click **Add value** and select **fraudulentuses**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-262">Under **Values**, click **Add value** and select **fraudulentuses**.</span></span>

15. <span data-ttu-id="8fae1-263">Under **Time window to display**, select the last five minutes.</span><span class="sxs-lookup"><span data-stu-id="8fae1-263">Under **Time window to display**, select the last five minutes.</span></span> <span data-ttu-id="8fae1-264">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-264">Click **Next**.</span></span>

16. <span data-ttu-id="8fae1-265">Specify **Show fraudulent uses over time** for the title and leave the subtitle for the tile blank, then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-265">Specify **Show fraudulent uses over time** for the title and leave the subtitle for the tile blank, then click **Apply**.</span></span> <span data-ttu-id="8fae1-266">You are returned to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="8fae1-266">You are returned to your dashboard.</span></span>

17. <span data-ttu-id="8fae1-267">Run the Anomaly Detector app again to send some data to the event hub.</span><span class="sxs-lookup"><span data-stu-id="8fae1-267">Run the Anomaly Detector app again to send some data to the event hub.</span></span> <span data-ttu-id="8fae1-268">You see the **Fraudulent uses** tile change as it analyzes the data, and the line chart shows data.</span><span class="sxs-lookup"><span data-stu-id="8fae1-268">You see the **Fraudulent uses** tile change as it analyzes the data, and the line chart shows data.</span></span> 

    ![Screenshot showing the Power BI results](./media/event-hubs-tutorial-visualize-anomalies/power-bi-results.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8fae1-270">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8fae1-270">Clean up resources</span></span>

<span data-ttu-id="8fae1-271">If you want to remove all of the resources you've created, remove the Power BI visualization data, then delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="8fae1-271">If you want to remove all of the resources you've created, remove the Power BI visualization data, then delete the resource group.</span></span> <span data-ttu-id="8fae1-272">Deleting the resource group deletes all resources contained within the group.</span><span class="sxs-lookup"><span data-stu-id="8fae1-272">Deleting the resource group deletes all resources contained within the group.</span></span> <span data-ttu-id="8fae1-273">In this case, it removes the event hub, Event Hub namespace, stream analytics job, and the resource group itself.</span><span class="sxs-lookup"><span data-stu-id="8fae1-273">In this case, it removes the event hub, Event Hub namespace, stream analytics job, and the resource group itself.</span></span> 

### <a name="clean-up-resources-in-the-power-bi-visualization"></a><span data-ttu-id="8fae1-274">Clean up resources in the Power BI visualization</span><span class="sxs-lookup"><span data-stu-id="8fae1-274">Clean up resources in the Power BI visualization</span></span>

<span data-ttu-id="8fae1-275">Log into your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="8fae1-275">Log into your Power BI account.</span></span> <span data-ttu-id="8fae1-276">Go to **My Workspace**.</span><span class="sxs-lookup"><span data-stu-id="8fae1-276">Go to **My Workspace**.</span></span> <span data-ttu-id="8fae1-277">On the line with your dashboard name, click the trash can icon.</span><span class="sxs-lookup"><span data-stu-id="8fae1-277">On the line with your dashboard name, click the trash can icon.</span></span> <span data-ttu-id="8fae1-278">Next, go to **DataSets** and click the trash can icon to delete the dataset (**contosoehdataset**).</span><span class="sxs-lookup"><span data-stu-id="8fae1-278">Next, go to **DataSets** and click the trash can icon to delete the dataset (**contosoehdataset**).</span></span>

### <a name="clean-up-resources-using-azure-cli"></a><span data-ttu-id="8fae1-279">Clean up resources using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fae1-279">Clean up resources using Azure CLI</span></span>

<span data-ttu-id="8fae1-280">To remove the resource group, use the [az group delete](/cli/azure/group?view=azure-cli-latest#az-group-delete) command.</span><span class="sxs-lookup"><span data-stu-id="8fae1-280">To remove the resource group, use the [az group delete](/cli/azure/group?view=azure-cli-latest#az-group-delete) command.</span></span>

```azurecli-interactive
az group delete --name $resourceGroup
```

### <a name="clean-up-resources-using-powershell"></a><span data-ttu-id="8fae1-281">Clean up resources using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fae1-281">Clean up resources using PowerShell</span></span>

<span data-ttu-id="8fae1-282">To remove the resource group, use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="8fae1-282">To remove the resource group, use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8fae1-283">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fae1-283">Next steps</span></span>

<span data-ttu-id="8fae1-284">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="8fae1-284">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8fae1-285">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="8fae1-285">Create an Event Hubs namespace</span></span>
> * <span data-ttu-id="8fae1-286">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="8fae1-286">Create an event hub</span></span>
> * <span data-ttu-id="8fae1-287">Run the app that simulates events and sends them to the event hub</span><span class="sxs-lookup"><span data-stu-id="8fae1-287">Run the app that simulates events and sends them to the event hub</span></span>
> * <span data-ttu-id="8fae1-288">Configure a Stream Analytics job to process events sent to the hub</span><span class="sxs-lookup"><span data-stu-id="8fae1-288">Configure a Stream Analytics job to process events sent to the hub</span></span>
> * <span data-ttu-id="8fae1-289">Configure a Power BI visualization to show the results</span><span class="sxs-lookup"><span data-stu-id="8fae1-289">Configure a Power BI visualization to show the results</span></span>

<span data-ttu-id="8fae1-290">Advance to the next article to learn more about Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8fae1-290">Advance to the next article to learn more about Azure Event Hubs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8fae1-291">Get started sending messages to Azure Event Hubs in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="8fae1-291">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>](event-hubs-dotnet-standard-getstarted-send.md)

[create a free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
