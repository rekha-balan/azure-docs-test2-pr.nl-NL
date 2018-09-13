---
title: Add the Azure SQL Database connector in your Logic Apps | Microsoft Docs
description: Overview of Azure SQL Database connector with REST API parameters
services: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia
ms.openlocfilehash: b01634afd6ae8cabd8caa9b08a4aee6c5e9c4654
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662030"
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="e733a-103">Get started with the Azure SQL Database connector</span><span class="sxs-lookup"><span data-stu-id="e733a-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="e733a-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span><span class="sxs-lookup"><span data-stu-id="e733a-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="e733a-105">With SQL Database, you:</span><span class="sxs-lookup"><span data-stu-id="e733a-105">With SQL Database, you:</span></span>

* <span data-ttu-id="e733a-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span><span class="sxs-lookup"><span data-stu-id="e733a-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="e733a-107">Use actions to get a row of data, insert a new row, and even delete.</span><span class="sxs-lookup"><span data-stu-id="e733a-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="e733a-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span><span class="sxs-lookup"><span data-stu-id="e733a-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="e733a-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span><span class="sxs-lookup"><span data-stu-id="e733a-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

> [!NOTE]
> <span data-ttu-id="e733a-110">This version of the article applies to Logic Apps general availability (GA).</span><span class="sxs-lookup"><span data-stu-id="e733a-110">This version of the article applies to Logic Apps general availability (GA).</span></span> 
> 
> 

<span data-ttu-id="e733a-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e733a-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="e733a-112">Connect to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e733a-112">Connect to Azure SQL Database</span></span>
<span data-ttu-id="e733a-113">Before your logic app can access any service, you first create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="e733a-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="e733a-114">A connection provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="e733a-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e733a-115">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span><span class="sxs-lookup"><span data-stu-id="e733a-115">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="e733a-116">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="e733a-116">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="e733a-117">So, in SQL Database, enter your SQL Database credentials to create the connection.</span><span class="sxs-lookup"><span data-stu-id="e733a-117">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="e733a-118">Create the connection</span><span class="sxs-lookup"><span data-stu-id="e733a-118">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e733a-119">Use a trigger</span><span class="sxs-lookup"><span data-stu-id="e733a-119">Use a trigger</span></span>
<span data-ttu-id="e733a-120">This connector does not have any triggers.</span><span class="sxs-lookup"><span data-stu-id="e733a-120">This connector does not have any triggers.</span></span> <span data-ttu-id="e733a-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span><span class="sxs-lookup"><span data-stu-id="e733a-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="e733a-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span><span class="sxs-lookup"><span data-stu-id="e733a-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e733a-123">Use an action</span><span class="sxs-lookup"><span data-stu-id="e733a-123">Use an action</span></span>
<span data-ttu-id="e733a-124">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="e733a-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e733a-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e733a-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e733a-126">Select the plus sign.</span><span class="sxs-lookup"><span data-stu-id="e733a-126">Select the plus sign.</span></span> <span data-ttu-id="e733a-127">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span><span class="sxs-lookup"><span data-stu-id="e733a-127">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="e733a-128">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="e733a-128">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e733a-129">In the text box, type “sql” to get a list of all the available actions.</span><span class="sxs-lookup"><span data-stu-id="e733a-129">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="e733a-130">In our example, choose **SQL Server - Get row**.</span><span class="sxs-lookup"><span data-stu-id="e733a-130">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="e733a-131">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span><span class="sxs-lookup"><span data-stu-id="e733a-131">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="e733a-132">If you are prompted for the connection information, then enter the details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="e733a-132">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="e733a-133">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span><span class="sxs-lookup"><span data-stu-id="e733a-133">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e733a-134">In this example, we return a row from a table.</span><span class="sxs-lookup"><span data-stu-id="e733a-134">In this example, we return a row from a table.</span></span> <span data-ttu-id="e733a-135">To see the data in this row, add another action that creates a file using the fields from the table.</span><span class="sxs-lookup"><span data-stu-id="e733a-135">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="e733a-136">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span><span class="sxs-lookup"><span data-stu-id="e733a-136">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="e733a-137">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="e733a-137">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="e733a-138">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="e733a-138">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="technical-details"></a><span data-ttu-id="e733a-139">Technical Details</span><span class="sxs-lookup"><span data-stu-id="e733a-139">Technical Details</span></span>
## <a name="sql-database-actions"></a><span data-ttu-id="e733a-140">SQL Database actions</span><span class="sxs-lookup"><span data-stu-id="e733a-140">SQL Database actions</span></span>
<span data-ttu-id="e733a-141">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="e733a-141">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e733a-142">The SQL Database connector includes the following actions.</span><span class="sxs-lookup"><span data-stu-id="e733a-142">The SQL Database connector includes the following actions.</span></span> 

| <span data-ttu-id="e733a-143">Action</span><span class="sxs-lookup"><span data-stu-id="e733a-143">Action</span></span> | <span data-ttu-id="e733a-144">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-144">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e733a-145">ExecuteProcedure</span><span class="sxs-lookup"><span data-stu-id="e733a-145">ExecuteProcedure</span></span>](connectors-create-api-sqlazure.md#execute-stored-procedure) |<span data-ttu-id="e733a-146">Executes a stored procedure in SQL</span><span class="sxs-lookup"><span data-stu-id="e733a-146">Executes a stored procedure in SQL</span></span> |
| [<span data-ttu-id="e733a-147">GetRow</span><span class="sxs-lookup"><span data-stu-id="e733a-147">GetRow</span></span>](connectors-create-api-sqlazure.md#get-row) |<span data-ttu-id="e733a-148">Retrieves a single row from a SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-148">Retrieves a single row from a SQL table</span></span> |
| [<span data-ttu-id="e733a-149">GetRows</span><span class="sxs-lookup"><span data-stu-id="e733a-149">GetRows</span></span>](connectors-create-api-sqlazure.md#get-rows) |<span data-ttu-id="e733a-150">Retrieves rows from a SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-150">Retrieves rows from a SQL table</span></span> |
| [<span data-ttu-id="e733a-151">InsertRow</span><span class="sxs-lookup"><span data-stu-id="e733a-151">InsertRow</span></span>](connectors-create-api-sqlazure.md#insert-row) |<span data-ttu-id="e733a-152">Inserts a new row into a SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-152">Inserts a new row into a SQL table</span></span> |
| [<span data-ttu-id="e733a-153">DeleteRow</span><span class="sxs-lookup"><span data-stu-id="e733a-153">DeleteRow</span></span>](connectors-create-api-sqlazure.md#delete-row) |<span data-ttu-id="e733a-154">Deletes a row from a SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-154">Deletes a row from a SQL table</span></span> |
| [<span data-ttu-id="e733a-155">GetTables</span><span class="sxs-lookup"><span data-stu-id="e733a-155">GetTables</span></span>](connectors-create-api-sqlazure.md#get-tables) |<span data-ttu-id="e733a-156">Retrieves tables from a SQL database</span><span class="sxs-lookup"><span data-stu-id="e733a-156">Retrieves tables from a SQL database</span></span> |
| [<span data-ttu-id="e733a-157">UpdateRow</span><span class="sxs-lookup"><span data-stu-id="e733a-157">UpdateRow</span></span>](connectors-create-api-sqlazure.md#update-row) |<span data-ttu-id="e733a-158">Updates an existing row in a SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-158">Updates an existing row in a SQL table</span></span> |

### <a name="action-details"></a><span data-ttu-id="e733a-159">Action Details</span><span class="sxs-lookup"><span data-stu-id="e733a-159">Action Details</span></span>
<span data-ttu-id="e733a-160">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span><span class="sxs-lookup"><span data-stu-id="e733a-160">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span></span>

#### <a name="execute-stored-procedure"></a><span data-ttu-id="e733a-161">Execute stored procedure</span><span class="sxs-lookup"><span data-stu-id="e733a-161">Execute stored procedure</span></span>
<span data-ttu-id="e733a-162">Executes a stored procedure in SQL.</span><span class="sxs-lookup"><span data-stu-id="e733a-162">Executes a stored procedure in SQL.</span></span>  

| <span data-ttu-id="e733a-163">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-163">Property Name</span></span> | <span data-ttu-id="e733a-164">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-164">Display Name</span></span> | <span data-ttu-id="e733a-165">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-166">procedure \*</span><span class="sxs-lookup"><span data-stu-id="e733a-166">procedure \*</span></span> |<span data-ttu-id="e733a-167">Procedure name</span><span class="sxs-lookup"><span data-stu-id="e733a-167">Procedure name</span></span> |<span data-ttu-id="e733a-168">The name of the stored procedure you want to execute</span><span class="sxs-lookup"><span data-stu-id="e733a-168">The name of the stored procedure you want to execute</span></span> |
| <span data-ttu-id="e733a-169">parameters \*</span><span class="sxs-lookup"><span data-stu-id="e733a-169">parameters \*</span></span> |<span data-ttu-id="e733a-170">Input parameters</span><span class="sxs-lookup"><span data-stu-id="e733a-170">Input parameters</span></span> |<span data-ttu-id="e733a-171">The parameters are dynamic and based on the stored procedure you choose.</span><span class="sxs-lookup"><span data-stu-id="e733a-171">The parameters are dynamic and based on the stored procedure you choose.</span></span> <br/><br/> <span data-ttu-id="e733a-172">For example, if you're using the Adventure Works sample database, choose the *ufnGetCustomerInformation* stored procedure.</span><span class="sxs-lookup"><span data-stu-id="e733a-172">For example, if you're using the Adventure Works sample database, choose the *ufnGetCustomerInformation* stored procedure.</span></span> <span data-ttu-id="e733a-173">The **Customer ID** input parameter is displayed.</span><span class="sxs-lookup"><span data-stu-id="e733a-173">The **Customer ID** input parameter is displayed.</span></span> <span data-ttu-id="e733a-174">Enter "6" or one of the other customer IDs.</span><span class="sxs-lookup"><span data-stu-id="e733a-174">Enter "6" or one of the other customer IDs.</span></span> |

<span data-ttu-id="e733a-175">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-175">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-176">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-176">Output Details</span></span>
<span data-ttu-id="e733a-177">ProcedureResult: Carries result of stored procedure execution</span><span class="sxs-lookup"><span data-stu-id="e733a-177">ProcedureResult: Carries result of stored procedure execution</span></span>

| <span data-ttu-id="e733a-178">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-178">Property Name</span></span> | <span data-ttu-id="e733a-179">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-179">Data Type</span></span> | <span data-ttu-id="e733a-180">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-180">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-181">OutputParameters</span><span class="sxs-lookup"><span data-stu-id="e733a-181">OutputParameters</span></span> |<span data-ttu-id="e733a-182">object</span><span class="sxs-lookup"><span data-stu-id="e733a-182">object</span></span> |<span data-ttu-id="e733a-183">Output parameter values</span><span class="sxs-lookup"><span data-stu-id="e733a-183">Output parameter values</span></span> |
| <span data-ttu-id="e733a-184">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="e733a-184">ReturnCode</span></span> |<span data-ttu-id="e733a-185">integer</span><span class="sxs-lookup"><span data-stu-id="e733a-185">integer</span></span> |<span data-ttu-id="e733a-186">Return code of a procedure</span><span class="sxs-lookup"><span data-stu-id="e733a-186">Return code of a procedure</span></span> |
| <span data-ttu-id="e733a-187">ResultSets</span><span class="sxs-lookup"><span data-stu-id="e733a-187">ResultSets</span></span> |<span data-ttu-id="e733a-188">object</span><span class="sxs-lookup"><span data-stu-id="e733a-188">object</span></span> |<span data-ttu-id="e733a-189">Result sets</span><span class="sxs-lookup"><span data-stu-id="e733a-189">Result sets</span></span> |

#### <a name="get-row"></a><span data-ttu-id="e733a-190">Get row</span><span class="sxs-lookup"><span data-stu-id="e733a-190">Get row</span></span>
<span data-ttu-id="e733a-191">Retrieves a single row from a SQL table.</span><span class="sxs-lookup"><span data-stu-id="e733a-191">Retrieves a single row from a SQL table.</span></span>  

| <span data-ttu-id="e733a-192">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-192">Property Name</span></span> | <span data-ttu-id="e733a-193">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-193">Display Name</span></span> | <span data-ttu-id="e733a-194">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-195">table \*</span><span class="sxs-lookup"><span data-stu-id="e733a-195">table \*</span></span> |<span data-ttu-id="e733a-196">Table name</span><span class="sxs-lookup"><span data-stu-id="e733a-196">Table name</span></span> |<span data-ttu-id="e733a-197">Name of SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-197">Name of SQL table</span></span> |
| <span data-ttu-id="e733a-198">id \*</span><span class="sxs-lookup"><span data-stu-id="e733a-198">id \*</span></span> |<span data-ttu-id="e733a-199">Row id</span><span class="sxs-lookup"><span data-stu-id="e733a-199">Row id</span></span> |<span data-ttu-id="e733a-200">Unique identifier of the row to retrieve</span><span class="sxs-lookup"><span data-stu-id="e733a-200">Unique identifier of the row to retrieve</span></span> |

<span data-ttu-id="e733a-201">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-201">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-202">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-202">Output Details</span></span>
<span data-ttu-id="e733a-203">Item</span><span class="sxs-lookup"><span data-stu-id="e733a-203">Item</span></span>

| <span data-ttu-id="e733a-204">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-204">Property Name</span></span> | <span data-ttu-id="e733a-205">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-205">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-206">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="e733a-206">ItemInternalId</span></span> |<span data-ttu-id="e733a-207">string</span><span class="sxs-lookup"><span data-stu-id="e733a-207">string</span></span> |

#### <a name="get-rows"></a><span data-ttu-id="e733a-208">Get rows</span><span class="sxs-lookup"><span data-stu-id="e733a-208">Get rows</span></span>
<span data-ttu-id="e733a-209">Retrieves rows from a SQL table.</span><span class="sxs-lookup"><span data-stu-id="e733a-209">Retrieves rows from a SQL table.</span></span>  

| <span data-ttu-id="e733a-210">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-210">Property Name</span></span> | <span data-ttu-id="e733a-211">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-211">Display Name</span></span> | <span data-ttu-id="e733a-212">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-212">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-213">table\*</span><span class="sxs-lookup"><span data-stu-id="e733a-213">table\*</span></span> |<span data-ttu-id="e733a-214">Table name</span><span class="sxs-lookup"><span data-stu-id="e733a-214">Table name</span></span> |<span data-ttu-id="e733a-215">Name of SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-215">Name of SQL table</span></span> |
| <span data-ttu-id="e733a-216">$skip</span><span class="sxs-lookup"><span data-stu-id="e733a-216">$skip</span></span> |<span data-ttu-id="e733a-217">Skip Count</span><span class="sxs-lookup"><span data-stu-id="e733a-217">Skip Count</span></span> |<span data-ttu-id="e733a-218">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="e733a-218">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="e733a-219">$top</span><span class="sxs-lookup"><span data-stu-id="e733a-219">$top</span></span> |<span data-ttu-id="e733a-220">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="e733a-220">Maximum Get Count</span></span> |<span data-ttu-id="e733a-221">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="e733a-221">Maximum number of entries to retrieve (default = 256)</span></span> |
| <span data-ttu-id="e733a-222">$filter</span><span class="sxs-lookup"><span data-stu-id="e733a-222">$filter</span></span> |<span data-ttu-id="e733a-223">Filter Query</span><span class="sxs-lookup"><span data-stu-id="e733a-223">Filter Query</span></span> |<span data-ttu-id="e733a-224">An ODATA filter query to restrict the number of entries</span><span class="sxs-lookup"><span data-stu-id="e733a-224">An ODATA filter query to restrict the number of entries</span></span> |
| <span data-ttu-id="e733a-225">$orderby</span><span class="sxs-lookup"><span data-stu-id="e733a-225">$orderby</span></span> |<span data-ttu-id="e733a-226">Order By</span><span class="sxs-lookup"><span data-stu-id="e733a-226">Order By</span></span> |<span data-ttu-id="e733a-227">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="e733a-227">An ODATA orderBy query for specifying the order of entries</span></span> |

<span data-ttu-id="e733a-228">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-228">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-229">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-229">Output Details</span></span>
<span data-ttu-id="e733a-230">ItemsList</span><span class="sxs-lookup"><span data-stu-id="e733a-230">ItemsList</span></span>

| <span data-ttu-id="e733a-231">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-231">Property Name</span></span> | <span data-ttu-id="e733a-232">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-232">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-233">value</span><span class="sxs-lookup"><span data-stu-id="e733a-233">value</span></span> |<span data-ttu-id="e733a-234">array</span><span class="sxs-lookup"><span data-stu-id="e733a-234">array</span></span> |

#### <a name="insert-row"></a><span data-ttu-id="e733a-235">Insert row</span><span class="sxs-lookup"><span data-stu-id="e733a-235">Insert row</span></span>
<span data-ttu-id="e733a-236">Inserts a new row into a SQL table.</span><span class="sxs-lookup"><span data-stu-id="e733a-236">Inserts a new row into a SQL table.</span></span>  

| <span data-ttu-id="e733a-237">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-237">Property Name</span></span> | <span data-ttu-id="e733a-238">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-238">Display Name</span></span> | <span data-ttu-id="e733a-239">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-239">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-240">table\*</span><span class="sxs-lookup"><span data-stu-id="e733a-240">table\*</span></span> |<span data-ttu-id="e733a-241">Table name</span><span class="sxs-lookup"><span data-stu-id="e733a-241">Table name</span></span> |<span data-ttu-id="e733a-242">Name of SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-242">Name of SQL table</span></span> |
| <span data-ttu-id="e733a-243">item\*</span><span class="sxs-lookup"><span data-stu-id="e733a-243">item\*</span></span> |<span data-ttu-id="e733a-244">Row</span><span class="sxs-lookup"><span data-stu-id="e733a-244">Row</span></span> |<span data-ttu-id="e733a-245">Row to insert into the specified table in SQL</span><span class="sxs-lookup"><span data-stu-id="e733a-245">Row to insert into the specified table in SQL</span></span> |

<span data-ttu-id="e733a-246">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-246">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-247">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-247">Output Details</span></span>
<span data-ttu-id="e733a-248">Item</span><span class="sxs-lookup"><span data-stu-id="e733a-248">Item</span></span>

| <span data-ttu-id="e733a-249">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-249">Property Name</span></span> | <span data-ttu-id="e733a-250">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-250">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-251">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="e733a-251">ItemInternalId</span></span> |<span data-ttu-id="e733a-252">string</span><span class="sxs-lookup"><span data-stu-id="e733a-252">string</span></span> |

#### <a name="delete-row"></a><span data-ttu-id="e733a-253">Delete row</span><span class="sxs-lookup"><span data-stu-id="e733a-253">Delete row</span></span>
<span data-ttu-id="e733a-254">Deletes a row from a SQL table.</span><span class="sxs-lookup"><span data-stu-id="e733a-254">Deletes a row from a SQL table.</span></span>  

| <span data-ttu-id="e733a-255">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-255">Property Name</span></span> | <span data-ttu-id="e733a-256">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-256">Display Name</span></span> | <span data-ttu-id="e733a-257">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-257">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-258">table\*</span><span class="sxs-lookup"><span data-stu-id="e733a-258">table\*</span></span> |<span data-ttu-id="e733a-259">Table name</span><span class="sxs-lookup"><span data-stu-id="e733a-259">Table name</span></span> |<span data-ttu-id="e733a-260">Name of SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-260">Name of SQL table</span></span> |
| <span data-ttu-id="e733a-261">id\*</span><span class="sxs-lookup"><span data-stu-id="e733a-261">id\*</span></span> |<span data-ttu-id="e733a-262">Row id</span><span class="sxs-lookup"><span data-stu-id="e733a-262">Row id</span></span> |<span data-ttu-id="e733a-263">Unique identifier of the row to delete</span><span class="sxs-lookup"><span data-stu-id="e733a-263">Unique identifier of the row to delete</span></span> |

<span data-ttu-id="e733a-264">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-264">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-265">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-265">Output Details</span></span>
<span data-ttu-id="e733a-266">None.</span><span class="sxs-lookup"><span data-stu-id="e733a-266">None.</span></span>

#### <a name="get-tables"></a><span data-ttu-id="e733a-267">Get tables</span><span class="sxs-lookup"><span data-stu-id="e733a-267">Get tables</span></span>
<span data-ttu-id="e733a-268">Retrieves tables from a SQL database.</span><span class="sxs-lookup"><span data-stu-id="e733a-268">Retrieves tables from a SQL database.</span></span>  

<span data-ttu-id="e733a-269">There are no parameters for this call.</span><span class="sxs-lookup"><span data-stu-id="e733a-269">There are no parameters for this call.</span></span> 

##### <a name="output-details"></a><span data-ttu-id="e733a-270">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-270">Output Details</span></span>
<span data-ttu-id="e733a-271">TablesList</span><span class="sxs-lookup"><span data-stu-id="e733a-271">TablesList</span></span>

| <span data-ttu-id="e733a-272">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-272">Property Name</span></span> | <span data-ttu-id="e733a-273">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-273">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-274">value</span><span class="sxs-lookup"><span data-stu-id="e733a-274">value</span></span> |<span data-ttu-id="e733a-275">array</span><span class="sxs-lookup"><span data-stu-id="e733a-275">array</span></span> |

#### <a name="update-row"></a><span data-ttu-id="e733a-276">Update row</span><span class="sxs-lookup"><span data-stu-id="e733a-276">Update row</span></span>
<span data-ttu-id="e733a-277">Updates an existing row in a SQL table.</span><span class="sxs-lookup"><span data-stu-id="e733a-277">Updates an existing row in a SQL table.</span></span>  

| <span data-ttu-id="e733a-278">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-278">Property Name</span></span> | <span data-ttu-id="e733a-279">Display Name</span><span class="sxs-lookup"><span data-stu-id="e733a-279">Display Name</span></span> | <span data-ttu-id="e733a-280">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-280">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e733a-281">table\*</span><span class="sxs-lookup"><span data-stu-id="e733a-281">table\*</span></span> |<span data-ttu-id="e733a-282">Table name</span><span class="sxs-lookup"><span data-stu-id="e733a-282">Table name</span></span> |<span data-ttu-id="e733a-283">Name of SQL table</span><span class="sxs-lookup"><span data-stu-id="e733a-283">Name of SQL table</span></span> |
| <span data-ttu-id="e733a-284">id\*</span><span class="sxs-lookup"><span data-stu-id="e733a-284">id\*</span></span> |<span data-ttu-id="e733a-285">Row id</span><span class="sxs-lookup"><span data-stu-id="e733a-285">Row id</span></span> |<span data-ttu-id="e733a-286">Unique identifier of the row to update</span><span class="sxs-lookup"><span data-stu-id="e733a-286">Unique identifier of the row to update</span></span> |
| <span data-ttu-id="e733a-287">item\*</span><span class="sxs-lookup"><span data-stu-id="e733a-287">item\*</span></span> |<span data-ttu-id="e733a-288">Row</span><span class="sxs-lookup"><span data-stu-id="e733a-288">Row</span></span> |<span data-ttu-id="e733a-289">Row with updated values</span><span class="sxs-lookup"><span data-stu-id="e733a-289">Row with updated values</span></span> |

<span data-ttu-id="e733a-290">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="e733a-290">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="e733a-291">Output Details</span><span class="sxs-lookup"><span data-stu-id="e733a-291">Output Details</span></span>
<span data-ttu-id="e733a-292">Item</span><span class="sxs-lookup"><span data-stu-id="e733a-292">Item</span></span>

| <span data-ttu-id="e733a-293">Property Name</span><span class="sxs-lookup"><span data-stu-id="e733a-293">Property Name</span></span> | <span data-ttu-id="e733a-294">Data Type</span><span class="sxs-lookup"><span data-stu-id="e733a-294">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-295">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="e733a-295">ItemInternalId</span></span> |<span data-ttu-id="e733a-296">string</span><span class="sxs-lookup"><span data-stu-id="e733a-296">string</span></span> |

### <a name="http-responses"></a><span data-ttu-id="e733a-297">HTTP Responses</span><span class="sxs-lookup"><span data-stu-id="e733a-297">HTTP Responses</span></span>
<span data-ttu-id="e733a-298">When making calls to the different actions, you may get certain responses.</span><span class="sxs-lookup"><span data-stu-id="e733a-298">When making calls to the different actions, you may get certain responses.</span></span> <span data-ttu-id="e733a-299">The following table outlines the responses and their descriptions:</span><span class="sxs-lookup"><span data-stu-id="e733a-299">The following table outlines the responses and their descriptions:</span></span>  

| <span data-ttu-id="e733a-300">Name</span><span class="sxs-lookup"><span data-stu-id="e733a-300">Name</span></span> | <span data-ttu-id="e733a-301">Description</span><span class="sxs-lookup"><span data-stu-id="e733a-301">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e733a-302">200</span><span class="sxs-lookup"><span data-stu-id="e733a-302">200</span></span> |<span data-ttu-id="e733a-303">OK</span><span class="sxs-lookup"><span data-stu-id="e733a-303">OK</span></span> |
| <span data-ttu-id="e733a-304">202</span><span class="sxs-lookup"><span data-stu-id="e733a-304">202</span></span> |<span data-ttu-id="e733a-305">Accepted</span><span class="sxs-lookup"><span data-stu-id="e733a-305">Accepted</span></span> |
| <span data-ttu-id="e733a-306">400</span><span class="sxs-lookup"><span data-stu-id="e733a-306">400</span></span> |<span data-ttu-id="e733a-307">Bad Request</span><span class="sxs-lookup"><span data-stu-id="e733a-307">Bad Request</span></span> |
| <span data-ttu-id="e733a-308">401</span><span class="sxs-lookup"><span data-stu-id="e733a-308">401</span></span> |<span data-ttu-id="e733a-309">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="e733a-309">Unauthorized</span></span> |
| <span data-ttu-id="e733a-310">403</span><span class="sxs-lookup"><span data-stu-id="e733a-310">403</span></span> |<span data-ttu-id="e733a-311">Forbidden</span><span class="sxs-lookup"><span data-stu-id="e733a-311">Forbidden</span></span> |
| <span data-ttu-id="e733a-312">404</span><span class="sxs-lookup"><span data-stu-id="e733a-312">404</span></span> |<span data-ttu-id="e733a-313">Not Found</span><span class="sxs-lookup"><span data-stu-id="e733a-313">Not Found</span></span> |
| <span data-ttu-id="e733a-314">500</span><span class="sxs-lookup"><span data-stu-id="e733a-314">500</span></span> |<span data-ttu-id="e733a-315">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="e733a-315">Internal Server Error.</span></span> <span data-ttu-id="e733a-316">Unknown error occurred</span><span class="sxs-lookup"><span data-stu-id="e733a-316">Unknown error occurred</span></span> |
| <span data-ttu-id="e733a-317">default</span><span class="sxs-lookup"><span data-stu-id="e733a-317">default</span></span> |<span data-ttu-id="e733a-318">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="e733a-318">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e733a-319">Next steps</span><span class="sxs-lookup"><span data-stu-id="e733a-319">Next steps</span></span>
<span data-ttu-id="e733a-320">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e733a-320">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e733a-321">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e733a-321">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>




