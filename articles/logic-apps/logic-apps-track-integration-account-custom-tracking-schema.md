---
title: Custom tracking schemas for B2B messages - Azure Logic Apps | Microsoft Docs
description: Create custom tracking schemas that monitor B2B messages in integration accounts for Azure Logic Apps with Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.date: 01/27/2017
ms.openlocfilehash: 68c5d6e68562d4027c102e1bde42c775648e58c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824257"
---
# <a name="create-custom-tracking-schemas-that-monitor-end-to-end-workflows-in-azure-logic-apps"></a><span data-ttu-id="c2718-103">Create custom tracking schemas that monitor end-to-end workflows in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c2718-103">Create custom tracking schemas that monitor end-to-end workflows in Azure Logic Apps</span></span>

<span data-ttu-id="c2718-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span><span class="sxs-lookup"><span data-stu-id="c2718-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="c2718-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span><span class="sxs-lookup"><span data-stu-id="c2718-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="c2718-106">This article provides custom code that you can use in the layers outside of your logic app.</span><span class="sxs-lookup"><span data-stu-id="c2718-106">This article provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="c2718-107">Custom tracking schema</span><span class="sxs-lookup"><span data-stu-id="c2718-107">Custom tracking schema</span></span>

```json
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
```

| <span data-ttu-id="c2718-108">Property</span><span class="sxs-lookup"><span data-stu-id="c2718-108">Property</span></span> | <span data-ttu-id="c2718-109">Type</span><span class="sxs-lookup"><span data-stu-id="c2718-109">Type</span></span> | <span data-ttu-id="c2718-110">Description</span><span class="sxs-lookup"><span data-stu-id="c2718-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2718-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="c2718-111">sourceType</span></span> |   | <span data-ttu-id="c2718-112">Type of the run source.</span><span class="sxs-lookup"><span data-stu-id="c2718-112">Type of the run source.</span></span> <span data-ttu-id="c2718-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span><span class="sxs-lookup"><span data-stu-id="c2718-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="c2718-114">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-114">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-115">Source</span><span class="sxs-lookup"><span data-stu-id="c2718-115">Source</span></span> |   | <span data-ttu-id="c2718-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span><span class="sxs-lookup"><span data-stu-id="c2718-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="c2718-117">If the source type is **custom**, the schema is a JToken.</span><span class="sxs-lookup"><span data-stu-id="c2718-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="c2718-118">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-118">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-119">systemId</span><span class="sxs-lookup"><span data-stu-id="c2718-119">systemId</span></span> | <span data-ttu-id="c2718-120">String</span><span class="sxs-lookup"><span data-stu-id="c2718-120">String</span></span> | <span data-ttu-id="c2718-121">Logic app system ID.</span><span class="sxs-lookup"><span data-stu-id="c2718-121">Logic app system ID.</span></span> <span data-ttu-id="c2718-122">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-122">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-123">runId</span><span class="sxs-lookup"><span data-stu-id="c2718-123">runId</span></span> | <span data-ttu-id="c2718-124">String</span><span class="sxs-lookup"><span data-stu-id="c2718-124">String</span></span> | <span data-ttu-id="c2718-125">Logic app run ID.</span><span class="sxs-lookup"><span data-stu-id="c2718-125">Logic app run ID.</span></span> <span data-ttu-id="c2718-126">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-126">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-127">operationName</span><span class="sxs-lookup"><span data-stu-id="c2718-127">operationName</span></span> | <span data-ttu-id="c2718-128">String</span><span class="sxs-lookup"><span data-stu-id="c2718-128">String</span></span> | <span data-ttu-id="c2718-129">Name of the operation (for example, action or trigger).</span><span class="sxs-lookup"><span data-stu-id="c2718-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="c2718-130">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-130">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="c2718-131">repeatItemScopeName</span></span> | <span data-ttu-id="c2718-132">String</span><span class="sxs-lookup"><span data-stu-id="c2718-132">String</span></span> | <span data-ttu-id="c2718-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span><span class="sxs-lookup"><span data-stu-id="c2718-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="c2718-134">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-134">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="c2718-135">repeatItemIndex</span></span> | <span data-ttu-id="c2718-136">Integer</span><span class="sxs-lookup"><span data-stu-id="c2718-136">Integer</span></span> | <span data-ttu-id="c2718-137">Whether the action is inside a `foreach`/`until` loop.</span><span class="sxs-lookup"><span data-stu-id="c2718-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="c2718-138">Indicates the repeated item index.</span><span class="sxs-lookup"><span data-stu-id="c2718-138">Indicates the repeated item index.</span></span> <span data-ttu-id="c2718-139">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-139">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="c2718-140">trackingId</span></span> | <span data-ttu-id="c2718-141">String</span><span class="sxs-lookup"><span data-stu-id="c2718-141">String</span></span> | <span data-ttu-id="c2718-142">Tracking ID, to correlate the messages.</span><span class="sxs-lookup"><span data-stu-id="c2718-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="c2718-143">(Optional)</span><span class="sxs-lookup"><span data-stu-id="c2718-143">(Optional)</span></span> |
| <span data-ttu-id="c2718-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="c2718-144">correlationId</span></span> | <span data-ttu-id="c2718-145">String</span><span class="sxs-lookup"><span data-stu-id="c2718-145">String</span></span> | <span data-ttu-id="c2718-146">Correlation ID, to correlate the messages.</span><span class="sxs-lookup"><span data-stu-id="c2718-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="c2718-147">(Optional)</span><span class="sxs-lookup"><span data-stu-id="c2718-147">(Optional)</span></span> |
| <span data-ttu-id="c2718-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="c2718-148">clientRequestId</span></span> | <span data-ttu-id="c2718-149">String</span><span class="sxs-lookup"><span data-stu-id="c2718-149">String</span></span> | <span data-ttu-id="c2718-150">Client can populate it to correlate messages.</span><span class="sxs-lookup"><span data-stu-id="c2718-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="c2718-151">(Optional)</span><span class="sxs-lookup"><span data-stu-id="c2718-151">(Optional)</span></span> |
| <span data-ttu-id="c2718-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="c2718-152">eventLevel</span></span> |   | <span data-ttu-id="c2718-153">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="c2718-153">Level of the event.</span></span> <span data-ttu-id="c2718-154">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-154">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="c2718-155">eventTime</span></span> |   | <span data-ttu-id="c2718-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="c2718-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="c2718-157">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-157">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-158">recordType</span><span class="sxs-lookup"><span data-stu-id="c2718-158">recordType</span></span> |   | <span data-ttu-id="c2718-159">Type of the track record.</span><span class="sxs-lookup"><span data-stu-id="c2718-159">Type of the track record.</span></span> <span data-ttu-id="c2718-160">Allowed value is **custom**.</span><span class="sxs-lookup"><span data-stu-id="c2718-160">Allowed value is **custom**.</span></span> <span data-ttu-id="c2718-161">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-161">(Mandatory)</span></span> |
| <span data-ttu-id="c2718-162">record</span><span class="sxs-lookup"><span data-stu-id="c2718-162">record</span></span> |   | <span data-ttu-id="c2718-163">Custom record type.</span><span class="sxs-lookup"><span data-stu-id="c2718-163">Custom record type.</span></span> <span data-ttu-id="c2718-164">Allowed format is JToken.</span><span class="sxs-lookup"><span data-stu-id="c2718-164">Allowed format is JToken.</span></span> <span data-ttu-id="c2718-165">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="c2718-165">(Mandatory)</span></span> |
||||

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="c2718-166">B2B protocol tracking schemas</span><span class="sxs-lookup"><span data-stu-id="c2718-166">B2B protocol tracking schemas</span></span>

<span data-ttu-id="c2718-167">For information about B2B protocol tracking schemas, see:</span><span class="sxs-lookup"><span data-stu-id="c2718-167">For information about B2B protocol tracking schemas, see:</span></span>

* [<span data-ttu-id="c2718-168">AS2 tracking schemas</span><span class="sxs-lookup"><span data-stu-id="c2718-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="c2718-169">X12 tracking schemas</span><span class="sxs-lookup"><span data-stu-id="c2718-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="c2718-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2718-170">Next steps</span></span>

* <span data-ttu-id="c2718-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md)</span><span class="sxs-lookup"><span data-stu-id="c2718-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md)</span></span>
* <span data-ttu-id="c2718-172">Learn about [tracking B2B messages in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)</span><span class="sxs-lookup"><span data-stu-id="c2718-172">Learn about [tracking B2B messages in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)</span></span>