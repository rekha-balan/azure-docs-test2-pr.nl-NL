---
title: Azure IoT Hub migrate to diagnostics settings | Microsoft Docs
description: How to update Azure IoT Hub to use Azure diagnostics settings instead of operations monitoring to monitor the status of operations on your IoT hub in real time.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 10/10/2017
ms.author: kgremban
ms.openlocfilehash: 85bdb4b4802283c591e4d7a9e8b14ae74fa44e8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967990"
---
# <a name="migrate-your-iot-hub-from-operations-monitoring-to-diagnostics-settings"></a><span data-ttu-id="cf658-103">Migrate your IoT Hub from operations monitoring to diagnostics settings</span><span class="sxs-lookup"><span data-stu-id="cf658-103">Migrate your IoT Hub from operations monitoring to diagnostics settings</span></span>

<span data-ttu-id="cf658-104">Customers using [operations monitoring][lnk-opsmon] to track the status of operations in IoT Hub can migrate that workflow to [Azure diagnostics settings][lnk-diagnostics-settings], a feature of Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="cf658-104">Customers using [operations monitoring][lnk-opsmon] to track the status of operations in IoT Hub can migrate that workflow to [Azure diagnostics settings][lnk-diagnostics-settings], a feature of Azure Monitor.</span></span> <span data-ttu-id="cf658-105">Diagnostics settings supply resource-level diagnostic information for many Azure services.</span><span class="sxs-lookup"><span data-stu-id="cf658-105">Diagnostics settings supply resource-level diagnostic information for many Azure services.</span></span>

<span data-ttu-id="cf658-106">The operations monitoring functionality of IoT Hub is deprecated, and will be removed in the future.</span><span class="sxs-lookup"><span data-stu-id="cf658-106">The operations monitoring functionality of IoT Hub is deprecated, and will be removed in the future.</span></span> <span data-ttu-id="cf658-107">This article provides steps to move your workloads from operations monitoring to diagnostics settings.</span><span class="sxs-lookup"><span data-stu-id="cf658-107">This article provides steps to move your workloads from operations monitoring to diagnostics settings.</span></span> <span data-ttu-id="cf658-108">For more information about the deprecation timeline, see [Monitor your Azure IoT solutions with Azure Monitor and Azure Resource Health][lnk-blog-announcement].</span><span class="sxs-lookup"><span data-stu-id="cf658-108">For more information about the deprecation timeline, see [Monitor your Azure IoT solutions with Azure Monitor and Azure Resource Health][lnk-blog-announcement].</span></span>

## <a name="update-iot-hub"></a><span data-ttu-id="cf658-109">Update IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf658-109">Update IoT Hub</span></span>

<span data-ttu-id="cf658-110">To update your IoT Hub in the Azure portal, first turn on diagnostics settings, then turn off operations monitoring.</span><span class="sxs-lookup"><span data-stu-id="cf658-110">To update your IoT Hub in the Azure portal, first turn on diagnostics settings, then turn off operations monitoring.</span></span>  

[!INCLUDE [iot-hub-diagnostics-settings](../../includes/iot-hub-diagnostics-settings.md)]

### <a name="turn-off-operations-monitoring"></a><span data-ttu-id="cf658-111">Turn off operations monitoring</span><span class="sxs-lookup"><span data-stu-id="cf658-111">Turn off operations monitoring</span></span>

<span data-ttu-id="cf658-112">Once you have tested the new diagnostics settings on your workflow, you can turn off the operations monitoring feature.</span><span class="sxs-lookup"><span data-stu-id="cf658-112">Once you have tested the new diagnostics settings on your workflow, you can turn off the operations monitoring feature.</span></span> 

1. <span data-ttu-id="cf658-113">In your IoT Hub menu, select **Operations monitoring**.</span><span class="sxs-lookup"><span data-stu-id="cf658-113">In your IoT Hub menu, select **Operations monitoring**.</span></span>
1. <span data-ttu-id="cf658-114">Under each monitoring category, select **None**.</span><span class="sxs-lookup"><span data-stu-id="cf658-114">Under each monitoring category, select **None**.</span></span>
1. <span data-ttu-id="cf658-115">Save the operations monitoring changes.</span><span class="sxs-lookup"><span data-stu-id="cf658-115">Save the operations monitoring changes.</span></span>

## <a name="update-applications-that-use-operations-monitoring"></a><span data-ttu-id="cf658-116">Update applications that use operations monitoring</span><span class="sxs-lookup"><span data-stu-id="cf658-116">Update applications that use operations monitoring</span></span>

<span data-ttu-id="cf658-117">The schemas for operations monitoring and diagnostics settings vary slightly.</span><span class="sxs-lookup"><span data-stu-id="cf658-117">The schemas for operations monitoring and diagnostics settings vary slightly.</span></span> <span data-ttu-id="cf658-118">It's important that you update the applications that use operations monitoring today to map to the schema used by diagnostics settings.</span><span class="sxs-lookup"><span data-stu-id="cf658-118">It's important that you update the applications that use operations monitoring today to map to the schema used by diagnostics settings.</span></span> 

<span data-ttu-id="cf658-119">Also, diagnostics settings offers tracking for five new categories.</span><span class="sxs-lookup"><span data-stu-id="cf658-119">Also, diagnostics settings offers tracking for five new categories.</span></span> <span data-ttu-id="cf658-120">After you update applications for the existing schema, add the new categories as well:</span><span class="sxs-lookup"><span data-stu-id="cf658-120">After you update applications for the existing schema, add the new categories as well:</span></span>

- <span data-ttu-id="cf658-121">Cloud-to-device twin operations</span><span class="sxs-lookup"><span data-stu-id="cf658-121">Cloud-to-device twin operations</span></span>
- <span data-ttu-id="cf658-122">Device-to-cloud twin operations</span><span class="sxs-lookup"><span data-stu-id="cf658-122">Device-to-cloud twin operations</span></span>
- <span data-ttu-id="cf658-123">Twin queries</span><span class="sxs-lookup"><span data-stu-id="cf658-123">Twin queries</span></span>
- <span data-ttu-id="cf658-124">Jobs operations</span><span class="sxs-lookup"><span data-stu-id="cf658-124">Jobs operations</span></span>
- <span data-ttu-id="cf658-125">Direct Methods</span><span class="sxs-lookup"><span data-stu-id="cf658-125">Direct Methods</span></span>

<span data-ttu-id="cf658-126">For the specific schema structures, see [Understand the schema for diagnostics settings][lnk-diagnostics-schema].</span><span class="sxs-lookup"><span data-stu-id="cf658-126">For the specific schema structures, see [Understand the schema for diagnostics settings][lnk-diagnostics-schema].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf658-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf658-127">Next steps</span></span>

- <span data-ttu-id="cf658-128">[Monitor the health of Azure IoT Hub and diagnose problems quickly][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="cf658-128">[Monitor the health of Azure IoT Hub and diagnose problems quickly][lnk-monitor]</span></span>

[lnk-opsmon]: iot-hub-operations-monitoring.md
[lnk-diagnostics-settings]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[lnk-diagnostics-schema]: iot-hub-monitor-resource-health.md#understand-the-logs
[lnk-blog-announcement]: https://azure.microsoft.com/blog/monitor-your-azure-iot-solutions-with-azure-monitor-and-azure-resource-health/
[lnk-monitor]: iot-hub-monitor-resource-health.md
