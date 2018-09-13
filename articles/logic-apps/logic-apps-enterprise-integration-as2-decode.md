---
title: Decode AS2 messages - Azure Logic Apps | Microsoft Docs
description: How to use the AS2 decoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: padmavc
ms.openlocfilehash: f3a1a50c3433d36bc90134e373a11e79c025e6eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661931"
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="84fe4-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="84fe4-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="84fe4-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span><span class="sxs-lookup"><span data-stu-id="84fe4-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="84fe4-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span><span class="sxs-lookup"><span data-stu-id="84fe4-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="84fe4-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="84fe4-106">Before you start</span></span>

<span data-ttu-id="84fe4-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="84fe4-107">Here's the items you need:</span></span>

* <span data-ttu-id="84fe4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="84fe4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="84fe4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="84fe4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="84fe4-110">You must have an integration account to use the Decode AS2 message connector.</span><span class="sxs-lookup"><span data-stu-id="84fe4-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="84fe4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="84fe4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="84fe4-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span><span class="sxs-lookup"><span data-stu-id="84fe4-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="84fe4-113">Decode AS2 messages</span><span class="sxs-lookup"><span data-stu-id="84fe4-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="84fe4-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="84fe4-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="84fe4-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span><span class="sxs-lookup"><span data-stu-id="84fe4-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="84fe4-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="84fe4-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="84fe4-117">In the search box, enter "AS2" for your filter.</span><span class="sxs-lookup"><span data-stu-id="84fe4-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="84fe4-118">Select **AS2 - Decode AS2 message**.</span><span class="sxs-lookup"><span data-stu-id="84fe4-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Search for "AS2"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="84fe4-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span><span class="sxs-lookup"><span data-stu-id="84fe4-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="84fe4-121">Name your connection, and select the integration account that you want to connect.</span><span class="sxs-lookup"><span data-stu-id="84fe4-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Create integration connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="84fe4-123">Properties with an asterisk are required.</span><span class="sxs-lookup"><span data-stu-id="84fe4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="84fe4-124">Property</span><span class="sxs-lookup"><span data-stu-id="84fe4-124">Property</span></span> | <span data-ttu-id="84fe4-125">Details</span><span class="sxs-lookup"><span data-stu-id="84fe4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="84fe4-126">Connection Name \*</span><span class="sxs-lookup"><span data-stu-id="84fe4-126">Connection Name \*</span></span> |<span data-ttu-id="84fe4-127">Enter any name for your connection.</span><span class="sxs-lookup"><span data-stu-id="84fe4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="84fe4-128">Integration Account \*</span><span class="sxs-lookup"><span data-stu-id="84fe4-128">Integration Account \*</span></span> |<span data-ttu-id="84fe4-129">Enter a name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="84fe4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="84fe4-130">Make sure that your integration account and logic app are in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="84fe4-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="84fe4-131">When you're done, your connection details should look similar to this example.</span><span class="sxs-lookup"><span data-stu-id="84fe4-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="84fe4-132">To finish creating your connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="84fe4-132">To finish creating your connection, choose **Create**.</span></span>

    ![integration connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="84fe4-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span><span class="sxs-lookup"><span data-stu-id="84fe4-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![integration connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="84fe4-136">For example:</span><span class="sxs-lookup"><span data-stu-id="84fe4-136">For example:</span></span>

    ![Select Body and Headers from Request outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="84fe4-138">AS2 decoder details</span><span class="sxs-lookup"><span data-stu-id="84fe4-138">AS2 decoder details</span></span>

<span data-ttu-id="84fe4-139">The Decode AS2 connector performs these tasks:</span><span class="sxs-lookup"><span data-stu-id="84fe4-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="84fe4-140">Processes AS2/HTTP headers</span><span class="sxs-lookup"><span data-stu-id="84fe4-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="84fe4-141">Verifies the signature (if configured)</span><span class="sxs-lookup"><span data-stu-id="84fe4-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="84fe4-142">Decrypts the messages (if configured)</span><span class="sxs-lookup"><span data-stu-id="84fe4-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="84fe4-143">Decompresses the message (if configured)</span><span class="sxs-lookup"><span data-stu-id="84fe4-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="84fe4-144">Reconciles a received MDN with the original outbound message</span><span class="sxs-lookup"><span data-stu-id="84fe4-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="84fe4-145">Updates and correlates records in the non-repudiation database</span><span class="sxs-lookup"><span data-stu-id="84fe4-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="84fe4-146">Writes records for AS2 status reporting</span><span class="sxs-lookup"><span data-stu-id="84fe4-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="84fe4-147">The output payload contents are base64 encoded</span><span class="sxs-lookup"><span data-stu-id="84fe4-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="84fe4-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span><span class="sxs-lookup"><span data-stu-id="84fe4-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="84fe4-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span><span class="sxs-lookup"><span data-stu-id="84fe4-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="84fe4-150">Sets the correlation tokens and properties on the MDN</span><span class="sxs-lookup"><span data-stu-id="84fe4-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="84fe4-151">Try this sample</span><span class="sxs-lookup"><span data-stu-id="84fe4-151">Try this sample</span></span>

<span data-ttu-id="84fe4-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="84fe4-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84fe4-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="84fe4-153">Next steps</span></span>
[<span data-ttu-id="84fe4-154">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="84fe4-154">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 






