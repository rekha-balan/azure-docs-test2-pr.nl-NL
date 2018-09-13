---
title: Set up a Device Provisioning Service using Azure CLI | Microsoft Docs
description: Azure Quickstart - Set up the Azure IoT Hub Device Provisioning Service using Azure CLI
author: wesmc7777
ms.author: wesmc
ms.date: 02/26/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: c9e3bbbc4fbe8a9aade3364d6cbe9e93b5798595
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856149"
---
# <a name="set-up-the-iot-hub-device-provisioning-service-with-azure-cli"></a><span data-ttu-id="62036-103">Set up the IoT Hub Device Provisioning Service with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="62036-103">Set up the IoT Hub Device Provisioning Service with Azure CLI</span></span>

<span data-ttu-id="62036-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="62036-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="62036-105">This QuickStart details using the Azure CLI to create an IoT hub and an IoT Hub Device Provisioning Service and to link the two services together.</span><span class="sxs-lookup"><span data-stu-id="62036-105">This QuickStart details using the Azure CLI to create an IoT hub and an IoT Hub Device Provisioning Service and to link the two services together.</span></span> 

<span data-ttu-id="62036-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="62036-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62036-107">Both the IoT hub and the provisioning service you create in this QuickStart will be publicly discoverable as DNS endpoints.</span><span class="sxs-lookup"><span data-stu-id="62036-107">Both the IoT hub and the provisioning service you create in this QuickStart will be publicly discoverable as DNS endpoints.</span></span> <span data-ttu-id="62036-108">Make sure to avoid any sensitive information if you decide to change the names used for these resources.</span><span class="sxs-lookup"><span data-stu-id="62036-108">Make sure to avoid any sensitive information if you decide to change the names used for these resources.</span></span>
>


[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]


## <a name="create-a-resource-group"></a><span data-ttu-id="62036-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="62036-109">Create a resource group</span></span>

<span data-ttu-id="62036-110">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="62036-110">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="62036-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="62036-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="62036-112">The following example creates a resource group named *my-sample-resource-group* in the *westus* location.</span><span class="sxs-lookup"><span data-stu-id="62036-112">The following example creates a resource group named *my-sample-resource-group* in the *westus* location.</span></span>

```azurecli-interactive 
az group create --name my-sample-resource-group --location westus
```

> [!TIP]
> <span data-ttu-id="62036-113">The example creates the resource group in the West US location.</span><span class="sxs-lookup"><span data-stu-id="62036-113">The example creates the resource group in the West US location.</span></span> <span data-ttu-id="62036-114">You can view a list of available locations by running the command `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="62036-114">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
>
>

## <a name="create-an-iot-hub"></a><span data-ttu-id="62036-115">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="62036-115">Create an IoT hub</span></span>

<span data-ttu-id="62036-116">Create an IoT hub with the [az iot hub create](/cli/azure/iot/hub#az-iot-hub-create) command.</span><span class="sxs-lookup"><span data-stu-id="62036-116">Create an IoT hub with the [az iot hub create](/cli/azure/iot/hub#az-iot-hub-create) command.</span></span>

<span data-ttu-id="62036-117">The following example creates an IoT hub named *my-sample-hub* in the *westus* location.</span><span class="sxs-lookup"><span data-stu-id="62036-117">The following example creates an IoT hub named *my-sample-hub* in the *westus* location.</span></span>  

```azurecli-interactive 
az iot hub create --name my-sample-hub --resource-group my-sample-resource-group --location westus
```

## <a name="create-a-provisioning-service"></a><span data-ttu-id="62036-118">Create a provisioning service</span><span class="sxs-lookup"><span data-stu-id="62036-118">Create a provisioning service</span></span>

<span data-ttu-id="62036-119">Create a provisioning service with the [az iot dps create](/cli/azure/iot/dps#az-iot-dps-create) command.</span><span class="sxs-lookup"><span data-stu-id="62036-119">Create a provisioning service with the [az iot dps create](/cli/azure/iot/dps#az-iot-dps-create) command.</span></span> 

<span data-ttu-id="62036-120">The following example creates an provisioning service named *my-sample-dps* in the *westus* location.</span><span class="sxs-lookup"><span data-stu-id="62036-120">The following example creates an provisioning service named *my-sample-dps* in the *westus* location.</span></span>  

```azurecli-interactive 
az iot dps create --name my-sample-dps --resource-group my-sample-resource-group --location westus
```

> [!TIP]
> <span data-ttu-id="62036-121">The example creates the provisioning service in the West US location.</span><span class="sxs-lookup"><span data-stu-id="62036-121">The example creates the provisioning service in the West US location.</span></span> <span data-ttu-id="62036-122">You can view a list of available locations by running the command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or by going to the [Azure Status](https://azure.microsoft.com/status/) page and searching for "Device Provisioning Service".</span><span class="sxs-lookup"><span data-stu-id="62036-122">You can view a list of available locations by running the command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or by going to the [Azure Status](https://azure.microsoft.com/status/) page and searching for "Device Provisioning Service".</span></span> <span data-ttu-id="62036-123">In commands, locations can be specified either in one word or multi-word format; for example: westus, West US, WEST US, etc. The value is not case sensitive.</span><span class="sxs-lookup"><span data-stu-id="62036-123">In commands, locations can be specified either in one word or multi-word format; for example: westus, West US, WEST US, etc. The value is not case sensitive.</span></span> <span data-ttu-id="62036-124">If you use multi-word format to specify location, enclose the value in quotes; for example, `-- location "West US"`.</span><span class="sxs-lookup"><span data-stu-id="62036-124">If you use multi-word format to specify location, enclose the value in quotes; for example, `-- location "West US"`.</span></span>
>


## <a name="get-the-connection-string-for-the-iot-hub"></a><span data-ttu-id="62036-125">Get the connection string for the IoT hub</span><span class="sxs-lookup"><span data-stu-id="62036-125">Get the connection string for the IoT hub</span></span>

<span data-ttu-id="62036-126">You need your IoT hub's connection string to link it with the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="62036-126">You need your IoT hub's connection string to link it with the Device Provisioning Service.</span></span> <span data-ttu-id="62036-127">Use the [az iot hub show-connection-string](/cli/azure/iot/hub#az-iot-hub-show-connection-string) command to get the connection string and use its output to set a variable that you will use when you link the two resources.</span><span class="sxs-lookup"><span data-stu-id="62036-127">Use the [az iot hub show-connection-string](/cli/azure/iot/hub#az-iot-hub-show-connection-string) command to get the connection string and use its output to set a variable that you will use when you link the two resources.</span></span> 

<span data-ttu-id="62036-128">The following example sets the *hubConnectionString* variable to the value of the connection string for the primary key of the hub's *iothubowner* policy.</span><span class="sxs-lookup"><span data-stu-id="62036-128">The following example sets the *hubConnectionString* variable to the value of the connection string for the primary key of the hub's *iothubowner* policy.</span></span> <span data-ttu-id="62036-129">You can specify a different policy with the `--policy-name` parameter.</span><span class="sxs-lookup"><span data-stu-id="62036-129">You can specify a different policy with the `--policy-name` parameter.</span></span> <span data-ttu-id="62036-130">The command uses the Azure CLI [query](/cli/azure/query-azure-cli) and [output](/cli/azure/format-output-azure-cli#tsv-output-format) options to extract the connection string from the command output.</span><span class="sxs-lookup"><span data-stu-id="62036-130">The command uses the Azure CLI [query](/cli/azure/query-azure-cli) and [output](/cli/azure/format-output-azure-cli#tsv-output-format) options to extract the connection string from the command output.</span></span>

```azurecli-interactive 
hubConnectionString=$(az iot hub show-connection-string --name my-sample-hub --key primary --query connectionString -o tsv)
```

<span data-ttu-id="62036-131">You can use the `echo` command to see the connection string.</span><span class="sxs-lookup"><span data-stu-id="62036-131">You can use the `echo` command to see the connection string.</span></span>

```azurecli-interactive 
echo $hubConnectionString
```

> [!NOTE]
> <span data-ttu-id="62036-132">These two commands are valid for a host running under Bash.</span><span class="sxs-lookup"><span data-stu-id="62036-132">These two commands are valid for a host running under Bash.</span></span> <span data-ttu-id="62036-133">If you are using a local Windows/CMD shell or a PowerShell host, you need to modify the commands to use  the correct syntax for that environment.</span><span class="sxs-lookup"><span data-stu-id="62036-133">If you are using a local Windows/CMD shell or a PowerShell host, you need to modify the commands to use  the correct syntax for that environment.</span></span>
>

## <a name="link-the-iot-hub-and-the-provisioning-service"></a><span data-ttu-id="62036-134">Link the IoT hub and the provisioning service</span><span class="sxs-lookup"><span data-stu-id="62036-134">Link the IoT hub and the provisioning service</span></span>

<span data-ttu-id="62036-135">Link the IoT hub and your provisioning service with the [az iot dps linked-hub create](/cli/azure/iot/dps/linked-hub#az-iot-dps-linked-hub-create) command.</span><span class="sxs-lookup"><span data-stu-id="62036-135">Link the IoT hub and your provisioning service with the [az iot dps linked-hub create](/cli/azure/iot/dps/linked-hub#az-iot-dps-linked-hub-create) command.</span></span> 

<span data-ttu-id="62036-136">The following example links an IoT hub named *my-sample-hub* in the *westus* location and a Device Provisioning service named *my-sample-dps*.</span><span class="sxs-lookup"><span data-stu-id="62036-136">The following example links an IoT hub named *my-sample-hub* in the *westus* location and a Device Provisioning service named *my-sample-dps*.</span></span> <span data-ttu-id="62036-137">It uses the connection string for *my-sample-hub* stored in the *hubConnectionString* variable in the previous step.</span><span class="sxs-lookup"><span data-stu-id="62036-137">It uses the connection string for *my-sample-hub* stored in the *hubConnectionString* variable in the previous step.</span></span>

```azurecli-interactive 
az iot dps linked-hub create --dps-name my-sample-dps --resource-group my-sample-resource-group --connection-string $hubConnectionString --location westus
```

## <a name="verify-the-provisioning-service"></a><span data-ttu-id="62036-138">Verify the provisioning service</span><span class="sxs-lookup"><span data-stu-id="62036-138">Verify the provisioning service</span></span>

<span data-ttu-id="62036-139">Get the details of your provisioning service with the [az iot dps show](/cli/azure/iot/dps#az-iot-dps-show) command.</span><span class="sxs-lookup"><span data-stu-id="62036-139">Get the details of your provisioning service with the [az iot dps show](/cli/azure/iot/dps#az-iot-dps-show) command.</span></span>

<span data-ttu-id="62036-140">The following example gets the details of a provisioning service named *my-sample-dps*.</span><span class="sxs-lookup"><span data-stu-id="62036-140">The following example gets the details of a provisioning service named *my-sample-dps*.</span></span> <span data-ttu-id="62036-141">The linked IoT hub is shown in the *properties.iotHubs* collection.</span><span class="sxs-lookup"><span data-stu-id="62036-141">The linked IoT hub is shown in the *properties.iotHubs* collection.</span></span>

```azurecli-interactive
az iot dps show --name my-sample-dps
```

## <a name="clean-up-resources"></a><span data-ttu-id="62036-142">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="62036-142">Clean up resources</span></span>

<span data-ttu-id="62036-143">Other Quickstarts in this collection build upon this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="62036-143">Other Quickstarts in this collection build upon this Quickstart.</span></span> <span data-ttu-id="62036-144">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="62036-144">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="62036-145">If you do not plan to continue, you can use the following commands to delete the provisioning service, the IoT hub or the resource group and all of its resources.</span><span class="sxs-lookup"><span data-stu-id="62036-145">If you do not plan to continue, you can use the following commands to delete the provisioning service, the IoT hub or the resource group and all of its resources.</span></span>

<span data-ttu-id="62036-146">To delete the provisioning service, run the [az iot dps delete](/cli/azure/iot/dps#az-iot-dps-delete) command:</span><span class="sxs-lookup"><span data-stu-id="62036-146">To delete the provisioning service, run the [az iot dps delete](/cli/azure/iot/dps#az-iot-dps-delete) command:</span></span>

```azurecli-interactive
az iot dps delete --name my-sample-dps --resource-group my-sample-resource-group
```
<span data-ttu-id="62036-147">To delete the IoT hub, run the [az iot hub delete](/cli/azure/iot/hub#az-iot-hub-delete) command:</span><span class="sxs-lookup"><span data-stu-id="62036-147">To delete the IoT hub, run the [az iot hub delete](/cli/azure/iot/hub#az-iot-hub-delete) command:</span></span>

```azurecli-interactive
az iot hub delete --name my-sample-hub --resource-group my-sample-resource-group
```

<span data-ttu-id="62036-148">To delete a resource group and all its resources, run the [az group delete](/cli/azure/group#az-group-delete) command:</span><span class="sxs-lookup"><span data-stu-id="62036-148">To delete a resource group and all its resources, run the [az group delete](/cli/azure/group#az-group-delete) command:</span></span>

```azurecli-interactive
az group delete --name my-sample-resource-group
```

## <a name="next-steps"></a><span data-ttu-id="62036-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="62036-149">Next steps</span></span>

<span data-ttu-id="62036-150">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning Service instance, and linked the two resources.</span><span class="sxs-lookup"><span data-stu-id="62036-150">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning Service instance, and linked the two resources.</span></span> <span data-ttu-id="62036-151">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span><span class="sxs-lookup"><span data-stu-id="62036-151">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62036-152">Quickstart to create simulated device</span><span class="sxs-lookup"><span data-stu-id="62036-152">Quickstart to create simulated device</span></span>](./quick-create-simulated-device.md)

