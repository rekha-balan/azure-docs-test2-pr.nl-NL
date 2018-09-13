---
title: Connect to MQ server - Azure Logic Apps | Microsoft Docs
description: Send and retrieve messages with an Azure or on-premises MQ server and Azure Logic Apps
author: valthom
manager: jeconnoc
ms.author: valthom
ms.date: 06/01/2017
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 03b8d6c7f61982184d23f3b119c87f4605da921b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967523"
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="15a0b-103">Connect to an IBM MQ server from logic apps using the MQ connector</span><span class="sxs-lookup"><span data-stu-id="15a0b-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="15a0b-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span><span class="sxs-lookup"><span data-stu-id="15a0b-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="15a0b-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span><span class="sxs-lookup"><span data-stu-id="15a0b-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="15a0b-106">This document is a starter guide to use the MQ connector.</span><span class="sxs-lookup"><span data-stu-id="15a0b-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="15a0b-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span><span class="sxs-lookup"><span data-stu-id="15a0b-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="15a0b-108">The MQ connector includes the following actions.</span><span class="sxs-lookup"><span data-stu-id="15a0b-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="15a0b-109">There are no triggers.</span><span class="sxs-lookup"><span data-stu-id="15a0b-109">There are no triggers.</span></span>

-   <span data-ttu-id="15a0b-110">Browse a single message without deleting the message from the IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="15a0b-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="15a0b-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="15a0b-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="15a0b-112">Receive a single message and delete the message from the IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="15a0b-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="15a0b-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="15a0b-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="15a0b-114">Send a single message to the IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="15a0b-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="15a0b-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15a0b-115">Prerequisites</span></span>

* <span data-ttu-id="15a0b-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span><span class="sxs-lookup"><span data-stu-id="15a0b-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="15a0b-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span><span class="sxs-lookup"><span data-stu-id="15a0b-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15a0b-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span><span class="sxs-lookup"><span data-stu-id="15a0b-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="15a0b-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="15a0b-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="15a0b-120">Officially supported IBM WebSphere MQ versions:</span><span class="sxs-lookup"><span data-stu-id="15a0b-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="15a0b-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="15a0b-121">MQ 7.5</span></span>
   * <span data-ttu-id="15a0b-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="15a0b-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="15a0b-123">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="15a0b-123">Create a logic app</span></span>

1. <span data-ttu-id="15a0b-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="15a0b-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span><span class="sxs-lookup"><span data-stu-id="15a0b-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="15a0b-126">Select **Pin to dashboard**, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="15a0b-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="15a0b-128">Add a trigger</span><span class="sxs-lookup"><span data-stu-id="15a0b-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="15a0b-129">The MQ Connector does not have any triggers.</span><span class="sxs-lookup"><span data-stu-id="15a0b-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="15a0b-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="15a0b-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="15a0b-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span><span class="sxs-lookup"><span data-stu-id="15a0b-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="15a0b-132">Select **Edit** within the Recurrence Trigger.</span><span class="sxs-lookup"><span data-stu-id="15a0b-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="15a0b-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="15a0b-134">Browse a single message</span><span class="sxs-lookup"><span data-stu-id="15a0b-134">Browse a single message</span></span>
1. <span data-ttu-id="15a0b-135">Select **+ New step**, and select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="15a0b-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="15a0b-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="15a0b-138">If there isn't an existing MQ connection, then create the connection:</span><span class="sxs-lookup"><span data-stu-id="15a0b-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="15a0b-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span><span class="sxs-lookup"><span data-stu-id="15a0b-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="15a0b-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span><span class="sxs-lookup"><span data-stu-id="15a0b-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="15a0b-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span><span class="sxs-lookup"><span data-stu-id="15a0b-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="15a0b-142">Select your gateway.</span><span class="sxs-lookup"><span data-stu-id="15a0b-142">Select your gateway.</span></span>
    3. <span data-ttu-id="15a0b-143">Select **Create** when finished.</span><span class="sxs-lookup"><span data-stu-id="15a0b-143">Select **Create** when finished.</span></span> <span data-ttu-id="15a0b-144">Your connection looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="15a0b-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="15a0b-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="15a0b-146">In the action properties, you can:</span><span class="sxs-lookup"><span data-stu-id="15a0b-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="15a0b-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span><span class="sxs-lookup"><span data-stu-id="15a0b-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="15a0b-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span><span class="sxs-lookup"><span data-stu-id="15a0b-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="15a0b-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span><span class="sxs-lookup"><span data-stu-id="15a0b-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="15a0b-150">Or, set it to **False** to not include additional message information in the output.</span><span class="sxs-lookup"><span data-stu-id="15a0b-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="15a0b-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span><span class="sxs-lookup"><span data-stu-id="15a0b-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="15a0b-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span><span class="sxs-lookup"><span data-stu-id="15a0b-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="15a0b-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="15a0b-154">**Save** your changes, and then **Run** your logic app:</span><span class="sxs-lookup"><span data-stu-id="15a0b-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="15a0b-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="15a0b-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span><span class="sxs-lookup"><span data-stu-id="15a0b-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="15a0b-157">Select the green checkmark to see details of each step.</span><span class="sxs-lookup"><span data-stu-id="15a0b-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="15a0b-158">Select **See raw outputs** to see additional details on the output data.</span><span class="sxs-lookup"><span data-stu-id="15a0b-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="15a0b-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="15a0b-160">Raw output:</span><span class="sxs-lookup"><span data-stu-id="15a0b-160">Raw output:</span></span>  
    ![Browse message raw output](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="15a0b-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span><span class="sxs-lookup"><span data-stu-id="15a0b-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="15a0b-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="15a0b-164">Browse multiple messages</span><span class="sxs-lookup"><span data-stu-id="15a0b-164">Browse multiple messages</span></span>
<span data-ttu-id="15a0b-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span><span class="sxs-lookup"><span data-stu-id="15a0b-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="15a0b-166">If **BatchSize** has no entry, all messages are returned.</span><span class="sxs-lookup"><span data-stu-id="15a0b-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="15a0b-167">The returned output is an array of messages.</span><span class="sxs-lookup"><span data-stu-id="15a0b-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="15a0b-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span><span class="sxs-lookup"><span data-stu-id="15a0b-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="15a0b-169">Select **Change connection** to create a new connection, or select a different connection.</span><span class="sxs-lookup"><span data-stu-id="15a0b-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="15a0b-170">The output of Browse messages shows:</span><span class="sxs-lookup"><span data-stu-id="15a0b-170">The output of Browse messages shows:</span></span>  
![Browse messages output](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="15a0b-172">Receive a single message</span><span class="sxs-lookup"><span data-stu-id="15a0b-172">Receive a single message</span></span>
<span data-ttu-id="15a0b-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span><span class="sxs-lookup"><span data-stu-id="15a0b-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="15a0b-174">When using **Receive message**, the message is deleted from the queue.</span><span class="sxs-lookup"><span data-stu-id="15a0b-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="15a0b-175">Receive multiple messages</span><span class="sxs-lookup"><span data-stu-id="15a0b-175">Receive multiple messages</span></span>
<span data-ttu-id="15a0b-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span><span class="sxs-lookup"><span data-stu-id="15a0b-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="15a0b-177">When using **Receive messages**, the messages are deleted from the queue.</span><span class="sxs-lookup"><span data-stu-id="15a0b-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="15a0b-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span><span class="sxs-lookup"><span data-stu-id="15a0b-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![MQ No Message Error](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="15a0b-180">Send a message</span><span class="sxs-lookup"><span data-stu-id="15a0b-180">Send a message</span></span>
1. <span data-ttu-id="15a0b-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span><span class="sxs-lookup"><span data-stu-id="15a0b-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="15a0b-182">Select **Change connection** to create a new connection, or select a different connection.</span><span class="sxs-lookup"><span data-stu-id="15a0b-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="15a0b-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span><span class="sxs-lookup"><span data-stu-id="15a0b-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="15a0b-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="15a0b-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="15a0b-185">The output of Send message looks like the following:</span><span class="sxs-lookup"><span data-stu-id="15a0b-185">The output of Send message looks like the following:</span></span>  
![Send Msg Output](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="15a0b-187">Connector-specific details</span><span class="sxs-lookup"><span data-stu-id="15a0b-187">Connector-specific details</span></span>

<span data-ttu-id="15a0b-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="15a0b-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a0b-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="15a0b-189">Next steps</span></span>
<span data-ttu-id="15a0b-190">[Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="15a0b-190">[Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="15a0b-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="15a0b-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
