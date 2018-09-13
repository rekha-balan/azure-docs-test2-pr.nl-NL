---
title: Azure IoT Hub IP connection filters | Microsoft Docs
description: How to use IP filtering to block connections from specific IP addresses for to your Azure IoT hub. You can block connections from individual or ranges of IP addresses.
services: iot-hub
documentationcenter: ''
author: BeatriceOltean
manager: timlt
editor: ''
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: boltean
ms.openlocfilehash: 45ad392aa5256471ce03a68c536bc9bf74135921
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661122"
---
# <a name="use-ip-filters"></a><span data-ttu-id="662d2-104">Use IP filters</span><span class="sxs-lookup"><span data-stu-id="662d2-104">Use IP filters</span></span>

<span data-ttu-id="662d2-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="662d2-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="662d2-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span><span class="sxs-lookup"><span data-stu-id="662d2-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="662d2-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span><span class="sxs-lookup"><span data-stu-id="662d2-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="662d2-108">When to use</span><span class="sxs-lookup"><span data-stu-id="662d2-108">When to use</span></span>

<span data-ttu-id="662d2-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span><span class="sxs-lookup"><span data-stu-id="662d2-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="662d2-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span><span class="sxs-lookup"><span data-stu-id="662d2-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="662d2-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="662d2-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="662d2-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span><span class="sxs-lookup"><span data-stu-id="662d2-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="662d2-113">How filter rules are applied</span><span class="sxs-lookup"><span data-stu-id="662d2-113">How filter rules are applied</span></span>

<span data-ttu-id="662d2-114">The IP filter rules are applied at the IoT Hub service level.</span><span class="sxs-lookup"><span data-stu-id="662d2-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="662d2-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span><span class="sxs-lookup"><span data-stu-id="662d2-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="662d2-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span><span class="sxs-lookup"><span data-stu-id="662d2-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="662d2-117">The response message does not mention the IP rule.</span><span class="sxs-lookup"><span data-stu-id="662d2-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="662d2-118">Default setting</span><span class="sxs-lookup"><span data-stu-id="662d2-118">Default setting</span></span>

<span data-ttu-id="662d2-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span><span class="sxs-lookup"><span data-stu-id="662d2-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="662d2-120">This default setting means that your hub accepts connections any IP address.</span><span class="sxs-lookup"><span data-stu-id="662d2-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="662d2-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span><span class="sxs-lookup"><span data-stu-id="662d2-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![IoT Hub default IP filter settings][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="662d2-123">Add or edit an IP filter rule</span><span class="sxs-lookup"><span data-stu-id="662d2-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="662d2-124">When you add an IP filter rule, you are prompted for the following values:</span><span class="sxs-lookup"><span data-stu-id="662d2-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="662d2-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span><span class="sxs-lookup"><span data-stu-id="662d2-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="662d2-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span><span class="sxs-lookup"><span data-stu-id="662d2-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="662d2-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span><span class="sxs-lookup"><span data-stu-id="662d2-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="662d2-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="662d2-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="662d2-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="662d2-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Add an IP filter rule to an IoT hub][img-ip-filter-add-rule]

<span data-ttu-id="662d2-131">After you save the rule, you see an alert notifying you that the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="662d2-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notification about saving an IP filter rule][img-ip-filter-save-new-rule]

<span data-ttu-id="662d2-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span><span class="sxs-lookup"><span data-stu-id="662d2-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="662d2-134">You can edit an existing rule by double-clicking the row that contains the rule.</span><span class="sxs-lookup"><span data-stu-id="662d2-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="662d2-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="662d2-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="662d2-136">Delete an IP filter rule</span><span class="sxs-lookup"><span data-stu-id="662d2-136">Delete an IP filter rule</span></span>

<span data-ttu-id="662d2-137">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="662d2-137">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Delete an IoT Hub IP filter rule][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="662d2-139">IP filter rule evaluation</span><span class="sxs-lookup"><span data-stu-id="662d2-139">IP filter rule evaluation</span></span>

<span data-ttu-id="662d2-140">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span><span class="sxs-lookup"><span data-stu-id="662d2-140">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="662d2-141">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="662d2-141">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="662d2-142">The next rule should reject all addresses by using the range 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="662d2-142">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="662d2-143">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span><span class="sxs-lookup"><span data-stu-id="662d2-143">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="662d2-144">To save your new IP filter rule order, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="662d2-144">To save your new IP filter rule order, click **Save**.</span></span>

![Change the order of your IoT Hub IP filter rules][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="662d2-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="662d2-146">Next steps</span></span>

<span data-ttu-id="662d2-147">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="662d2-147">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="662d2-148">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="662d2-148">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="662d2-149">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="662d2-149">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md




