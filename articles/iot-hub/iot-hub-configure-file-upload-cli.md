---
title: Configure file upload to IoT Hub using Azure CLI | Microsoft Docs
description: How to configure file uploads to Azure IoT Hub using the cross-platform Azure CLI.
author: dominicbetts
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6cd0b657c8d0352c41e0da538396b166d633306a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870354"
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="63a2b-103">Configure IoT Hub file uploads using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="63a2b-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="63a2b-104">To [upload files from a device](iot-hub-devguide-file-upload.md), you must first associate an Azure Storage account with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-104">To [upload files from a device](iot-hub-devguide-file-upload.md), you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="63a2b-105">You can use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="63a2b-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="63a2b-106">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="63a2b-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="63a2b-107">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="63a2b-107">An active Azure account.</span></span> <span data-ttu-id="63a2b-108">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="63a2b-108">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>

* <span data-ttu-id="63a2b-109">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="63a2b-109">[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

* <span data-ttu-id="63a2b-110">An Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-110">An Azure IoT hub.</span></span> <span data-ttu-id="63a2b-111">If you don't have an IoT hub, you can use the [`az iot hub create` command](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-create) to create one or [Create an IoT hub using the portal](iot-hub-create-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63a2b-111">If you don't have an IoT hub, you can use the [`az iot hub create` command](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-create) to create one or [Create an IoT hub using the portal](iot-hub-create-through-portal.md).</span></span>

* <span data-ttu-id="63a2b-112">An Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="63a2b-112">An Azure Storage account.</span></span> <span data-ttu-id="63a2b-113">If you don't have an Azure Storage account, you can use the [Azure CLI - Manage storage accounts](../storage/common/storage-azure-cli.md#manage-storage-accounts) to create one or use the portal to [Create a storage account](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="63a2b-113">If you don't have an Azure Storage account, you can use the [Azure CLI - Manage storage accounts](../storage/common/storage-azure-cli.md#manage-storage-accounts) to create one or use the portal to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="63a2b-114">Sign in and set your Azure account</span><span class="sxs-lookup"><span data-stu-id="63a2b-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="63a2b-115">Sign in to your Azure account and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="63a2b-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="63a2b-116">At the command prompt, run the [login command](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest):</span><span class="sxs-lookup"><span data-stu-id="63a2b-116">At the command prompt, run the [login command](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest):</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="63a2b-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span><span class="sxs-lookup"><span data-stu-id="63a2b-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="63a2b-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="63a2b-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="63a2b-119">Use the following [command to list the Azure accounts](https://docs.microsoft.com/cli/azure/account) available for you to use:</span><span class="sxs-lookup"><span data-stu-id="63a2b-119">Use the following [command to list the Azure accounts](https://docs.microsoft.com/cli/azure/account) available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="63a2b-120">Use the following command to select the subscription that you want to use to run the commands to create your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-120">Use the following command to select the subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="63a2b-121">You can use either the subscription name or ID from the output of the previous command:</span><span class="sxs-lookup"><span data-stu-id="63a2b-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="63a2b-122">Retrieve your storage account details</span><span class="sxs-lookup"><span data-stu-id="63a2b-122">Retrieve your storage account details</span></span>

<span data-ttu-id="63a2b-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span><span class="sxs-lookup"><span data-stu-id="63a2b-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="63a2b-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="63a2b-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="63a2b-125">The storage account must be in the same subscription as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="63a2b-126">You also need the name of a blob container in the storage account.</span><span class="sxs-lookup"><span data-stu-id="63a2b-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="63a2b-127">Use the following command to retrieve your storage account keys:</span><span class="sxs-lookup"><span data-stu-id="63a2b-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} \
  --resource-group {your storage account resource group}
```

<span data-ttu-id="63a2b-128">Make a note of the **connectionString** value.</span><span class="sxs-lookup"><span data-stu-id="63a2b-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="63a2b-129">You need it in the following steps.</span><span class="sxs-lookup"><span data-stu-id="63a2b-129">You need it in the following steps.</span></span>

<span data-ttu-id="63a2b-130">You can either use an existing blob container for your file uploads or create a new one:</span><span class="sxs-lookup"><span data-stu-id="63a2b-130">You can either use an existing blob container for your file uploads or create a new one:</span></span>

* <span data-ttu-id="63a2b-131">To list the existing blob containers in your storage account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="63a2b-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="63a2b-132">To create a blob container in your storage account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="63a2b-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} \
      --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="63a2b-133">File upload</span><span class="sxs-lookup"><span data-stu-id="63a2b-133">File upload</span></span>

<span data-ttu-id="63a2b-134">You can now configure your IoT hub to enable the ability to [upload files to the IoT hub](iot-hub-devguide-file-upload.md) using your storage account details.</span><span class="sxs-lookup"><span data-stu-id="63a2b-134">You can now configure your IoT hub to enable the ability to [upload files to the IoT hub](iot-hub-devguide-file-upload.md) using your storage account details.</span></span>

<span data-ttu-id="63a2b-135">The configuration requires the following values:</span><span class="sxs-lookup"><span data-stu-id="63a2b-135">The configuration requires the following values:</span></span>

* <span data-ttu-id="63a2b-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="63a2b-137">You retrieved the necessary storage account information in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="63a2b-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="63a2b-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span><span class="sxs-lookup"><span data-stu-id="63a2b-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

* <span data-ttu-id="63a2b-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span><span class="sxs-lookup"><span data-stu-id="63a2b-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

* <span data-ttu-id="63a2b-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="63a2b-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="63a2b-141">Set to one hour by default.</span><span class="sxs-lookup"><span data-stu-id="63a2b-141">Set to one hour by default.</span></span>

* <span data-ttu-id="63a2b-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span><span class="sxs-lookup"><span data-stu-id="63a2b-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="63a2b-143">Set to one day by default.</span><span class="sxs-lookup"><span data-stu-id="63a2b-143">Set to one day by default.</span></span>

* <span data-ttu-id="63a2b-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span><span class="sxs-lookup"><span data-stu-id="63a2b-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="63a2b-145">Set to 10 by default.</span><span class="sxs-lookup"><span data-stu-id="63a2b-145">Set to 10 by default.</span></span>

<span data-ttu-id="63a2b-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="63a2b-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<!--Robinsh this is out of date, add cloud powershell -->

<span data-ttu-id="63a2b-147">In a bash shell, use:</span><span class="sxs-lookup"><span data-stu-id="63a2b-147">In a bash shell, use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} \
  --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"

az iot hub update --name {your iot hub name} \
  --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"

az iot hub update --name {your iot hub name} \
  --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} \
  --set properties.enableFileUploadNotifications=true

az iot hub update --name {your iot hub name} \
  --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10

az iot hub update --name {your iot hub name} \
  --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="63a2b-148">You can review the file upload configuration on your IoT hub using the following command:</span><span class="sxs-lookup"><span data-stu-id="63a2b-148">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="63a2b-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="63a2b-149">Next steps</span></span>

<span data-ttu-id="63a2b-150">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device](iot-hub-devguide-file-upload.md).</span><span class="sxs-lookup"><span data-stu-id="63a2b-150">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device](iot-hub-devguide-file-upload.md).</span></span>

<span data-ttu-id="63a2b-151">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="63a2b-151">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* [<span data-ttu-id="63a2b-152">Bulk manage IoT devices</span><span class="sxs-lookup"><span data-stu-id="63a2b-152">Bulk manage IoT devices</span></span>](iot-hub-bulk-identity-mgmt.md)
* [<span data-ttu-id="63a2b-153">IoT Hub metrics</span><span class="sxs-lookup"><span data-stu-id="63a2b-153">IoT Hub metrics</span></span>](iot-hub-metrics.md)
* [<span data-ttu-id="63a2b-154">Operations monitoring</span><span class="sxs-lookup"><span data-stu-id="63a2b-154">Operations monitoring</span></span>](iot-hub-operations-monitoring.md)

<span data-ttu-id="63a2b-155">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="63a2b-155">To further explore the capabilities of IoT Hub, see:</span></span>

* [<span data-ttu-id="63a2b-156">IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="63a2b-156">IoT Hub developer guide</span></span>](iot-hub-devguide.md)
* [<span data-ttu-id="63a2b-157">Deploying AI to edge devices with Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="63a2b-157">Deploying AI to edge devices with Azure IoT Edge</span></span>](../iot-edge/tutorial-simulate-device-linux.md)
* [<span data-ttu-id="63a2b-158">Secure your IoT solution from the ground up</span><span class="sxs-lookup"><span data-stu-id="63a2b-158">Secure your IoT solution from the ground up</span></span>](../iot-fundamentals/iot-security-ground-up.md)
