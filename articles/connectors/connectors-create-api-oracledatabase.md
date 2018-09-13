---
title: Connect to Oracle Database - Azure Logic Apps | Microsoft Docs
description: Insert and manage records with Oracle Database REST APIs and Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 03/29/2017
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 8e83a246c815a01b417f7658535906c396bf5996
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44770425"
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="faffa-103">Get started with the Oracle Database connector</span><span class="sxs-lookup"><span data-stu-id="faffa-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="faffa-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span><span class="sxs-lookup"><span data-stu-id="faffa-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="faffa-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span><span class="sxs-lookup"><span data-stu-id="faffa-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="faffa-106">With this connector, you can:</span><span class="sxs-lookup"><span data-stu-id="faffa-106">With this connector, you can:</span></span>

* <span data-ttu-id="faffa-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span><span class="sxs-lookup"><span data-stu-id="faffa-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="faffa-108">Use actions to get a row of data, insert a new row, and even delete.</span><span class="sxs-lookup"><span data-stu-id="faffa-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="faffa-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span><span class="sxs-lookup"><span data-stu-id="faffa-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="faffa-110">This article shows you how to use the Oracle Database connector in a logic app.</span><span class="sxs-lookup"><span data-stu-id="faffa-110">This article shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faffa-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="faffa-111">Prerequisites</span></span>

* <span data-ttu-id="faffa-112">Supported Oracle versions:</span><span class="sxs-lookup"><span data-stu-id="faffa-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="faffa-113">Oracle 9 and later</span><span class="sxs-lookup"><span data-stu-id="faffa-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="faffa-114">Oracle client software 8.1.7 and later</span><span class="sxs-lookup"><span data-stu-id="faffa-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="faffa-115">Install the on-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="faffa-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="faffa-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span><span class="sxs-lookup"><span data-stu-id="faffa-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="faffa-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span><span class="sxs-lookup"><span data-stu-id="faffa-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="faffa-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span><span class="sxs-lookup"><span data-stu-id="faffa-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="faffa-119">The same gateway can be used with multiple services, and multiple data sources.</span><span class="sxs-lookup"><span data-stu-id="faffa-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="faffa-120">So, you may only need to install the gateway once.</span><span class="sxs-lookup"><span data-stu-id="faffa-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="faffa-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="faffa-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="faffa-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span><span class="sxs-lookup"><span data-stu-id="faffa-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="faffa-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span><span class="sxs-lookup"><span data-stu-id="faffa-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="faffa-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span><span class="sxs-lookup"><span data-stu-id="faffa-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="faffa-125">See the common errors in this article.</span><span class="sxs-lookup"><span data-stu-id="faffa-125">See the common errors in this article.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="faffa-126">Add the connector</span><span class="sxs-lookup"><span data-stu-id="faffa-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="faffa-127">This connector does not have any triggers.</span><span class="sxs-lookup"><span data-stu-id="faffa-127">This connector does not have any triggers.</span></span> <span data-ttu-id="faffa-128">It has only actions.</span><span class="sxs-lookup"><span data-stu-id="faffa-128">It has only actions.</span></span> <span data-ttu-id="faffa-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span><span class="sxs-lookup"><span data-stu-id="faffa-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="faffa-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="faffa-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="faffa-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span><span class="sxs-lookup"><span data-stu-id="faffa-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="faffa-132">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="faffa-132">Select **Save**.</span></span> <span data-ttu-id="faffa-133">When you save, a request URL is automatically generated.</span><span class="sxs-lookup"><span data-stu-id="faffa-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="faffa-134">Select **New step**, and select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="faffa-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="faffa-135">Type in `oracle` to see the available actions:</span><span class="sxs-lookup"><span data-stu-id="faffa-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="faffa-136">This is also the quickest way to see the triggers and actions available for any connector.</span><span class="sxs-lookup"><span data-stu-id="faffa-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="faffa-137">Type in part of the connector name, such as `oracle`.</span><span class="sxs-lookup"><span data-stu-id="faffa-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="faffa-138">The designer lists any triggers and any actions.</span><span class="sxs-lookup"><span data-stu-id="faffa-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="faffa-139">Select one of the actions, such as **Oracle Database - Get row**.</span><span class="sxs-lookup"><span data-stu-id="faffa-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="faffa-140">Select **Connect via on-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="faffa-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="faffa-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span><span class="sxs-lookup"><span data-stu-id="faffa-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="faffa-142">Once connected, select a table from the list, and enter the row ID to your table.</span><span class="sxs-lookup"><span data-stu-id="faffa-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="faffa-143">You need to know the identifier to the table.</span><span class="sxs-lookup"><span data-stu-id="faffa-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="faffa-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="faffa-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="faffa-145">This gives you the identifiable information you need to proceed.</span><span class="sxs-lookup"><span data-stu-id="faffa-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="faffa-146">In the following example, job data is being returned from a Human Resources database:</span><span class="sxs-lookup"><span data-stu-id="faffa-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="faffa-147">In this next step, you can use any of the other connectors to build your workflow.</span><span class="sxs-lookup"><span data-stu-id="faffa-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="faffa-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span><span class="sxs-lookup"><span data-stu-id="faffa-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="faffa-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span><span class="sxs-lookup"><span data-stu-id="faffa-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="faffa-150">**Save** your logic app, and then select **Run**.</span><span class="sxs-lookup"><span data-stu-id="faffa-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="faffa-151">Close the designer, and look at the runs history for the status.</span><span class="sxs-lookup"><span data-stu-id="faffa-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="faffa-152">If it fails, select the failed message row.</span><span class="sxs-lookup"><span data-stu-id="faffa-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="faffa-153">The designer opens, and shows you which step failed, and also shows the error information.</span><span class="sxs-lookup"><span data-stu-id="faffa-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="faffa-154">If it succeeds, then you should receive an email with the information you added.</span><span class="sxs-lookup"><span data-stu-id="faffa-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="faffa-155">Workflow ideas</span><span class="sxs-lookup"><span data-stu-id="faffa-155">Workflow ideas</span></span>

* <span data-ttu-id="faffa-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span><span class="sxs-lookup"><span data-stu-id="faffa-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="faffa-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="faffa-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="faffa-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span><span class="sxs-lookup"><span data-stu-id="faffa-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="faffa-159">Messages are sent to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="faffa-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="faffa-160">You want to get these messages, and put them in a database.</span><span class="sxs-lookup"><span data-stu-id="faffa-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="faffa-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span><span class="sxs-lookup"><span data-stu-id="faffa-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="faffa-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span><span class="sxs-lookup"><span data-stu-id="faffa-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="faffa-163">Common errors</span><span class="sxs-lookup"><span data-stu-id="faffa-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="faffa-164">**Error**: Cannot reach the Gateway</span><span class="sxs-lookup"><span data-stu-id="faffa-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="faffa-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span><span class="sxs-lookup"><span data-stu-id="faffa-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="faffa-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="faffa-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="faffa-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span><span class="sxs-lookup"><span data-stu-id="faffa-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="faffa-168">You can also restart the on-premises data gateway service (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="faffa-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-see-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="faffa-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span><span class="sxs-lookup"><span data-stu-id="faffa-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="faffa-170">See [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span><span class="sxs-lookup"><span data-stu-id="faffa-170">See [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="faffa-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span><span class="sxs-lookup"><span data-stu-id="faffa-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="faffa-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="faffa-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="faffa-173">**Error**: Table '[Tablename]' does not define any key columns</span><span class="sxs-lookup"><span data-stu-id="faffa-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="faffa-174">**Cause**: The table does not have any primary key.</span><span class="sxs-lookup"><span data-stu-id="faffa-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="faffa-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span><span class="sxs-lookup"><span data-stu-id="faffa-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="faffa-176">Currently not supported</span><span class="sxs-lookup"><span data-stu-id="faffa-176">Currently not supported</span></span>

* <span data-ttu-id="faffa-177">Views and stored procedures</span><span class="sxs-lookup"><span data-stu-id="faffa-177">Views and stored procedures</span></span> 
* <span data-ttu-id="faffa-178">Any table with composite keys</span><span class="sxs-lookup"><span data-stu-id="faffa-178">Any table with composite keys</span></span>
* <span data-ttu-id="faffa-179">Nested object types in tables</span><span class="sxs-lookup"><span data-stu-id="faffa-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="faffa-180">Connector-specific details</span><span class="sxs-lookup"><span data-stu-id="faffa-180">Connector-specific details</span></span>

<span data-ttu-id="faffa-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="faffa-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="faffa-182">Get some help</span><span class="sxs-lookup"><span data-stu-id="faffa-182">Get some help</span></span>

<span data-ttu-id="faffa-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span><span class="sxs-lookup"><span data-stu-id="faffa-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="faffa-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="faffa-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="faffa-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="faffa-185">Next steps</span></span>
<span data-ttu-id="faffa-186">[Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), and explore the available connectors in Logic Apps at [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="faffa-186">[Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), and explore the available connectors in Logic Apps at [APIs list](apis-list.md).</span></span>
