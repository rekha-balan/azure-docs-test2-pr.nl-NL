---
title: Custom tracking schemas for B2B monitoring - Azure Logic Apps | Microsoft Docs
description: Create custom tracking schemas to monitor B2B messages from transactions in your Azure Integration Account.
author: padmavc
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a663a4e79c30b97e6390b7ff7f83deec131384a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556514"
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="55c8f-103">Enable tracking to monitor your complete workflow, end-to-end</span><span class="sxs-lookup"><span data-stu-id="55c8f-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="55c8f-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span><span class="sxs-lookup"><span data-stu-id="55c8f-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="55c8f-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span><span class="sxs-lookup"><span data-stu-id="55c8f-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="55c8f-106">This topic provides custom code that you can use in the layers outside of your logic app.</span><span class="sxs-lookup"><span data-stu-id="55c8f-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="55c8f-107">Custom tracking schema</span><span class="sxs-lookup"><span data-stu-id="55c8f-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="55c8f-108">Property</span><span class="sxs-lookup"><span data-stu-id="55c8f-108">Property</span></span> | <span data-ttu-id="55c8f-109">Type</span><span class="sxs-lookup"><span data-stu-id="55c8f-109">Type</span></span> | <span data-ttu-id="55c8f-110">Description</span><span class="sxs-lookup"><span data-stu-id="55c8f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55c8f-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="55c8f-111">sourceType</span></span> |   | <span data-ttu-id="55c8f-112">Type of the run source.</span><span class="sxs-lookup"><span data-stu-id="55c8f-112">Type of the run source.</span></span> <span data-ttu-id="55c8f-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span><span class="sxs-lookup"><span data-stu-id="55c8f-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="55c8f-114">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-114">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-115">Source</span><span class="sxs-lookup"><span data-stu-id="55c8f-115">Source</span></span> |   | <span data-ttu-id="55c8f-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span><span class="sxs-lookup"><span data-stu-id="55c8f-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="55c8f-117">If the source type is **custom**, the schema is a JToken.</span><span class="sxs-lookup"><span data-stu-id="55c8f-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="55c8f-118">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-118">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-119">systemId</span><span class="sxs-lookup"><span data-stu-id="55c8f-119">systemId</span></span> | <span data-ttu-id="55c8f-120">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-120">String</span></span> | <span data-ttu-id="55c8f-121">Logic app system ID.</span><span class="sxs-lookup"><span data-stu-id="55c8f-121">Logic app system ID.</span></span> <span data-ttu-id="55c8f-122">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-122">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-123">runId</span><span class="sxs-lookup"><span data-stu-id="55c8f-123">runId</span></span> | <span data-ttu-id="55c8f-124">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-124">String</span></span> | <span data-ttu-id="55c8f-125">Logic app run ID.</span><span class="sxs-lookup"><span data-stu-id="55c8f-125">Logic app run ID.</span></span> <span data-ttu-id="55c8f-126">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-126">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-127">operationName</span><span class="sxs-lookup"><span data-stu-id="55c8f-127">operationName</span></span> | <span data-ttu-id="55c8f-128">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-128">String</span></span> | <span data-ttu-id="55c8f-129">Name of the operation (for example, action or trigger).</span><span class="sxs-lookup"><span data-stu-id="55c8f-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="55c8f-130">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-130">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="55c8f-131">repeatItemScopeName</span></span> | <span data-ttu-id="55c8f-132">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-132">String</span></span> | <span data-ttu-id="55c8f-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span><span class="sxs-lookup"><span data-stu-id="55c8f-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="55c8f-134">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-134">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="55c8f-135">repeatItemIndex</span></span> | <span data-ttu-id="55c8f-136">Integer</span><span class="sxs-lookup"><span data-stu-id="55c8f-136">Integer</span></span> | <span data-ttu-id="55c8f-137">Whether the action is inside a `foreach`/`until` loop.</span><span class="sxs-lookup"><span data-stu-id="55c8f-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="55c8f-138">Indicates the repeated item index.</span><span class="sxs-lookup"><span data-stu-id="55c8f-138">Indicates the repeated item index.</span></span> <span data-ttu-id="55c8f-139">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-139">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="55c8f-140">trackingId</span></span> | <span data-ttu-id="55c8f-141">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-141">String</span></span> | <span data-ttu-id="55c8f-142">Tracking ID, to correlate the messages.</span><span class="sxs-lookup"><span data-stu-id="55c8f-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="55c8f-143">(Optional)</span><span class="sxs-lookup"><span data-stu-id="55c8f-143">(Optional)</span></span> |
| <span data-ttu-id="55c8f-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="55c8f-144">correlationId</span></span> | <span data-ttu-id="55c8f-145">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-145">String</span></span> | <span data-ttu-id="55c8f-146">Correlation ID, to correlate the messages.</span><span class="sxs-lookup"><span data-stu-id="55c8f-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="55c8f-147">(Optional)</span><span class="sxs-lookup"><span data-stu-id="55c8f-147">(Optional)</span></span> |
| <span data-ttu-id="55c8f-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="55c8f-148">clientRequestId</span></span> | <span data-ttu-id="55c8f-149">String</span><span class="sxs-lookup"><span data-stu-id="55c8f-149">String</span></span> | <span data-ttu-id="55c8f-150">Client can populate it to correlate messages.</span><span class="sxs-lookup"><span data-stu-id="55c8f-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="55c8f-151">(Optional)</span><span class="sxs-lookup"><span data-stu-id="55c8f-151">(Optional)</span></span> |
| <span data-ttu-id="55c8f-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="55c8f-152">eventLevel</span></span> |   | <span data-ttu-id="55c8f-153">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="55c8f-153">Level of the event.</span></span> <span data-ttu-id="55c8f-154">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-154">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="55c8f-155">eventTime</span></span> |   | <span data-ttu-id="55c8f-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="55c8f-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="55c8f-157">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-157">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-158">recordType</span><span class="sxs-lookup"><span data-stu-id="55c8f-158">recordType</span></span> |   | <span data-ttu-id="55c8f-159">Type of the track record.</span><span class="sxs-lookup"><span data-stu-id="55c8f-159">Type of the track record.</span></span> <span data-ttu-id="55c8f-160">Allowed value is **custom**.</span><span class="sxs-lookup"><span data-stu-id="55c8f-160">Allowed value is **custom**.</span></span> <span data-ttu-id="55c8f-161">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-161">(Mandatory)</span></span> |
| <span data-ttu-id="55c8f-162">record</span><span class="sxs-lookup"><span data-stu-id="55c8f-162">record</span></span> |   | <span data-ttu-id="55c8f-163">Custom record type.</span><span class="sxs-lookup"><span data-stu-id="55c8f-163">Custom record type.</span></span> <span data-ttu-id="55c8f-164">Allowed format is JToken.</span><span class="sxs-lookup"><span data-stu-id="55c8f-164">Allowed format is JToken.</span></span> <span data-ttu-id="55c8f-165">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="55c8f-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="55c8f-166">B2B protocol tracking schemas</span><span class="sxs-lookup"><span data-stu-id="55c8f-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="55c8f-167">For information about B2B protocol tracking schemas, see:</span><span class="sxs-lookup"><span data-stu-id="55c8f-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="55c8f-168">AS2 tracking schemas</span><span class="sxs-lookup"><span data-stu-id="55c8f-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="55c8f-169">X12 tracking schemas</span><span class="sxs-lookup"><span data-stu-id="55c8f-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="55c8f-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="55c8f-170">Next steps</span></span>
* <span data-ttu-id="55c8f-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="55c8f-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="55c8f-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="55c8f-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="55c8f-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55c8f-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
