---
title: AS2 tracking schemas for B2B monitoring - Azure Logic Apps | Microsoft Docs
description: Use AS2 tracking schemas to monitor B2B messages from transactions in your Azure Integration Account.
author: padmavc
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e9c9cfda4dda1ec3f1b002016118bd49d540e90a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660699"
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-to-monitor-success-errors-and-message-properties"></a><span data-ttu-id="9101a-103">Start or enable tracking of AS2 messages and MDNs to monitor success, errors, and message properties</span><span class="sxs-lookup"><span data-stu-id="9101a-103">Start or enable tracking of AS2 messages and MDNs to monitor success, errors, and message properties</span></span>
<span data-ttu-id="9101a-104">You can use these AS2 tracking schemas in your Azure integration account to help you monitor business-to-business (B2B) transactions:</span><span class="sxs-lookup"><span data-stu-id="9101a-104">You can use these AS2 tracking schemas in your Azure integration account to help you monitor business-to-business (B2B) transactions:</span></span>

* <span data-ttu-id="9101a-105">AS2 message tracking schema</span><span class="sxs-lookup"><span data-stu-id="9101a-105">AS2 message tracking schema</span></span>
* <span data-ttu-id="9101a-106">AS2 MDN tracking schema</span><span class="sxs-lookup"><span data-stu-id="9101a-106">AS2 MDN tracking schema</span></span>

## <a name="as2-message-tracking-schema"></a><span data-ttu-id="9101a-107">AS2 message tracking schema</span><span class="sxs-lookup"><span data-stu-id="9101a-107">AS2 message tracking schema</span></span>
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| <span data-ttu-id="9101a-108">Property</span><span class="sxs-lookup"><span data-stu-id="9101a-108">Property</span></span> | <span data-ttu-id="9101a-109">Type</span><span class="sxs-lookup"><span data-stu-id="9101a-109">Type</span></span> | <span data-ttu-id="9101a-110">Description</span><span class="sxs-lookup"><span data-stu-id="9101a-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9101a-111">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="9101a-111">senderPartnerName</span></span> | <span data-ttu-id="9101a-112">String</span><span class="sxs-lookup"><span data-stu-id="9101a-112">String</span></span> | <span data-ttu-id="9101a-113">AS2 message sender's partner name.</span><span class="sxs-lookup"><span data-stu-id="9101a-113">AS2 message sender's partner name.</span></span> <span data-ttu-id="9101a-114">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-114">(Optional)</span></span> |
| <span data-ttu-id="9101a-115">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="9101a-115">receiverPartnerName</span></span> | <span data-ttu-id="9101a-116">String</span><span class="sxs-lookup"><span data-stu-id="9101a-116">String</span></span> | <span data-ttu-id="9101a-117">AS2 message receiver's partner name.</span><span class="sxs-lookup"><span data-stu-id="9101a-117">AS2 message receiver's partner name.</span></span> <span data-ttu-id="9101a-118">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-118">(Optional)</span></span> |
| <span data-ttu-id="9101a-119">as2To</span><span class="sxs-lookup"><span data-stu-id="9101a-119">as2To</span></span> | <span data-ttu-id="9101a-120">String</span><span class="sxs-lookup"><span data-stu-id="9101a-120">String</span></span> | <span data-ttu-id="9101a-121">AS2 message receiver’s name, from the headers of the AS2 message.</span><span class="sxs-lookup"><span data-stu-id="9101a-121">AS2 message receiver’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="9101a-122">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-122">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-123">as2From</span><span class="sxs-lookup"><span data-stu-id="9101a-123">as2From</span></span> | <span data-ttu-id="9101a-124">String</span><span class="sxs-lookup"><span data-stu-id="9101a-124">String</span></span> | <span data-ttu-id="9101a-125">AS2 message sender’s name, from the headers of the AS2 message.</span><span class="sxs-lookup"><span data-stu-id="9101a-125">AS2 message sender’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="9101a-126">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-126">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-127">agreementName</span><span class="sxs-lookup"><span data-stu-id="9101a-127">agreementName</span></span> | <span data-ttu-id="9101a-128">String</span><span class="sxs-lookup"><span data-stu-id="9101a-128">String</span></span> | <span data-ttu-id="9101a-129">Name of the AS2 agreement to which the messages are resolved.</span><span class="sxs-lookup"><span data-stu-id="9101a-129">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="9101a-130">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-130">(Optional)</span></span> |
| <span data-ttu-id="9101a-131">direction</span><span class="sxs-lookup"><span data-stu-id="9101a-131">direction</span></span> | <span data-ttu-id="9101a-132">String</span><span class="sxs-lookup"><span data-stu-id="9101a-132">String</span></span> | <span data-ttu-id="9101a-133">Direction of the message flow, receive or send.</span><span class="sxs-lookup"><span data-stu-id="9101a-133">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="9101a-134">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-134">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-135">messageId</span><span class="sxs-lookup"><span data-stu-id="9101a-135">messageId</span></span> | <span data-ttu-id="9101a-136">String</span><span class="sxs-lookup"><span data-stu-id="9101a-136">String</span></span> | <span data-ttu-id="9101a-137">AS2 message ID, from the headers of the AS2 message (Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-137">AS2 message ID, from the headers of the AS2 message (Optional)</span></span> |
| <span data-ttu-id="9101a-138">dispositionType</span><span class="sxs-lookup"><span data-stu-id="9101a-138">dispositionType</span></span> |<span data-ttu-id="9101a-139">String</span><span class="sxs-lookup"><span data-stu-id="9101a-139">String</span></span> | <span data-ttu-id="9101a-140">Message Disposition Notification (MDN) disposition type value.</span><span class="sxs-lookup"><span data-stu-id="9101a-140">Message Disposition Notification (MDN) disposition type value.</span></span> <span data-ttu-id="9101a-141">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-141">(Optional)</span></span> |
| <span data-ttu-id="9101a-142">fileName</span><span class="sxs-lookup"><span data-stu-id="9101a-142">fileName</span></span> | <span data-ttu-id="9101a-143">String</span><span class="sxs-lookup"><span data-stu-id="9101a-143">String</span></span> | <span data-ttu-id="9101a-144">File name, from the header of the AS2 message.</span><span class="sxs-lookup"><span data-stu-id="9101a-144">File name, from the header of the AS2 message.</span></span> <span data-ttu-id="9101a-145">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-145">(Optional)</span></span> |
| <span data-ttu-id="9101a-146">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="9101a-146">isMessageFailed</span></span> |<span data-ttu-id="9101a-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-147">Boolean</span></span> | <span data-ttu-id="9101a-148">Whether the AS2 message failed.</span><span class="sxs-lookup"><span data-stu-id="9101a-148">Whether the AS2 message failed.</span></span> <span data-ttu-id="9101a-149">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-149">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-150">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="9101a-150">isMessageSigned</span></span> | <span data-ttu-id="9101a-151">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-151">Boolean</span></span> | <span data-ttu-id="9101a-152">Whether the AS2 message was signed.</span><span class="sxs-lookup"><span data-stu-id="9101a-152">Whether the AS2 message was signed.</span></span> <span data-ttu-id="9101a-153">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-153">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-154">isMessageEncrypted</span><span class="sxs-lookup"><span data-stu-id="9101a-154">isMessageEncrypted</span></span> | <span data-ttu-id="9101a-155">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-155">Boolean</span></span> | <span data-ttu-id="9101a-156">Whether the AS2 message was encrypted.</span><span class="sxs-lookup"><span data-stu-id="9101a-156">Whether the AS2 message was encrypted.</span></span> <span data-ttu-id="9101a-157">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-157">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-158">isMessageCompressed</span><span class="sxs-lookup"><span data-stu-id="9101a-158">isMessageCompressed</span></span> |<span data-ttu-id="9101a-159">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-159">Boolean</span></span> | <span data-ttu-id="9101a-160">Whether the AS2 message was compressed.</span><span class="sxs-lookup"><span data-stu-id="9101a-160">Whether the AS2 message was compressed.</span></span> <span data-ttu-id="9101a-161">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-161">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-162">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="9101a-162">correlationMessageId</span></span> | <span data-ttu-id="9101a-163">String</span><span class="sxs-lookup"><span data-stu-id="9101a-163">String</span></span> | <span data-ttu-id="9101a-164">AS2 message ID, to correlate messages with MDNs.</span><span class="sxs-lookup"><span data-stu-id="9101a-164">AS2 message ID, to correlate messages with MDNs.</span></span> <span data-ttu-id="9101a-165">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-165">(Optional)</span></span> |
| <span data-ttu-id="9101a-166">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="9101a-166">incomingHeaders</span></span> |<span data-ttu-id="9101a-167">Dictionary of JToken</span><span class="sxs-lookup"><span data-stu-id="9101a-167">Dictionary of JToken</span></span> | <span data-ttu-id="9101a-168">Incoming AS2 message header details.</span><span class="sxs-lookup"><span data-stu-id="9101a-168">Incoming AS2 message header details.</span></span> <span data-ttu-id="9101a-169">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-169">(Optional)</span></span> |
| <span data-ttu-id="9101a-170">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="9101a-170">outgoingHeaders</span></span> |<span data-ttu-id="9101a-171">Dictionary of JToken</span><span class="sxs-lookup"><span data-stu-id="9101a-171">Dictionary of JToken</span></span> | <span data-ttu-id="9101a-172">Outgoing AS2 message header details.</span><span class="sxs-lookup"><span data-stu-id="9101a-172">Outgoing AS2 message header details.</span></span> <span data-ttu-id="9101a-173">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-173">(Optional)</span></span> |
| <span data-ttu-id="9101a-174">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="9101a-174">isNrrEnabled</span></span> | <span data-ttu-id="9101a-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-175">Boolean</span></span> | <span data-ttu-id="9101a-176">Use default value if the value is not known.</span><span class="sxs-lookup"><span data-stu-id="9101a-176">Use default value if the value is not known.</span></span> <span data-ttu-id="9101a-177">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-177">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-178">isMdnExpected</span><span class="sxs-lookup"><span data-stu-id="9101a-178">isMdnExpected</span></span> | <span data-ttu-id="9101a-179">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-179">Boolean</span></span> | <span data-ttu-id="9101a-180">Use default value if the value is not known.</span><span class="sxs-lookup"><span data-stu-id="9101a-180">Use default value if the value is not known.</span></span> <span data-ttu-id="9101a-181">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-181">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-182">mdnType</span><span class="sxs-lookup"><span data-stu-id="9101a-182">mdnType</span></span> | <span data-ttu-id="9101a-183">Enum</span><span class="sxs-lookup"><span data-stu-id="9101a-183">Enum</span></span> | <span data-ttu-id="9101a-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span><span class="sxs-lookup"><span data-stu-id="9101a-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span></span> <span data-ttu-id="9101a-185">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-185">(Mandatory)</span></span> |

## <a name="as2-mdn-tracking-schema"></a><span data-ttu-id="9101a-186">AS2 MDN tracking schema</span><span class="sxs-lookup"><span data-stu-id="9101a-186">AS2 MDN tracking schema</span></span>
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| <span data-ttu-id="9101a-187">Property</span><span class="sxs-lookup"><span data-stu-id="9101a-187">Property</span></span> | <span data-ttu-id="9101a-188">Type</span><span class="sxs-lookup"><span data-stu-id="9101a-188">Type</span></span> | <span data-ttu-id="9101a-189">Description</span><span class="sxs-lookup"><span data-stu-id="9101a-189">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9101a-190">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="9101a-190">senderPartnerName</span></span> | <span data-ttu-id="9101a-191">String</span><span class="sxs-lookup"><span data-stu-id="9101a-191">String</span></span> | <span data-ttu-id="9101a-192">AS2 message sender's partner name.</span><span class="sxs-lookup"><span data-stu-id="9101a-192">AS2 message sender's partner name.</span></span> <span data-ttu-id="9101a-193">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-193">(Optional)</span></span> |
| <span data-ttu-id="9101a-194">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="9101a-194">receiverPartnerName</span></span> | <span data-ttu-id="9101a-195">String</span><span class="sxs-lookup"><span data-stu-id="9101a-195">String</span></span> | <span data-ttu-id="9101a-196">AS2 message receiver's partner name.</span><span class="sxs-lookup"><span data-stu-id="9101a-196">AS2 message receiver's partner name.</span></span> <span data-ttu-id="9101a-197">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-197">(Optional)</span></span> |
| <span data-ttu-id="9101a-198">as2To</span><span class="sxs-lookup"><span data-stu-id="9101a-198">as2To</span></span> | <span data-ttu-id="9101a-199">String</span><span class="sxs-lookup"><span data-stu-id="9101a-199">String</span></span> | <span data-ttu-id="9101a-200">Partner name who receives the AS2 message.</span><span class="sxs-lookup"><span data-stu-id="9101a-200">Partner name who receives the AS2 message.</span></span> <span data-ttu-id="9101a-201">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-201">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-202">as2From</span><span class="sxs-lookup"><span data-stu-id="9101a-202">as2From</span></span> | <span data-ttu-id="9101a-203">String</span><span class="sxs-lookup"><span data-stu-id="9101a-203">String</span></span> | <span data-ttu-id="9101a-204">Partner name who sends the AS2 message.</span><span class="sxs-lookup"><span data-stu-id="9101a-204">Partner name who sends the AS2 message.</span></span> <span data-ttu-id="9101a-205">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-205">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-206">agreementName</span><span class="sxs-lookup"><span data-stu-id="9101a-206">agreementName</span></span> | <span data-ttu-id="9101a-207">String</span><span class="sxs-lookup"><span data-stu-id="9101a-207">String</span></span> | <span data-ttu-id="9101a-208">Name of the AS2 agreement to which the messages are resolved.</span><span class="sxs-lookup"><span data-stu-id="9101a-208">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="9101a-209">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-209">(Optional)</span></span> |
| <span data-ttu-id="9101a-210">direction</span><span class="sxs-lookup"><span data-stu-id="9101a-210">direction</span></span> |<span data-ttu-id="9101a-211">String</span><span class="sxs-lookup"><span data-stu-id="9101a-211">String</span></span> | <span data-ttu-id="9101a-212">Direction of the message flow, receive or send.</span><span class="sxs-lookup"><span data-stu-id="9101a-212">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="9101a-213">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-213">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-214">messageId</span><span class="sxs-lookup"><span data-stu-id="9101a-214">messageId</span></span> | <span data-ttu-id="9101a-215">String</span><span class="sxs-lookup"><span data-stu-id="9101a-215">String</span></span> | <span data-ttu-id="9101a-216">AS2 message ID.</span><span class="sxs-lookup"><span data-stu-id="9101a-216">AS2 message ID.</span></span> <span data-ttu-id="9101a-217">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-217">(Optional)</span></span> |
| <span data-ttu-id="9101a-218">originalMessageId</span><span class="sxs-lookup"><span data-stu-id="9101a-218">originalMessageId</span></span> |<span data-ttu-id="9101a-219">String</span><span class="sxs-lookup"><span data-stu-id="9101a-219">String</span></span> | <span data-ttu-id="9101a-220">AS2 original message ID.</span><span class="sxs-lookup"><span data-stu-id="9101a-220">AS2 original message ID.</span></span> <span data-ttu-id="9101a-221">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-221">(Optional)</span></span> |
| <span data-ttu-id="9101a-222">dispositionType</span><span class="sxs-lookup"><span data-stu-id="9101a-222">dispositionType</span></span> | <span data-ttu-id="9101a-223">String</span><span class="sxs-lookup"><span data-stu-id="9101a-223">String</span></span> | <span data-ttu-id="9101a-224">MDN disposition type value.</span><span class="sxs-lookup"><span data-stu-id="9101a-224">MDN disposition type value.</span></span> <span data-ttu-id="9101a-225">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-225">(Optional)</span></span> |
| <span data-ttu-id="9101a-226">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="9101a-226">isMessageFailed</span></span> |<span data-ttu-id="9101a-227">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-227">Boolean</span></span> | <span data-ttu-id="9101a-228">Whether the AS2 message failed.</span><span class="sxs-lookup"><span data-stu-id="9101a-228">Whether the AS2 message failed.</span></span> <span data-ttu-id="9101a-229">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-229">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-230">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="9101a-230">isMessageSigned</span></span> |<span data-ttu-id="9101a-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-231">Boolean</span></span> | <span data-ttu-id="9101a-232">Whether the AS2 message was signed.</span><span class="sxs-lookup"><span data-stu-id="9101a-232">Whether the AS2 message was signed.</span></span> <span data-ttu-id="9101a-233">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-233">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-234">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="9101a-234">isNrrEnabled</span></span> | <span data-ttu-id="9101a-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="9101a-235">Boolean</span></span> | <span data-ttu-id="9101a-236">Use default value if the value is not known.</span><span class="sxs-lookup"><span data-stu-id="9101a-236">Use default value if the value is not known.</span></span> <span data-ttu-id="9101a-237">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-237">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-238">statusCode</span><span class="sxs-lookup"><span data-stu-id="9101a-238">statusCode</span></span> | <span data-ttu-id="9101a-239">Enum</span><span class="sxs-lookup"><span data-stu-id="9101a-239">Enum</span></span> | <span data-ttu-id="9101a-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span><span class="sxs-lookup"><span data-stu-id="9101a-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span></span> <span data-ttu-id="9101a-241">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-241">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-242">micVerificationStatus</span><span class="sxs-lookup"><span data-stu-id="9101a-242">micVerificationStatus</span></span> | <span data-ttu-id="9101a-243">Enum</span><span class="sxs-lookup"><span data-stu-id="9101a-243">Enum</span></span> | <span data-ttu-id="9101a-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span><span class="sxs-lookup"><span data-stu-id="9101a-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span></span> <span data-ttu-id="9101a-245">(Mandatory)</span><span class="sxs-lookup"><span data-stu-id="9101a-245">(Mandatory)</span></span> |
| <span data-ttu-id="9101a-246">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="9101a-246">correlationMessageId</span></span> | <span data-ttu-id="9101a-247">String</span><span class="sxs-lookup"><span data-stu-id="9101a-247">String</span></span> | <span data-ttu-id="9101a-248">Correlation ID.</span><span class="sxs-lookup"><span data-stu-id="9101a-248">Correlation ID.</span></span> <span data-ttu-id="9101a-249">The original messaged ID (the message ID of the message for which MDN is configured).</span><span class="sxs-lookup"><span data-stu-id="9101a-249">The original messaged ID (the message ID of the message for which MDN is configured).</span></span> <span data-ttu-id="9101a-250">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-250">(Optional)</span></span> |
| <span data-ttu-id="9101a-251">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="9101a-251">incomingHeaders</span></span> | <span data-ttu-id="9101a-252">Dictionary of JToken</span><span class="sxs-lookup"><span data-stu-id="9101a-252">Dictionary of JToken</span></span> | <span data-ttu-id="9101a-253">Indicates incoming message header details.</span><span class="sxs-lookup"><span data-stu-id="9101a-253">Indicates incoming message header details.</span></span> <span data-ttu-id="9101a-254">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-254">(Optional)</span></span> |
| <span data-ttu-id="9101a-255">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="9101a-255">outgoingHeaders</span></span> |<span data-ttu-id="9101a-256">Dictionary of JToken</span><span class="sxs-lookup"><span data-stu-id="9101a-256">Dictionary of JToken</span></span> | <span data-ttu-id="9101a-257">Indicates outgoing message header details.</span><span class="sxs-lookup"><span data-stu-id="9101a-257">Indicates outgoing message header details.</span></span> <span data-ttu-id="9101a-258">(Optional)</span><span class="sxs-lookup"><span data-stu-id="9101a-258">(Optional)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9101a-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="9101a-259">Next steps</span></span>
* <span data-ttu-id="9101a-260">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9101a-260">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>    
* <span data-ttu-id="9101a-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="9101a-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="9101a-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9101a-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="9101a-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9101a-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>   
* <span data-ttu-id="9101a-264">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="9101a-264">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
