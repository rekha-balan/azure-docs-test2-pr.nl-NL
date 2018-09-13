---
title: Configure message routing with Azure IoT Hub (.NET) | Microsoft Docs
description: Configure message routing with Azure IoT Hub
author: robinsh
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: tutorial
ms.date: 05/01/2018
ms.author: robinsh
ms.custom: mvc
ms.openlocfilehash: a52ab4ff65312088e65d56006b6f99a7470b88f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867309"
---
# <a name="tutorial-configure-message-routing-with-iot-hub"></a><span data-ttu-id="96d6c-103">Tutorial: Configure message routing with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="96d6c-103">Tutorial: Configure message routing with IoT Hub</span></span>

<span data-ttu-id="96d6c-104">Message routing enables sending telemetry data from your IoT devices to built-in Event Hub-compatible endpoints or custom endpoints such as blob storage, Service Bus Queue, Service Bus Topic, and Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="96d6c-104">Message routing enables sending telemetry data from your IoT devices to built-in Event Hub-compatible endpoints or custom endpoints such as blob storage, Service Bus Queue, Service Bus Topic, and Event Hubs.</span></span> <span data-ttu-id="96d6c-105">While configuring message routing, you can create routing rules to customize the route that matches a certain rule.</span><span class="sxs-lookup"><span data-stu-id="96d6c-105">While configuring message routing, you can create routing rules to customize the route that matches a certain rule.</span></span> <span data-ttu-id="96d6c-106">Once set up, the incoming data is automatically routed to the endpoints by the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-106">Once set up, the incoming data is automatically routed to the endpoints by the IoT Hub.</span></span> 

<span data-ttu-id="96d6c-107">In this tutorial, you learn how to set up and use routing rules with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-107">In this tutorial, you learn how to set up and use routing rules with IoT Hub.</span></span> <span data-ttu-id="96d6c-108">You will route messages from an IoT device to one of multiple services, including blob storage and a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-108">You will route messages from an IoT device to one of multiple services, including blob storage and a Service Bus queue.</span></span> <span data-ttu-id="96d6c-109">Messages to the Service Bus queue will be picked up by a Logic App and sent via e-mail.</span><span class="sxs-lookup"><span data-stu-id="96d6c-109">Messages to the Service Bus queue will be picked up by a Logic App and sent via e-mail.</span></span> <span data-ttu-id="96d6c-110">Messages that do not have routing specifically set up are sent to the default endpoint, and viewed in a Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="96d6c-110">Messages that do not have routing specifically set up are sent to the default endpoint, and viewed in a Power BI visualization.</span></span>

<span data-ttu-id="96d6c-111">In this tutorial, you perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="96d6c-111">In this tutorial, you perform the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96d6c-112">Using Azure CLI or PowerShell, set up the base resources -- an IoT hub, a storage account, a Service Bus queue, and a simulated device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-112">Using Azure CLI or PowerShell, set up the base resources -- an IoT hub, a storage account, a Service Bus queue, and a simulated device.</span></span>
> * <span data-ttu-id="96d6c-113">Configure endpoints and routes in IoT hub for the storage account and Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-113">Configure endpoints and routes in IoT hub for the storage account and Service Bus queue.</span></span>
> * <span data-ttu-id="96d6c-114">Create a Logic App that is triggered and sends e-mail when a message is added to the Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-114">Create a Logic App that is triggered and sends e-mail when a message is added to the Service Bus queue.</span></span>
> * <span data-ttu-id="96d6c-115">Download and run an app that simulates an IoT Device sending messages to the hub for the different routing options.</span><span class="sxs-lookup"><span data-stu-id="96d6c-115">Download and run an app that simulates an IoT Device sending messages to the hub for the different routing options.</span></span>
> * <span data-ttu-id="96d6c-116">Create a Power BI visualization for data sent to the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-116">Create a Power BI visualization for data sent to the default endpoint.</span></span>
> * <span data-ttu-id="96d6c-117">View the results ...</span><span class="sxs-lookup"><span data-stu-id="96d6c-117">View the results ...</span></span>
> * <span data-ttu-id="96d6c-118">...in the Service Bus queue and e-mails.</span><span class="sxs-lookup"><span data-stu-id="96d6c-118">...in the Service Bus queue and e-mails.</span></span>
> * <span data-ttu-id="96d6c-119">...in the storage account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-119">...in the storage account.</span></span>
> * <span data-ttu-id="96d6c-120">...in the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="96d6c-120">...in the Power BI visualization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d6c-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96d6c-121">Prerequisites</span></span>

- <span data-ttu-id="96d6c-122">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="96d6c-122">An Azure subscription.</span></span> <span data-ttu-id="96d6c-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="96d6c-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

- <span data-ttu-id="96d6c-124">Install [Visual Studio for Windows](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="96d6c-124">Install [Visual Studio for Windows](https://www.visualstudio.com/).</span></span> 

- <span data-ttu-id="96d6c-125">A Power BI account to analyze the default endpoint's stream analytics.</span><span class="sxs-lookup"><span data-stu-id="96d6c-125">A Power BI account to analyze the default endpoint's stream analytics.</span></span> <span data-ttu-id="96d6c-126">([Try Power BI for free](https://app.powerbi.com/signupredirect?pbi_source=web).)</span><span class="sxs-lookup"><span data-stu-id="96d6c-126">([Try Power BI for free](https://app.powerbi.com/signupredirect?pbi_source=web).)</span></span>

- <span data-ttu-id="96d6c-127">An Office 365 account to send notification e-mails.</span><span class="sxs-lookup"><span data-stu-id="96d6c-127">An Office 365 account to send notification e-mails.</span></span> 

<span data-ttu-id="96d6c-128">You need either Azure CLI or Azure PowerShell to do the setup steps for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="96d6c-128">You need either Azure CLI or Azure PowerShell to do the setup steps for this tutorial.</span></span> 

<span data-ttu-id="96d6c-129">To use Azure CLI, while you can install Azure CLI locally, we recommend you use the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="96d6c-129">To use Azure CLI, while you can install Azure CLI locally, we recommend you use the Azure Cloud Shell.</span></span> <span data-ttu-id="96d6c-130">Azure Cloud Shell is a free, interactive shell that you can use to run Azure CLI scripts.</span><span class="sxs-lookup"><span data-stu-id="96d6c-130">Azure Cloud Shell is a free, interactive shell that you can use to run Azure CLI scripts.</span></span> <span data-ttu-id="96d6c-131">Common Azure tools are preinstalled and configured in Cloud Shell for you to use with your account, so you don't have to install them locally.</span><span class="sxs-lookup"><span data-stu-id="96d6c-131">Common Azure tools are preinstalled and configured in Cloud Shell for you to use with your account, so you don't have to install them locally.</span></span> 

<span data-ttu-id="96d6c-132">To use PowerShell, install it locally using the instructions below.</span><span class="sxs-lookup"><span data-stu-id="96d6c-132">To use PowerShell, install it locally using the instructions below.</span></span> 

### <a name="azure-cloud-shell"></a><span data-ttu-id="96d6c-133">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="96d6c-133">Azure Cloud Shell</span></span>

<span data-ttu-id="96d6c-134">There are a few ways to open Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="96d6c-134">There are a few ways to open Cloud Shell:</span></span>

|  |   |
|-----------------------------------------------|---|
| <span data-ttu-id="96d6c-135">Select **Try It** in the upper-right corner of a code block.</span><span class="sxs-lookup"><span data-stu-id="96d6c-135">Select **Try It** in the upper-right corner of a code block.</span></span> | ![Cloud Shell in this article](./media/tutorial-routing/cli-try-it.png) |
| <span data-ttu-id="96d6c-137">Open Cloud Shell in your browser.</span><span class="sxs-lookup"><span data-stu-id="96d6c-137">Open Cloud Shell in your browser.</span></span> | [![https://shell.azure.com/bash](./media/tutorial-routing/launchcloudshell.png)](https://shell.azure.com) |
| <span data-ttu-id="96d6c-138">Select the **Cloud Shell** button on the menu in the upper-right corner of the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96d6c-138">Select the **Cloud Shell** button on the menu in the upper-right corner of the [Azure portal](https://portal.azure.com).</span></span> |    ![Cloud Shell in the portal](./media/tutorial-routing/cloud-shell-menu.png) |
|  |  |

### <a name="using-azure-cli-locally"></a><span data-ttu-id="96d6c-140">Using Azure CLI locally</span><span class="sxs-lookup"><span data-stu-id="96d6c-140">Using Azure CLI locally</span></span>

<span data-ttu-id="96d6c-141">If you would rather use CLI locally than use Cloud Shell, you must have Azure CLI module version 2.0.30.0 or later.</span><span class="sxs-lookup"><span data-stu-id="96d6c-141">If you would rather use CLI locally than use Cloud Shell, you must have Azure CLI module version 2.0.30.0 or later.</span></span> <span data-ttu-id="96d6c-142">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="96d6c-142">Run `az --version` to find the version.</span></span> <span data-ttu-id="96d6c-143">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="96d6c-143">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

### <a name="using-powershell-locally"></a><span data-ttu-id="96d6c-144">Using PowerShell locally</span><span class="sxs-lookup"><span data-stu-id="96d6c-144">Using PowerShell locally</span></span>

<span data-ttu-id="96d6c-145">This tutorial requires Azure PowerShell module version 5.7 or later.</span><span class="sxs-lookup"><span data-stu-id="96d6c-145">This tutorial requires Azure PowerShell module version 5.7 or later.</span></span> <span data-ttu-id="96d6c-146">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="96d6c-146">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="96d6c-147">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="96d6c-147">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="set-up-resources"></a><span data-ttu-id="96d6c-148">Set up resources</span><span class="sxs-lookup"><span data-stu-id="96d6c-148">Set up resources</span></span>

<span data-ttu-id="96d6c-149">For this tutorial, you need an IoT hub, a storage account, and a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-149">For this tutorial, you need an IoT hub, a storage account, and a Service Bus queue.</span></span> <span data-ttu-id="96d6c-150">These resources can all be created using Azure CLI or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96d6c-150">These resources can all be created using Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="96d6c-151">Use the same resource group and location for all of the resources.</span><span class="sxs-lookup"><span data-stu-id="96d6c-151">Use the same resource group and location for all of the resources.</span></span> <span data-ttu-id="96d6c-152">Then at the end, you can remove everything in one step by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-152">Then at the end, you can remove everything in one step by deleting the resource group.</span></span>

<span data-ttu-id="96d6c-153">The following sections describe how to do these required steps.</span><span class="sxs-lookup"><span data-stu-id="96d6c-153">The following sections describe how to do these required steps.</span></span> <span data-ttu-id="96d6c-154">Follow the CLI *or* the PowerShell instructinos.</span><span class="sxs-lookup"><span data-stu-id="96d6c-154">Follow the CLI *or* the PowerShell instructinos.</span></span>

1. <span data-ttu-id="96d6c-155">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="96d6c-155">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span></span> 

    <!-- When they add the Basic tier, change this to use Basic instead of Standard. -->

1. <span data-ttu-id="96d6c-156">Create an IoT hub in the S1 tier.</span><span class="sxs-lookup"><span data-stu-id="96d6c-156">Create an IoT hub in the S1 tier.</span></span> <span data-ttu-id="96d6c-157">Add a consumer group to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-157">Add a consumer group to your IoT hub.</span></span> <span data-ttu-id="96d6c-158">The consumer group is used by the Azure Stream Analytics when retrieving data.</span><span class="sxs-lookup"><span data-stu-id="96d6c-158">The consumer group is used by the Azure Stream Analytics when retrieving data.</span></span>

1. <span data-ttu-id="96d6c-159">Create a standard V1 storage account with Standard_LRS replication.</span><span class="sxs-lookup"><span data-stu-id="96d6c-159">Create a standard V1 storage account with Standard_LRS replication.</span></span>

1. <span data-ttu-id="96d6c-160">Create a Service Bus namespace and queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-160">Create a Service Bus namespace and queue.</span></span> 

1. <span data-ttu-id="96d6c-161">Create a device identity for the simulated device that sends messages to your hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-161">Create a device identity for the simulated device that sends messages to your hub.</span></span> <span data-ttu-id="96d6c-162">Save the key for the testing phase.</span><span class="sxs-lookup"><span data-stu-id="96d6c-162">Save the key for the testing phase.</span></span>

### <a name="azure-cli-instructions"></a><span data-ttu-id="96d6c-163">Azure CLI instructions</span><span class="sxs-lookup"><span data-stu-id="96d6c-163">Azure CLI instructions</span></span>

<span data-ttu-id="96d6c-164">The easiest way to use this script is to copy it and paste it into Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="96d6c-164">The easiest way to use this script is to copy it and paste it into Cloud Shell.</span></span> <span data-ttu-id="96d6c-165">Assuming you are already logged in, it will run the script one line at a time.</span><span class="sxs-lookup"><span data-stu-id="96d6c-165">Assuming you are already logged in, it will run the script one line at a time.</span></span> 

```azurecli-interactive

# This is the IOT Extension for Azure CLI.
# You only need to install this the first time.
# You need it to create the device identity. 
az extension add --name azure-cli-iot-ext

# Set the values for the resource names that don't have to be globally unique.
# The resources that have to have unique names are named in the script below
#   with a random number concatenated to the name so you can probably just
#   run this script, and it will work with no conflicts.
location=westus
resourceGroup=ContosoResources
iotHubConsumerGroup=ContosoConsumers
containerName=contosoresults
iotDeviceName=Contoso-Test-Device 

# Create the resource group to be used
#   for all the resources for this tutorial.
az group create --name $resourceGroup \
    --location $location

# The IoT hub name must be globally unique, so add a random number to the end.
iotHubName=ContosoTestHub$RANDOM
echo "IoT hub name = " $iotHubName

# Create the IoT hub.
az iot hub create --name $iotHubName \
    --resource-group $resourceGroup \
    --sku S1 --location $location

# Add a consumer group to the IoT hub.
az iot hub consumer-group create --hub-name $iotHubName \
    --name $iotHubConsumerGroup

# The storage account name must be globally unique, so add a random number to the end.
storageAccountName=contosostorage$RANDOM
echo "Storage account name = " $storageAccountName

# Create the storage account to be used as a routing destination.
az storage account create --name $storageAccountName \
    --resource-group $resourceGroup \
    --location $location \
    --sku Standard_LRS

# Get the primary storage account key. 
#    You need this to create the container.
storageAccountKey=$(az storage account keys list \
    --resource-group $resourceGroup \
    --account-name $storageAccountName \
    --query "[0].value" | tr -d '"') 

# See the value of the storage account key.
echo "$storageAccountKey"

# Create the container in the storage account. 
az storage container create --name $containerName \
    --account-name $storageAccountName \
    --account-key $storageAccountKey \
    --public-access off 

# The Service Bus namespace must be globally unique, so add a random number to the end.
sbNameSpace=ContosoSBNamespace$RANDOM
echo "Service Bus namespace = " $sbNameSpace

# Create the Service Bus namespace.
az servicebus namespace create --resource-group $resourceGroup \
    --name $sbNameSpace \
    --location $location
    
# The Service Bus queue name must be globally unique, so add a random number to the end.
sbQueueName=ContosoSBQueue$RANDOM
echo "Service Bus queue name = " $sbQueueName

# Create the Service Bus queue to be used as a routing destination.
az servicebus queue create --name $sbQueueName \
    --namespace-name $sbNameSpace \
    --resource-group $resourceGroup

# Create the IoT device identity to be used for testing.
az iot hub device-identity create --device-id $iotDeviceName \
    --hub-name $iotHubName

# Retrieve the information about the device identity, then copy the primary key to
#   Notepad. You need this to run the device simulation during the testing phase.
az iot hub device-identity show --device-id $iotDeviceName \
    --hub-name $iotHubName

```

### <a name="powershell-instructions"></a><span data-ttu-id="96d6c-166">PowerShell instructions</span><span class="sxs-lookup"><span data-stu-id="96d6c-166">PowerShell instructions</span></span>

<span data-ttu-id="96d6c-167">The easiest way to use this script is to open [PowerShell ISE](https://docs.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise?view=powershell-6), copy the script to the clipboard, and then paste the whole script into the script window.</span><span class="sxs-lookup"><span data-stu-id="96d6c-167">The easiest way to use this script is to open [PowerShell ISE](https://docs.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise?view=powershell-6), copy the script to the clipboard, and then paste the whole script into the script window.</span></span> <span data-ttu-id="96d6c-168">Then you can change the values for the resource names (if you wish), and run the entire script.</span><span class="sxs-lookup"><span data-stu-id="96d6c-168">Then you can change the values for the resource names (if you wish), and run the entire script.</span></span> 

```azurepowershell-interactive
# Log into Azure account.
Login-AzureRMAccount

# Set the values for the resource names that don't have to be globally unique.
# The resources that have to have unique names are named in the script below
#   with a random number concatenated to the name so you can probably just
#   run this script, and it will work with no conflicts.
$location = "West US"
$resourceGroup = "ContosoResources"
$iotHubConsumerGroup = "ContosoConsumers"
$containerName = "contosoresults"
$iotDeviceName = "Contoso-Test-Device"

# Create the resource group to be used 
#   for all resources for this tutorial.
New-AzureRmResourceGroup -Name $resourceGroup -Location $location

# The IoT hub name must be globally unique, so add a random number to the end.
$iotHubName = "ContosoTestHub$(Get-Random)"
Write-Host "IoT hub name is " $iotHubName

# Create the IoT hub.
New-AzureRmIotHub -ResourceGroupName $resourceGroup `
    -Name $iotHubName `
    -SkuName "S1" `
    -Location $location `
    -Units 1

# Add a consumer group to the IoT hub for the 'events' endpoint.
Add-AzureRmIotHubEventHubConsumerGroup -ResourceGroupName $resourceGroup `
  -Name $iotHubName `
  -EventHubConsumerGroupName $iotHubConsumerGroup `
  -EventHubEndpointName "events"

# The storage account name must be globally unique, so add a random number to the end.
$storageAccountName = "contosostorage$(Get-Random)"
Write-Host "storage account name is " $storageAccountName

# Create the storage account to be used as a routing destination.
# Save the context for the storage account 
#   to be used when creating a container.
$storageAccount = New-AzureRmStorageAccount -ResourceGroupName $resourceGroup `
    -Name $storageAccountName `
    -Location $location `
    -SkuName Standard_LRS `
    -Kind Storage
$storageContext = $storageAccount.Context 

# Create the container in the storage account.
New-AzureStorageContainer -Name $containerName `
    -Context $storageContext

# The Service Bus namespace must be globally unique,
#   so add a random number to the end.
$serviceBusNamespace = "ContosoSBNamespace$(Get-Random)"
Write-Host "Service Bus namespace is " $serviceBusNamespace

# Create the Service Bus namespace.
New-AzureRmServiceBusNamespace -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name $serviceBusNamespace 

# The Service Bus queue name must be globally unique,
#  so add a random number to the end.
$serviceBusQueueName  = "ContosoSBQueue$(Get-Random)"
Write-Host "Service Bus queue name is " $serviceBusQueueName 

# Create the Service Bus queue to be used as a routing destination.
New-AzureRmServiceBusQueue -ResourceGroupName $resourceGroup `
    -Namespace $serviceBusNamespace `
    -Name $serviceBusQueueName 

```

<span data-ttu-id="96d6c-169">Next, create a device identity and save its key for later use.</span><span class="sxs-lookup"><span data-stu-id="96d6c-169">Next, create a device identity and save its key for later use.</span></span> <span data-ttu-id="96d6c-170">This device identity is used by the simulation application to send messages to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-170">This device identity is used by the simulation application to send messages to the IoT hub.</span></span> <span data-ttu-id="96d6c-171">This capability is not available in PowerShell, but you can create the device in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96d6c-171">This capability is not available in PowerShell, but you can create the device in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="96d6c-172">Open the [Azure portal](https://portal.azure.com) and log into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-172">Open the [Azure portal](https://portal.azure.com) and log into your Azure account.</span></span>

1. <span data-ttu-id="96d6c-173">Click on **Resource groups** and select your resource group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-173">Click on **Resource groups** and select your resource group.</span></span> <span data-ttu-id="96d6c-174">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-174">This tutorial uses **ContosoResources**.</span></span>

1. <span data-ttu-id="96d6c-175">In the list of resources, click your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-175">In the list of resources, click your IoT hub.</span></span> <span data-ttu-id="96d6c-176">This tutorial uses **ContosoTestHub**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-176">This tutorial uses **ContosoTestHub**.</span></span> <span data-ttu-id="96d6c-177">Select **IoT Devices** from the Hub pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-177">Select **IoT Devices** from the Hub pane.</span></span>

1. <span data-ttu-id="96d6c-178">Click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-178">Click **+ Add**.</span></span> <span data-ttu-id="96d6c-179">On the Add Device pane, fill in the device ID.</span><span class="sxs-lookup"><span data-stu-id="96d6c-179">On the Add Device pane, fill in the device ID.</span></span> <span data-ttu-id="96d6c-180">This tutorial uses **Contoso-Test-Device**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-180">This tutorial uses **Contoso-Test-Device**.</span></span> <span data-ttu-id="96d6c-181">Leave the keys empty, and check **Auto Generate Keys**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-181">Leave the keys empty, and check **Auto Generate Keys**.</span></span> <span data-ttu-id="96d6c-182">Make sure **Connect device to IoT hub** is enabled.</span><span class="sxs-lookup"><span data-stu-id="96d6c-182">Make sure **Connect device to IoT hub** is enabled.</span></span> <span data-ttu-id="96d6c-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-183">Click **Save**.</span></span>

   ![Screenshot showing the add-device screen.](./media/tutorial-routing/add-device.png)

1. <span data-ttu-id="96d6c-185">Now that it's been created, click on the device to see the generated keys.</span><span class="sxs-lookup"><span data-stu-id="96d6c-185">Now that it's been created, click on the device to see the generated keys.</span></span> <span data-ttu-id="96d6c-186">Click the Copy icon on the Primary key and save it somewhere such as Notepad for the testing phase of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="96d6c-186">Click the Copy icon on the Primary key and save it somewhere such as Notepad for the testing phase of this tutorial.</span></span>

   ![Screenshot showing the device details, including the keys.](./media/tutorial-routing/device-details.png)

## <a name="set-up-message-routing"></a><span data-ttu-id="96d6c-188">Set up message routing</span><span class="sxs-lookup"><span data-stu-id="96d6c-188">Set up message routing</span></span>

<span data-ttu-id="96d6c-189">You are going to route messages to different resources based on properties attached to the message by the simulated device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-189">You are going to route messages to different resources based on properties attached to the message by the simulated device.</span></span> <span data-ttu-id="96d6c-190">Messages that are not custom routed are sent to the default endpoint (messages/events).</span><span class="sxs-lookup"><span data-stu-id="96d6c-190">Messages that are not custom routed are sent to the default endpoint (messages/events).</span></span> 

|<span data-ttu-id="96d6c-191">value</span><span class="sxs-lookup"><span data-stu-id="96d6c-191">value</span></span> |<span data-ttu-id="96d6c-192">Result</span><span class="sxs-lookup"><span data-stu-id="96d6c-192">Result</span></span>|
|------|------|
|<span data-ttu-id="96d6c-193">level="storage"</span><span class="sxs-lookup"><span data-stu-id="96d6c-193">level="storage"</span></span> |<span data-ttu-id="96d6c-194">Write to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="96d6c-194">Write to Azure Storage.</span></span>|
|<span data-ttu-id="96d6c-195">level="critical"</span><span class="sxs-lookup"><span data-stu-id="96d6c-195">level="critical"</span></span> |<span data-ttu-id="96d6c-196">Write to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-196">Write to a Service Bus queue.</span></span> <span data-ttu-id="96d6c-197">A Logic App retrieves the message from the queue and uses Office 365 to e-mail the message.</span><span class="sxs-lookup"><span data-stu-id="96d6c-197">A Logic App retrieves the message from the queue and uses Office 365 to e-mail the message.</span></span>|
|<span data-ttu-id="96d6c-198">default</span><span class="sxs-lookup"><span data-stu-id="96d6c-198">default</span></span> |<span data-ttu-id="96d6c-199">Display this data using Power BI.</span><span class="sxs-lookup"><span data-stu-id="96d6c-199">Display this data using Power BI.</span></span>|

### <a name="routing-to-a-storage-account"></a><span data-ttu-id="96d6c-200">Routing to a storage account</span><span class="sxs-lookup"><span data-stu-id="96d6c-200">Routing to a storage account</span></span> 

<span data-ttu-id="96d6c-201">Now set up the routing for the storage account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-201">Now set up the routing for the storage account.</span></span> <span data-ttu-id="96d6c-202">Define an endpoint, and then set up a route for that endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-202">Define an endpoint, and then set up a route for that endpoint.</span></span> <span data-ttu-id="96d6c-203">Messages where the **level** property is set to **storage** are written to a storage account automatically.</span><span class="sxs-lookup"><span data-stu-id="96d6c-203">Messages where the **level** property is set to **storage** are written to a storage account automatically.</span></span>

1. <span data-ttu-id="96d6c-204">In the [Azure portal](https://portal.azure.com), click **Resource Groups**, then select your resource group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-204">In the [Azure portal](https://portal.azure.com), click **Resource Groups**, then select your resource group.</span></span> <span data-ttu-id="96d6c-205">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-205">This tutorial uses **ContosoResources**.</span></span> <span data-ttu-id="96d6c-206">Click the IoT hub under the list of resources.</span><span class="sxs-lookup"><span data-stu-id="96d6c-206">Click the IoT hub under the list of resources.</span></span> <span data-ttu-id="96d6c-207">This tutorial uses **ContosoTestHub**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-207">This tutorial uses **ContosoTestHub**.</span></span> <span data-ttu-id="96d6c-208">Click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-208">Click **Endpoints**.</span></span> <span data-ttu-id="96d6c-209">In the **Endpoints** pane, click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-209">In the **Endpoints** pane, click **+Add**.</span></span> <span data-ttu-id="96d6c-210">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="96d6c-210">Enter the following information:</span></span>

   <span data-ttu-id="96d6c-211">**Name**: Enter a name for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-211">**Name**: Enter a name for the endpoint.</span></span> <span data-ttu-id="96d6c-212">This tutorial uses **StorageContainer**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-212">This tutorial uses **StorageContainer**.</span></span>
   
   <span data-ttu-id="96d6c-213">**Endpoint Type**: Select **Azure Storage Container** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-213">**Endpoint Type**: Select **Azure Storage Container** from the dropdown list.</span></span>

   <span data-ttu-id="96d6c-214">Click **Pick a container** to see the list of storage accounts.</span><span class="sxs-lookup"><span data-stu-id="96d6c-214">Click **Pick a container** to see the list of storage accounts.</span></span> <span data-ttu-id="96d6c-215">Select your storage account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-215">Select your storage account.</span></span> <span data-ttu-id="96d6c-216">This tutorial uses **contosostorage**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-216">This tutorial uses **contosostorage**.</span></span> <span data-ttu-id="96d6c-217">Next, select the container.</span><span class="sxs-lookup"><span data-stu-id="96d6c-217">Next, select the container.</span></span> <span data-ttu-id="96d6c-218">This tutorial uses **contosoresults**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-218">This tutorial uses **contosoresults**.</span></span> <span data-ttu-id="96d6c-219">Click **Select**, which returns you to the **Add endpoint** pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-219">Click **Select**, which returns you to the **Add endpoint** pane.</span></span> 
   
   ![Screenshot showing adding an endpoint.](./media/tutorial-routing/add-endpoint-storage-account.png)
   
   <span data-ttu-id="96d6c-221">Click **OK** to finish adding the endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-221">Click **OK** to finish adding the endpoint.</span></span>
   
1. <span data-ttu-id="96d6c-222">Click **Routes** on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-222">Click **Routes** on your IoT hub.</span></span> <span data-ttu-id="96d6c-223">You're going to create a routing rule that routes messages to the storage container you just added as an endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-223">You're going to create a routing rule that routes messages to the storage container you just added as an endpoint.</span></span> <span data-ttu-id="96d6c-224">Click **+Add** at the top of the Routes pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-224">Click **+Add** at the top of the Routes pane.</span></span> <span data-ttu-id="96d6c-225">Fill in the fields on the screen.</span><span class="sxs-lookup"><span data-stu-id="96d6c-225">Fill in the fields on the screen.</span></span> 

   <span data-ttu-id="96d6c-226">**Name**: Enter a name for your routing rule.</span><span class="sxs-lookup"><span data-stu-id="96d6c-226">**Name**: Enter a name for your routing rule.</span></span> <span data-ttu-id="96d6c-227">This tutorial uses **StorageRule**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-227">This tutorial uses **StorageRule**.</span></span>

   <span data-ttu-id="96d6c-228">**Data source**: Select **Device Messages** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-228">**Data source**: Select **Device Messages** from the dropdown list.</span></span>

   <span data-ttu-id="96d6c-229">**Endpoint**: Select the endpoint you just set up.</span><span class="sxs-lookup"><span data-stu-id="96d6c-229">**Endpoint**: Select the endpoint you just set up.</span></span> <span data-ttu-id="96d6c-230">This tutorial uses **StorageContainer**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-230">This tutorial uses **StorageContainer**.</span></span> 
   
   <span data-ttu-id="96d6c-231">**Query string**: Enter `level="storage"` as the query string.</span><span class="sxs-lookup"><span data-stu-id="96d6c-231">**Query string**: Enter `level="storage"` as the query string.</span></span> 

   ![Screenshot showing creating a routing rule for the storage account.](./media/tutorial-routing/create-a-new-routing-rule-storage.png)
   
   <span data-ttu-id="96d6c-233">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-233">Click **Save**.</span></span> <span data-ttu-id="96d6c-234">When it finishes, it returns to the Routes pane, where you can see your new routing rule for storage.</span><span class="sxs-lookup"><span data-stu-id="96d6c-234">When it finishes, it returns to the Routes pane, where you can see your new routing rule for storage.</span></span> <span data-ttu-id="96d6c-235">Close the Routes pane, which returns you to the Resource group page.</span><span class="sxs-lookup"><span data-stu-id="96d6c-235">Close the Routes pane, which returns you to the Resource group page.</span></span>

### <a name="routing-to-a-service-bus-queue"></a><span data-ttu-id="96d6c-236">Routing to a Service Bus queue</span><span class="sxs-lookup"><span data-stu-id="96d6c-236">Routing to a Service Bus queue</span></span> 

<span data-ttu-id="96d6c-237">Now set up the routing for the Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-237">Now set up the routing for the Service Bus queue.</span></span> <span data-ttu-id="96d6c-238">Define an endpoint, and then set up a route for that endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-238">Define an endpoint, and then set up a route for that endpoint.</span></span> <span data-ttu-id="96d6c-239">Messages where the **level** property is set to **critical** are written to the Service Bus queue, which triggers a Logic App, which then sends an e-mail with the information.</span><span class="sxs-lookup"><span data-stu-id="96d6c-239">Messages where the **level** property is set to **critical** are written to the Service Bus queue, which triggers a Logic App, which then sends an e-mail with the information.</span></span> 

1. <span data-ttu-id="96d6c-240">On the Resource group page, click your IoT hub, then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-240">On the Resource group page, click your IoT hub, then click **Endpoints**.</span></span> <span data-ttu-id="96d6c-241">In the **Endpoints** pane, click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-241">In the **Endpoints** pane, click **+Add**.</span></span> <span data-ttu-id="96d6c-242">Enter the following information.</span><span class="sxs-lookup"><span data-stu-id="96d6c-242">Enter the following information.</span></span>

   <span data-ttu-id="96d6c-243">**Name**: Enter a name for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-243">**Name**: Enter a name for the endpoint.</span></span> <span data-ttu-id="96d6c-244">This tutorial uses **CriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-244">This tutorial uses **CriticalQueue**.</span></span> 

   <span data-ttu-id="96d6c-245">**Endpoint Type**: Select **Service Bus queue** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-245">**Endpoint Type**: Select **Service Bus queue** from the dropdown list.</span></span>

   <span data-ttu-id="96d6c-246">**Service Bus namespace**: Select the Service Bus namespace for this tutorial from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-246">**Service Bus namespace**: Select the Service Bus namespace for this tutorial from the dropdown list.</span></span> <span data-ttu-id="96d6c-247">This tutorial uses **ContosoSBNamespace**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-247">This tutorial uses **ContosoSBNamespace**.</span></span>

   <span data-ttu-id="96d6c-248">**Service Bus queue**: Select the Service Bus queue from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-248">**Service Bus queue**: Select the Service Bus queue from the dropdown list.</span></span> <span data-ttu-id="96d6c-249">This tutorial uses **contososbqueue**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-249">This tutorial uses **contososbqueue**.</span></span>

   ![Screenshot showing adding an endpoint for the Service Bus queue.](./media/tutorial-routing/add-endpoint-sb-queue.png)

   <span data-ttu-id="96d6c-251">Click **OK** to save the endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-251">Click **OK** to save the endpoint.</span></span> <span data-ttu-id="96d6c-252">After it's finished, close the Endpoints pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-252">After it's finished, close the Endpoints pane.</span></span> 
    
1. <span data-ttu-id="96d6c-253">Click **Routes** on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-253">Click **Routes** on your IoT hub.</span></span> <span data-ttu-id="96d6c-254">You're going to create a routing rule that routes messages to the Service Bus queue you just added as an endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-254">You're going to create a routing rule that routes messages to the Service Bus queue you just added as an endpoint.</span></span> <span data-ttu-id="96d6c-255">Click **+Add** at the top of the Routes pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-255">Click **+Add** at the top of the Routes pane.</span></span> <span data-ttu-id="96d6c-256">Fill in the fields on the screen.</span><span class="sxs-lookup"><span data-stu-id="96d6c-256">Fill in the fields on the screen.</span></span> 

   <span data-ttu-id="96d6c-257">**Name**: Enter a name for your routing rule.</span><span class="sxs-lookup"><span data-stu-id="96d6c-257">**Name**: Enter a name for your routing rule.</span></span> <span data-ttu-id="96d6c-258">This tutorial uses **SBQueueRule**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-258">This tutorial uses **SBQueueRule**.</span></span> 

   <span data-ttu-id="96d6c-259">**Data source**: Select **Device Messages** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-259">**Data source**: Select **Device Messages** from the dropdown list.</span></span>

   <span data-ttu-id="96d6c-260">**Endpoint**: Select the endpoint you just set up, **CriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-260">**Endpoint**: Select the endpoint you just set up, **CriticalQueue**.</span></span>

   <span data-ttu-id="96d6c-261">**Query string**: Enter `level="critical"` as the query string.</span><span class="sxs-lookup"><span data-stu-id="96d6c-261">**Query string**: Enter `level="critical"` as the query string.</span></span> 

   ![Screenshot showing creating a routing rule for the Service Bus queue.](./media/tutorial-routing/create-a-new-routing-rule-sbqueue.png)
   
   <span data-ttu-id="96d6c-263">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-263">Click **Save**.</span></span> <span data-ttu-id="96d6c-264">When it returns to the Routes pane, you see both of your new routing rules, as displayed here.</span><span class="sxs-lookup"><span data-stu-id="96d6c-264">When it returns to the Routes pane, you see both of your new routing rules, as displayed here.</span></span>

   ![Screenshot showing the routes you just set up.](./media/tutorial-routing/show-routing-rules-for-hub.png)

   <span data-ttu-id="96d6c-266">Close the Routes pane, which returns you to the Resource group page.</span><span class="sxs-lookup"><span data-stu-id="96d6c-266">Close the Routes pane, which returns you to the Resource group page.</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="96d6c-267">Create a Logic App</span><span class="sxs-lookup"><span data-stu-id="96d6c-267">Create a Logic App</span></span>  

<span data-ttu-id="96d6c-268">The Service Bus queue is to be used for receiving messages designated as critical.</span><span class="sxs-lookup"><span data-stu-id="96d6c-268">The Service Bus queue is to be used for receiving messages designated as critical.</span></span> <span data-ttu-id="96d6c-269">Set up a Logic app to monitor the Service Bus queue, and send an e-mail when a message is added to the queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-269">Set up a Logic app to monitor the Service Bus queue, and send an e-mail when a message is added to the queue.</span></span> 

1. <span data-ttu-id="96d6c-270">In the [Azure portal](https://portal.azure.com), click **+ Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-270">In the [Azure portal](https://portal.azure.com), click **+ Create a resource**.</span></span> <span data-ttu-id="96d6c-271">Put **logic app** in the search box and click Enter.</span><span class="sxs-lookup"><span data-stu-id="96d6c-271">Put **logic app** in the search box and click Enter.</span></span> <span data-ttu-id="96d6c-272">From the search results displayed, select Logic App, then click **Create** to continue to the **Create logic app** pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-272">From the search results displayed, select Logic App, then click **Create** to continue to the **Create logic app** pane.</span></span> <span data-ttu-id="96d6c-273">Fill in the fields.</span><span class="sxs-lookup"><span data-stu-id="96d6c-273">Fill in the fields.</span></span> 

   <span data-ttu-id="96d6c-274">**Name**: This field is the name of the logic app.</span><span class="sxs-lookup"><span data-stu-id="96d6c-274">**Name**: This field is the name of the logic app.</span></span> <span data-ttu-id="96d6c-275">This tutorial uses **ContosoLogicApp**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-275">This tutorial uses **ContosoLogicApp**.</span></span> 

   <span data-ttu-id="96d6c-276">**Subscription**: Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="96d6c-276">**Subscription**: Select your Azure subscription.</span></span>

   <span data-ttu-id="96d6c-277">**Resource group**: Click **Use existing** and select your resource group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-277">**Resource group**: Click **Use existing** and select your resource group.</span></span> <span data-ttu-id="96d6c-278">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-278">This tutorial uses **ContosoResources**.</span></span> 

   <span data-ttu-id="96d6c-279">**Location**: Use your location.</span><span class="sxs-lookup"><span data-stu-id="96d6c-279">**Location**: Use your location.</span></span> <span data-ttu-id="96d6c-280">This tutorial uses **West US**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-280">This tutorial uses **West US**.</span></span> 

   <span data-ttu-id="96d6c-281">**Log Analytics**: This toggle should be turned off.</span><span class="sxs-lookup"><span data-stu-id="96d6c-281">**Log Analytics**: This toggle should be turned off.</span></span> 

   ![Screenshot showing the Create Logic App screen.](./media/tutorial-routing/create-logic-app.png)

   <span data-ttu-id="96d6c-283">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-283">Click **Create**.</span></span>

1. <span data-ttu-id="96d6c-284">Now go to the Logic App.</span><span class="sxs-lookup"><span data-stu-id="96d6c-284">Now go to the Logic App.</span></span> <span data-ttu-id="96d6c-285">The easiest way to get to the Logic App is to click on **Resource groups**, select your resource group (this tutorial uses **ContosoResources**), then select the Logic App from the list of resources.</span><span class="sxs-lookup"><span data-stu-id="96d6c-285">The easiest way to get to the Logic App is to click on **Resource groups**, select your resource group (this tutorial uses **ContosoResources**), then select the Logic App from the list of resources.</span></span> <span data-ttu-id="96d6c-286">The Logic Apps Designer page appears (you might have to scroll over to the right to see the full page).</span><span class="sxs-lookup"><span data-stu-id="96d6c-286">The Logic Apps Designer page appears (you might have to scroll over to the right to see the full page).</span></span> <span data-ttu-id="96d6c-287">On the Logic Apps Designer page, scroll down until you see the tile that says **Blank Logic App +** and click it.</span><span class="sxs-lookup"><span data-stu-id="96d6c-287">On the Logic Apps Designer page, scroll down until you see the tile that says **Blank Logic App +** and click it.</span></span> 

1. <span data-ttu-id="96d6c-288">A list of connectors is displayed.</span><span class="sxs-lookup"><span data-stu-id="96d6c-288">A list of connectors is displayed.</span></span> <span data-ttu-id="96d6c-289">Select **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-289">Select **Service Bus**.</span></span> 

   ![Screenshot showing the list of connectors.](./media/tutorial-routing/logic-app-connectors.png)

1. <span data-ttu-id="96d6c-291">A list of triggers is displayed.</span><span class="sxs-lookup"><span data-stu-id="96d6c-291">A list of triggers is displayed.</span></span> <span data-ttu-id="96d6c-292">Select **Service Bus - When a message is received in a queue (auto-complete)**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-292">Select **Service Bus - When a message is received in a queue (auto-complete)**.</span></span> 

   ![Screenshot showing the list of triggers for the Service Bus.](./media/tutorial-routing/logic-app-triggers.png)

1. <span data-ttu-id="96d6c-294">On the next screen, fill in the Connection Name.</span><span class="sxs-lookup"><span data-stu-id="96d6c-294">On the next screen, fill in the Connection Name.</span></span> <span data-ttu-id="96d6c-295">This tutorial uses **ContosoConnection**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-295">This tutorial uses **ContosoConnection**.</span></span> 

   ![Screenshot showing setting up the connection for the Service Bus queue.](./media/tutorial-routing/logic-app-define-connection.png)

   <span data-ttu-id="96d6c-297">Click the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="96d6c-297">Click the Service Bus namespace.</span></span> <span data-ttu-id="96d6c-298">This tutorial uses **ContosoSBNamespace**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-298">This tutorial uses **ContosoSBNamespace**.</span></span> <span data-ttu-id="96d6c-299">When you select the namespace, the portal queries the Service Bus namespace to retrieve the keys.</span><span class="sxs-lookup"><span data-stu-id="96d6c-299">When you select the namespace, the portal queries the Service Bus namespace to retrieve the keys.</span></span> <span data-ttu-id="96d6c-300">Select **RootManageSharedAccessKey** and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-300">Select **RootManageSharedAccessKey** and click **Create**.</span></span> 
   
   ![Screenshot showing finishing setting up the connection.](./media/tutorial-routing/logic-app-finish-connection.png)

1. <span data-ttu-id="96d6c-302">On the next screen, select the name of the queue (this tutorial uses **contososbqueue**) from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="96d6c-302">On the next screen, select the name of the queue (this tutorial uses **contososbqueue**) from the dropdown list.</span></span> <span data-ttu-id="96d6c-303">You can use the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="96d6c-303">You can use the defaults for the rest of the fields.</span></span> 

   ![Screenshot showing the queue options.](./media/tutorial-routing/logic-app-queue-options.png)

1. <span data-ttu-id="96d6c-305">Now set up the action to send an e-mail when a message is received in the queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-305">Now set up the action to send an e-mail when a message is received in the queue.</span></span> <span data-ttu-id="96d6c-306">In the Logic Apps Designer, click **+ New step** to add a step, then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-306">In the Logic Apps Designer, click **+ New step** to add a step, then click **Add an action**.</span></span> <span data-ttu-id="96d6c-307">In the **Choose an action** pane, find and click **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-307">In the **Choose an action** pane, find and click **Office 365 Outlook**.</span></span> <span data-ttu-id="96d6c-308">On the triggers screen, select **Office 365 Outlook - Send an email**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-308">On the triggers screen, select **Office 365 Outlook - Send an email**.</span></span>  

   ![Screenshot showing the Office365 options.](./media/tutorial-routing/logic-app-select-outlook.png)

1. <span data-ttu-id="96d6c-310">Next, log into your Office 365 account to set up the connection.</span><span class="sxs-lookup"><span data-stu-id="96d6c-310">Next, log into your Office 365 account to set up the connection.</span></span> <span data-ttu-id="96d6c-311">Specify the e-mail addresses for the recipient(s) of the e-mails.</span><span class="sxs-lookup"><span data-stu-id="96d6c-311">Specify the e-mail addresses for the recipient(s) of the e-mails.</span></span> <span data-ttu-id="96d6c-312">Also specify the subject, and type what message you'd like the recipient to see in the body.</span><span class="sxs-lookup"><span data-stu-id="96d6c-312">Also specify the subject, and type what message you'd like the recipient to see in the body.</span></span> <span data-ttu-id="96d6c-313">For testing, fill in your own e-mail address as the recipient.</span><span class="sxs-lookup"><span data-stu-id="96d6c-313">For testing, fill in your own e-mail address as the recipient.</span></span>

   <span data-ttu-id="96d6c-314">Click **Add dynamic content** to show the content from the message that you can include.</span><span class="sxs-lookup"><span data-stu-id="96d6c-314">Click **Add dynamic content** to show the content from the message that you can include.</span></span> <span data-ttu-id="96d6c-315">Select **Content** -- it will include the message in the e-mail.</span><span class="sxs-lookup"><span data-stu-id="96d6c-315">Select **Content** -- it will include the message in the e-mail.</span></span> 

   ![Screenshot showing the e-mail options for the logic app.](./media/tutorial-routing/logic-app-send-email.png)

1. <span data-ttu-id="96d6c-317">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-317">Click **Save**.</span></span> <span data-ttu-id="96d6c-318">Then close the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="96d6c-318">Then close the Logic App Designer.</span></span>

## <a name="set-up-azure-stream-analytics"></a><span data-ttu-id="96d6c-319">Set up Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="96d6c-319">Set up Azure Stream Analytics</span></span>

<span data-ttu-id="96d6c-320">To see the data in a Power BI visualization, first set up a Stream Analytics job to retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="96d6c-320">To see the data in a Power BI visualization, first set up a Stream Analytics job to retrieve the data.</span></span> <span data-ttu-id="96d6c-321">Remember that only the messages where the **level** is **normal** are sent to the default endpoint, and will be retrieved by the Stream Analytics job for the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="96d6c-321">Remember that only the messages where the **level** is **normal** are sent to the default endpoint, and will be retrieved by the Stream Analytics job for the Power BI visualization.</span></span>

### <a name="create-the-stream-analytics-job"></a><span data-ttu-id="96d6c-322">Create the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="96d6c-322">Create the Stream Analytics job</span></span>

1. <span data-ttu-id="96d6c-323">In the [Azure portal](https://portal.azure.com), click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-323">In the [Azure portal](https://portal.azure.com), click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span></span>

1. <span data-ttu-id="96d6c-324">Enter the following information for the job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-324">Enter the following information for the job.</span></span>

   <span data-ttu-id="96d6c-325">**Job name**: The name of the job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-325">**Job name**: The name of the job.</span></span> <span data-ttu-id="96d6c-326">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="96d6c-326">The name must be globally unique.</span></span> <span data-ttu-id="96d6c-327">This tutorial uses **contosoJob**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-327">This tutorial uses **contosoJob**.</span></span>

   <span data-ttu-id="96d6c-328">**Resource group**: Use the same resource group used by your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-328">**Resource group**: Use the same resource group used by your IoT hub.</span></span> <span data-ttu-id="96d6c-329">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-329">This tutorial uses **ContosoResources**.</span></span> 

   <span data-ttu-id="96d6c-330">**Location**: Use the same location used in the setup script.</span><span class="sxs-lookup"><span data-stu-id="96d6c-330">**Location**: Use the same location used in the setup script.</span></span> <span data-ttu-id="96d6c-331">This tutorial uses **West US**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-331">This tutorial uses **West US**.</span></span> 

   ![Screenshot showing how to create the stream analytics job.](./media/tutorial-routing/stream-analytics-create-job.png)

1. <span data-ttu-id="96d6c-333">Click **Create** to create the job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-333">Click **Create** to create the job.</span></span> <span data-ttu-id="96d6c-334">To get back to the job, click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-334">To get back to the job, click **Resource groups**.</span></span> <span data-ttu-id="96d6c-335">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-335">This tutorial uses **ContosoResources**.</span></span> <span data-ttu-id="96d6c-336">Select the resource group, then click the Stream Analytics job in the list of resources.</span><span class="sxs-lookup"><span data-stu-id="96d6c-336">Select the resource group, then click the Stream Analytics job in the list of resources.</span></span> 

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="96d6c-337">Add an input to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="96d6c-337">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="96d6c-338">Under **Job Topology**, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-338">Under **Job Topology**, click **Inputs**.</span></span>

1. <span data-ttu-id="96d6c-339">In the **Inputs** pane, click **Add stream input** and select IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-339">In the **Inputs** pane, click **Add stream input** and select IoT Hub.</span></span> <span data-ttu-id="96d6c-340">On the screen that comes up, fill in the following fields:</span><span class="sxs-lookup"><span data-stu-id="96d6c-340">On the screen that comes up, fill in the following fields:</span></span>

   <span data-ttu-id="96d6c-341">**Input alias**: This tutorial uses **contosoinputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-341">**Input alias**: This tutorial uses **contosoinputs**.</span></span>

   <span data-ttu-id="96d6c-342">**Subscription**: Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="96d6c-342">**Subscription**: Select your subscription.</span></span>

   <span data-ttu-id="96d6c-343">**IoT Hub**: Select the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-343">**IoT Hub**: Select the IoT Hub.</span></span> <span data-ttu-id="96d6c-344">This tutorial uses **ContosoTestHub**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-344">This tutorial uses **ContosoTestHub**.</span></span>

   <span data-ttu-id="96d6c-345">**Endpoint**: Select **Messaging**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-345">**Endpoint**: Select **Messaging**.</span></span> <span data-ttu-id="96d6c-346">(If you select Operations Monitoring, you get the telemetry data about the IoT hub rather than the data you're sending through.)</span><span class="sxs-lookup"><span data-stu-id="96d6c-346">(If you select Operations Monitoring, you get the telemetry data about the IoT hub rather than the data you're sending through.)</span></span> 

   <span data-ttu-id="96d6c-347">**Shared access policy name**: Select **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-347">**Shared access policy name**: Select **iothubowner**.</span></span> <span data-ttu-id="96d6c-348">The portal fills in the Shared Access Policy Key for you.</span><span class="sxs-lookup"><span data-stu-id="96d6c-348">The portal fills in the Shared Access Policy Key for you.</span></span>

   <span data-ttu-id="96d6c-349">**Consumer group**: Select the consumer group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="96d6c-349">**Consumer group**: Select the consumer group you created earlier.</span></span> <span data-ttu-id="96d6c-350">This tutorial uses **contosoconsumers**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-350">This tutorial uses **contosoconsumers**.</span></span>
   
   <span data-ttu-id="96d6c-351">For the rest of the fields, accept the defaults.</span><span class="sxs-lookup"><span data-stu-id="96d6c-351">For the rest of the fields, accept the defaults.</span></span> 

   ![Screenshot showing how to set up the inputs for the stream analytics job.](./media/tutorial-routing/stream-analytics-job-inputs.png)

1. <span data-ttu-id="96d6c-353">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-353">Click **Save**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="96d6c-354">Add an output to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="96d6c-354">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="96d6c-355">Under **Job Topology**, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-355">Under **Job Topology**, click **Outputs**.</span></span>

1. <span data-ttu-id="96d6c-356">In the **Outputs** pane, click **Add**, and then select **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-356">In the **Outputs** pane, click **Add**, and then select **Power BI**.</span></span> <span data-ttu-id="96d6c-357">On the screen that comes up, fill in the following fields:</span><span class="sxs-lookup"><span data-stu-id="96d6c-357">On the screen that comes up, fill in the following fields:</span></span>

   <span data-ttu-id="96d6c-358">**Output alias**: The unique alias for the output.</span><span class="sxs-lookup"><span data-stu-id="96d6c-358">**Output alias**: The unique alias for the output.</span></span> <span data-ttu-id="96d6c-359">This tutorial uses **contosooutputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-359">This tutorial uses **contosooutputs**.</span></span> 

   <span data-ttu-id="96d6c-360">**Dataset name**: Name of the dataset to be used in Power BI.</span><span class="sxs-lookup"><span data-stu-id="96d6c-360">**Dataset name**: Name of the dataset to be used in Power BI.</span></span> <span data-ttu-id="96d6c-361">This tutorial uses **contosodataset**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-361">This tutorial uses **contosodataset**.</span></span> 

   <span data-ttu-id="96d6c-362">**Table name**: Name of the table to be used in Power BI.</span><span class="sxs-lookup"><span data-stu-id="96d6c-362">**Table name**: Name of the table to be used in Power BI.</span></span> <span data-ttu-id="96d6c-363">This tutorial uses **contosotable**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-363">This tutorial uses **contosotable**.</span></span>

   <span data-ttu-id="96d6c-364">Accept the defaults for the rest of the fields.</span><span class="sxs-lookup"><span data-stu-id="96d6c-364">Accept the defaults for the rest of the fields.</span></span>

1. <span data-ttu-id="96d6c-365">Click **Authorize**, and sign into your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-365">Click **Authorize**, and sign into your Power BI account.</span></span>

   ![Screenshot showing how to set up the outputs for the stream analytics job.](./media/tutorial-routing/stream-analytics-job-outputs.png)

1. <span data-ttu-id="96d6c-367">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-367">Click **Save**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="96d6c-368">Configure the query of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="96d6c-368">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="96d6c-369">Under **Job Topology**, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-369">Under **Job Topology**, click **Query**.</span></span>

1. <span data-ttu-id="96d6c-370">Replace `[YourInputAlias]` with the input alias of the job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-370">Replace `[YourInputAlias]` with the input alias of the job.</span></span> <span data-ttu-id="96d6c-371">This tutorial uses **contosoinputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-371">This tutorial uses **contosoinputs**.</span></span>

1. <span data-ttu-id="96d6c-372">Replace `[YourOutputAlias]` with the output alias of the job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-372">Replace `[YourOutputAlias]` with the output alias of the job.</span></span> <span data-ttu-id="96d6c-373">This tutorial uses **contosooutputs**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-373">This tutorial uses **contosooutputs**.</span></span>

   ![Screenshot showing how to set up the query for the stream analytics job.](./media/tutorial-routing/stream-analytics-job-query.png)

1. <span data-ttu-id="96d6c-375">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-375">Click **Save**.</span></span>

1. <span data-ttu-id="96d6c-376">Close the Query pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-376">Close the Query pane.</span></span> <span data-ttu-id="96d6c-377">This returns you to the view of the resources in the Resource Group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-377">This returns you to the view of the resources in the Resource Group.</span></span> <span data-ttu-id="96d6c-378">Click the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-378">Click the Stream Analytics job.</span></span> <span data-ttu-id="96d6c-379">This tutorial calls it **contosoJob**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-379">This tutorial calls it **contosoJob**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="96d6c-380">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="96d6c-380">Run the Stream Analytics job</span></span>

<span data-ttu-id="96d6c-381">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-381">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="96d6c-382">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-382">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

<span data-ttu-id="96d6c-383">To set up the Power BI report, you need data, so you'll set up Power BI after creating the device and running the device simulation application.</span><span class="sxs-lookup"><span data-stu-id="96d6c-383">To set up the Power BI report, you need data, so you'll set up Power BI after creating the device and running the device simulation application.</span></span>

## <a name="run-simulated-device-app"></a><span data-ttu-id="96d6c-384">Run Simulated Device app</span><span class="sxs-lookup"><span data-stu-id="96d6c-384">Run Simulated Device app</span></span>

<span data-ttu-id="96d6c-385">Earlier in the script setup section, you set up a device to simulate using an IoT device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-385">Earlier in the script setup section, you set up a device to simulate using an IoT device.</span></span> <span data-ttu-id="96d6c-386">In this section, you download a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96d6c-386">In this section, you download a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span> <span data-ttu-id="96d6c-387">This application sends messages for each of the different routing methods.</span><span class="sxs-lookup"><span data-stu-id="96d6c-387">This application sends messages for each of the different routing methods.</span></span> 

<span data-ttu-id="96d6c-388">Download the solution for the [IoT Device Simulation](https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="96d6c-388">Download the solution for the [IoT Device Simulation](https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip).</span></span> <span data-ttu-id="96d6c-389">This downloads a repo with several applications in it; the solution you are looking for is in iot-hub/Tutorials/Routing/SimulatedDevice/.</span><span class="sxs-lookup"><span data-stu-id="96d6c-389">This downloads a repo with several applications in it; the solution you are looking for is in iot-hub/Tutorials/Routing/SimulatedDevice/.</span></span>

<span data-ttu-id="96d6c-390">Double-click on the solution file (SimulatedDevice.sln) to open the code in Visual Studio, then open Program.cs.</span><span class="sxs-lookup"><span data-stu-id="96d6c-390">Double-click on the solution file (SimulatedDevice.sln) to open the code in Visual Studio, then open Program.cs.</span></span> <span data-ttu-id="96d6c-391">Substitute `{iot hub hostname}` with the IoT hub host name.</span><span class="sxs-lookup"><span data-stu-id="96d6c-391">Substitute `{iot hub hostname}` with the IoT hub host name.</span></span> <span data-ttu-id="96d6c-392">The format of the IoT hub host name is **{iot-hub-name}.azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-392">The format of the IoT hub host name is **{iot-hub-name}.azure-devices.net**.</span></span> <span data-ttu-id="96d6c-393">For this tutorial, the hub host name is **ContosoTestHub.azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-393">For this tutorial, the hub host name is **ContosoTestHub.azure-devices.net**.</span></span> <span data-ttu-id="96d6c-394">Next, substitute `{device key}` with the device key you saved earlier when setting up the simulated device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-394">Next, substitute `{device key}` with the device key you saved earlier when setting up the simulated device.</span></span> 

   ```csharp
        static string myDeviceId = "contoso-test-device";
        static string iotHubUri = "ContosoTestHub.azure-devices.net";
        // This is the primary key for the device. This is in the portal. 
        // Find your IoT hub in the portal > IoT devices > select your device > copy the key. 
        static string deviceKey = "{your device key here}";
   ```

## <a name="run-and-test"></a><span data-ttu-id="96d6c-395">Run and test</span><span class="sxs-lookup"><span data-stu-id="96d6c-395">Run and test</span></span> 

<span data-ttu-id="96d6c-396">Run the console application.</span><span class="sxs-lookup"><span data-stu-id="96d6c-396">Run the console application.</span></span> <span data-ttu-id="96d6c-397">Wait a few minutes.</span><span class="sxs-lookup"><span data-stu-id="96d6c-397">Wait a few minutes.</span></span> <span data-ttu-id="96d6c-398">You can see the messages being sent on the console screen of the application.</span><span class="sxs-lookup"><span data-stu-id="96d6c-398">You can see the messages being sent on the console screen of the application.</span></span>

<span data-ttu-id="96d6c-399">The app sends a new device-to-cloud message to the IoT hub every second.</span><span class="sxs-lookup"><span data-stu-id="96d6c-399">The app sends a new device-to-cloud message to the IoT hub every second.</span></span> <span data-ttu-id="96d6c-400">The message contains a JSON-serialized object with the device ID, temperature, humidity, and message level, which defaults to `normal`.</span><span class="sxs-lookup"><span data-stu-id="96d6c-400">The message contains a JSON-serialized object with the device ID, temperature, humidity, and message level, which defaults to `normal`.</span></span> <span data-ttu-id="96d6c-401">It randomly assigns a level of `critical` or `storage`, causing the message to be routed to the storage account or to the Service Bus queue (which triggers your Logic App to send an e-mail).</span><span class="sxs-lookup"><span data-stu-id="96d6c-401">It randomly assigns a level of `critical` or `storage`, causing the message to be routed to the storage account or to the Service Bus queue (which triggers your Logic App to send an e-mail).</span></span> <span data-ttu-id="96d6c-402">The default (`normal`) readings will be displayed in the BI report you set up next.</span><span class="sxs-lookup"><span data-stu-id="96d6c-402">The default (`normal`) readings will be displayed in the BI report you set up next.</span></span>

<span data-ttu-id="96d6c-403">If everything is set up correctly, at this point you should see the following results:</span><span class="sxs-lookup"><span data-stu-id="96d6c-403">If everything is set up correctly, at this point you should see the following results:</span></span>

1. <span data-ttu-id="96d6c-404">You start getting e-mails about critical messages.</span><span class="sxs-lookup"><span data-stu-id="96d6c-404">You start getting e-mails about critical messages.</span></span> 

   ![Screenshot showing the resulting emails.](./media/tutorial-routing/results-in-email.png)

   <span data-ttu-id="96d6c-406">This means the following:</span><span class="sxs-lookup"><span data-stu-id="96d6c-406">This means the following:</span></span>

   * <span data-ttu-id="96d6c-407">The routing to the Service Bus queue is working correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-407">The routing to the Service Bus queue is working correctly.</span></span>
   * <span data-ttu-id="96d6c-408">The Logic App retrieving the message from the Service Bus queue is working correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-408">The Logic App retrieving the message from the Service Bus queue is working correctly.</span></span>
   * <span data-ttu-id="96d6c-409">The Logic App connector to Outlook is working correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-409">The Logic App connector to Outlook is working correctly.</span></span> 

1. <span data-ttu-id="96d6c-410">In the [Azure portal](https://portal.azure.com), click **Resource groups** and select your Resource Group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-410">In the [Azure portal](https://portal.azure.com), click **Resource groups** and select your Resource Group.</span></span> <span data-ttu-id="96d6c-411">This tutorial uses **ContosoResources**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-411">This tutorial uses **ContosoResources**.</span></span> <span data-ttu-id="96d6c-412">Select the storage account, click **Blobs**, then select the Container.</span><span class="sxs-lookup"><span data-stu-id="96d6c-412">Select the storage account, click **Blobs**, then select the Container.</span></span> <span data-ttu-id="96d6c-413">This tutorial uses **contosoresults**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-413">This tutorial uses **contosoresults**.</span></span> <span data-ttu-id="96d6c-414">You should see a folder, and you can drill down through the directories until you see one or more files.</span><span class="sxs-lookup"><span data-stu-id="96d6c-414">You should see a folder, and you can drill down through the directories until you see one or more files.</span></span> <span data-ttu-id="96d6c-415">Open one of those files; they contain the entries routed to the storage account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-415">Open one of those files; they contain the entries routed to the storage account.</span></span> 

   ![Screenshot showing the result files in storage.](./media/tutorial-routing/results-in-storage.png)

<span data-ttu-id="96d6c-417">This means the following:</span><span class="sxs-lookup"><span data-stu-id="96d6c-417">This means the following:</span></span>

   * <span data-ttu-id="96d6c-418">The routing to the storage account is working correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-418">The routing to the storage account is working correctly.</span></span>

<span data-ttu-id="96d6c-419">Now with the application still running, set up the Power BI visualization to see the messages coming through the default routing.</span><span class="sxs-lookup"><span data-stu-id="96d6c-419">Now with the application still running, set up the Power BI visualization to see the messages coming through the default routing.</span></span> 

## <a name="set-up-the-power-bi-visualizations"></a><span data-ttu-id="96d6c-420">Set up the Power BI Visualizations</span><span class="sxs-lookup"><span data-stu-id="96d6c-420">Set up the Power BI Visualizations</span></span>

1. <span data-ttu-id="96d6c-421">Sign in to your [Power BI](https://powerbi.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-421">Sign in to your [Power BI](https://powerbi.microsoft.com/) account.</span></span>

1. <span data-ttu-id="96d6c-422">Go to **Workspaces** and select the workspace that you set when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-422">Go to **Workspaces** and select the workspace that you set when you created the output for the Stream Analytics job.</span></span> <span data-ttu-id="96d6c-423">This tutorial uses **My Workspace**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-423">This tutorial uses **My Workspace**.</span></span> 

1. <span data-ttu-id="96d6c-424">Click **Datasets**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-424">Click **Datasets**.</span></span>

   <span data-ttu-id="96d6c-425">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-425">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span> <span data-ttu-id="96d6c-426">This tutorial uses **contosodataset**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-426">This tutorial uses **contosodataset**.</span></span> <span data-ttu-id="96d6c-427">(It may take 5-10 minutes for the dataset to show up the first time.)</span><span class="sxs-lookup"><span data-stu-id="96d6c-427">(It may take 5-10 minutes for the dataset to show up the first time.)</span></span>

1. <span data-ttu-id="96d6c-428">Under **ACTIONS**, click the first icon to create a report.</span><span class="sxs-lookup"><span data-stu-id="96d6c-428">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Screenshot showing Power BI workspace with Actions and report icon highlighted.](./media/tutorial-routing/power-bi-actions.png)

1. <span data-ttu-id="96d6c-430">Create a line chart to show real-time temperature over time.</span><span class="sxs-lookup"><span data-stu-id="96d6c-430">Create a line chart to show real-time temperature over time.</span></span>

   <span data-ttu-id="96d6c-431">a.</span><span class="sxs-lookup"><span data-stu-id="96d6c-431">a.</span></span> <span data-ttu-id="96d6c-432">On the report creation page, add a line chart by clicking the line chart icon.</span><span class="sxs-lookup"><span data-stu-id="96d6c-432">On the report creation page, add a line chart by clicking the line chart icon.</span></span>

   ![Screenshot showing the visualizations and fields.](./media/tutorial-routing/power-bi-visualizations-and-fields.png)

   <span data-ttu-id="96d6c-434">b.</span><span class="sxs-lookup"><span data-stu-id="96d6c-434">b.</span></span> <span data-ttu-id="96d6c-435">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="96d6c-435">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span> <span data-ttu-id="96d6c-436">This tutorial uses **contosotable**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-436">This tutorial uses **contosotable**.</span></span>

   <span data-ttu-id="96d6c-437">c.</span><span class="sxs-lookup"><span data-stu-id="96d6c-437">c.</span></span> <span data-ttu-id="96d6c-438">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span><span class="sxs-lookup"><span data-stu-id="96d6c-438">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>

   <span data-ttu-id="96d6c-439">d.</span><span class="sxs-lookup"><span data-stu-id="96d6c-439">d.</span></span> <span data-ttu-id="96d6c-440">Drag **temperature** to **Values**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-440">Drag **temperature** to **Values**.</span></span>

   <span data-ttu-id="96d6c-441">A line chart is created.</span><span class="sxs-lookup"><span data-stu-id="96d6c-441">A line chart is created.</span></span> <span data-ttu-id="96d6c-442">The x-axis displays date and time in the UTC time zone.</span><span class="sxs-lookup"><span data-stu-id="96d6c-442">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="96d6c-443">The y-axis displays temperature from the sensor.</span><span class="sxs-lookup"><span data-stu-id="96d6c-443">The y-axis displays temperature from the sensor.</span></span>

1. <span data-ttu-id="96d6c-444">Create another line chart to show real-time humidity over time.</span><span class="sxs-lookup"><span data-stu-id="96d6c-444">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="96d6c-445">To set up the second chart, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span><span class="sxs-lookup"><span data-stu-id="96d6c-445">To set up the second chart, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Screenshot showing the final Power BI report with the two charts.](./media/tutorial-routing/power-bi-report.png)

1. <span data-ttu-id="96d6c-447">Click **Save** to save the report.</span><span class="sxs-lookup"><span data-stu-id="96d6c-447">Click **Save** to save the report.</span></span>

<span data-ttu-id="96d6c-448">You should be able to see data on both charts.</span><span class="sxs-lookup"><span data-stu-id="96d6c-448">You should be able to see data on both charts.</span></span> <span data-ttu-id="96d6c-449">This means the following:</span><span class="sxs-lookup"><span data-stu-id="96d6c-449">This means the following:</span></span>

   * <span data-ttu-id="96d6c-450">The routing to the default endpoint is working correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-450">The routing to the default endpoint is working correctly.</span></span>
   * <span data-ttu-id="96d6c-451">The Azure Stream Analytics job is streaming correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-451">The Azure Stream Analytics job is streaming correctly.</span></span>
   * <span data-ttu-id="96d6c-452">The Power BI Visualization is set up correctly.</span><span class="sxs-lookup"><span data-stu-id="96d6c-452">The Power BI Visualization is set up correctly.</span></span>

<span data-ttu-id="96d6c-453">You can refresh the charts to see the most recent data by clicking the Refresh button on the top of the Power BI window.</span><span class="sxs-lookup"><span data-stu-id="96d6c-453">You can refresh the charts to see the most recent data by clicking the Refresh button on the top of the Power BI window.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="96d6c-454">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="96d6c-454">Clean up resources</span></span> 

<span data-ttu-id="96d6c-455">If you want to remove all of the resources you've created, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-455">If you want to remove all of the resources you've created, delete the resource group.</span></span> <span data-ttu-id="96d6c-456">This action deletes all resources contained within the group.</span><span class="sxs-lookup"><span data-stu-id="96d6c-456">This action deletes all resources contained within the group.</span></span> <span data-ttu-id="96d6c-457">In this case, it removes the IoT hub, the Service Bus namespace and queue, the Logic App, the storage account, and the resource group itself.</span><span class="sxs-lookup"><span data-stu-id="96d6c-457">In this case, it removes the IoT hub, the Service Bus namespace and queue, the Logic App, the storage account, and the resource group itself.</span></span> 

### <a name="clean-up-resources-in-the-power-bi-visualization"></a><span data-ttu-id="96d6c-458">Clean up resources in the Power BI visualization</span><span class="sxs-lookup"><span data-stu-id="96d6c-458">Clean up resources in the Power BI visualization</span></span>

<span data-ttu-id="96d6c-459">Log into your [Power BI](https://powerbi.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-459">Log into your [Power BI](https://powerbi.microsoft.com/) account.</span></span> <span data-ttu-id="96d6c-460">Go to your workspace.</span><span class="sxs-lookup"><span data-stu-id="96d6c-460">Go to your workspace.</span></span> <span data-ttu-id="96d6c-461">This tutorial uses **My Workspace**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-461">This tutorial uses **My Workspace**.</span></span> <span data-ttu-id="96d6c-462">To remove the Power BI visualization, go to DataSets and click the trash can icon to delete the dataset.</span><span class="sxs-lookup"><span data-stu-id="96d6c-462">To remove the Power BI visualization, go to DataSets and click the trash can icon to delete the dataset.</span></span> <span data-ttu-id="96d6c-463">This tutorial uses **contosodataset**.</span><span class="sxs-lookup"><span data-stu-id="96d6c-463">This tutorial uses **contosodataset**.</span></span> <span data-ttu-id="96d6c-464">When you remove the dataset, the report is removed as well.</span><span class="sxs-lookup"><span data-stu-id="96d6c-464">When you remove the dataset, the report is removed as well.</span></span>

### <a name="clean-up-resources-using-azure-cli"></a><span data-ttu-id="96d6c-465">Clean up resources using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96d6c-465">Clean up resources using Azure CLI</span></span>

<span data-ttu-id="96d6c-466">To remove the resource group, use the [az group delete](https://docs.microsoft.com/cli/azure/group?view=azure-cli-latest#az-group-delete) command.</span><span class="sxs-lookup"><span data-stu-id="96d6c-466">To remove the resource group, use the [az group delete](https://docs.microsoft.com/cli/azure/group?view=azure-cli-latest#az-group-delete) command.</span></span>

```azurecli-interactive
az group delete --name $resourceGroup
```
### <a name="clean-up-resources-using-powershell"></a><span data-ttu-id="96d6c-467">Clean up resources using PowerShell</span><span class="sxs-lookup"><span data-stu-id="96d6c-467">Clean up resources using PowerShell</span></span>

<span data-ttu-id="96d6c-468">To remove the resource group, use the [Remove-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="96d6c-468">To remove the resource group, use the [Remove-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) command.</span></span> <span data-ttu-id="96d6c-469">$resourceGroup was set to **ContosoIoTRG1** back at the beginning of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="96d6c-469">$resourceGroup was set to **ContosoIoTRG1** back at the beginning of this tutorial.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name $resourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="96d6c-470">Next steps</span><span class="sxs-lookup"><span data-stu-id="96d6c-470">Next steps</span></span>

<span data-ttu-id="96d6c-471">In this tutorial, you learned how to use message routing to route IoT Hub messages to different destinations by performing the following tasks.</span><span class="sxs-lookup"><span data-stu-id="96d6c-471">In this tutorial, you learned how to use message routing to route IoT Hub messages to different destinations by performing the following tasks.</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="96d6c-472">Using Azure CLI or PowerShell, set up the base resources -- an IoT hub, a storage account, a Service Bus queue, and a simulated device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-472">Using Azure CLI or PowerShell, set up the base resources -- an IoT hub, a storage account, a Service Bus queue, and a simulated device.</span></span>
> * <span data-ttu-id="96d6c-473">Configure endpoints and routes in IoT hub for the storage account and Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-473">Configure endpoints and routes in IoT hub for the storage account and Service Bus queue.</span></span>
> * <span data-ttu-id="96d6c-474">Create a Logic App that is triggered and sends e-mail when a message is added to the Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="96d6c-474">Create a Logic App that is triggered and sends e-mail when a message is added to the Service Bus queue.</span></span>
> * <span data-ttu-id="96d6c-475">Download and run an app that simulates an IoT Device sending messages to the hub for the different routing options.</span><span class="sxs-lookup"><span data-stu-id="96d6c-475">Download and run an app that simulates an IoT Device sending messages to the hub for the different routing options.</span></span>
> * <span data-ttu-id="96d6c-476">Create a Power BI visualization for data sent to the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="96d6c-476">Create a Power BI visualization for data sent to the default endpoint.</span></span>
> * <span data-ttu-id="96d6c-477">View the results ...</span><span class="sxs-lookup"><span data-stu-id="96d6c-477">View the results ...</span></span>
> * <span data-ttu-id="96d6c-478">...in the Service Bus queue and e-mails.</span><span class="sxs-lookup"><span data-stu-id="96d6c-478">...in the Service Bus queue and e-mails.</span></span>
> * <span data-ttu-id="96d6c-479">...in the storage account.</span><span class="sxs-lookup"><span data-stu-id="96d6c-479">...in the storage account.</span></span>
> * <span data-ttu-id="96d6c-480">...in the Power BI visualization.</span><span class="sxs-lookup"><span data-stu-id="96d6c-480">...in the Power BI visualization.</span></span>

<span data-ttu-id="96d6c-481">Advance to the next tutorial to learn how to manage the state of an IoT device.</span><span class="sxs-lookup"><span data-stu-id="96d6c-481">Advance to the next tutorial to learn how to manage the state of an IoT device.</span></span> 

> [!div class="nextstepaction"]
[<span data-ttu-id="96d6c-482">Configure your devices from a back-end service</span><span class="sxs-lookup"><span data-stu-id="96d6c-482">Configure your devices from a back-end service</span></span>](tutorial-device-twins.md)

 <!--  [Manage the state of a device](./tutorial-manage-state.md) -->
