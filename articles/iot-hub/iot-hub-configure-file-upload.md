---
title: Use the Azure portal to configure file upload | Microsoft Docs
description: How to use the Azure portal to configure your IoT hub to enable file uploads from connected devices. Includes information about configuring the destination Azure storage account.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: a9f9eeaed2716c5d492099568fd6f90080471af2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775404"
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="057b4-104">Configure IoT Hub file uploads using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="057b4-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="057b4-105">File upload</span><span class="sxs-lookup"><span data-stu-id="057b4-105">File upload</span></span>

<span data-ttu-id="057b4-106">To use the [file upload functionality in IoT Hub](iot-hub-devguide-file-upload.md), you must first associate an Azure Storage account with your hub.</span><span class="sxs-lookup"><span data-stu-id="057b4-106">To use the [file upload functionality in IoT Hub](iot-hub-devguide-file-upload.md), you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="057b4-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span><span class="sxs-lookup"><span data-stu-id="057b4-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![View IoT Hub file upload settings in the portal](./media/iot-hub-configure-file-upload/file-upload-settings.png)

* <span data-ttu-id="057b4-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="057b4-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="057b4-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span><span class="sxs-lookup"><span data-stu-id="057b4-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="057b4-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span><span class="sxs-lookup"><span data-stu-id="057b4-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

   ![View storage containers for file upload in the portal](./media/iot-hub-configure-file-upload/file-upload-container-selection.png)

* <span data-ttu-id="057b4-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span><span class="sxs-lookup"><span data-stu-id="057b4-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

* <span data-ttu-id="057b4-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="057b4-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="057b4-115">Set to one hour by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="057b4-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

* <span data-ttu-id="057b4-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span><span class="sxs-lookup"><span data-stu-id="057b4-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="057b4-117">Set to one day by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="057b4-117">Set to one day by default but can be customized to other values using the slider.</span></span>

* <span data-ttu-id="057b4-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span><span class="sxs-lookup"><span data-stu-id="057b4-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="057b4-119">Set to 10 by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="057b4-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

   ![Configure IoT Hub file upload in the portal](./media/iot-hub-configure-file-upload/file-upload-selected-container.png)

## <a name="next-steps"></a><span data-ttu-id="057b4-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="057b4-121">Next steps</span></span>

<span data-ttu-id="057b4-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device](iot-hub-devguide-file-upload.md) in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="057b4-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device](iot-hub-devguide-file-upload.md) in the IoT Hub developer guide.</span></span>

<span data-ttu-id="057b4-123">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="057b4-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* [<span data-ttu-id="057b4-124">Bulk manage IoT devices</span><span class="sxs-lookup"><span data-stu-id="057b4-124">Bulk manage IoT devices</span></span>](iot-hub-bulk-identity-mgmt.md)
* [<span data-ttu-id="057b4-125">IoT Hub metrics</span><span class="sxs-lookup"><span data-stu-id="057b4-125">IoT Hub metrics</span></span>](iot-hub-metrics.md)
* [<span data-ttu-id="057b4-126">Operations monitoring</span><span class="sxs-lookup"><span data-stu-id="057b4-126">Operations monitoring</span></span>](iot-hub-operations-monitoring.md)

<span data-ttu-id="057b4-127">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="057b4-127">To further explore the capabilities of IoT Hub, see:</span></span>

* [<span data-ttu-id="057b4-128">IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="057b4-128">IoT Hub developer guide</span></span>](iot-hub-devguide.md)
* [<span data-ttu-id="057b4-129">Deploying AI to edge devices with Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="057b4-129">Deploying AI to edge devices with Azure IoT Edge</span></span>](../iot-edge/tutorial-simulate-device-linux.md)
* [<span data-ttu-id="057b4-130">Secure your IoT solution from the ground up</span><span class="sxs-lookup"><span data-stu-id="057b4-130">Secure your IoT solution from the ground up</span></span>](../iot-fundamentals/iot-security-ground-up.md)
