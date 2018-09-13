---
title: Azure IoT Hub IP connection filters | Microsoft Docs
description: How to use IP filtering to block connections from specific IP addresses for to your Azure IoT hub. You can block connections from individual or ranges of IP addresses.
author: rezasherafat
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 05/23/2017
ms.author: rezas
ms.openlocfilehash: 864af9cae35912d95f2c0bf0b574a5ca2404a608
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825448"
---
# <a name="use-ip-filters"></a><span data-ttu-id="e587c-104">Use IP filters</span><span class="sxs-lookup"><span data-stu-id="e587c-104">Use IP filters</span></span>

<span data-ttu-id="e587c-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e587c-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="e587c-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span><span class="sxs-lookup"><span data-stu-id="e587c-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="e587c-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span><span class="sxs-lookup"><span data-stu-id="e587c-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="e587c-108">When to use</span><span class="sxs-lookup"><span data-stu-id="e587c-108">When to use</span></span>

<span data-ttu-id="e587c-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span><span class="sxs-lookup"><span data-stu-id="e587c-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="e587c-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span><span class="sxs-lookup"><span data-stu-id="e587c-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="e587c-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e587c-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="e587c-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span><span class="sxs-lookup"><span data-stu-id="e587c-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="e587c-113">How filter rules are applied</span><span class="sxs-lookup"><span data-stu-id="e587c-113">How filter rules are applied</span></span>

<span data-ttu-id="e587c-114">The IP filter rules are applied at the IoT Hub service level.</span><span class="sxs-lookup"><span data-stu-id="e587c-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="e587c-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span><span class="sxs-lookup"><span data-stu-id="e587c-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="e587c-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span><span class="sxs-lookup"><span data-stu-id="e587c-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="e587c-117">The response message does not mention the IP rule.</span><span class="sxs-lookup"><span data-stu-id="e587c-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="e587c-118">Default setting</span><span class="sxs-lookup"><span data-stu-id="e587c-118">Default setting</span></span>

<span data-ttu-id="e587c-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span><span class="sxs-lookup"><span data-stu-id="e587c-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="e587c-120">This default setting means that your hub accepts connections any IP address.</span><span class="sxs-lookup"><span data-stu-id="e587c-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="e587c-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span><span class="sxs-lookup"><span data-stu-id="e587c-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![IoT Hub default IP filter settings][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="e587c-123">Add or edit an IP filter rule</span><span class="sxs-lookup"><span data-stu-id="e587c-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="e587c-124">When you add an IP filter rule, you are prompted for the following values:</span><span class="sxs-lookup"><span data-stu-id="e587c-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="e587c-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span><span class="sxs-lookup"><span data-stu-id="e587c-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="e587c-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span><span class="sxs-lookup"><span data-stu-id="e587c-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="e587c-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span><span class="sxs-lookup"><span data-stu-id="e587c-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="e587c-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="e587c-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="e587c-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="e587c-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Add an IP filter rule to an IoT hub][img-ip-filter-add-rule]

<span data-ttu-id="e587c-131">After you save the rule, you see an alert notifying you that the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="e587c-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notification about saving an IP filter rule][img-ip-filter-save-new-rule]

<span data-ttu-id="e587c-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span><span class="sxs-lookup"><span data-stu-id="e587c-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="e587c-134">You can edit an existing rule by double-clicking the row that contains the rule.</span><span class="sxs-lookup"><span data-stu-id="e587c-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="e587c-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e587c-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="e587c-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span><span class="sxs-lookup"><span data-stu-id="e587c-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="e587c-137">Delete an IP filter rule</span><span class="sxs-lookup"><span data-stu-id="e587c-137">Delete an IP filter rule</span></span>

<span data-ttu-id="e587c-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e587c-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Delete an IoT Hub IP filter rule][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="e587c-140">IP filter rule evaluation</span><span class="sxs-lookup"><span data-stu-id="e587c-140">IP filter rule evaluation</span></span>

<span data-ttu-id="e587c-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span><span class="sxs-lookup"><span data-stu-id="e587c-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="e587c-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="e587c-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="e587c-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="e587c-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="e587c-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span><span class="sxs-lookup"><span data-stu-id="e587c-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="e587c-145">To save your new IP filter rule order, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e587c-145">To save your new IP filter rule order, click **Save**.</span></span>

![Change the order of your IoT Hub IP filter rules][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="e587c-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="e587c-147">Next steps</span></span>

<span data-ttu-id="e587c-148">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="e587c-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="e587c-149">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="e587c-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="e587c-150">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="e587c-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md
