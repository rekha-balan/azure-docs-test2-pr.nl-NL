---
title: Use the Azure portal to configure file upload | Microsoft Docs
description: How to use the Azure portal to configure your IoT hub to enable file uploads from connected devices. Includes information about configuring the destination Azure storage account.
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
ms.date: 04/07/2017
ms.author: dobett
ms.openlocfilehash: 35ec83e47a2e2f6d597eec9848b41f9bc1a1d118
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552227"
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="8b43f-104">Configure IoT Hub file uploads using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8b43f-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="8b43f-105">File upload</span><span class="sxs-lookup"><span data-stu-id="8b43f-105">File upload</span></span>

<span data-ttu-id="8b43f-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span><span class="sxs-lookup"><span data-stu-id="8b43f-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="8b43f-107">Select the **File upload** settings to display a list of file upload properties for the IoT hub that is being modified.</span><span class="sxs-lookup"><span data-stu-id="8b43f-107">Select the **File upload** settings to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![View IoT Hub file upload settings in the portal][13]

<span data-ttu-id="8b43f-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b43f-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="8b43f-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span><span class="sxs-lookup"><span data-stu-id="8b43f-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="8b43f-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span><span class="sxs-lookup"><span data-stu-id="8b43f-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![View storage containers for file upload in the portal][14]

<span data-ttu-id="8b43f-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span><span class="sxs-lookup"><span data-stu-id="8b43f-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="8b43f-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b43f-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="8b43f-115">Set to one hour by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="8b43f-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="8b43f-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span><span class="sxs-lookup"><span data-stu-id="8b43f-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="8b43f-117">Set to one day by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="8b43f-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="8b43f-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span><span class="sxs-lookup"><span data-stu-id="8b43f-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="8b43f-119">Set to 10 by default but can be customized to other values using the slider.</span><span class="sxs-lookup"><span data-stu-id="8b43f-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Configure IoT Hub file upload in the portal][15]

## <a name="next-steps"></a><span data-ttu-id="8b43f-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b43f-121">Next steps</span></span>

<span data-ttu-id="8b43f-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="8b43f-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="8b43f-123">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="8b43f-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="8b43f-124">[Bulk manage IoT devices][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="8b43f-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="8b43f-125">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="8b43f-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="8b43f-126">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="8b43f-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="8b43f-127">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="8b43f-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8b43f-128">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8b43f-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8b43f-129">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="8b43f-129">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>
* <span data-ttu-id="8b43f-130">[Secure your IoT solution from the ground up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="8b43f-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md



