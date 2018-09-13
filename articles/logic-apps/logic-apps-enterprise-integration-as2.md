---
title: AS2 messages for B2B enterprise integration - Azure Logic Apps | Microsoft Docs
description: Exchange AS2 messages for B2B enterprise integration with Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: mandia
ms.openlocfilehash: 7975dde0e8bdf4560ee404627df2e75cc2b81b68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556728"
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="0a58a-103">Exchange AS2 messages for enterprise integration with logic apps</span><span class="sxs-lookup"><span data-stu-id="0a58a-103">Exchange AS2 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="0a58a-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span><span class="sxs-lookup"><span data-stu-id="0a58a-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="0a58a-105">Here are the steps for how to create an AS2 agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-105">Here are the steps for how to create an AS2 agreement.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0a58a-106">Before you start</span><span class="sxs-lookup"><span data-stu-id="0a58a-106">Before you start</span></span>

<span data-ttu-id="0a58a-107">Here's the items you need:</span><span class="sxs-lookup"><span data-stu-id="0a58a-107">Here's the items you need:</span></span>

* <span data-ttu-id="0a58a-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0a58a-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="0a58a-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with the AS2 qualifier under **Business Identities**</span><span class="sxs-lookup"><span data-stu-id="0a58a-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with the AS2 qualifier under **Business Identities**</span></span>

> [!NOTE]
> <span data-ttu-id="0a58a-110">When you create an agreement, the content in the agreement file must match the agreement type.</span><span class="sxs-lookup"><span data-stu-id="0a58a-110">When you create an agreement, the content in the agreement file must match the agreement type.</span></span>    

<span data-ttu-id="0a58a-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span><span class="sxs-lookup"><span data-stu-id="0a58a-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span></span>

## <a name="create-an-as2-agreement"></a><span data-ttu-id="0a58a-112">Create an AS2 agreement</span><span class="sxs-lookup"><span data-stu-id="0a58a-112">Create an AS2 agreement</span></span>

1.  <span data-ttu-id="0a58a-113">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="0a58a-113">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span>  

2.  <span data-ttu-id="0a58a-114">From the left menu, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-114">From the left menu, select **More services**.</span></span> <span data-ttu-id="0a58a-115">In the search box, enter **integration** as your filter.</span><span class="sxs-lookup"><span data-stu-id="0a58a-115">In the search box, enter **integration** as your filter.</span></span> <span data-ttu-id="0a58a-116">In the results list, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-116">In the results list, select **Integration Accounts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="0a58a-117">If you don't see **More services**, you might have to expand the menu first.</span><span class="sxs-lookup"><span data-stu-id="0a58a-117">If you don't see **More services**, you might have to expand the menu first.</span></span> <span data-ttu-id="0a58a-118">At the top of the collapsed menu, select **Show menu**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-118">At the top of the collapsed menu, select **Show menu**.</span></span>

    ![More services, filter on "integration", select "Integration Accounts"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. <span data-ttu-id="0a58a-120">In the **Integration Accounts** blade that opens, select the integration account where you want to create the agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-120">In the **Integration Accounts** blade that opens, select the integration account where you want to create the agreement.</span></span>
<span data-ttu-id="0a58a-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span><span class="sxs-lookup"><span data-stu-id="0a58a-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>  

    ![Select the integration account where to create the agreement](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="0a58a-123">Choose the **Agreements** tile.</span><span class="sxs-lookup"><span data-stu-id="0a58a-123">Choose the **Agreements** tile.</span></span> <span data-ttu-id="0a58a-124">If you don't have an Agreements tile, add the tile first.</span><span class="sxs-lookup"><span data-stu-id="0a58a-124">If you don't have an Agreements tile, add the tile first.</span></span>

    ![Choose "Agreements" tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="0a58a-126">In the Agreements blade that opens, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-126">In the Agreements blade that opens, choose **Add**.</span></span>

    ![Choose "Add"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. <span data-ttu-id="0a58a-128">Under **Add**, enter a **Name** for your agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-128">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="0a58a-129">For **Agreement type**, select **AS2**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-129">For **Agreement type**, select **AS2**.</span></span> <span data-ttu-id="0a58a-130">Select the **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-130">Select the **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span>

    ![Provide agreement details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | <span data-ttu-id="0a58a-132">Property</span><span class="sxs-lookup"><span data-stu-id="0a58a-132">Property</span></span> | <span data-ttu-id="0a58a-133">Description</span><span class="sxs-lookup"><span data-stu-id="0a58a-133">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="0a58a-134">Name</span><span class="sxs-lookup"><span data-stu-id="0a58a-134">Name</span></span> |<span data-ttu-id="0a58a-135">Name of the agreement</span><span class="sxs-lookup"><span data-stu-id="0a58a-135">Name of the agreement</span></span> |
    | <span data-ttu-id="0a58a-136">Agreement Type</span><span class="sxs-lookup"><span data-stu-id="0a58a-136">Agreement Type</span></span> | <span data-ttu-id="0a58a-137">Should be AS2</span><span class="sxs-lookup"><span data-stu-id="0a58a-137">Should be AS2</span></span> |
    | <span data-ttu-id="0a58a-138">Host Partner</span><span class="sxs-lookup"><span data-stu-id="0a58a-138">Host Partner</span></span> |<span data-ttu-id="0a58a-139">An agreement needs both a host and guest partner.</span><span class="sxs-lookup"><span data-stu-id="0a58a-139">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="0a58a-140">The host partner represents the organization that configures the agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-140">The host partner represents the organization that configures the agreement.</span></span> |
    | <span data-ttu-id="0a58a-141">Host Identity</span><span class="sxs-lookup"><span data-stu-id="0a58a-141">Host Identity</span></span> |<span data-ttu-id="0a58a-142">An identifier for the host partner</span><span class="sxs-lookup"><span data-stu-id="0a58a-142">An identifier for the host partner</span></span> |
    | <span data-ttu-id="0a58a-143">Guest Partner</span><span class="sxs-lookup"><span data-stu-id="0a58a-143">Guest Partner</span></span> |<span data-ttu-id="0a58a-144">An agreement needs both a host and guest partner.</span><span class="sxs-lookup"><span data-stu-id="0a58a-144">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="0a58a-145">The guest partner represents the organization that's doing business with the host partner.</span><span class="sxs-lookup"><span data-stu-id="0a58a-145">The guest partner represents the organization that's doing business with the host partner.</span></span> |
    | <span data-ttu-id="0a58a-146">Guest Identity</span><span class="sxs-lookup"><span data-stu-id="0a58a-146">Guest Identity</span></span> |<span data-ttu-id="0a58a-147">An identifier for the guest partner</span><span class="sxs-lookup"><span data-stu-id="0a58a-147">An identifier for the guest partner</span></span> |
    | <span data-ttu-id="0a58a-148">Receive Settings</span><span class="sxs-lookup"><span data-stu-id="0a58a-148">Receive Settings</span></span> |<span data-ttu-id="0a58a-149">These properties apply to all messages received by an agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-149">These properties apply to all messages received by an agreement.</span></span> |
    | <span data-ttu-id="0a58a-150">Send Settings</span><span class="sxs-lookup"><span data-stu-id="0a58a-150">Send Settings</span></span> |<span data-ttu-id="0a58a-151">These properties apply to all messages sent by an agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-151">These properties apply to all messages sent by an agreement.</span></span> |

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="0a58a-152">Configure how your agreement handles received messages</span><span class="sxs-lookup"><span data-stu-id="0a58a-152">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="0a58a-153">Now that you've set the agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-153">Now that you've set the agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="0a58a-154">Under **Add**, select **Receive Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-154">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="0a58a-155">Configure these properties based on your agreement with the partner that exchanges messages with you.</span><span class="sxs-lookup"><span data-stu-id="0a58a-155">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="0a58a-156">For property descriptions, see the table in this section.</span><span class="sxs-lookup"><span data-stu-id="0a58a-156">For property descriptions, see the table in this section.</span></span>

    ![Configure "Receive Settings"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. <span data-ttu-id="0a58a-158">Optionally, you can override the properties of incoming messages by selecting **Override message properties**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-158">Optionally, you can override the properties of incoming messages by selecting **Override message properties**.</span></span>

3. <span data-ttu-id="0a58a-159">To require all incoming messages to be signed, select **Message should be signed**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-159">To require all incoming messages to be signed, select **Message should be signed**.</span></span> <span data-ttu-id="0a58a-160">From the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating the signature on the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-160">From the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating the signature on the messages.</span></span> <span data-ttu-id="0a58a-161">Or create the certificate, if you don't have one.</span><span class="sxs-lookup"><span data-stu-id="0a58a-161">Or create the certificate, if you don't have one.</span></span>

4.  <span data-ttu-id="0a58a-162">To require all incoming messages to be encrypted, select **Message should be encrypted**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-162">To require all incoming messages to be encrypted, select **Message should be encrypted**.</span></span> <span data-ttu-id="0a58a-163">From the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-163">From the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span></span> <span data-ttu-id="0a58a-164">Or create the certificate, if you don't have one.</span><span class="sxs-lookup"><span data-stu-id="0a58a-164">Or create the certificate, if you don't have one.</span></span>

5. <span data-ttu-id="0a58a-165">To require messages to be compressed, select **Message should be compressed**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-165">To require messages to be compressed, select **Message should be compressed**.</span></span>

6. <span data-ttu-id="0a58a-166">To send a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-166">To send a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span></span>

7. <span data-ttu-id="0a58a-167">To send signed MDNs for received messages, select **Send signed MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-167">To send signed MDNs for received messages, select **Send signed MDN**.</span></span>

8. <span data-ttu-id="0a58a-168">To send asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-168">To send asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span></span>

9. <span data-ttu-id="0a58a-169">After you're done, make sure to save your settings by choosing **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-169">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="0a58a-170">Now your agreement is ready to handle incoming messages that conform to your selected settings.</span><span class="sxs-lookup"><span data-stu-id="0a58a-170">Now your agreement is ready to handle incoming messages that conform to your selected settings.</span></span>

| <span data-ttu-id="0a58a-171">Property</span><span class="sxs-lookup"><span data-stu-id="0a58a-171">Property</span></span> | <span data-ttu-id="0a58a-172">Description</span><span class="sxs-lookup"><span data-stu-id="0a58a-172">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a58a-173">Override message properties</span><span class="sxs-lookup"><span data-stu-id="0a58a-173">Override message properties</span></span> |<span data-ttu-id="0a58a-174">Indicates that properties in received messages can be overridden.</span><span class="sxs-lookup"><span data-stu-id="0a58a-174">Indicates that properties in received messages can be overridden.</span></span> |
| <span data-ttu-id="0a58a-175">Message should be signed</span><span class="sxs-lookup"><span data-stu-id="0a58a-175">Message should be signed</span></span> |<span data-ttu-id="0a58a-176">Requires messages to be digitally signed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-176">Requires messages to be digitally signed.</span></span> <span data-ttu-id="0a58a-177">Configure the guest partner public certificate for signature verification.</span><span class="sxs-lookup"><span data-stu-id="0a58a-177">Configure the guest partner public certificate for signature verification.</span></span>  |
| <span data-ttu-id="0a58a-178">Message should be encrypted</span><span class="sxs-lookup"><span data-stu-id="0a58a-178">Message should be encrypted</span></span> |<span data-ttu-id="0a58a-179">Requires messages to be encrypted.</span><span class="sxs-lookup"><span data-stu-id="0a58a-179">Requires messages to be encrypted.</span></span> <span data-ttu-id="0a58a-180">Non-encrypted messages are rejected.</span><span class="sxs-lookup"><span data-stu-id="0a58a-180">Non-encrypted messages are rejected.</span></span> <span data-ttu-id="0a58a-181">Configure the host partner private certificate for decrypting the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-181">Configure the host partner private certificate for decrypting the messages.</span></span>  |
| <span data-ttu-id="0a58a-182">Message should be compressed</span><span class="sxs-lookup"><span data-stu-id="0a58a-182">Message should be compressed</span></span> |<span data-ttu-id="0a58a-183">Requires messages to be compressed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-183">Requires messages to be compressed.</span></span> <span data-ttu-id="0a58a-184">Non-compressed messages are rejected.</span><span class="sxs-lookup"><span data-stu-id="0a58a-184">Non-compressed messages are rejected.</span></span> |
| <span data-ttu-id="0a58a-185">MDN Text</span><span class="sxs-lookup"><span data-stu-id="0a58a-185">MDN Text</span></span> |<span data-ttu-id="0a58a-186">The default message disposition notification (MDN) to be sent to the message sender.</span><span class="sxs-lookup"><span data-stu-id="0a58a-186">The default message disposition notification (MDN) to be sent to the message sender.</span></span> |
| <span data-ttu-id="0a58a-187">Send MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-187">Send MDN</span></span> |<span data-ttu-id="0a58a-188">Requires MDNs to be sent.</span><span class="sxs-lookup"><span data-stu-id="0a58a-188">Requires MDNs to be sent.</span></span> |
| <span data-ttu-id="0a58a-189">Send signed MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-189">Send signed MDN</span></span> |<span data-ttu-id="0a58a-190">Requires MDNs to be signed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-190">Requires MDNs to be signed.</span></span> |
| <span data-ttu-id="0a58a-191">MIC Algorithm</span><span class="sxs-lookup"><span data-stu-id="0a58a-191">MIC Algorithm</span></span> |<span data-ttu-id="0a58a-192">Select the algorithm to use for signing messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-192">Select the algorithm to use for signing messages.</span></span> |
| <span data-ttu-id="0a58a-193">Send asynchronous MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-193">Send asynchronous MDN</span></span> | <span data-ttu-id="0a58a-194">Requires messages to be sent asynchronously.</span><span class="sxs-lookup"><span data-stu-id="0a58a-194">Requires messages to be sent asynchronously.</span></span> |
| <span data-ttu-id="0a58a-195">URL</span><span class="sxs-lookup"><span data-stu-id="0a58a-195">URL</span></span> | <span data-ttu-id="0a58a-196">Specify the URL where to send the MDNs.</span><span class="sxs-lookup"><span data-stu-id="0a58a-196">Specify the URL where to send the MDNs.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="0a58a-197">Configure how your agreement sends messages</span><span class="sxs-lookup"><span data-stu-id="0a58a-197">Configure how your agreement sends messages</span></span>

<span data-ttu-id="0a58a-198">You can configure how this agreement identifies and handles outgoing messages that you send to your partners through this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-198">You can configure how this agreement identifies and handles outgoing messages that you send to your partners through this agreement.</span></span>

1.  <span data-ttu-id="0a58a-199">Under **Add**, select **Send Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-199">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="0a58a-200">Configure these properties based on your agreement with the partner that exchanges messages with you.</span><span class="sxs-lookup"><span data-stu-id="0a58a-200">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="0a58a-201">For property descriptions, see the table in this section.</span><span class="sxs-lookup"><span data-stu-id="0a58a-201">For property descriptions, see the table in this section.</span></span>

    ![Set the "Send Settings" properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-5.png)

2. <span data-ttu-id="0a58a-203">To send signed messages to your partner, select **Enable message signing**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-203">To send signed messages to your partner, select **Enable message signing**.</span></span> <span data-ttu-id="0a58a-204">For signing the messages, in the **MIC Algorithm** list, select the *host partner private certificate MIC Algorithm*.</span><span class="sxs-lookup"><span data-stu-id="0a58a-204">For signing the messages, in the **MIC Algorithm** list, select the *host partner private certificate MIC Algorithm*.</span></span> <span data-ttu-id="0a58a-205">And in the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="0a58a-205">And in the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

3. <span data-ttu-id="0a58a-206">To send encrypted messages to the partner, select **Enable message encryption**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-206">To send encrypted messages to the partner, select **Enable message encryption**.</span></span> <span data-ttu-id="0a58a-207">For encrypting the messages, in the **Encryption Algorithm** list, select the *guest partner public certificate algorithm*.</span><span class="sxs-lookup"><span data-stu-id="0a58a-207">For encrypting the messages, in the **Encryption Algorithm** list, select the *guest partner public certificate algorithm*.</span></span>
<span data-ttu-id="0a58a-208">And in the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="0a58a-208">And in the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

4. <span data-ttu-id="0a58a-209">To compress the message, select **Enable message compression**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-209">To compress the message, select **Enable message compression**.</span></span>

5. <span data-ttu-id="0a58a-210">To unfold the HTTP content-type header into a single line, select **Unfold HTTP headers**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-210">To unfold the HTTP content-type header into a single line, select **Unfold HTTP headers**.</span></span>

6. <span data-ttu-id="0a58a-211">To receive synchronous MDNs for the sent messages, select **Request MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-211">To receive synchronous MDNs for the sent messages, select **Request MDN**.</span></span>

7. <span data-ttu-id="0a58a-212">To receive signed MDNs for the sent messages, select **Request signed MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-212">To receive signed MDNs for the sent messages, select **Request signed MDN**.</span></span>

8. <span data-ttu-id="0a58a-213">To receive asynchronous MDNs for the sent messages, select **Request asynchronous MDN**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-213">To receive asynchronous MDNs for the sent messages, select **Request asynchronous MDN**.</span></span> <span data-ttu-id="0a58a-214">If you select this option, enter the URL for where to send the MDNs.</span><span class="sxs-lookup"><span data-stu-id="0a58a-214">If you select this option, enter the URL for where to send the MDNs.</span></span>

9. <span data-ttu-id="0a58a-215">To require non-repudiation of receipt, select **Enable NRR**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-215">To require non-repudiation of receipt, select **Enable NRR**.</span></span>

10. <span data-ttu-id="0a58a-216">After you're done, make sure to save your settings by choosing **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a58a-216">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="0a58a-217">Now your agreement is ready to handle outgoing messages that conform to your selected settings.</span><span class="sxs-lookup"><span data-stu-id="0a58a-217">Now your agreement is ready to handle outgoing messages that conform to your selected settings.</span></span>

| <span data-ttu-id="0a58a-218">Property</span><span class="sxs-lookup"><span data-stu-id="0a58a-218">Property</span></span> | <span data-ttu-id="0a58a-219">Description</span><span class="sxs-lookup"><span data-stu-id="0a58a-219">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a58a-220">Enable message signing</span><span class="sxs-lookup"><span data-stu-id="0a58a-220">Enable message signing</span></span> |<span data-ttu-id="0a58a-221">Requires all messages that are sent from the agreement to be signed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-221">Requires all messages that are sent from the agreement to be signed.</span></span> |
| <span data-ttu-id="0a58a-222">MIC Algorithm</span><span class="sxs-lookup"><span data-stu-id="0a58a-222">MIC Algorithm</span></span> |<span data-ttu-id="0a58a-223">The algorithm to use for signing messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-223">The algorithm to use for signing messages.</span></span> <span data-ttu-id="0a58a-224">Configures the host partner private certificate MIC Algorithm for signing the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-224">Configures the host partner private certificate MIC Algorithm for signing the messages.</span></span> |
| <span data-ttu-id="0a58a-225">Certificate</span><span class="sxs-lookup"><span data-stu-id="0a58a-225">Certificate</span></span> |<span data-ttu-id="0a58a-226">Select the certificate to use for signing messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-226">Select the certificate to use for signing messages.</span></span> <span data-ttu-id="0a58a-227">Configures the host partner private certificate for signing the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-227">Configures the host partner private certificate for signing the messages.</span></span> |
| <span data-ttu-id="0a58a-228">Enable message encryption</span><span class="sxs-lookup"><span data-stu-id="0a58a-228">Enable message encryption</span></span> |<span data-ttu-id="0a58a-229">Requires encryption of all messages that are sent from this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-229">Requires encryption of all messages that are sent from this agreement.</span></span> <span data-ttu-id="0a58a-230">Configures the guest partner public certificate algorithm for encrypting the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-230">Configures the guest partner public certificate algorithm for encrypting the messages.</span></span> |
| <span data-ttu-id="0a58a-231">Encryption Algorithm</span><span class="sxs-lookup"><span data-stu-id="0a58a-231">Encryption Algorithm</span></span> |<span data-ttu-id="0a58a-232">The encryption algorithm to use for message encryption.</span><span class="sxs-lookup"><span data-stu-id="0a58a-232">The encryption algorithm to use for message encryption.</span></span> <span data-ttu-id="0a58a-233">Configures the guest partner public certificate for encrypting the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-233">Configures the guest partner public certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="0a58a-234">Certificate</span><span class="sxs-lookup"><span data-stu-id="0a58a-234">Certificate</span></span> |<span data-ttu-id="0a58a-235">The certificate to use to encrypt messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-235">The certificate to use to encrypt messages.</span></span> <span data-ttu-id="0a58a-236">Configures the guest partner private certificate for encrypting the messages.</span><span class="sxs-lookup"><span data-stu-id="0a58a-236">Configures the guest partner private certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="0a58a-237">Enable message compression</span><span class="sxs-lookup"><span data-stu-id="0a58a-237">Enable message compression</span></span> |<span data-ttu-id="0a58a-238">Requires compression of all messages that are sent from this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-238">Requires compression of all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="0a58a-239">Unfold HTTP headers</span><span class="sxs-lookup"><span data-stu-id="0a58a-239">Unfold HTTP headers</span></span> |<span data-ttu-id="0a58a-240">Places the HTTP content-type header onto a single line.</span><span class="sxs-lookup"><span data-stu-id="0a58a-240">Places the HTTP content-type header onto a single line.</span></span> |
| <span data-ttu-id="0a58a-241">Request MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-241">Request MDN</span></span> |<span data-ttu-id="0a58a-242">Requires an MDN for all messages that are sent from this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-242">Requires an MDN for all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="0a58a-243">Request signed MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-243">Request signed MDN</span></span> |<span data-ttu-id="0a58a-244">Requires all MDNs that are sent to this agreement to be signed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-244">Requires all MDNs that are sent to this agreement to be signed.</span></span> |
| <span data-ttu-id="0a58a-245">Request asynchronous MDN</span><span class="sxs-lookup"><span data-stu-id="0a58a-245">Request asynchronous MDN</span></span> |<span data-ttu-id="0a58a-246">Requires asynchronous MDNs to be sent to this agreement.</span><span class="sxs-lookup"><span data-stu-id="0a58a-246">Requires asynchronous MDNs to be sent to this agreement.</span></span> |
| <span data-ttu-id="0a58a-247">URL</span><span class="sxs-lookup"><span data-stu-id="0a58a-247">URL</span></span> |<span data-ttu-id="0a58a-248">Specify the URL where to send the MDNs.</span><span class="sxs-lookup"><span data-stu-id="0a58a-248">Specify the URL where to send the MDNs.</span></span> |
| <span data-ttu-id="0a58a-249">Enable NRR</span><span class="sxs-lookup"><span data-stu-id="0a58a-249">Enable NRR</span></span> |<span data-ttu-id="0a58a-250">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that the data was received as addressed.</span><span class="sxs-lookup"><span data-stu-id="0a58a-250">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that the data was received as addressed.</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="0a58a-251">Find your created agreement</span><span class="sxs-lookup"><span data-stu-id="0a58a-251">Find your created agreement</span></span>

1.  <span data-ttu-id="0a58a-252">After you finish setting all your agreement properties, on the **Add** blade, choose **OK** to finish creating your agreement and return to your integration account blade.</span><span class="sxs-lookup"><span data-stu-id="0a58a-252">After you finish setting all your agreement properties, on the **Add** blade, choose **OK** to finish creating your agreement and return to your integration account blade.</span></span>

    <span data-ttu-id="0a58a-253">Your newly added agreement now appears in your **Agreements** list.</span><span class="sxs-lookup"><span data-stu-id="0a58a-253">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="0a58a-254">You can also view your agreements in your integration account overview.</span><span class="sxs-lookup"><span data-stu-id="0a58a-254">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="0a58a-255">On your integration account blade, choose **Overview**, then select the **Agreements** tile.</span><span class="sxs-lookup"><span data-stu-id="0a58a-255">On your integration account blade, choose **Overview**, then select the **Agreements** tile.</span></span> 

    ![Choose "Agreements" tile to view all agreements](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="next-steps"></a><span data-ttu-id="0a58a-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a58a-257">Next steps</span></span>
* [<span data-ttu-id="0a58a-258">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0a58a-258">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  








