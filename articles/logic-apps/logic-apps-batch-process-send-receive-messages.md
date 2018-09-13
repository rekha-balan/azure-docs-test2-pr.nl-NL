---
title: Batch process messages as a group or collection - Azure Logic Apps | Microsoft Docs
description: Send and receive messages as batches in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: estfan, jonfan, LADocs
ms.topic: article
ms.date: 08/19/2018
ms.openlocfilehash: ee1df77dc18350a64082cb62c297a53700cad223
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858040"
---
# <a name="send-receive-and-batch-process-messages-in-azure-logic-apps"></a><span data-ttu-id="716ad-103">Send, receive, and batch process messages in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="716ad-103">Send, receive, and batch process messages in Azure Logic Apps</span></span>

<span data-ttu-id="716ad-104">To send and process messages together in a specific way as groups, you can create a batching solution that collects messages into a *batch* until your specified criteria are met for releasing and processing the batched messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-104">To send and process messages together in a specific way as groups, you can create a batching solution that collects messages into a *batch* until your specified criteria are met for releasing and processing the batched messages.</span></span> <span data-ttu-id="716ad-105">Batching can reduce how often your logic app processes messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-105">Batching can reduce how often your logic app processes messages.</span></span> <span data-ttu-id="716ad-106">This article shows how to build a batching solution by creating two logic apps within the same Azure subscription, Azure region, and following this specific order:</span><span class="sxs-lookup"><span data-stu-id="716ad-106">This article shows how to build a batching solution by creating two logic apps within the same Azure subscription, Azure region, and following this specific order:</span></span> 

* <span data-ttu-id="716ad-107">The ["batch receiver"](#batch-receiver) logic app, which accepts and collects messages into a batch until your specified criteria is met for releasing and processing those messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-107">The ["batch receiver"](#batch-receiver) logic app, which accepts and collects messages into a batch until your specified criteria is met for releasing and processing those messages.</span></span>

  <span data-ttu-id="716ad-108">Make sure you first create the batch receiver so you can later select the batch destination when you create the batch sender.</span><span class="sxs-lookup"><span data-stu-id="716ad-108">Make sure you first create the batch receiver so you can later select the batch destination when you create the batch sender.</span></span>

* <span data-ttu-id="716ad-109">One or more ["batch sender"](#batch-sender) logic apps, which send the messages to the previously created batch receiver.</span><span class="sxs-lookup"><span data-stu-id="716ad-109">One or more ["batch sender"](#batch-sender) logic apps, which send the messages to the previously created batch receiver.</span></span> 

   <span data-ttu-id="716ad-110">You can also specify a unique key, such as a customer number, that *partitions* or divides the target batch into logical subsets based on that key.</span><span class="sxs-lookup"><span data-stu-id="716ad-110">You can also specify a unique key, such as a customer number, that *partitions* or divides the target batch into logical subsets based on that key.</span></span> <span data-ttu-id="716ad-111">That way, the receiver app can collect all items with the same key and process them together.</span><span class="sxs-lookup"><span data-stu-id="716ad-111">That way, the receiver app can collect all items with the same key and process them together.</span></span>

<span data-ttu-id="716ad-112">Make sure your batch receiver and batch sender share the same Azure subscription *and* Azure region.</span><span class="sxs-lookup"><span data-stu-id="716ad-112">Make sure your batch receiver and batch sender share the same Azure subscription *and* Azure region.</span></span> <span data-ttu-id="716ad-113">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span><span class="sxs-lookup"><span data-stu-id="716ad-113">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="716ad-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="716ad-114">Prerequisites</span></span>

<span data-ttu-id="716ad-115">To follow this example, you need these items:</span><span class="sxs-lookup"><span data-stu-id="716ad-115">To follow this example, you need these items:</span></span>

* <span data-ttu-id="716ad-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="716ad-116">An Azure subscription.</span></span> <span data-ttu-id="716ad-117">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="716ad-117">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="716ad-118">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="716ad-118">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="716ad-119">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="716ad-119">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

* <span data-ttu-id="716ad-120">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="716ad-120">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span> 

* <span data-ttu-id="716ad-121">To use Visual Studio rather than the Azure portal, make sure you [set up Visual Studio for working with Logic Apps](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="716ad-121">To use Visual Studio rather than the Azure portal, make sure you [set up Visual Studio for working with Logic Apps](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span></span>

<a name="batch-receiver"></a>

## <a name="create-batch-receiver"></a><span data-ttu-id="716ad-122">Create batch receiver</span><span class="sxs-lookup"><span data-stu-id="716ad-122">Create batch receiver</span></span>

<span data-ttu-id="716ad-123">Before you can send messages to a batch, that batch must first exist as the destination where you send those messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-123">Before you can send messages to a batch, that batch must first exist as the destination where you send those messages.</span></span> <span data-ttu-id="716ad-124">So first, you must create the "batch receiver" logic app, which starts with the **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="716ad-124">So first, you must create the "batch receiver" logic app, which starts with the **Batch** trigger.</span></span> <span data-ttu-id="716ad-125">That way, when you create the "batch sender" logic app, you can select the batch receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-125">That way, when you create the "batch sender" logic app, you can select the batch receiver logic app.</span></span> <span data-ttu-id="716ad-126">The batch receiver continues collecting messages until your specified criteria is met for releasing and processing those messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-126">The batch receiver continues collecting messages until your specified criteria is met for releasing and processing those messages.</span></span> <span data-ttu-id="716ad-127">While batch receivers don't need to know anything about batch senders, batch senders must know the destination where they send the messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-127">While batch receivers don't need to know anything about batch senders, batch senders must know the destination where they send the messages.</span></span> 

1. <span data-ttu-id="716ad-128">In the [Azure portal](https://portal.azure.com) or Visual Studio, create a logic app with this name: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="716ad-128">In the [Azure portal](https://portal.azure.com) or Visual Studio, create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="716ad-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="716ad-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="716ad-130">In the search box, enter "batch" as your filter.</span><span class="sxs-lookup"><span data-stu-id="716ad-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="716ad-131">Select this trigger: **Batch messages**</span><span class="sxs-lookup"><span data-stu-id="716ad-131">Select this trigger: **Batch messages**</span></span>

   ![Add "Batch messages" trigger](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="716ad-133">Set the batch receiver properties:</span><span class="sxs-lookup"><span data-stu-id="716ad-133">Set the batch receiver properties:</span></span> 

   | <span data-ttu-id="716ad-134">Property</span><span class="sxs-lookup"><span data-stu-id="716ad-134">Property</span></span> | <span data-ttu-id="716ad-135">Description</span><span class="sxs-lookup"><span data-stu-id="716ad-135">Description</span></span> | 
   |----------|-------------|
   | <span data-ttu-id="716ad-136">**Batch Mode**</span><span class="sxs-lookup"><span data-stu-id="716ad-136">**Batch Mode**</span></span> | <span data-ttu-id="716ad-137">- **Inline**: For defining release criteria inside the batch trigger</span><span class="sxs-lookup"><span data-stu-id="716ad-137">- **Inline**: For defining release criteria inside the batch trigger</span></span> <br><span data-ttu-id="716ad-138">- **Integration Account**: For defining multiple release criteria configurations through an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="716ad-138">- **Integration Account**: For defining multiple release criteria configurations through an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span> <span data-ttu-id="716ad-139">With an integration account, you can maintain these configurations all in one place rather than in separate logic apps.</span><span class="sxs-lookup"><span data-stu-id="716ad-139">With an integration account, you can maintain these configurations all in one place rather than in separate logic apps.</span></span> | 
   | <span data-ttu-id="716ad-140">**Batch Name**</span><span class="sxs-lookup"><span data-stu-id="716ad-140">**Batch Name**</span></span> | <span data-ttu-id="716ad-141">The name for your batch, which is "TestBatch" in this example, and applies only to **Inline** batch mode</span><span class="sxs-lookup"><span data-stu-id="716ad-141">The name for your batch, which is "TestBatch" in this example, and applies only to **Inline** batch mode</span></span> |  
   | <span data-ttu-id="716ad-142">**Release Criteria**</span><span class="sxs-lookup"><span data-stu-id="716ad-142">**Release Criteria**</span></span> | <span data-ttu-id="716ad-143">Applies only to **Inline** batch mode and specifies the criteria to meet before processing each batch:</span><span class="sxs-lookup"><span data-stu-id="716ad-143">Applies only to **Inline** batch mode and specifies the criteria to meet before processing each batch:</span></span> <p><span data-ttu-id="716ad-144">- **Message count based**: The number of messages to collect in the batch, for example, 10 messages</span><span class="sxs-lookup"><span data-stu-id="716ad-144">- **Message count based**: The number of messages to collect in the batch, for example, 10 messages</span></span> <br><span data-ttu-id="716ad-145">- **Size based**: The maximum batch size in bytes, for example, 100 MB</span><span class="sxs-lookup"><span data-stu-id="716ad-145">- **Size based**: The maximum batch size in bytes, for example, 100 MB</span></span> <br><span data-ttu-id="716ad-146">- **Schedule based**: The interval and frequency between batch releases, for example, 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="716ad-146">- **Schedule based**: The interval and frequency between batch releases, for example, 10 minutes.</span></span> <span data-ttu-id="716ad-147">You can also specify a start date and time.</span><span class="sxs-lookup"><span data-stu-id="716ad-147">You can also specify a start date and time.</span></span> <br><span data-ttu-id="716ad-148">- **Select all**: Use all the specified criteria.</span><span class="sxs-lookup"><span data-stu-id="716ad-148">- **Select all**: Use all the specified criteria.</span></span> | 
   ||| 
   
   <span data-ttu-id="716ad-149">This example selects all the criteria:</span><span class="sxs-lookup"><span data-stu-id="716ad-149">This example selects all the criteria:</span></span>

   ![Provide Batch trigger details](./media/logic-apps-batch-process-send-receive-messages/batch-receiver-criteria.png)

4. <span data-ttu-id="716ad-151">Now add one or more actions that process each batch.</span><span class="sxs-lookup"><span data-stu-id="716ad-151">Now add one or more actions that process each batch.</span></span> 

   <span data-ttu-id="716ad-152">For this example, add an action that sends an email when the batch trigger fires.</span><span class="sxs-lookup"><span data-stu-id="716ad-152">For this example, add an action that sends an email when the batch trigger fires.</span></span> 
   <span data-ttu-id="716ad-153">The trigger runs and sends an email when the batch either has 10 messages, reaches 10 MB, or after 10 minutes pass.</span><span class="sxs-lookup"><span data-stu-id="716ad-153">The trigger runs and sends an email when the batch either has 10 messages, reaches 10 MB, or after 10 minutes pass.</span></span>

   1. <span data-ttu-id="716ad-154">Under the batch trigger, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="716ad-154">Under the batch trigger, choose **New step**.</span></span>

   2. <span data-ttu-id="716ad-155">In the search box, enter "send email" as your filter.</span><span class="sxs-lookup"><span data-stu-id="716ad-155">In the search box, enter "send email" as your filter.</span></span>
   <span data-ttu-id="716ad-156">Based on your email provider, select an email connector.</span><span class="sxs-lookup"><span data-stu-id="716ad-156">Based on your email provider, select an email connector.</span></span>
      
      <span data-ttu-id="716ad-157">For example, if you have a personal account, such as @outlook.com or @hotmail.com, select the Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="716ad-157">For example, if you have a personal account, such as @outlook.com or @hotmail.com, select the Outlook.com connector.</span></span> 
      <span data-ttu-id="716ad-158">If you have a Gmail account, select the Gmail connector.</span><span class="sxs-lookup"><span data-stu-id="716ad-158">If you have a Gmail account, select the Gmail connector.</span></span> 
      <span data-ttu-id="716ad-159">This example uses Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="716ad-159">This example uses Office 365 Outlook.</span></span> 

   3. <span data-ttu-id="716ad-160">Select this action: **Send an email - <*email provider*>**</span><span class="sxs-lookup"><span data-stu-id="716ad-160">Select this action: **Send an email - <*email provider*>**</span></span>

      <span data-ttu-id="716ad-161">For example:</span><span class="sxs-lookup"><span data-stu-id="716ad-161">For example:</span></span>

      ![Select "Send an email" action for your email provider](./media/logic-apps-batch-process-send-receive-messages/batch-receiver-send-email-action.png)

5. <span data-ttu-id="716ad-163">If prompted, sign in to your email account.</span><span class="sxs-lookup"><span data-stu-id="716ad-163">If prompted, sign in to your email account.</span></span> 

6. <span data-ttu-id="716ad-164">Set the properties for the action you added.</span><span class="sxs-lookup"><span data-stu-id="716ad-164">Set the properties for the action you added.</span></span>

   * <span data-ttu-id="716ad-165">In the **To** box, enter the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="716ad-165">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="716ad-166">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="716ad-166">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="716ad-167">In the **Subject** box, when the dynamic content list appears, select the **Partition Name** field.</span><span class="sxs-lookup"><span data-stu-id="716ad-167">In the **Subject** box, when the dynamic content list appears, select the **Partition Name** field.</span></span>

     ![From the dynamic content list, select "Partition Name"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="716ad-169">In a later section, you can specify a unique partition key that divides the target batch into logical subsets to where you can send messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-169">In a later section, you can specify a unique partition key that divides the target batch into logical subsets to where you can send messages.</span></span> 
     <span data-ttu-id="716ad-170">Each set has a unique number that's generated by the batch sender logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-170">Each set has a unique number that's generated by the batch sender logic app.</span></span> 
     <span data-ttu-id="716ad-171">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span><span class="sxs-lookup"><span data-stu-id="716ad-171">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="716ad-172">A partition has a limit of 5,000 messages or 80 MB.</span><span class="sxs-lookup"><span data-stu-id="716ad-172">A partition has a limit of 5,000 messages or 80 MB.</span></span> <span data-ttu-id="716ad-173">If either condition is met, Logic Apps might release the batch, even when your defined release condition isn't met.</span><span class="sxs-lookup"><span data-stu-id="716ad-173">If either condition is met, Logic Apps might release the batch, even when your defined release condition isn't met.</span></span>

   * <span data-ttu-id="716ad-174">In the **Body** box, when the dynamic content list appears, select the **Message Id** field.</span><span class="sxs-lookup"><span data-stu-id="716ad-174">In the **Body** box, when the dynamic content list appears, select the **Message Id** field.</span></span> 

     <span data-ttu-id="716ad-175">The Logic Apps Designer automatically adds a "For each" loop around the send email action because that action accepts an array as input.</span><span class="sxs-lookup"><span data-stu-id="716ad-175">The Logic Apps Designer automatically adds a "For each" loop around the send email action because that action accepts an array as input.</span></span> 
     <span data-ttu-id="716ad-176">This loop sends an email for each message in the batch.</span><span class="sxs-lookup"><span data-stu-id="716ad-176">This loop sends an email for each message in the batch.</span></span> 
     <span data-ttu-id="716ad-177">So, when the batch trigger is set to 10 messages, you get 10 emails each time the trigger fires.</span><span class="sxs-lookup"><span data-stu-id="716ad-177">So, when the batch trigger is set to 10 messages, you get 10 emails each time the trigger fires.</span></span>

     ![For "Body", select "Message Id"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

7.  <span data-ttu-id="716ad-179">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-179">Save your logic app.</span></span> <span data-ttu-id="716ad-180">You've now created a batch receiver.</span><span class="sxs-lookup"><span data-stu-id="716ad-180">You've now created a batch receiver.</span></span>

    ![Save your logic app](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

8. <span data-ttu-id="716ad-182">If you're using Visual Studio, make sure you [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span><span class="sxs-lookup"><span data-stu-id="716ad-182">If you're using Visual Studio, make sure you [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span></span> <span data-ttu-id="716ad-183">Otherwise, you can't select the batch receiver when you create the batch sender.</span><span class="sxs-lookup"><span data-stu-id="716ad-183">Otherwise, you can't select the batch receiver when you create the batch sender.</span></span>

<a name="batch-sender"></a>

## <a name="create-batch-sender"></a><span data-ttu-id="716ad-184">Create batch sender</span><span class="sxs-lookup"><span data-stu-id="716ad-184">Create batch sender</span></span>

<span data-ttu-id="716ad-185">Now create one or more batch sender logic apps that send messages to the batch receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-185">Now create one or more batch sender logic apps that send messages to the batch receiver logic app.</span></span> <span data-ttu-id="716ad-186">In each batch sender, you specify the batch receiver and batch name, message content, and any other settings.</span><span class="sxs-lookup"><span data-stu-id="716ad-186">In each batch sender, you specify the batch receiver and batch name, message content, and any other settings.</span></span> <span data-ttu-id="716ad-187">You can optionally provide a unique partition key to divide the batch into logical subsets for collecting messages with that key.</span><span class="sxs-lookup"><span data-stu-id="716ad-187">You can optionally provide a unique partition key to divide the batch into logical subsets for collecting messages with that key.</span></span> 

* <span data-ttu-id="716ad-188">Make sure you've already [created your batch receiver](#batch-receiver) so when you create your batch sender, you can select the existing batch receiver as the destination batch.</span><span class="sxs-lookup"><span data-stu-id="716ad-188">Make sure you've already [created your batch receiver](#batch-receiver) so when you create your batch sender, you can select the existing batch receiver as the destination batch.</span></span> <span data-ttu-id="716ad-189">While batch receivers don't need to know anything about batch senders, batch senders must know where to send messages.</span><span class="sxs-lookup"><span data-stu-id="716ad-189">While batch receivers don't need to know anything about batch senders, batch senders must know where to send messages.</span></span> 

* <span data-ttu-id="716ad-190">Make sure your batch receiver and batch sender share the same Azure region *and* Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="716ad-190">Make sure your batch receiver and batch sender share the same Azure region *and* Azure subscription.</span></span> <span data-ttu-id="716ad-191">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span><span class="sxs-lookup"><span data-stu-id="716ad-191">If they don't, you can't select the batch receiver when you create the batch sender because they're not visible to each other.</span></span>

1. <span data-ttu-id="716ad-192">Create another logic app with this name: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="716ad-192">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="716ad-193">In the search box, enter "recurrence" as your filter.</span><span class="sxs-lookup"><span data-stu-id="716ad-193">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="716ad-194">Select this trigger: **Recurrence - Schedule**</span><span class="sxs-lookup"><span data-stu-id="716ad-194">Select this trigger: **Recurrence - Schedule**</span></span>

      ![Add the "Recurrence - Schedule" trigger](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-sender.png)

   2. <span data-ttu-id="716ad-196">Set the frequency and interval to run the sender logic app every minute.</span><span class="sxs-lookup"><span data-stu-id="716ad-196">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Set frequency and interval for recurrence trigger](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-sender-details.png)

2. <span data-ttu-id="716ad-198">Add a new action for sending messages to a batch.</span><span class="sxs-lookup"><span data-stu-id="716ad-198">Add a new action for sending messages to a batch.</span></span>

   1. <span data-ttu-id="716ad-199">Under the recurrence trigger, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="716ad-199">Under the recurrence trigger, choose **New step**.</span></span>

   2. <span data-ttu-id="716ad-200">In the search box, enter "batch" as your filter.</span><span class="sxs-lookup"><span data-stu-id="716ad-200">In the search box, enter "batch" as your filter.</span></span> 
   <span data-ttu-id="716ad-201">Select the **Actions** list, and then select this action: **Choose a Logic Apps workflow with batch trigger - Send messages to batch**</span><span class="sxs-lookup"><span data-stu-id="716ad-201">Select the **Actions** list, and then select this action: **Choose a Logic Apps workflow with batch trigger - Send messages to batch**</span></span>

      ![Select "Choose a Logic Apps workflow with batch trigger"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   3. <span data-ttu-id="716ad-203">Select your batch receiver logic app that you previously created.</span><span class="sxs-lookup"><span data-stu-id="716ad-203">Select your batch receiver logic app that you previously created.</span></span>

      ![Select "batch receiver" logic app](./media/logic-apps-batch-process-send-receive-messages/batch-sender-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="716ad-205">The list also shows any other logic apps that have batch triggers.</span><span class="sxs-lookup"><span data-stu-id="716ad-205">The list also shows any other logic apps that have batch triggers.</span></span> 
      > 
      > <span data-ttu-id="716ad-206">If you're using Visual Studio, and you don't see any batch receivers to select, check that you deployed your batch receiver to Azure.</span><span class="sxs-lookup"><span data-stu-id="716ad-206">If you're using Visual Studio, and you don't see any batch receivers to select, check that you deployed your batch receiver to Azure.</span></span> <span data-ttu-id="716ad-207">If you haven't, learn how to [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span><span class="sxs-lookup"><span data-stu-id="716ad-207">If you haven't, learn how to [deploy your batch receiver logic app to Azure](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#deploy-logic-app-to-azure).</span></span> 

   4. <span data-ttu-id="716ad-208">Select this action: **Batch_messages - <*your-batch-receiver*>**</span><span class="sxs-lookup"><span data-stu-id="716ad-208">Select this action: **Batch_messages - <*your-batch-receiver*>**</span></span>

      ![Select this action: "Batch_messages - <your-logic-app>"](./media/logic-apps-batch-process-send-receive-messages/batch-sender-select-batch.png)

3. <span data-ttu-id="716ad-210">Set the batch sender's properties:</span><span class="sxs-lookup"><span data-stu-id="716ad-210">Set the batch sender's properties:</span></span>

   | <span data-ttu-id="716ad-211">Property</span><span class="sxs-lookup"><span data-stu-id="716ad-211">Property</span></span> | <span data-ttu-id="716ad-212">Description</span><span class="sxs-lookup"><span data-stu-id="716ad-212">Description</span></span> | 
   |----------|-------------| 
   | <span data-ttu-id="716ad-213">**Batch Name**</span><span class="sxs-lookup"><span data-stu-id="716ad-213">**Batch Name**</span></span> | <span data-ttu-id="716ad-214">The batch name defined by the receiver logic app, which is "TestBatch" in this example</span><span class="sxs-lookup"><span data-stu-id="716ad-214">The batch name defined by the receiver logic app, which is "TestBatch" in this example</span></span> <p><span data-ttu-id="716ad-215">**Important**: The batch name gets validated at runtime and must match the name specified by the receiver logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-215">**Important**: The batch name gets validated at runtime and must match the name specified by the receiver logic app.</span></span> <span data-ttu-id="716ad-216">Changing the batch name causes the batch sender to fail.</span><span class="sxs-lookup"><span data-stu-id="716ad-216">Changing the batch name causes the batch sender to fail.</span></span> | 
   | <span data-ttu-id="716ad-217">**Message Content**</span><span class="sxs-lookup"><span data-stu-id="716ad-217">**Message Content**</span></span> | <span data-ttu-id="716ad-218">The content for the message you want to send</span><span class="sxs-lookup"><span data-stu-id="716ad-218">The content for the message you want to send</span></span> | 
   ||| 

   <span data-ttu-id="716ad-219">For this example, add this expression, which inserts the current date and time into the message content that you send to the batch:</span><span class="sxs-lookup"><span data-stu-id="716ad-219">For this example, add this expression, which inserts the current date and time into the message content that you send to the batch:</span></span>

   1. <span data-ttu-id="716ad-220">Click inside the **Message Content** box.</span><span class="sxs-lookup"><span data-stu-id="716ad-220">Click inside the **Message Content** box.</span></span> 

   2. <span data-ttu-id="716ad-221">When the dynamic content list appears, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="716ad-221">When the dynamic content list appears, choose **Expression**.</span></span> 

   3. <span data-ttu-id="716ad-222">Enter the expression `utcnow()`, and then choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="716ad-222">Enter the expression `utcnow()`, and then choose **OK**.</span></span> 

      ![In "Message Content", choose "Expression", enter "utcnow()", and choose "OK".](./media/logic-apps-batch-process-send-receive-messages/batch-sender-details.png)

4. <span data-ttu-id="716ad-224">Now set up a partition for the batch.</span><span class="sxs-lookup"><span data-stu-id="716ad-224">Now set up a partition for the batch.</span></span> <span data-ttu-id="716ad-225">In the "BatchReceiver" action, choose **Show advanced options** and set these properties:</span><span class="sxs-lookup"><span data-stu-id="716ad-225">In the "BatchReceiver" action, choose **Show advanced options** and set these properties:</span></span>

   | <span data-ttu-id="716ad-226">Property</span><span class="sxs-lookup"><span data-stu-id="716ad-226">Property</span></span> | <span data-ttu-id="716ad-227">Description</span><span class="sxs-lookup"><span data-stu-id="716ad-227">Description</span></span> | 
   |----------|-------------| 
   | <span data-ttu-id="716ad-228">**Partition Name**</span><span class="sxs-lookup"><span data-stu-id="716ad-228">**Partition Name**</span></span> | <span data-ttu-id="716ad-229">An optional unique partition key to use for dividing the target batch into logical subsets and collect messages based on that key</span><span class="sxs-lookup"><span data-stu-id="716ad-229">An optional unique partition key to use for dividing the target batch into logical subsets and collect messages based on that key</span></span> | 
   | <span data-ttu-id="716ad-230">**Message Id**</span><span class="sxs-lookup"><span data-stu-id="716ad-230">**Message Id**</span></span> | <span data-ttu-id="716ad-231">An optional message identifier that is a generated globally unique identifier (GUID) when empty</span><span class="sxs-lookup"><span data-stu-id="716ad-231">An optional message identifier that is a generated globally unique identifier (GUID) when empty</span></span> | 
   ||| 

   <span data-ttu-id="716ad-232">For this example, in the **Partition Name** box, add an expression that generates a random number between one and five.</span><span class="sxs-lookup"><span data-stu-id="716ad-232">For this example, in the **Partition Name** box, add an expression that generates a random number between one and five.</span></span> <span data-ttu-id="716ad-233">Leave the **Message Id** box empty.</span><span class="sxs-lookup"><span data-stu-id="716ad-233">Leave the **Message Id** box empty.</span></span>
   
   1. <span data-ttu-id="716ad-234">Click inside the **Partition Name** box so that the dynamic content list appears.</span><span class="sxs-lookup"><span data-stu-id="716ad-234">Click inside the **Partition Name** box so that the dynamic content list appears.</span></span> 

   2. <span data-ttu-id="716ad-235">In the dynamic content list, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="716ad-235">In the dynamic content list, choose **Expression**.</span></span>
   
   3. <span data-ttu-id="716ad-236">Enter the expression `rand(1,6)`, and then choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="716ad-236">Enter the expression `rand(1,6)`, and then choose **OK**.</span></span>

      ![Set up a partition for your target batch](./media/logic-apps-batch-process-send-receive-messages/batch-sender-partition-advanced-options.png)

      <span data-ttu-id="716ad-238">This **rand** function generates a number between one and five.</span><span class="sxs-lookup"><span data-stu-id="716ad-238">This **rand** function generates a number between one and five.</span></span> 
      <span data-ttu-id="716ad-239">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span><span class="sxs-lookup"><span data-stu-id="716ad-239">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

5. <span data-ttu-id="716ad-240">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="716ad-240">Save your logic app.</span></span> <span data-ttu-id="716ad-241">Your sender logic app now looks similar to this example:</span><span class="sxs-lookup"><span data-stu-id="716ad-241">Your sender logic app now looks similar to this example:</span></span>

   ![Save your sender logic app](./media/logic-apps-batch-process-send-receive-messages/batch-sender-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="716ad-243">Test your logic apps</span><span class="sxs-lookup"><span data-stu-id="716ad-243">Test your logic apps</span></span>

<span data-ttu-id="716ad-244">To test your batching solution, leave your logic apps running for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="716ad-244">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="716ad-245">Soon, you start getting emails in groups of five, all with the same partition key.</span><span class="sxs-lookup"><span data-stu-id="716ad-245">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="716ad-246">Your batch sender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span><span class="sxs-lookup"><span data-stu-id="716ad-246">Your batch sender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="716ad-247">Each time the batch has five items with the same partition key, your batch receiver logic app fires and sends mail for each message.</span><span class="sxs-lookup"><span data-stu-id="716ad-247">Each time the batch has five items with the same partition key, your batch receiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="716ad-248">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span><span class="sxs-lookup"><span data-stu-id="716ad-248">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="716ad-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="716ad-249">Next steps</span></span>

* [<span data-ttu-id="716ad-250">Build on logic app definitions by using JSON</span><span class="sxs-lookup"><span data-stu-id="716ad-250">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="716ad-251">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span><span class="sxs-lookup"><span data-stu-id="716ad-251">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="716ad-252">Exception handling and error logging for logic apps</span><span class="sxs-lookup"><span data-stu-id="716ad-252">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
