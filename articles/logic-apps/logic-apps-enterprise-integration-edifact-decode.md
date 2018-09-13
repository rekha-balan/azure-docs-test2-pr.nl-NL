---
title: Decode EDIFACT messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and generate XML for transaction sets with the EDIFACT message decoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: c7e8eb74d836e8416b78a261e987aee81d9f662d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550777"
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="77521-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="77521-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="77521-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and generate acknowledgment for processed transactions.</span><span class="sxs-lookup"><span data-stu-id="77521-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and generate acknowledgment for processed transactions.</span></span> <span data-ttu-id="77521-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="77521-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="77521-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="77521-106">Before you start</span></span>

<span data-ttu-id="77521-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="77521-107">Here's the items you need:</span></span>

* <span data-ttu-id="77521-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="77521-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="77521-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="77521-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="77521-110">You must have an integration account to use the Decode EDIFACT message connector.</span><span class="sxs-lookup"><span data-stu-id="77521-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="77521-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="77521-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="77521-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="77521-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="77521-113">Decode EDIFACT messages</span><span class="sxs-lookup"><span data-stu-id="77521-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="77521-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="77521-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="77521-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="77521-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="77521-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="77521-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="77521-117">In the search box, enter "EDIFACT" as your filter.</span><span class="sxs-lookup"><span data-stu-id="77521-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="77521-118">Select **Decode EDIFACT Message**.</span><span class="sxs-lookup"><span data-stu-id="77521-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![search EDIFACT](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="77521-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="77521-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="77521-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="77521-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![create integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="77521-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="77521-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="77521-124">Property</span><span class="sxs-lookup"><span data-stu-id="77521-124">Property</span></span> | <span data-ttu-id="77521-125">Details</span><span class="sxs-lookup"><span data-stu-id="77521-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="77521-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="77521-126">Connection Name \*</span></span> |<span data-ttu-id="77521-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="77521-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="77521-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="77521-128">Integration Account \*</span></span> |<span data-ttu-id="77521-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="77521-129">Enter a name for your integration account.</span></span> <span data-ttu-id="77521-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="77521-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="77521-131">When you're done to finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="77521-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="77521-132">Your connection details should look similar to this example:</span><span class="sxs-lookup"><span data-stu-id="77521-132">Your connection details should look similar to this example:</span></span>

    ![integration account details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="77521-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span><span class="sxs-lookup"><span data-stu-id="77521-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![integration account connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="77521-136">For example:</span><span class="sxs-lookup"><span data-stu-id="77521-136">For example:</span></span>

    ![Select EDIFACT flat file message for decoding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="77521-138">EDIFACT decoder details</span><span class="sxs-lookup"><span data-stu-id="77521-138">EDIFACT decoder details</span></span>

<span data-ttu-id="77521-139">The Decode EDIFACT connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="77521-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="77521-140">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier</span><span class="sxs-lookup"><span data-stu-id="77521-140">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier</span></span>
* <span data-ttu-id="77521-141">Splits multiple interchanges in a single message into separate.</span><span class="sxs-lookup"><span data-stu-id="77521-141">Splits multiple interchanges in a single message into separate.</span></span>
* <span data-ttu-id="77521-142">Validates the envelope against trading partner agreement</span><span class="sxs-lookup"><span data-stu-id="77521-142">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="77521-143">Disassembles the interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="77521-144">Validates EDI and partner-specific properties includes</span><span class="sxs-lookup"><span data-stu-id="77521-144">Validates EDI and partner-specific properties includes</span></span>
  * <span data-ttu-id="77521-145">Validation of the structure of the interchange envelope.</span><span class="sxs-lookup"><span data-stu-id="77521-145">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="77521-146">Schema validation of the envelope against the control schema.</span><span class="sxs-lookup"><span data-stu-id="77521-146">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="77521-147">Schema validation of the transaction-set data elements against the message schema.</span><span class="sxs-lookup"><span data-stu-id="77521-147">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="77521-148">EDI validation performed on transaction-set data elements</span><span class="sxs-lookup"><span data-stu-id="77521-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="77521-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span><span class="sxs-lookup"><span data-stu-id="77521-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="77521-150">Checks the interchange control number against previously received interchanges.</span><span class="sxs-lookup"><span data-stu-id="77521-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="77521-151">Checks the group control number against other group control numbers in the interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="77521-152">Checks the transaction set control number against other transaction set control numbers in that group.</span><span class="sxs-lookup"><span data-stu-id="77521-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="77521-153">Generates an XML document for each transaction set.</span><span class="sxs-lookup"><span data-stu-id="77521-153">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="77521-154">Converts the entire interchange to XML</span><span class="sxs-lookup"><span data-stu-id="77521-154">Converts the entire interchange to XML</span></span> 
  * <span data-ttu-id="77521-155">Split Interchange as transaction sets - suspend transaction sets on error: Parses each transaction set in an interchange into a separate XML document.</span><span class="sxs-lookup"><span data-stu-id="77521-155">Split Interchange as transaction sets - suspend transaction sets on error: Parses each transaction set in an interchange into a separate XML document.</span></span> <span data-ttu-id="77521-156">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends only those transaction sets.</span><span class="sxs-lookup"><span data-stu-id="77521-156">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends only those transaction sets.</span></span> 
  * <span data-ttu-id="77521-157">Split Interchange as transaction sets - suspend interchange on error: Parses each transaction set in an interchange into a separate XML document.</span><span class="sxs-lookup"><span data-stu-id="77521-157">Split Interchange as transaction sets - suspend interchange on error: Parses each transaction set in an interchange into a separate XML document.</span></span>  <span data-ttu-id="77521-158">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends the entire interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-158">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends the entire interchange.</span></span>
  * <span data-ttu-id="77521-159">Preserve Interchange - suspend transaction sets on error: Creates an XML document for the entire batched interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-159">Preserve Interchange - suspend transaction sets on error: Creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="77521-160">EDIFACT Decode suspends only those transaction sets that fail validation, while continuing to process all other transaction sets</span><span class="sxs-lookup"><span data-stu-id="77521-160">EDIFACT Decode suspends only those transaction sets that fail validation, while continuing to process all other transaction sets</span></span>
  * <span data-ttu-id="77521-161">Preserve Interchange - suspend interchange on error: Creates an XML document for the entire batched interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-161">Preserve Interchange - suspend interchange on error: Creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="77521-162">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends the entire interchange,</span><span class="sxs-lookup"><span data-stu-id="77521-162">If one or more transaction sets in the interchange fail validation, then EDIFACT Decode suspends the entire interchange,</span></span> 
* <span data-ttu-id="77521-163">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span><span class="sxs-lookup"><span data-stu-id="77521-163">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="77521-164">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span><span class="sxs-lookup"><span data-stu-id="77521-164">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="77521-165">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span><span class="sxs-lookup"><span data-stu-id="77521-165">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="next-steps"></a><span data-ttu-id="77521-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="77521-166">Next steps</span></span>
[<span data-ttu-id="77521-167">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="77521-167">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 






