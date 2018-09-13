---
title: Microsoft Azure IoT Suite overview | Microsoft Docs
description: Overview of how Azure IoT Suite delivers internet of things preconfigured solutions to collect, analyze, and store data, provide visualizations, and integrate with other systems.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ecae2cb9c0cdc78226c100cd287b840b6b2a6bb8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550808"
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="93155-103">Overview of Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="93155-103">Overview of Azure IoT Suite</span></span>
<span data-ttu-id="93155-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span><span class="sxs-lookup"><span data-stu-id="93155-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="93155-105">These enterprise grade services enable you to:</span><span class="sxs-lookup"><span data-stu-id="93155-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="93155-106">Collect data from devices</span><span class="sxs-lookup"><span data-stu-id="93155-106">Collect data from devices</span></span>
* <span data-ttu-id="93155-107">Analyze data streams in-motion</span><span class="sxs-lookup"><span data-stu-id="93155-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="93155-108">Store and query large data sets</span><span class="sxs-lookup"><span data-stu-id="93155-108">Store and query large data sets</span></span>
* <span data-ttu-id="93155-109">Visualize both real-time and historical data</span><span class="sxs-lookup"><span data-stu-id="93155-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="93155-110">Integrate with back-office systems</span><span class="sxs-lookup"><span data-stu-id="93155-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="93155-111">Manage your devices</span><span class="sxs-lookup"><span data-stu-id="93155-111">Manage your devices</span></span>

<span data-ttu-id="93155-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span><span class="sxs-lookup"><span data-stu-id="93155-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="93155-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="93155-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="93155-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span><span class="sxs-lookup"><span data-stu-id="93155-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="93155-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="93155-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="93155-116">The following video provides an introduction to Azure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="93155-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="93155-117">Azure IoT services in Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="93155-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="93155-118">The preconfigured solutions typically use the following services:</span><span class="sxs-lookup"><span data-stu-id="93155-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="93155-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span><span class="sxs-lookup"><span data-stu-id="93155-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="93155-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span><span class="sxs-lookup"><span data-stu-id="93155-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="93155-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span><span class="sxs-lookup"><span data-stu-id="93155-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="93155-122">The service also enables you to [manage your devices][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="93155-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="93155-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span><span class="sxs-lookup"><span data-stu-id="93155-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="93155-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span><span class="sxs-lookup"><span data-stu-id="93155-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="93155-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span><span class="sxs-lookup"><span data-stu-id="93155-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="93155-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span><span class="sxs-lookup"><span data-stu-id="93155-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="93155-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span><span class="sxs-lookup"><span data-stu-id="93155-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="93155-128">[Azure Storage][lnk-azure-storage] and [Azure DocumentDB][lnk-document-db] provide the data storage capabilities.</span><span class="sxs-lookup"><span data-stu-id="93155-128">[Azure Storage][lnk-azure-storage] and [Azure DocumentDB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="93155-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span><span class="sxs-lookup"><span data-stu-id="93155-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="93155-130">The solutions use DocumentDB to store device metadata and enable the device management capabilities of the solutions.</span><span class="sxs-lookup"><span data-stu-id="93155-130">The solutions use DocumentDB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="93155-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span><span class="sxs-lookup"><span data-stu-id="93155-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="93155-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span><span class="sxs-lookup"><span data-stu-id="93155-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="93155-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="93155-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="93155-134">Preconfigured solutions</span><span class="sxs-lookup"><span data-stu-id="93155-134">Preconfigured solutions</span></span>
<span data-ttu-id="93155-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as *Remote monitoring* and *Predictive maintenance*.</span><span class="sxs-lookup"><span data-stu-id="93155-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as *Remote monitoring* and *Predictive maintenance*.</span></span> <span data-ttu-id="93155-136">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span><span class="sxs-lookup"><span data-stu-id="93155-136">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93155-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="93155-137">Next steps</span></span>
<span data-ttu-id="93155-138">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="93155-138">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="93155-139">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="93155-139">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
