---
title: Encode X12 messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and convert XML-encoded messages with X12 message encoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: 7b3624f2b9aab779afaf773ae9776bbddbf11ea4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555182"
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="60511-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="60511-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="60511-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span><span class="sxs-lookup"><span data-stu-id="60511-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="60511-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="60511-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="60511-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="60511-106">Before you start</span></span>

<span data-ttu-id="60511-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="60511-107">Here's the items you need:</span></span>

* <span data-ttu-id="60511-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="60511-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="60511-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="60511-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="60511-110">You must have an integration account to use the Encode X12 message connector.</span><span class="sxs-lookup"><span data-stu-id="60511-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="60511-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="60511-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="60511-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="60511-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="60511-113">Encode X12 messages</span><span class="sxs-lookup"><span data-stu-id="60511-113">Encode X12 messages</span></span>

1. <span data-ttu-id="60511-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="60511-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="60511-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="60511-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="60511-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="60511-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="60511-117">In the search box, enter "x12" for your filter.</span><span class="sxs-lookup"><span data-stu-id="60511-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="60511-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span><span class="sxs-lookup"><span data-stu-id="60511-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Search for "x12"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="60511-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="60511-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="60511-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="60511-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![integration account connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="60511-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="60511-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="60511-124">Property</span><span class="sxs-lookup"><span data-stu-id="60511-124">Property</span></span> | <span data-ttu-id="60511-125">Details</span><span class="sxs-lookup"><span data-stu-id="60511-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="60511-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="60511-126">Connection Name \*</span></span> |<span data-ttu-id="60511-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="60511-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="60511-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="60511-128">Integration Account \*</span></span> |<span data-ttu-id="60511-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="60511-129">Enter a name for your integration account.</span></span> <span data-ttu-id="60511-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="60511-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="60511-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="60511-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="60511-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="60511-132">To finish creating your connection, choose **Create**.</span></span>

    ![integration account connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="60511-134">Your connection is now created.</span><span class="sxs-lookup"><span data-stu-id="60511-134">Your connection is now created.</span></span>

    ![integration account connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="60511-136">Encode X12 messages by agreement name</span><span class="sxs-lookup"><span data-stu-id="60511-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="60511-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span><span class="sxs-lookup"><span data-stu-id="60511-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="60511-138">Enter the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="60511-138">Enter the XML message to encode.</span></span>

![Enter X12 agreement name and XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="60511-140">Encode X12 messages by identities</span><span class="sxs-lookup"><span data-stu-id="60511-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="60511-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span><span class="sxs-lookup"><span data-stu-id="60511-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="60511-142">Select the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="60511-142">Select the XML message to encode.</span></span>
   
![Provide identities for sender and receiver, select XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="60511-144">X12 Encode details</span><span class="sxs-lookup"><span data-stu-id="60511-144">X12 Encode details</span></span>

<span data-ttu-id="60511-145">The X12 Encode connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="60511-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="60511-146">Agreement resolution by matching sender and receiver context properties.</span><span class="sxs-lookup"><span data-stu-id="60511-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="60511-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span><span class="sxs-lookup"><span data-stu-id="60511-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="60511-148">Applies transaction set header and trailer segments</span><span class="sxs-lookup"><span data-stu-id="60511-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="60511-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span><span class="sxs-lookup"><span data-stu-id="60511-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="60511-150">Replaces separators in the payload data</span><span class="sxs-lookup"><span data-stu-id="60511-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="60511-151">Validates EDI and partner-specific properties</span><span class="sxs-lookup"><span data-stu-id="60511-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="60511-152">Schema validation of the transaction-set data elements against the message Schema</span><span class="sxs-lookup"><span data-stu-id="60511-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="60511-153">EDI validation performed on transaction-set data elements.</span><span class="sxs-lookup"><span data-stu-id="60511-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="60511-154">Extended validation performed on transaction-set data elements</span><span class="sxs-lookup"><span data-stu-id="60511-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="60511-155">Requests a Technical and/or Functional acknowledgment (if configured).</span><span class="sxs-lookup"><span data-stu-id="60511-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="60511-156">A Technical Acknowledgment generates as a result of header validation.</span><span class="sxs-lookup"><span data-stu-id="60511-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="60511-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span><span class="sxs-lookup"><span data-stu-id="60511-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="60511-158">A Functional Acknowledgment generates as a result of body validation.</span><span class="sxs-lookup"><span data-stu-id="60511-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="60511-159">The functional acknowledgment reports each error encountered while processing the received document</span><span class="sxs-lookup"><span data-stu-id="60511-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="next-steps"></a><span data-ttu-id="60511-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="60511-160">Next steps</span></span>
[<span data-ttu-id="60511-161">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="60511-161">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 







