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
# <a name="get-started-with-the-azure-sql-database-connector"></a>Get started with the Azure SQL Database connector
Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables. 

With SQL Database, you:

* Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.
* Use actions to get a row of data, insert a new row, and even delete. For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action). 

This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.

> [!NOTE]
> This version of the article applies to Logic Apps general availability (GA). 
> 
> 

To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-to-azure-sql-database"></a>Connect to Azure SQL Database
Before your logic app can access any service, you first create a *connection* to the service. A connection provides connectivity between a logic app and another service. For example, to connect to SQL Database, you first create a SQL Database *connection*. To create a connection, you enter the credentials you normally use to access the service you are connecting to. So, in SQL Database, enter your SQL Database credentials to create the connection. 

#### <a name="create-the-connection"></a>Create the connection
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Use a trigger
This connector does not have any triggers. Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more. [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.

## <a name="use-an-action"></a>Use an action
An action is an operation carried out by the workflow defined in a logic app. [Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Select the plus sign. You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/add-action.png)
2. Choose **Add an action**.
3. In the text box, type “sql” to get a list of all the available actions.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/sql-1.png) 
4. In our example, choose **SQL Server - Get row**. If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-sqlazure/sample-table.png)
   
    If you are prompted for the connection information, then enter the details to create the connection. [Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties. 
   
   > [!NOTE]
   > In this example, we return a row from a table. To see the data in this row, add another action that creates a file using the fields from the table. For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account. 
   > 
   > 
5. **Save** your changes (top left corner of the toolbar). Your logic app is saved and may be automatically enabled.

## <a name="technical-details"></a>Technical Details
## <a name="sql-database-actions"></a>SQL Database actions
An action is an operation carried out by the workflow defined in a logic app. The SQL Database connector includes the following actions. 

| Action | Description |
| --- | --- |
| [ExecuteProcedure](connectors-create-api-sqlazure.md#execute-stored-procedure) |Executes a stored procedure in SQL |
| [GetRow](connectors-create-api-sqlazure.md#get-row) |Retrieves a single row from a SQL table |
| [GetRows](connectors-create-api-sqlazure.md#get-rows) |Retrieves rows from a SQL table |
| [InsertRow](connectors-create-api-sqlazure.md#insert-row) |Inserts a new row into a SQL table |
| [DeleteRow](connectors-create-api-sqlazure.md#delete-row) |Deletes a row from a SQL table |
| [GetTables](connectors-create-api-sqlazure.md#get-tables) |Retrieves tables from a SQL database |
| [UpdateRow](connectors-create-api-sqlazure.md#update-row) |Updates an existing row in a SQL table |

### <a name="action-details"></a>Action Details
In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.

#### <a name="execute-stored-procedure"></a>Execute stored procedure
Executes a stored procedure in SQL.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| procedure * |Procedure name |The name of the stored procedure you want to execute |
| parameters * |Input parameters |The parameters are dynamic and based on the stored procedure you choose. <br/><br/> For example, if you're using the Adventure Works sample database, choose the *ufnGetCustomerInformation* stored procedure. The **Customer ID** input parameter is displayed. Enter "6" or one of the other customer IDs. |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
ProcedureResult: Carries result of stored procedure execution

| Property Name | Data Type | Description |
| --- | --- | --- |
| OutputParameters |object |Output parameter values |
| ReturnCode |integer |Return code of a procedure |
| ResultSets |object |Result sets |

#### <a name="get-row"></a>Get row
Retrieves a single row from a SQL table.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| table * |Table name |Name of SQL table |
| id * |Row id |Unique identifier of the row to retrieve |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

#### <a name="get-rows"></a>Get rows
Retrieves rows from a SQL table.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Table name |Name of SQL table |
| $skip |Skip Count |Number of entries to skip (default = 0) |
| $top |Maximum Get Count |Maximum number of entries to retrieve (default = 256) |
| $filter |Filter Query |An ODATA filter query to restrict the number of entries |
| $orderby |Order By |An ODATA orderBy query for specifying the order of entries |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
ItemsList

| Property Name | Data Type |
| --- | --- |
| value |array |

#### <a name="insert-row"></a>Insert row
Inserts a new row into a SQL table.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Table name |Name of SQL table |
| item* |Row |Row to insert into the specified table in SQL |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

#### <a name="delete-row"></a>Delete row
Deletes a row from a SQL table.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Table name |Name of SQL table |
| id* |Row id |Unique identifier of the row to delete |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
None.

#### <a name="get-tables"></a>Get tables
Retrieves tables from a SQL database.  

There are no parameters for this call. 

##### <a name="output-details"></a>Output Details
TablesList

| Property Name | Data Type |
| --- | --- |
| value |array |

#### <a name="update-row"></a>Update row
Updates an existing row in a SQL table.  

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Table name |Name of SQL table |
| id* |Row id |Unique identifier of the row to update |
| item* |Row |Row with updated values |

An asterisk (*) means the property is required.

##### <a name="output-details"></a>Output Details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

### <a name="http-responses"></a>HTTP Responses
When making calls to the different actions, you may get certain responses. The following table outlines the responses and their descriptions:  

| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occurred |
| default |Operation Failed. |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md). Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).




