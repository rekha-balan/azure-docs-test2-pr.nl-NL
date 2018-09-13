---
title: Decode X12 messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and generate XML for transaction sets with the X12 message decoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: c8192a800d36f4d2c490f6ebd1f27f38fc2591c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550339"
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="0c81f-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0c81f-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="0c81f-104">With the Decode X12 message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and generate acknowledgment for processed transactions.</span><span class="sxs-lookup"><span data-stu-id="0c81f-104">With the Decode X12 message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and generate acknowledgment for processed transactions.</span></span> <span data-ttu-id="0c81f-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="0c81f-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0c81f-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="0c81f-106">Before you start</span></span>

<span data-ttu-id="0c81f-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="0c81f-107">Here's the items you need:</span></span>

* <span data-ttu-id="0c81f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="0c81f-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="0c81f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0c81f-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="0c81f-110">You must have an integration account to use the Decode X12 message connector.</span><span class="sxs-lookup"><span data-stu-id="0c81f-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="0c81f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="0c81f-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="0c81f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="0c81f-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="0c81f-113">Decode X12 messages</span><span class="sxs-lookup"><span data-stu-id="0c81f-113">Decode X12 messages</span></span>

1. <span data-ttu-id="0c81f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c81f-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="0c81f-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="0c81f-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="0c81f-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="0c81f-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="0c81f-117">In the search box, enter "x12" for your filter.</span><span class="sxs-lookup"><span data-stu-id="0c81f-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="0c81f-118">Select **X12 - Decode X12 message**.</span><span class="sxs-lookup"><span data-stu-id="0c81f-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Search for "x12"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="0c81f-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="0c81f-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="0c81f-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="0c81f-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Provide integration account connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="0c81f-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="0c81f-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="0c81f-124">Property</span><span class="sxs-lookup"><span data-stu-id="0c81f-124">Property</span></span> | <span data-ttu-id="0c81f-125">Details</span><span class="sxs-lookup"><span data-stu-id="0c81f-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="0c81f-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="0c81f-126">Connection Name \*</span></span> |<span data-ttu-id="0c81f-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="0c81f-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="0c81f-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="0c81f-128">Integration Account \*</span></span> |<span data-ttu-id="0c81f-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="0c81f-129">Enter a name for your integration account.</span></span> <span data-ttu-id="0c81f-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="0c81f-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="0c81f-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="0c81f-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="0c81f-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c81f-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![integration account connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="0c81f-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span><span class="sxs-lookup"><span data-stu-id="0c81f-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![integration account connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="0c81f-136">For example:</span><span class="sxs-lookup"><span data-stu-id="0c81f-136">For example:</span></span>

    ![Select X12 flat file message for decoding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="0c81f-138">X12 Decode details</span><span class="sxs-lookup"><span data-stu-id="0c81f-138">X12 Decode details</span></span>

<span data-ttu-id="0c81f-139">The X12 Decode connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="0c81f-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="0c81f-140">Validates the envelope against trading partner agreement</span><span class="sxs-lookup"><span data-stu-id="0c81f-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="0c81f-141">Generates an XML document for each transaction set.</span><span class="sxs-lookup"><span data-stu-id="0c81f-141">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="0c81f-142">Validates EDI and partner-specific properties</span><span class="sxs-lookup"><span data-stu-id="0c81f-142">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="0c81f-143">EDI structural validation, and extended schema validation</span><span class="sxs-lookup"><span data-stu-id="0c81f-143">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="0c81f-144">Validation of the structure of the interchange envelope.</span><span class="sxs-lookup"><span data-stu-id="0c81f-144">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="0c81f-145">Schema validation of the envelope against the control schema.</span><span class="sxs-lookup"><span data-stu-id="0c81f-145">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="0c81f-146">Schema validation of the transaction-set data elements against the message schema.</span><span class="sxs-lookup"><span data-stu-id="0c81f-146">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="0c81f-147">EDI validation performed on transaction-set data elements</span><span class="sxs-lookup"><span data-stu-id="0c81f-147">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="0c81f-148">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span><span class="sxs-lookup"><span data-stu-id="0c81f-148">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="0c81f-149">Checks the interchange control number against previously received interchanges.</span><span class="sxs-lookup"><span data-stu-id="0c81f-149">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="0c81f-150">Checks the group control number against other group control numbers in the interchange.</span><span class="sxs-lookup"><span data-stu-id="0c81f-150">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="0c81f-151">Checks the transaction set control number against other transaction set control numbers in that group.</span><span class="sxs-lookup"><span data-stu-id="0c81f-151">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="0c81f-152">Converts the entire interchange to XML</span><span class="sxs-lookup"><span data-stu-id="0c81f-152">Converts the entire interchange to XML</span></span> 
  * <span data-ttu-id="0c81f-153">Split Interchange as transaction sets - suspend transaction sets on error: Parses each transaction set in an interchange into a separate XML document.</span><span class="sxs-lookup"><span data-stu-id="0c81f-153">Split Interchange as transaction sets - suspend transaction sets on error: Parses each transaction set in an interchange into a separate XML document.</span></span> <span data-ttu-id="0c81f-154">If one or more transaction sets in the interchange fail validation, X12 Decode suspends only those transaction sets.</span><span class="sxs-lookup"><span data-stu-id="0c81f-154">If one or more transaction sets in the interchange fail validation, X12 Decode suspends only those transaction sets.</span></span>
  * <span data-ttu-id="0c81f-155">Split Interchange as transaction sets - suspend interchange on error: Parses each transaction set in an interchange into a separate XML document.</span><span class="sxs-lookup"><span data-stu-id="0c81f-155">Split Interchange as transaction sets - suspend interchange on error: Parses each transaction set in an interchange into a separate XML document.</span></span>  <span data-ttu-id="0c81f-156">If one or more transaction sets in the interchange fail validation, X12 Decode suspends the entire interchange.</span><span class="sxs-lookup"><span data-stu-id="0c81f-156">If one or more transaction sets in the interchange fail validation, X12 Decode suspends the entire interchange.</span></span>
  * <span data-ttu-id="0c81f-157">Preserve Interchange - suspend transaction sets on error: Creates an XML document for the entire batched interchange.</span><span class="sxs-lookup"><span data-stu-id="0c81f-157">Preserve Interchange - suspend transaction sets on error: Creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="0c81f-158">X12 Decode suspends only those transaction sets that fail validation, while continuing to process all other transaction sets</span><span class="sxs-lookup"><span data-stu-id="0c81f-158">X12 Decode suspends only those transaction sets that fail validation, while continuing to process all other transaction sets</span></span>
  * <span data-ttu-id="0c81f-159">Preserve Interchange - suspend interchange on error: Creates an XML document for the entire batched interchange.</span><span class="sxs-lookup"><span data-stu-id="0c81f-159">Preserve Interchange - suspend interchange on error: Creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="0c81f-160">If one or more transaction sets in the interchange fail validation, X12 Decode suspends the entire interchange,</span><span class="sxs-lookup"><span data-stu-id="0c81f-160">If one or more transaction sets in the interchange fail validation, X12 Decode suspends the entire interchange,</span></span> 
* <span data-ttu-id="0c81f-161">Generates a Technical and/or Functional acknowledgment (if configured).</span><span class="sxs-lookup"><span data-stu-id="0c81f-161">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="0c81f-162">A Technical Acknowledgment generates as a result of header validation.</span><span class="sxs-lookup"><span data-stu-id="0c81f-162">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="0c81f-163">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span><span class="sxs-lookup"><span data-stu-id="0c81f-163">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="0c81f-164">A Functional Acknowledgment generates as a result of body validation.</span><span class="sxs-lookup"><span data-stu-id="0c81f-164">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="0c81f-165">The functional acknowledgment reports each error encountered while processing the received document</span><span class="sxs-lookup"><span data-stu-id="0c81f-165">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c81f-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c81f-166">Next steps</span></span>
[<span data-ttu-id="0c81f-167">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0c81f-167">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 






