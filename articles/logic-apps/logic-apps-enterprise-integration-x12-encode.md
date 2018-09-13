---
title: Encode X12 messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and convert XML-encoded messages with X12 message encoder in Azure Logic Apps with Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.date: 01/27/2017
ms.openlocfilehash: 7f1d9f3c6bd768855e60686d2a7c35491d65e22c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827151"
---
# <a name="encode-x12-messages-in-azure-logic-apps-with-enterprise-integration-pack"></a><span data-ttu-id="e5c06-103">Encode X12 messages in Azure Logic Apps with Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="e5c06-103">Encode X12 messages in Azure Logic Apps with Enterprise Integration Pack</span></span>

<span data-ttu-id="e5c06-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span><span class="sxs-lookup"><span data-stu-id="e5c06-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="e5c06-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="e5c06-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e5c06-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="e5c06-106">Before you start</span></span>

<span data-ttu-id="e5c06-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="e5c06-107">Here's the items you need:</span></span>

* <span data-ttu-id="e5c06-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="e5c06-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="e5c06-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e5c06-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="e5c06-110">You must have an integration account to use the Encode X12 message connector.</span><span class="sxs-lookup"><span data-stu-id="e5c06-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="e5c06-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="e5c06-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="e5c06-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="e5c06-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="e5c06-113">Encode X12 messages</span><span class="sxs-lookup"><span data-stu-id="e5c06-113">Encode X12 messages</span></span>

1. <span data-ttu-id="e5c06-114">[Create a logic app](quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="e5c06-114">[Create a logic app](quickstart-create-first-logic-app-workflow.md).</span></span>

2. <span data-ttu-id="e5c06-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="e5c06-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="e5c06-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="e5c06-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="e5c06-117">In the search box, enter "x12" for your filter.</span><span class="sxs-lookup"><span data-stu-id="e5c06-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="e5c06-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span><span class="sxs-lookup"><span data-stu-id="e5c06-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Search for "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="e5c06-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="e5c06-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="e5c06-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="e5c06-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![integration account connection](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="e5c06-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="e5c06-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="e5c06-124">Property</span><span class="sxs-lookup"><span data-stu-id="e5c06-124">Property</span></span> | <span data-ttu-id="e5c06-125">Details</span><span class="sxs-lookup"><span data-stu-id="e5c06-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="e5c06-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="e5c06-126">Connection Name \*</span></span> |<span data-ttu-id="e5c06-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="e5c06-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="e5c06-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="e5c06-128">Integration Account \*</span></span> |<span data-ttu-id="e5c06-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="e5c06-129">Enter a name for your integration account.</span></span> <span data-ttu-id="e5c06-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="e5c06-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="e5c06-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="e5c06-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="e5c06-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="e5c06-132">To finish creating your connection, choose **Create**.</span></span>

    ![integration account connection created](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="e5c06-134">Your connection is now created.</span><span class="sxs-lookup"><span data-stu-id="e5c06-134">Your connection is now created.</span></span>

    ![integration account connection details](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="e5c06-136">Encode X12 messages by agreement name</span><span class="sxs-lookup"><span data-stu-id="e5c06-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="e5c06-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span><span class="sxs-lookup"><span data-stu-id="e5c06-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="e5c06-138">Enter the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="e5c06-138">Enter the XML message to encode.</span></span>

![Enter X12 agreement name and XML message to encode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="e5c06-140">Encode X12 messages by identities</span><span class="sxs-lookup"><span data-stu-id="e5c06-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="e5c06-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span><span class="sxs-lookup"><span data-stu-id="e5c06-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="e5c06-142">Select the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="e5c06-142">Select the XML message to encode.</span></span>
   
![Provide identities for sender and receiver, select XML message to encode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="e5c06-144">X12 Encode details</span><span class="sxs-lookup"><span data-stu-id="e5c06-144">X12 Encode details</span></span>

<span data-ttu-id="e5c06-145">The X12 Encode connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="e5c06-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="e5c06-146">Agreement resolution by matching sender and receiver context properties.</span><span class="sxs-lookup"><span data-stu-id="e5c06-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="e5c06-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span><span class="sxs-lookup"><span data-stu-id="e5c06-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="e5c06-148">Applies transaction set header and trailer segments</span><span class="sxs-lookup"><span data-stu-id="e5c06-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="e5c06-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span><span class="sxs-lookup"><span data-stu-id="e5c06-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="e5c06-150">Replaces separators in the payload data</span><span class="sxs-lookup"><span data-stu-id="e5c06-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="e5c06-151">Validates EDI and partner-specific properties</span><span class="sxs-lookup"><span data-stu-id="e5c06-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="e5c06-152">Schema validation of the transaction-set data elements against the message Schema</span><span class="sxs-lookup"><span data-stu-id="e5c06-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="e5c06-153">EDI validation performed on transaction-set data elements.</span><span class="sxs-lookup"><span data-stu-id="e5c06-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="e5c06-154">Extended validation performed on transaction-set data elements</span><span class="sxs-lookup"><span data-stu-id="e5c06-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="e5c06-155">Requests a Technical and/or Functional acknowledgment (if configured).</span><span class="sxs-lookup"><span data-stu-id="e5c06-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="e5c06-156">A Technical Acknowledgment generates as a result of header validation.</span><span class="sxs-lookup"><span data-stu-id="e5c06-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="e5c06-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span><span class="sxs-lookup"><span data-stu-id="e5c06-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="e5c06-158">A Functional Acknowledgment generates as a result of body validation.</span><span class="sxs-lookup"><span data-stu-id="e5c06-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="e5c06-159">The functional acknowledgment reports each error encountered while processing the received document</span><span class="sxs-lookup"><span data-stu-id="e5c06-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="e5c06-160">View the swagger</span><span class="sxs-lookup"><span data-stu-id="e5c06-160">View the swagger</span></span>
<span data-ttu-id="e5c06-161">See the [swagger details](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="e5c06-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5c06-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5c06-162">Next steps</span></span>
[<span data-ttu-id="e5c06-163">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="e5c06-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 

