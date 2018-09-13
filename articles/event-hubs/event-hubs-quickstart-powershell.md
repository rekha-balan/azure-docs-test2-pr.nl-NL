---
title: Azure Quickstart - Create an event hub using PowerShell | Microsoft Docs
description: This quickstart describes how to create an event hub using Azure PowerShell and then send and receive events using .NET Standard SDK.
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: b1f0c0d06f6c5f99a843a384e1dda667b967a02b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871035"
---
# <a name="quickstart-create-an-event-hub-using-azure-powershell"></a><span data-ttu-id="f3461-103">Quickstart: Create an event hub using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3461-103">Quickstart: Create an event hub using Azure PowerShell</span></span>

<span data-ttu-id="f3461-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="f3461-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="f3461-105">This quickstart shows how to create an event hub using Azure PowerShell, and then send to and receive from an event hub using the .NET Standard SDK.</span><span class="sxs-lookup"><span data-stu-id="f3461-105">This quickstart shows how to create an event hub using Azure PowerShell, and then send to and receive from an event hub using the .NET Standard SDK.</span></span>

<span data-ttu-id="f3461-106">To complete this quickstart, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f3461-106">To complete this quickstart, you need an Azure subscription.</span></span> <span data-ttu-id="f3461-107">If you don't have one, [create a free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="f3461-107">If you don't have one, [create a free account][] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3461-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f3461-108">Prerequisites</span></span>

<span data-ttu-id="f3461-109">To complete this tutorial, make sure you have:</span><span class="sxs-lookup"><span data-stu-id="f3461-109">To complete this tutorial, make sure you have:</span></span>

- <span data-ttu-id="f3461-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span><span class="sxs-lookup"><span data-stu-id="f3461-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span></span>
- <span data-ttu-id="f3461-111">[.NET Standard SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f3461-111">[.NET Standard SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f3461-112">If you're using PowerShell locally, you must run the latest version of PowerShell to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="f3461-112">If you're using PowerShell locally, you must run the latest version of PowerShell to complete this quickstart.</span></span> <span data-ttu-id="f3461-113">If you need to install or upgrade, see [Install and Configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.7.0).</span><span class="sxs-lookup"><span data-stu-id="f3461-113">If you need to install or upgrade, see [Install and Configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.7.0).</span></span>

## <a name="provision-resources"></a><span data-ttu-id="f3461-114">Provision resources</span><span class="sxs-lookup"><span data-stu-id="f3461-114">Provision resources</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f3461-115">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f3461-115">Create a resource group</span></span>

<span data-ttu-id="f3461-116">A resource group is a logical collection of Azure resources, and you need a resource group to create an event hub.</span><span class="sxs-lookup"><span data-stu-id="f3461-116">A resource group is a logical collection of Azure resources, and you need a resource group to create an event hub.</span></span> 

<span data-ttu-id="f3461-117">The following example creates a resource group in the East US region.</span><span class="sxs-lookup"><span data-stu-id="f3461-117">The following example creates a resource group in the East US region.</span></span> <span data-ttu-id="f3461-118">Replace `myResourceGroup` with the name of the resource group you want to use:</span><span class="sxs-lookup"><span data-stu-id="f3461-118">Replace `myResourceGroup` with the name of the resource group you want to use:</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup –Name myResourceGroup –Location eastus
```

### <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="f3461-119">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="f3461-119">Create an Event Hubs namespace</span></span>

<span data-ttu-id="f3461-120">Once your resource group is made, create an Event Hubs namespace within that resource group.</span><span class="sxs-lookup"><span data-stu-id="f3461-120">Once your resource group is made, create an Event Hubs namespace within that resource group.</span></span> <span data-ttu-id="f3461-121">An Event Hubs namespace provides a unique fully-qualified domain name in which you can create your event hub.</span><span class="sxs-lookup"><span data-stu-id="f3461-121">An Event Hubs namespace provides a unique fully-qualified domain name in which you can create your event hub.</span></span> <span data-ttu-id="f3461-122">Replace `namespace_name` with a unique name for your namespace:</span><span class="sxs-lookup"><span data-stu-id="f3461-122">Replace `namespace_name` with a unique name for your namespace:</span></span>

```azurepowershell-interactive
New-AzureRmEventHubNamespace -ResourceGroupName myResourceGroup -NamespaceName namespace_name -Location eastus
```

### <a name="create-an-event-hub"></a><span data-ttu-id="f3461-123">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="f3461-123">Create an event hub</span></span>

<span data-ttu-id="f3461-124">Now that you have an Event Hubs namespace, create an event hub within that namespace:</span><span class="sxs-lookup"><span data-stu-id="f3461-124">Now that you have an Event Hubs namespace, create an event hub within that namespace:</span></span>

```azurepowershell-interactive
New-AzureRmEventHub -ResourceGroupName myResourceGroup -NamespaceName namespace_name -EventHubName eventhub_name
```

### <a name="create-a-storage-account-for-event-processor-host"></a><span data-ttu-id="f3461-125">Create a storage account for Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="f3461-125">Create a storage account for Event Processor Host</span></span>

<span data-ttu-id="f3461-126">Event Processor Host simplifies receiving events from Event Hubs by managing checkpoints and parallel receivers.</span><span class="sxs-lookup"><span data-stu-id="f3461-126">Event Processor Host simplifies receiving events from Event Hubs by managing checkpoints and parallel receivers.</span></span> <span data-ttu-id="f3461-127">For checkpointing, Event Processor Host requires a storage account.</span><span class="sxs-lookup"><span data-stu-id="f3461-127">For checkpointing, Event Processor Host requires a storage account.</span></span> <span data-ttu-id="f3461-128">To create a storage account and get its keys, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="f3461-128">To create a storage account and get its keys, run the following commands:</span></span>

```azurepowershell-interactive
# Create a standard general purpose storage account 
New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name storage_account_name -Location eastus -SkuName Standard_LRS 
e
# Retrieve the storage account key for accessing it
Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name storage_account_name
```

### <a name="get-the-connection-string"></a><span data-ttu-id="f3461-129">Get the connection string</span><span class="sxs-lookup"><span data-stu-id="f3461-129">Get the connection string</span></span>

<span data-ttu-id="f3461-130">A connection string is required to connect to your event hub and process events.</span><span class="sxs-lookup"><span data-stu-id="f3461-130">A connection string is required to connect to your event hub and process events.</span></span> <span data-ttu-id="f3461-131">To get your connection string, run:</span><span class="sxs-lookup"><span data-stu-id="f3461-131">To get your connection string, run:</span></span>

```azurepowershell-interactive
Get-AzureRmEventHubKey -ResourceGroupName myResourceGroup -NamespaceName namespace_name -Name RootManageSharedAccessKey
```

## <a name="stream-into-event-hubs"></a><span data-ttu-id="f3461-132">Stream into Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3461-132">Stream into Event Hubs</span></span>

<span data-ttu-id="f3461-133">You can now start streaming into your Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f3461-133">You can now start streaming into your Event Hubs.</span></span> <span data-ttu-id="f3461-134">The samples can be downloaded or Git cloned from the [Event Hubs repo](https://github.com/Azure/azure-event-hubs)</span><span class="sxs-lookup"><span data-stu-id="f3461-134">The samples can be downloaded or Git cloned from the [Event Hubs repo](https://github.com/Azure/azure-event-hubs)</span></span>

### <a name="ingest-events"></a><span data-ttu-id="f3461-135">Ingest events</span><span class="sxs-lookup"><span data-stu-id="f3461-135">Ingest events</span></span>

<span data-ttu-id="f3461-136">To start streaming events, download the [SampleSender](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) from GitHub, or clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="f3461-136">To start streaming events, download the [SampleSender](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) from GitHub, or clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span></span>

```bash
git clone https://github.com/Azure/azure-event-hubs.git
```

<span data-ttu-id="f3461-137">Navigate to \azure-event-hubs\samples\DotNet\Microsoft.Azure.EventHubs\SampleSender folder, and load the SampleSender.sln file into Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3461-137">Navigate to \azure-event-hubs\samples\DotNet\Microsoft.Azure.EventHubs\SampleSender folder, and load the SampleSender.sln file into Visual Studio.</span></span>

<span data-ttu-id="f3461-138">Next, add the [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) Nuget package to the project.</span><span class="sxs-lookup"><span data-stu-id="f3461-138">Next, add the [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) Nuget package to the project.</span></span>

<span data-ttu-id="f3461-139">In the Program.cs file, replace the following placeholders with your event hub name and connection string:</span><span class="sxs-lookup"><span data-stu-id="f3461-139">In the Program.cs file, replace the following placeholders with your event hub name and connection string:</span></span>

```C#
private const string EhConnectionString = "Event Hubs connection string";
private const string EhEntityPath = "Event Hub name";

```

<span data-ttu-id="f3461-140">Now, build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="f3461-140">Now, build and run the sample.</span></span> <span data-ttu-id="f3461-141">You can see the events being ingested into your event hub:</span><span class="sxs-lookup"><span data-stu-id="f3461-141">You can see the events being ingested into your event hub:</span></span>

![][3]

### <a name="receive-and-process-events"></a><span data-ttu-id="f3461-142">Receive and process events</span><span class="sxs-lookup"><span data-stu-id="f3461-142">Receive and process events</span></span>

<span data-ttu-id="f3461-143">Now download the Event Processor Host receiver sample, which receives the messages you just sent.</span><span class="sxs-lookup"><span data-stu-id="f3461-143">Now download the Event Processor Host receiver sample, which receives the messages you just sent.</span></span> <span data-ttu-id="f3461-144">Download [SampleEphReceiver](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) from GitHub, or clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="f3461-144">Download [SampleEphReceiver](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) from GitHub, or clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span></span>

```bash
git clone https://github.com/Azure/azure-event-hubs.git
```

<span data-ttu-id="f3461-145">Navigate to the \azure-event-hubs\samples\DotNet\Microsoft.Azure.EventHubs\SampleEphReceiver folder, and load the SampleEphReceiver.sln solution file into Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3461-145">Navigate to the \azure-event-hubs\samples\DotNet\Microsoft.Azure.EventHubs\SampleEphReceiver folder, and load the SampleEphReceiver.sln solution file into Visual Studio.</span></span>

<span data-ttu-id="f3461-146">Next, add the [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [Microsoft.Azure.EventHubs.Processor](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) Nuget packages to the project.</span><span class="sxs-lookup"><span data-stu-id="f3461-146">Next, add the [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [Microsoft.Azure.EventHubs.Processor](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) Nuget packages to the project.</span></span>

<span data-ttu-id="f3461-147">In the Program.cs file, replace the following constants with their corresponding values:</span><span class="sxs-lookup"><span data-stu-id="f3461-147">In the Program.cs file, replace the following constants with their corresponding values:</span></span>

```C#
private const string EventHubConnectionString = "Event Hubs connection string";
private const string EventHubName = "Event Hub name";
private const string StorageContainerName = "Storage account container name";
private const string StorageAccountName = "Storage account name";
private const string StorageAccountKey = "Storage account key";
```

<span data-ttu-id="f3461-148">Now, build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="f3461-148">Now, build and run the sample.</span></span> <span data-ttu-id="f3461-149">You can see the events being received into your sample application:</span><span class="sxs-lookup"><span data-stu-id="f3461-149">You can see the events being received into your sample application:</span></span>

![][4]

<span data-ttu-id="f3461-150">On the Azure portal, you can view the rate at which events are being processed for a given Event Hubs namespace as shown:</span><span class="sxs-lookup"><span data-stu-id="f3461-150">On the Azure portal, you can view the rate at which events are being processed for a given Event Hubs namespace as shown:</span></span>

![][5]

## <a name="clean-up-resources"></a><span data-ttu-id="f3461-151">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f3461-151">Clean up resources</span></span>

<span data-ttu-id="f3461-152">When you've completed this quickstart, you can delete your resource group and the namespace, storage account, and event hub within it.</span><span class="sxs-lookup"><span data-stu-id="f3461-152">When you've completed this quickstart, you can delete your resource group and the namespace, storage account, and event hub within it.</span></span> <span data-ttu-id="f3461-153">Replace `myResourceGroup` with the name of the resource group you created.</span><span class="sxs-lookup"><span data-stu-id="f3461-153">Replace `myResourceGroup` with the name of the resource group you created.</span></span> 

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f3461-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3461-154">Next steps</span></span>

<span data-ttu-id="f3461-155">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span><span class="sxs-lookup"><span data-stu-id="f3461-155">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span></span> <span data-ttu-id="f3461-156">To learn more, continue with the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="f3461-156">To learn more, continue with the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3461-157">Visualize data anomalies on Event Hubs data streams</span><span class="sxs-lookup"><span data-stu-id="f3461-157">Visualize data anomalies on Event Hubs data streams</span></span>](event-hubs-tutorial-visualize-anomalies.md)

[create a free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
[Install and Configure Azure PowerShell]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[New-AzureRmResourceGroup]: https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup
[fully qualified domain name]: https://wikipedia.org/wiki/Fully_qualified_domain_name
[3]: ./media/event-hubs-quickstart-powershell/sender1.png
[4]: ./media/event-hubs-quickstart-powershell/receiver1.png
[5]: ./media/event-hubs-quickstart-powershell/metrics.png
