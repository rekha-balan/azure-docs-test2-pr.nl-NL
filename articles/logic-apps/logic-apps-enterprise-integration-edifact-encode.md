---
title: Encode EDIFACT messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and generate XML with EDIFACT message encoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: b0fe1902a75927a7cd92acbe2ae782996784dfe1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563039"
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="61bba-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="61bba-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="61bba-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span><span class="sxs-lookup"><span data-stu-id="61bba-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="61bba-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="61bba-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="61bba-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="61bba-106">Before you start</span></span>

<span data-ttu-id="61bba-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="61bba-107">Here's the items you need:</span></span>

* <span data-ttu-id="61bba-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="61bba-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="61bba-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="61bba-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="61bba-110">You must have an integration account to use the Encode EDIFACT message connector.</span><span class="sxs-lookup"><span data-stu-id="61bba-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="61bba-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="61bba-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="61bba-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="61bba-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="61bba-113">Encode EDIFACT messages</span><span class="sxs-lookup"><span data-stu-id="61bba-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="61bba-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="61bba-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="61bba-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="61bba-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="61bba-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="61bba-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="61bba-117">In the search box, enter "EDIFACT" as your filter.</span><span class="sxs-lookup"><span data-stu-id="61bba-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="61bba-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span><span class="sxs-lookup"><span data-stu-id="61bba-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![search EDIFACT](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="61bba-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="61bba-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="61bba-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="61bba-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![create integration account connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="61bba-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="61bba-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="61bba-124">Property</span><span class="sxs-lookup"><span data-stu-id="61bba-124">Property</span></span> | <span data-ttu-id="61bba-125">Details</span><span class="sxs-lookup"><span data-stu-id="61bba-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="61bba-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="61bba-126">Connection Name \*</span></span> |<span data-ttu-id="61bba-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="61bba-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="61bba-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="61bba-128">Integration Account \*</span></span> |<span data-ttu-id="61bba-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="61bba-129">Enter a name for your integration account.</span></span> <span data-ttu-id="61bba-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="61bba-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="61bba-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="61bba-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="61bba-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="61bba-132">To finish creating your connection, choose **Create**.</span></span>

    ![integration account connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="61bba-134">Your connection is now created.</span><span class="sxs-lookup"><span data-stu-id="61bba-134">Your connection is now created.</span></span>

    ![integration account connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="61bba-136">Encode EDIFACT Message by agreement name</span><span class="sxs-lookup"><span data-stu-id="61bba-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="61bba-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span><span class="sxs-lookup"><span data-stu-id="61bba-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="61bba-138">Enter the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="61bba-138">Enter the XML message to encode.</span></span>

![Enter EDIFACT agreement name and XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="61bba-140">Encode EDIFACT Message by identities</span><span class="sxs-lookup"><span data-stu-id="61bba-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="61bba-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span><span class="sxs-lookup"><span data-stu-id="61bba-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="61bba-142">Select the XML message to encode.</span><span class="sxs-lookup"><span data-stu-id="61bba-142">Select the XML message to encode.</span></span>

![Provide identities for sender and receiver, select XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="61bba-144">EDIFACT Encode details</span><span class="sxs-lookup"><span data-stu-id="61bba-144">EDIFACT Encode details</span></span>

<span data-ttu-id="61bba-145">The Encode EDIFACT connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="61bba-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="61bba-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span><span class="sxs-lookup"><span data-stu-id="61bba-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="61bba-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span><span class="sxs-lookup"><span data-stu-id="61bba-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="61bba-148">Applies transaction set header and trailer segments</span><span class="sxs-lookup"><span data-stu-id="61bba-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="61bba-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span><span class="sxs-lookup"><span data-stu-id="61bba-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="61bba-150">Replaces separators in the payload data</span><span class="sxs-lookup"><span data-stu-id="61bba-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="61bba-151">Validates EDI and partner-specific properties</span><span class="sxs-lookup"><span data-stu-id="61bba-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="61bba-152">Schema validation of the transaction-set data elements against the message schema.</span><span class="sxs-lookup"><span data-stu-id="61bba-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="61bba-153">EDI validation performed on transaction-set data elements.</span><span class="sxs-lookup"><span data-stu-id="61bba-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="61bba-154">Extended validation performed on transaction-set data elements</span><span class="sxs-lookup"><span data-stu-id="61bba-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="61bba-155">Generates an XML document for each transaction set.</span><span class="sxs-lookup"><span data-stu-id="61bba-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="61bba-156">Requests a Technical and/or Functional acknowledgment (if configured).</span><span class="sxs-lookup"><span data-stu-id="61bba-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="61bba-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span><span class="sxs-lookup"><span data-stu-id="61bba-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="61bba-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span><span class="sxs-lookup"><span data-stu-id="61bba-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="next-steps"></a><span data-ttu-id="61bba-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="61bba-159">Next steps</span></span>
[<span data-ttu-id="61bba-160">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="61bba-160">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 







