---
title: Use the Azure PowerShell to configure file upload | Microsoft Docs
description: How to use the Azure PowerShell cmdlets to configure your IoT hub to enable file uploads from connected devices. Includes information about configuring the destination Azure storage account.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: dobett
ms.openlocfilehash: 5ae6057dbcbffa5d8496819d015ec060d7ca6cc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661263"
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="33bf0-104">Configure IoT Hub file uploads using PowerShell</span><span class="sxs-lookup"><span data-stu-id="33bf0-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="33bf0-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="33bf0-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="33bf0-106">You can use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="33bf0-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="33bf0-107">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="33bf0-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="33bf0-108">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="33bf0-108">An active Azure account.</span></span> <span data-ttu-id="33bf0-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="33bf0-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="33bf0-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="33bf0-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="33bf0-111">An Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="33bf0-111">An Azure IoT hub.</span></span> <span data-ttu-id="33bf0-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="33bf0-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="33bf0-113">An Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="33bf0-113">An Azure storage account.</span></span> <span data-ttu-id="33bf0-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="33bf0-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="33bf0-115">Sign in and set your Azure account</span><span class="sxs-lookup"><span data-stu-id="33bf0-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="33bf0-116">Sign in to your Azure account and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="33bf0-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="33bf0-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="33bf0-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="33bf0-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="33bf0-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="33bf0-119">Use the following command to list the Azure subscriptions available for you to use:</span><span class="sxs-lookup"><span data-stu-id="33bf0-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="33bf0-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="33bf0-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="33bf0-121">You can use either the subscription name or ID from the output of the previous command:</span><span class="sxs-lookup"><span data-stu-id="33bf0-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="33bf0-122">Retrieve your storage account details</span><span class="sxs-lookup"><span data-stu-id="33bf0-122">Retrieve your storage account details</span></span>

<span data-ttu-id="33bf0-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span><span class="sxs-lookup"><span data-stu-id="33bf0-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="33bf0-124">You need the connection string of an Azure storage account in the same subscription as your IoT hub to configure file uploads from your devices.</span><span class="sxs-lookup"><span data-stu-id="33bf0-124">You need the connection string of an Azure storage account in the same subscription as your IoT hub to configure file uploads from your devices.</span></span> <span data-ttu-id="33bf0-125">You also need the name of a blob container in the storage account.</span><span class="sxs-lookup"><span data-stu-id="33bf0-125">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="33bf0-126">Use the following command to retrieve your storage account keys:</span><span class="sxs-lookup"><span data-stu-id="33bf0-126">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="33bf0-127">Make a note of the **key1** storage account key value.</span><span class="sxs-lookup"><span data-stu-id="33bf0-127">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="33bf0-128">You need it in the following steps.</span><span class="sxs-lookup"><span data-stu-id="33bf0-128">You need it in the following steps.</span></span>

<span data-ttu-id="33bf0-129">You can either use an existing blob container for your file uploads or create new one:</span><span class="sxs-lookup"><span data-stu-id="33bf0-129">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="33bf0-130">To list the existing blob containers in your storage account, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="33bf0-130">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="33bf0-131">To create a blob container in your storage account, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="33bf0-131">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="33bf0-132">Configure your IoT hub</span><span class="sxs-lookup"><span data-stu-id="33bf0-132">Configure your IoT hub</span></span>

<span data-ttu-id="33bf0-133">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span><span class="sxs-lookup"><span data-stu-id="33bf0-133">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="33bf0-134">The configuration requires the following values:</span><span class="sxs-lookup"><span data-stu-id="33bf0-134">The configuration requires the following values:</span></span>

<span data-ttu-id="33bf0-135">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="33bf0-135">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="33bf0-136">You retrieved the necessary storage account information in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="33bf0-136">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="33bf0-137">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span><span class="sxs-lookup"><span data-stu-id="33bf0-137">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="33bf0-138">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span><span class="sxs-lookup"><span data-stu-id="33bf0-138">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="33bf0-139">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33bf0-139">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="33bf0-140">Set to one hour by default.</span><span class="sxs-lookup"><span data-stu-id="33bf0-140">Set to one hour by default.</span></span>

<span data-ttu-id="33bf0-141">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span><span class="sxs-lookup"><span data-stu-id="33bf0-141">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="33bf0-142">Set to one day by default.</span><span class="sxs-lookup"><span data-stu-id="33bf0-142">Set to one day by default.</span></span>

<span data-ttu-id="33bf0-143">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span><span class="sxs-lookup"><span data-stu-id="33bf0-143">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="33bf0-144">Set to 10 by default.</span><span class="sxs-lookup"><span data-stu-id="33bf0-144">Set to 10 by default.</span></span>

<span data-ttu-id="33bf0-145">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="33bf0-145">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a><span data-ttu-id="33bf0-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="33bf0-146">Next steps</span></span>
<span data-ttu-id="33bf0-147">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="33bf0-147">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="33bf0-148">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="33bf0-148">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="33bf0-149">[Bulk manage IoT devices][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="33bf0-149">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="33bf0-150">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="33bf0-150">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="33bf0-151">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="33bf0-151">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="33bf0-152">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="33bf0-152">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="33bf0-153">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="33bf0-153">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="33bf0-154">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="33bf0-154">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>
* <span data-ttu-id="33bf0-155">[Secure your IoT solution from the ground up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="33bf0-155">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azureps-cmdlets-docs/
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.iothub/v1.1.0/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]: ../storage/storage-create-storage-account.md