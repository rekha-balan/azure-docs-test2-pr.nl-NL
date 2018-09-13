---
title: Batch process EDI messages as a group or collection - Azure Logic Apps | Microsoft Docs
description: Send EDI messages for batch processing in logic apps
services: logic-apps
ms.service: logic-apps
author: divyaswarnkar
ms.author: divswa
ms.reviewer: estfan, LADocs
ms.topic: article
ms.date: 08/19/2018
ms.openlocfilehash: 7e058b7cebb9c2cdc3fb8b97bf99554b2f26dd8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856459"
---
# <a name="send-edi-messages-in-batches-to-trading-partners-with-azure-logic-apps"></a><span data-ttu-id="92b14-103">Send EDI messages in batches to trading partners with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="92b14-103">Send EDI messages in batches to trading partners with Azure Logic Apps</span></span>

<span data-ttu-id="92b14-104">In business to business (B2B) scenarios, partners often exchange messages in groups or *batches*.</span><span class="sxs-lookup"><span data-stu-id="92b14-104">In business to business (B2B) scenarios, partners often exchange messages in groups or *batches*.</span></span> <span data-ttu-id="92b14-105">When you build a batching solution with Logic Apps, you can send messages to trading partners and process those messages together in batches.</span><span class="sxs-lookup"><span data-stu-id="92b14-105">When you build a batching solution with Logic Apps, you can send messages to trading partners and process those messages together in batches.</span></span> <span data-ttu-id="92b14-106">This article shows how you can batch process EDI messages, using X12 as an example, by creating a "batch sender" logic app and a "batch receiver" logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-106">This article shows how you can batch process EDI messages, using X12 as an example, by creating a "batch sender" logic app and a "batch receiver" logic app.</span></span> 

<span data-ttu-id="92b14-107">Batching X12 messages works like batching other messages; you use a batch trigger that collects messages into a batch and a batch action that sends messages to the batch.</span><span class="sxs-lookup"><span data-stu-id="92b14-107">Batching X12 messages works like batching other messages; you use a batch trigger that collects messages into a batch and a batch action that sends messages to the batch.</span></span> <span data-ttu-id="92b14-108">Also, X12 batching includes an X12 encoding step before the messages go to the trading partner or other destination.</span><span class="sxs-lookup"><span data-stu-id="92b14-108">Also, X12 batching includes an X12 encoding step before the messages go to the trading partner or other destination.</span></span> <span data-ttu-id="92b14-109">To learn more about the batch trigger and action, see [Batch process messages](../logic-apps/logic-apps-batch-process-send-receive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="92b14-109">To learn more about the batch trigger and action, see [Batch process messages](../logic-apps/logic-apps-batch-process-send-receive-messages.md).</span></span>

<span data-ttu-id="92b14-110">In this article, you'll build a batching solution by creating two logic apps within the same Azure subscription, Azure region, and following this specific order:</span><span class="sxs-lookup"><span data-stu-id="92b14-110">In this article, you'll build a batching solution by creating two logic apps within the same Azure subscription, Azure region, and following this specific order:</span></span>

* <span data-ttu-id="92b14-111">A ["batch receiver"](#receiver) logic app, which accepts and collects messages into a batch until your specified criteria is met for releasing and processing those messages.</span><span class="sxs-lookup"><span data-stu-id="92b14-111">A ["batch receiver"](#receiver) logic app, which accepts and collects messages into a batch until your specified criteria is met for releasing and processing those messages.</span></span> <span data-ttu-id="92b14-112">In this scenario, the batch receiver also encodes the messages in the batch by using the specified X12 agreement or partner identities.</span><span class="sxs-lookup"><span data-stu-id="92b14-112">In this scenario, the batch receiver also encodes the messages in the batch by using the specified X12 agreement or partner identities.</span></span>

  <span data-ttu-id="92b14-113">Make sure you first create the batch receiver so you can later select the batch destination when you create the batch sender.</span><span class="sxs-lookup"><span data-stu-id="92b14-113">Make sure you first create the batch receiver so you can later select the batch destination when you create the batch sender.</span></span>

* <span data-ttu-id="92b14-114">A ["batch sender"](#sender) logic app, which sends the messages to the previously created batch receiver.</span><span class="sxs-lookup"><span data-stu-id="92b14-114">A ["batch sender"](#sender) logic app, which sends the messages to the previously created batch receiver.</span></span> 

<span data-ttu-id="92b14-115">Make sure your batch receiver and batch sender share the same Azure subscription *and* Azure region.</span><span class="sxs-lookup"><span data-stu-id="92b14-115">Make sure your batch receiver and batch sender share the same Azure subscription *and* Azure region.</span></span> <span data-ttu-id="92b14-116">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span><span class="sxs-lookup"><span data-stu-id="92b14-116">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92b14-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92b14-117">Prerequisites</span></span>

<span data-ttu-id="92b14-118">To follow this example, you need these items:</span><span class="sxs-lookup"><span data-stu-id="92b14-118">To follow this example, you need these items:</span></span>

* <span data-ttu-id="92b14-119">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="92b14-119">An Azure subscription.</span></span> <span data-ttu-id="92b14-120">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="92b14-120">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="92b14-121">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="92b14-121">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="92b14-122">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="92b14-122">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="92b14-123">An existing [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) that's associated with your Azure subscription and is linked to your logic apps</span><span class="sxs-lookup"><span data-stu-id="92b14-123">An existing [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) that's associated with your Azure subscription and is linked to your logic apps</span></span>

* <span data-ttu-id="92b14-124">At least two existing [partners](../logic-apps/logic-apps-enterprise-integration-partners.md) in your integration account.</span><span class="sxs-lookup"><span data-stu-id="92b14-124">At least two existing [partners](../logic-apps/logic-apps-enterprise-integration-partners.md) in your integration account.</span></span> <span data-ttu-id="92b14-125">Each partner must use the X12 (Standard Carrier Alpha Code) qualifier as a business identity in the partner's properties.</span><span class="sxs-lookup"><span data-stu-id="92b14-125">Each partner must use the X12 (Standard Carrier Alpha Code) qualifier as a business identity in the partner's properties.</span></span>

* <span data-ttu-id="92b14-126">An existing [X12 agreement](../logic-apps/logic-apps-enterprise-integration-x12.md) in your integration account</span><span class="sxs-lookup"><span data-stu-id="92b14-126">An existing [X12 agreement](../logic-apps/logic-apps-enterprise-integration-x12.md) in your integration account</span></span>

* <span data-ttu-id="92b14-127">To use Visual Studio rather than the Azure portal, make sure you [set up Visual Studio for working with Logic Apps](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="92b14-127">To use Visual Studio rather than the Azure portal, make sure you [set up Visual Studio for working with Logic Apps](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span></span>

<a name="receiver"></a>

## <a name="create-x12-batch-receiver"></a><span data-ttu-id="92b14-128">Create X12 batch receiver</span><span class="sxs-lookup"><span data-stu-id="92b14-128">Create X12 batch receiver</span></span>

<span data-ttu-id="92b14-129">Before you can send messages to a batch, that batch must first exist as the destination where you send those messages.</span><span class="sxs-lookup"><span data-stu-id="92b14-129">Before you can send messages to a batch, that batch must first exist as the destination where you send those messages.</span></span> <span data-ttu-id="92b14-130">So first, you must create the "batch receiver" logic app, which starts with the **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="92b14-130">So first, you must create the "batch receiver" logic app, which starts with the **Batch** trigger.</span></span> <span data-ttu-id="92b14-131">That way, when you create the "batch sender" logic app, you can select the batch receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-131">That way, when you create the "batch sender" logic app, you can select the batch receiver logic app.</span></span> <span data-ttu-id="92b14-132">The batch receiver continues collecting messages until your specified criteria is met for releasing and processing those messages.</span><span class="sxs-lookup"><span data-stu-id="92b14-132">The batch receiver continues collecting messages until your specified criteria is met for releasing and processing those messages.</span></span> <span data-ttu-id="92b14-133">While batch receivers don't need to know anything about batch senders, batch senders must know the destination where they send the messages.</span><span class="sxs-lookup"><span data-stu-id="92b14-133">While batch receivers don't need to know anything about batch senders, batch senders must know the destination where they send the messages.</span></span> 

<span data-ttu-id="92b14-134">For this batch receiver, you specify the batch mode, name, release criteria, X12 agreement, and other settings.</span><span class="sxs-lookup"><span data-stu-id="92b14-134">For this batch receiver, you specify the batch mode, name, release criteria, X12 agreement, and other settings.</span></span> 

1. <span data-ttu-id="92b14-135">In the [Azure portal](https://portal.azure.com) or Visual Studio, create a logic app with this name: "BatchX12Messages"</span><span class="sxs-lookup"><span data-stu-id="92b14-135">In the [Azure portal](https://portal.azure.com) or Visual Studio, create a logic app with this name: "BatchX12Messages"</span></span>

2. <span data-ttu-id="92b14-136">[Link your logic app to your integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md#link-account).</span><span class="sxs-lookup"><span data-stu-id="92b14-136">[Link your logic app to your integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md#link-account).</span></span>

3. <span data-ttu-id="92b14-137">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="92b14-137">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="92b14-138">In the search box, enter "batch" as your filter.</span><span class="sxs-lookup"><span data-stu-id="92b14-138">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="92b14-139">Select this trigger: **Batch messages**</span><span class="sxs-lookup"><span data-stu-id="92b14-139">Select this trigger: **Batch messages**</span></span>

   ![Add Batch trigger](./media/logic-apps-scenario-EDI-send-batch-messages/add-batch-receiver-trigger.png)

4. <span data-ttu-id="92b14-141">Set the batch receiver properties:</span><span class="sxs-lookup"><span data-stu-id="92b14-141">Set the batch receiver properties:</span></span> 

   | <span data-ttu-id="92b14-142">Property</span><span class="sxs-lookup"><span data-stu-id="92b14-142">Property</span></span> | <span data-ttu-id="92b14-143">Value</span><span class="sxs-lookup"><span data-stu-id="92b14-143">Value</span></span> | <span data-ttu-id="92b14-144">Notes</span><span class="sxs-lookup"><span data-stu-id="92b14-144">Notes</span></span> | 
   |----------|-------|-------|
   | <span data-ttu-id="92b14-145">**Batch Mode**</span><span class="sxs-lookup"><span data-stu-id="92b14-145">**Batch Mode**</span></span> | <span data-ttu-id="92b14-146">Inline</span><span class="sxs-lookup"><span data-stu-id="92b14-146">Inline</span></span> |  |  
   | <span data-ttu-id="92b14-147">**Batch Name**</span><span class="sxs-lookup"><span data-stu-id="92b14-147">**Batch Name**</span></span> | <span data-ttu-id="92b14-148">TestBatch</span><span class="sxs-lookup"><span data-stu-id="92b14-148">TestBatch</span></span> | <span data-ttu-id="92b14-149">Available only with **Inline** batch mode</span><span class="sxs-lookup"><span data-stu-id="92b14-149">Available only with **Inline** batch mode</span></span> | 
   | <span data-ttu-id="92b14-150">**Release Criteria**</span><span class="sxs-lookup"><span data-stu-id="92b14-150">**Release Criteria**</span></span> | <span data-ttu-id="92b14-151">Message count based, Schedule based</span><span class="sxs-lookup"><span data-stu-id="92b14-151">Message count based, Schedule based</span></span> | <span data-ttu-id="92b14-152">Available only with **Inline** batch mode</span><span class="sxs-lookup"><span data-stu-id="92b14-152">Available only with **Inline** batch mode</span></span> | 
   | <span data-ttu-id="92b14-153">**Message Count**</span><span class="sxs-lookup"><span data-stu-id="92b14-153">**Message Count**</span></span> | <span data-ttu-id="92b14-154">10</span><span class="sxs-lookup"><span data-stu-id="92b14-154">10</span></span> | <span data-ttu-id="92b14-155">Available only with **Message count based** release criteria</span><span class="sxs-lookup"><span data-stu-id="92b14-155">Available only with **Message count based** release criteria</span></span> | 
   | <span data-ttu-id="92b14-156">**Interval**</span><span class="sxs-lookup"><span data-stu-id="92b14-156">**Interval**</span></span> | <span data-ttu-id="92b14-157">10</span><span class="sxs-lookup"><span data-stu-id="92b14-157">10</span></span> | <span data-ttu-id="92b14-158">Available only with **Schedule based** release criteria</span><span class="sxs-lookup"><span data-stu-id="92b14-158">Available only with **Schedule based** release criteria</span></span> | 
   | <span data-ttu-id="92b14-159">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="92b14-159">**Frequency**</span></span> | <span data-ttu-id="92b14-160">minute</span><span class="sxs-lookup"><span data-stu-id="92b14-160">minute</span></span> | <span data-ttu-id="92b14-161">Available only with **Schedule based** release criteria</span><span class="sxs-lookup"><span data-stu-id="92b14-161">Available only with **Schedule based** release criteria</span></span> | 
   ||| 

   ![Provide batch trigger details](./media/logic-apps-scenario-EDI-send-batch-messages/batch-receiver-release-criteria.png)

   > [!NOTE]
   > <span data-ttu-id="92b14-163">This example doesn't set up a partition for the batch, so each batch uses the same partition key.</span><span class="sxs-lookup"><span data-stu-id="92b14-163">This example doesn't set up a partition for the batch, so each batch uses the same partition key.</span></span> <span data-ttu-id="92b14-164">To learn more about partitions, see [Batch process messages](../logic-apps/logic-apps-batch-process-send-receive-messages.md#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="92b14-164">To learn more about partitions, see [Batch process messages](../logic-apps/logic-apps-batch-process-send-receive-messages.md#batch-sender).</span></span>

5. <span data-ttu-id="92b14-165">Now add an action that encodes each batch:</span><span class="sxs-lookup"><span data-stu-id="92b14-165">Now add an action that encodes each batch:</span></span> 

   1. <span data-ttu-id="92b14-166">Under the batch trigger, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="92b14-166">Under the batch trigger, choose **New step**.</span></span>

   2. <span data-ttu-id="92b14-167">In the search box, enter "X12 batch" as your filter, and select this action (any version): **Batch encode <*version*> - X12**</span><span class="sxs-lookup"><span data-stu-id="92b14-167">In the search box, enter "X12 batch" as your filter, and select this action (any version): **Batch encode <*version*> - X12**</span></span> 

      ![Select X12 Batch Encode action](./media/logic-apps-scenario-EDI-send-batch-messages/add-batch-encode-action.png)

   3. <span data-ttu-id="92b14-169">If you didn't previously connect to your integration account, create the connection now.</span><span class="sxs-lookup"><span data-stu-id="92b14-169">If you didn't previously connect to your integration account, create the connection now.</span></span> <span data-ttu-id="92b14-170">Provide a name for your connection, select the integration account you want, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="92b14-170">Provide a name for your connection, select the integration account you want, and then choose **Create**.</span></span>

      ![Create connection between batch encoder and integration account](./media/logic-apps-scenario-EDI-send-batch-messages/batch-encoder-connect-integration-account.png)

   4. <span data-ttu-id="92b14-172">Set these properties for your batch encoder action:</span><span class="sxs-lookup"><span data-stu-id="92b14-172">Set these properties for your batch encoder action:</span></span>

      | <span data-ttu-id="92b14-173">Property</span><span class="sxs-lookup"><span data-stu-id="92b14-173">Property</span></span> | <span data-ttu-id="92b14-174">Description</span><span class="sxs-lookup"><span data-stu-id="92b14-174">Description</span></span> |
      |----------|-------------|
      | <span data-ttu-id="92b14-175">**Name of X12 agreement**</span><span class="sxs-lookup"><span data-stu-id="92b14-175">**Name of X12 agreement**</span></span> | <span data-ttu-id="92b14-176">Open the list, and select your existing agreement.</span><span class="sxs-lookup"><span data-stu-id="92b14-176">Open the list, and select your existing agreement.</span></span> <p><span data-ttu-id="92b14-177">If your list is empty, make sure you [link your logic app to the integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md#link-account) that has the agreement you want.</span><span class="sxs-lookup"><span data-stu-id="92b14-177">If your list is empty, make sure you [link your logic app to the integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md#link-account) that has the agreement you want.</span></span> | 
      | <span data-ttu-id="92b14-178">**BatchName**</span><span class="sxs-lookup"><span data-stu-id="92b14-178">**BatchName**</span></span> | <span data-ttu-id="92b14-179">Click inside this box, and after the dynamic content list appears, select the **Batch Name** token.</span><span class="sxs-lookup"><span data-stu-id="92b14-179">Click inside this box, and after the dynamic content list appears, select the **Batch Name** token.</span></span> | 
      | <span data-ttu-id="92b14-180">**PartitionName**</span><span class="sxs-lookup"><span data-stu-id="92b14-180">**PartitionName**</span></span> | <span data-ttu-id="92b14-181">Click inside this box, and after the dynamic content list appears, select the **Partition Name** token.</span><span class="sxs-lookup"><span data-stu-id="92b14-181">Click inside this box, and after the dynamic content list appears, select the **Partition Name** token.</span></span> | 
      | <span data-ttu-id="92b14-182">**Items**</span><span class="sxs-lookup"><span data-stu-id="92b14-182">**Items**</span></span> | <span data-ttu-id="92b14-183">Close the item details box, and then click inside this box.</span><span class="sxs-lookup"><span data-stu-id="92b14-183">Close the item details box, and then click inside this box.</span></span> <span data-ttu-id="92b14-184">After the dynamic content list appears, select the **Batched Items** token.</span><span class="sxs-lookup"><span data-stu-id="92b14-184">After the dynamic content list appears, select the **Batched Items** token.</span></span> | 
      ||| 

      ![Batch Encode action details](./media/logic-apps-scenario-EDI-send-batch-messages/batch-encode-action-details.png)

      <span data-ttu-id="92b14-186">For the **Items** box:</span><span class="sxs-lookup"><span data-stu-id="92b14-186">For the **Items** box:</span></span>

      ![Batch Encode action items](./media/logic-apps-scenario-EDI-send-batch-messages/batch-encode-action-items.png)

6. <span data-ttu-id="92b14-188">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-188">Save your logic app.</span></span> 

7. <span data-ttu-id="92b14-189">If you're using Visual Studio, make sure you [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span><span class="sxs-lookup"><span data-stu-id="92b14-189">If you're using Visual Studio, make sure you [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span></span> <span data-ttu-id="92b14-190">Otherwise, you can't select the batch receiver when you create the batch sender.</span><span class="sxs-lookup"><span data-stu-id="92b14-190">Otherwise, you can't select the batch receiver when you create the batch sender.</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="92b14-191">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="92b14-191">Test your logic app</span></span>

<span data-ttu-id="92b14-192">To make sure your batch receiver works as expected, you can add an HTTP action for testing purposes, and send a batched message to the [Request Bin service](https://requestbin.fullcontact.com/).</span><span class="sxs-lookup"><span data-stu-id="92b14-192">To make sure your batch receiver works as expected, you can add an HTTP action for testing purposes, and send a batched message to the [Request Bin service](https://requestbin.fullcontact.com/).</span></span> 

1. <span data-ttu-id="92b14-193">Under the X12 encode action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="92b14-193">Under the X12 encode action, choose **New step**.</span></span> 

2. <span data-ttu-id="92b14-194">In the search box, enter "http" as your filter.</span><span class="sxs-lookup"><span data-stu-id="92b14-194">In the search box, enter "http" as your filter.</span></span> <span data-ttu-id="92b14-195">Select this action: **HTTP - HTTP**</span><span class="sxs-lookup"><span data-stu-id="92b14-195">Select this action: **HTTP - HTTP**</span></span>
    
   ![Select HTTP action](./media/logic-apps-scenario-EDI-send-batch-messages/batch-receiver-add-http-action.png)

3. <span data-ttu-id="92b14-197">Set the properties for the HTTP action:</span><span class="sxs-lookup"><span data-stu-id="92b14-197">Set the properties for the HTTP action:</span></span>

   | <span data-ttu-id="92b14-198">Property</span><span class="sxs-lookup"><span data-stu-id="92b14-198">Property</span></span> | <span data-ttu-id="92b14-199">Description</span><span class="sxs-lookup"><span data-stu-id="92b14-199">Description</span></span> | 
   |----------|-------------|
   | <span data-ttu-id="92b14-200">**Method**</span><span class="sxs-lookup"><span data-stu-id="92b14-200">**Method**</span></span> | <span data-ttu-id="92b14-201">From this list, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="92b14-201">From this list, select **POST**.</span></span> | 
   | <span data-ttu-id="92b14-202">**Uri**</span><span class="sxs-lookup"><span data-stu-id="92b14-202">**Uri**</span></span> | <span data-ttu-id="92b14-203">Generate a URI for your request bin, and then enter that URI in this box.</span><span class="sxs-lookup"><span data-stu-id="92b14-203">Generate a URI for your request bin, and then enter that URI in this box.</span></span> | 
   | <span data-ttu-id="92b14-204">**Body**</span><span class="sxs-lookup"><span data-stu-id="92b14-204">**Body**</span></span> | <span data-ttu-id="92b14-205">Click inside this box, and after the dynamic content list opens, select the **Body** token, which appears in the section, **Batch encode by agreement name**.</span><span class="sxs-lookup"><span data-stu-id="92b14-205">Click inside this box, and after the dynamic content list opens, select the **Body** token, which appears in the section, **Batch encode by agreement name**.</span></span> <p><span data-ttu-id="92b14-206">If you don't see the **Body** token, next to **Batch encode by agreement name**, select **See more**.</span><span class="sxs-lookup"><span data-stu-id="92b14-206">If you don't see the **Body** token, next to **Batch encode by agreement name**, select **See more**.</span></span> | 
   ||| 

   ![Provide HTTP action details](./media/logic-apps-scenario-EDI-send-batch-messages/batch-receiver-add-http-action-details.png)

4. <span data-ttu-id="92b14-208">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-208">Save your logic app.</span></span> 

   <span data-ttu-id="92b14-209">Your batch receiver logic app looks like this example:</span><span class="sxs-lookup"><span data-stu-id="92b14-209">Your batch receiver logic app looks like this example:</span></span> 

   ![Save your batch receiver logic app](./media/logic-apps-scenario-EDI-send-batch-messages/batch-receiver-finished.png)

<a name="sender"></a>

## <a name="create-x12-batch-sender"></a><span data-ttu-id="92b14-211">Create X12 batch sender</span><span class="sxs-lookup"><span data-stu-id="92b14-211">Create X12 batch sender</span></span>

<span data-ttu-id="92b14-212">Now create one or more logic apps that send messages to the batch receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-212">Now create one or more logic apps that send messages to the batch receiver logic app.</span></span> <span data-ttu-id="92b14-213">In each batch sender, you specify the batch receiver logic app and batch name, message content, and any other settings.</span><span class="sxs-lookup"><span data-stu-id="92b14-213">In each batch sender, you specify the batch receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="92b14-214">You can optionally provide a unique partition key to divide the batch into subsets to collect messages with that key.</span><span class="sxs-lookup"><span data-stu-id="92b14-214">You can optionally provide a unique partition key to divide the batch into subsets to collect messages with that key.</span></span> 

* <span data-ttu-id="92b14-215">Make sure you've already [created your batch receiver](#receiver) so when you create your batch sender, you can select the existing batch receiver as the destination batch.</span><span class="sxs-lookup"><span data-stu-id="92b14-215">Make sure you've already [created your batch receiver](#receiver) so when you create your batch sender, you can select the existing batch receiver as the destination batch.</span></span> <span data-ttu-id="92b14-216">While batch receivers don't need to know anything about batch senders, batch senders must know where to send messages.</span><span class="sxs-lookup"><span data-stu-id="92b14-216">While batch receivers don't need to know anything about batch senders, batch senders must know where to send messages.</span></span> 

* <span data-ttu-id="92b14-217">Make sure your batch receiver and batch sender share the same Azure region *and* Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="92b14-217">Make sure your batch receiver and batch sender share the same Azure region *and* Azure subscription.</span></span> <span data-ttu-id="92b14-218">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span><span class="sxs-lookup"><span data-stu-id="92b14-218">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span></span>

1. <span data-ttu-id="92b14-219">Create another logic app with this name: "SendX12MessagesToBatch"</span><span class="sxs-lookup"><span data-stu-id="92b14-219">Create another logic app with this name: "SendX12MessagesToBatch"</span></span> 

2. <span data-ttu-id="92b14-220">In the search box, enter "when a http request" as your filter.</span><span class="sxs-lookup"><span data-stu-id="92b14-220">In the search box, enter "when a http request" as your filter.</span></span> <span data-ttu-id="92b14-221">Select this trigger: **When a HTTP request is received**</span><span class="sxs-lookup"><span data-stu-id="92b14-221">Select this trigger: **When a HTTP request is received**</span></span> 
   
   ![Add the Request trigger](./media/logic-apps-scenario-EDI-send-batch-messages/add-request-trigger-sender.png)

3. <span data-ttu-id="92b14-223">Add an action for sending messages to a batch.</span><span class="sxs-lookup"><span data-stu-id="92b14-223">Add an action for sending messages to a batch.</span></span>

   1. <span data-ttu-id="92b14-224">Under the HTTP request action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="92b14-224">Under the HTTP request action, choose **New step**.</span></span>

   2. <span data-ttu-id="92b14-225">In the search box, enter "batch" as your filter.</span><span class="sxs-lookup"><span data-stu-id="92b14-225">In the search box, enter "batch" as your filter.</span></span> 
   <span data-ttu-id="92b14-226">Select the **Actions** list, and then select this action: **Choose a Logic Apps workflow with batch trigger - Send messages to batch**</span><span class="sxs-lookup"><span data-stu-id="92b14-226">Select the **Actions** list, and then select this action: **Choose a Logic Apps workflow with batch trigger - Send messages to batch**</span></span>

      ![Select "Choose a Logic Apps workflow with batch trigger"](./media/logic-apps-scenario-EDI-send-batch-messages/batch-sender-select-batch-trigger.png)

   3. <span data-ttu-id="92b14-228">Now select your "BatchX12Messages" logic app that you previously created.</span><span class="sxs-lookup"><span data-stu-id="92b14-228">Now select your "BatchX12Messages" logic app that you previously created.</span></span>

      ![Select "batch receiver" logic app](./media/logic-apps-scenario-EDI-send-batch-messages/batch-sender-select-batch-receiver.png)

   4. <span data-ttu-id="92b14-230">Select this action: **Batch_messages - <*your-batch-receiver*>**</span><span class="sxs-lookup"><span data-stu-id="92b14-230">Select this action: **Batch_messages - <*your-batch-receiver*>**</span></span>

      ![Select "Batch_messages" action](./media/logic-apps-scenario-EDI-send-batch-messages/batch-sender-select-batch-messages-action.png)

4. <span data-ttu-id="92b14-232">Set the batch sender's properties.</span><span class="sxs-lookup"><span data-stu-id="92b14-232">Set the batch sender's properties.</span></span>

   | <span data-ttu-id="92b14-233">Property</span><span class="sxs-lookup"><span data-stu-id="92b14-233">Property</span></span> | <span data-ttu-id="92b14-234">Description</span><span class="sxs-lookup"><span data-stu-id="92b14-234">Description</span></span> | 
   |----------|-------------| 
   | <span data-ttu-id="92b14-235">**Batch Name**</span><span class="sxs-lookup"><span data-stu-id="92b14-235">**Batch Name**</span></span> | <span data-ttu-id="92b14-236">The batch name defined by the receiver logic app, which is "TestBatch" in this example</span><span class="sxs-lookup"><span data-stu-id="92b14-236">The batch name defined by the receiver logic app, which is "TestBatch" in this example</span></span> <p><span data-ttu-id="92b14-237">**Important**: The batch name gets validated at runtime and must match the name specified by the receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-237">**Important**: The batch name gets validated at runtime and must match the name specified by the receiver logic app.</span></span> <span data-ttu-id="92b14-238">Changing the batch name causes the batch sender to fail.</span><span class="sxs-lookup"><span data-stu-id="92b14-238">Changing the batch name causes the batch sender to fail.</span></span> | 
   | <span data-ttu-id="92b14-239">**Message Content**</span><span class="sxs-lookup"><span data-stu-id="92b14-239">**Message Content**</span></span> | <span data-ttu-id="92b14-240">The content for the message you want to send, which is the **Body** token in this example</span><span class="sxs-lookup"><span data-stu-id="92b14-240">The content for the message you want to send, which is the **Body** token in this example</span></span> | 
   ||| 
   
   ![Set batch properties](./media/logic-apps-scenario-EDI-send-batch-messages/batch-sender-set-batch-properties.png)

5. <span data-ttu-id="92b14-242">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="92b14-242">Save your logic app.</span></span> 

   <span data-ttu-id="92b14-243">Your batch sender logic app looks like this example:</span><span class="sxs-lookup"><span data-stu-id="92b14-243">Your batch sender logic app looks like this example:</span></span>

   ![Save your batch sender logic app](./media/logic-apps-scenario-EDI-send-batch-messages/batch-sender-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="92b14-245">Test your logic apps</span><span class="sxs-lookup"><span data-stu-id="92b14-245">Test your logic apps</span></span>

<span data-ttu-id="92b14-246">To test your batching solution, post X12 messages to your batch sender logic app from [Postman](https://www.getpostman.com/postman) or a similar tool.</span><span class="sxs-lookup"><span data-stu-id="92b14-246">To test your batching solution, post X12 messages to your batch sender logic app from [Postman](https://www.getpostman.com/postman) or a similar tool.</span></span> <span data-ttu-id="92b14-247">Soon, you start getting X12 messages in your request bin, either every 10 minutes or in batches of 10, all with the same partition key.</span><span class="sxs-lookup"><span data-stu-id="92b14-247">Soon, you start getting X12 messages in your request bin, either every 10 minutes or in batches of 10, all with the same partition key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b14-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="92b14-248">Next steps</span></span>

* [<span data-ttu-id="92b14-249">Process messages as batches</span><span class="sxs-lookup"><span data-stu-id="92b14-249">Process messages as batches</span></span>](../logic-apps/logic-apps-batch-process-send-receive-messages.md) 
