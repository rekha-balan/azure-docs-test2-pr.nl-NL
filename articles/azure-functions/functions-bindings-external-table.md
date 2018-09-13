---
title: External Table binding for Azure Functions (experimental)
description: Using External Table bindings in Azure Functions
services: functions
author: alexkarcher-msft
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 24728414747d8ad8a8d7ee0d8a21be2177a15ddd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857352"
---
# <a name="external-table-binding-for-azure-functions-experimental"></a><span data-ttu-id="75d7d-103">External Table binding for Azure Functions (experimental)</span><span class="sxs-lookup"><span data-stu-id="75d7d-103">External Table binding for Azure Functions (experimental)</span></span>

<span data-ttu-id="75d7d-104">This article explains how to work with tabular data on SaaS providers, such as Sharepoint and Dynamics, in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="75d7d-104">This article explains how to work with tabular data on SaaS providers, such as Sharepoint and Dynamics, in Azure Functions.</span></span> <span data-ttu-id="75d7d-105">Azure Functions supports input and output bindings for external tables.</span><span class="sxs-lookup"><span data-stu-id="75d7d-105">Azure Functions supports input and output bindings for external tables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75d7d-106">The External Table binding is experimental and might never reach Generally Available (GA) status.</span><span class="sxs-lookup"><span data-stu-id="75d7d-106">The External Table binding is experimental and might never reach Generally Available (GA) status.</span></span> <span data-ttu-id="75d7d-107">It is included only in Azure Functions 1.x, and there are no plans to add it to Azure Functions 2.x.</span><span class="sxs-lookup"><span data-stu-id="75d7d-107">It is included only in Azure Functions 1.x, and there are no plans to add it to Azure Functions 2.x.</span></span> <span data-ttu-id="75d7d-108">For scenarios that require access to data in SaaS providers, consider using [logic apps that call into functions](functions-twitter-email.md).</span><span class="sxs-lookup"><span data-stu-id="75d7d-108">For scenarios that require access to data in SaaS providers, consider using [logic apps that call into functions](functions-twitter-email.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="75d7d-109">API connections</span><span class="sxs-lookup"><span data-stu-id="75d7d-109">API connections</span></span>

<span data-ttu-id="75d7d-110">Table bindings leverage external API connections to authenticate with third-party SaaS providers.</span><span class="sxs-lookup"><span data-stu-id="75d7d-110">Table bindings leverage external API connections to authenticate with third-party SaaS providers.</span></span> 

<span data-ttu-id="75d7d-111">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group.</span><span class="sxs-lookup"><span data-stu-id="75d7d-111">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group.</span></span>

### <a name="available-api-connections-tables"></a><span data-ttu-id="75d7d-112">Available API connections (tables)</span><span class="sxs-lookup"><span data-stu-id="75d7d-112">Available API connections (tables)</span></span>

|<span data-ttu-id="75d7d-113">Connector</span><span class="sxs-lookup"><span data-stu-id="75d7d-113">Connector</span></span>|<span data-ttu-id="75d7d-114">Trigger</span><span class="sxs-lookup"><span data-stu-id="75d7d-114">Trigger</span></span>|<span data-ttu-id="75d7d-115">Input</span><span class="sxs-lookup"><span data-stu-id="75d7d-115">Input</span></span>|<span data-ttu-id="75d7d-116">Output</span><span class="sxs-lookup"><span data-stu-id="75d7d-116">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="75d7d-117">DB2</span><span class="sxs-lookup"><span data-stu-id="75d7d-117">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="75d7d-118">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-118">x</span></span>|<span data-ttu-id="75d7d-119">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-119">x</span></span>
|[<span data-ttu-id="75d7d-120">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="75d7d-120">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="75d7d-121">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-121">x</span></span>|<span data-ttu-id="75d7d-122">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-122">x</span></span>
|[<span data-ttu-id="75d7d-123">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="75d7d-123">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="75d7d-124">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-124">x</span></span>|<span data-ttu-id="75d7d-125">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-125">x</span></span>
|[<span data-ttu-id="75d7d-126">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="75d7d-126">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="75d7d-127">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-127">x</span></span>|<span data-ttu-id="75d7d-128">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-128">x</span></span>
|[<span data-ttu-id="75d7d-129">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="75d7d-129">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="75d7d-130">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-130">x</span></span>|<span data-ttu-id="75d7d-131">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-131">x</span></span>
|[<span data-ttu-id="75d7d-132">Informix</span><span class="sxs-lookup"><span data-stu-id="75d7d-132">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="75d7d-133">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-133">x</span></span>|<span data-ttu-id="75d7d-134">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-134">x</span></span>
|[<span data-ttu-id="75d7d-135">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="75d7d-135">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="75d7d-136">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-136">x</span></span>|<span data-ttu-id="75d7d-137">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-137">x</span></span>
|[<span data-ttu-id="75d7d-138">MySQL</span><span class="sxs-lookup"><span data-stu-id="75d7d-138">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="75d7d-139">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-139">x</span></span>|<span data-ttu-id="75d7d-140">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-140">x</span></span>
|[<span data-ttu-id="75d7d-141">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="75d7d-141">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="75d7d-142">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-142">x</span></span>|<span data-ttu-id="75d7d-143">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-143">x</span></span>
|[<span data-ttu-id="75d7d-144">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="75d7d-144">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="75d7d-145">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-145">x</span></span>|<span data-ttu-id="75d7d-146">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-146">x</span></span>
|[<span data-ttu-id="75d7d-147">Salesforce</span><span class="sxs-lookup"><span data-stu-id="75d7d-147">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="75d7d-148">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-148">x</span></span>|<span data-ttu-id="75d7d-149">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-149">x</span></span>
|[<span data-ttu-id="75d7d-150">SharePoint</span><span class="sxs-lookup"><span data-stu-id="75d7d-150">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="75d7d-151">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-151">x</span></span>|<span data-ttu-id="75d7d-152">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-152">x</span></span>
|[<span data-ttu-id="75d7d-153">SQL Server</span><span class="sxs-lookup"><span data-stu-id="75d7d-153">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="75d7d-154">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-154">x</span></span>|<span data-ttu-id="75d7d-155">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-155">x</span></span>
|[<span data-ttu-id="75d7d-156">Teradata</span><span class="sxs-lookup"><span data-stu-id="75d7d-156">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="75d7d-157">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-157">x</span></span>|<span data-ttu-id="75d7d-158">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-158">x</span></span>
|<span data-ttu-id="75d7d-159">UserVoice</span><span class="sxs-lookup"><span data-stu-id="75d7d-159">UserVoice</span></span>||<span data-ttu-id="75d7d-160">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-160">x</span></span>|<span data-ttu-id="75d7d-161">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-161">x</span></span>
|<span data-ttu-id="75d7d-162">Zendesk</span><span class="sxs-lookup"><span data-stu-id="75d7d-162">Zendesk</span></span>||<span data-ttu-id="75d7d-163">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-163">x</span></span>|<span data-ttu-id="75d7d-164">x</span><span class="sxs-lookup"><span data-stu-id="75d7d-164">x</span></span>

> [!NOTE]
> <span data-ttu-id="75d7d-165">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="75d7d-165">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span>

## <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="75d7d-166">Creating an API connection: step by step</span><span class="sxs-lookup"><span data-stu-id="75d7d-166">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="75d7d-167">In the Azure portal page for your function app, select the plus sign (**+**) to create a function.</span><span class="sxs-lookup"><span data-stu-id="75d7d-167">In the Azure portal page for your function app, select the plus sign (**+**) to create a function.</span></span>

1. <span data-ttu-id="75d7d-168">In the **Scenario** box, select **Experimental**.</span><span class="sxs-lookup"><span data-stu-id="75d7d-168">In the **Scenario** box, select **Experimental**.</span></span>

1. <span data-ttu-id="75d7d-169">Select **External table**.</span><span class="sxs-lookup"><span data-stu-id="75d7d-169">Select **External table**.</span></span>

1. <span data-ttu-id="75d7d-170">Select a language.</span><span class="sxs-lookup"><span data-stu-id="75d7d-170">Select a language.</span></span>

2. <span data-ttu-id="75d7d-171">Under **External Table connection**, select an existing connection or select **new**.</span><span class="sxs-lookup"><span data-stu-id="75d7d-171">Under **External Table connection**, select an existing connection or select **new**.</span></span>

1. <span data-ttu-id="75d7d-172">For a new connection, configure the settings, and select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="75d7d-172">For a new connection, configure the settings, and select **Authorize**.</span></span>

1. <span data-ttu-id="75d7d-173">Select **Create** to create the function.</span><span class="sxs-lookup"><span data-stu-id="75d7d-173">Select **Create** to create the function.</span></span>

1. <span data-ttu-id="75d7d-174">Select **Integrate > External Table**.</span><span class="sxs-lookup"><span data-stu-id="75d7d-174">Select **Integrate > External Table**.</span></span>

1. <span data-ttu-id="75d7d-175">Configure the connection to use your target table.</span><span class="sxs-lookup"><span data-stu-id="75d7d-175">Configure the connection to use your target table.</span></span> <span data-ttu-id="75d7d-176">These settings will vary between SaaS providers.</span><span class="sxs-lookup"><span data-stu-id="75d7d-176">These settings will vary between SaaS providers.</span></span> <span data-ttu-id="75d7d-177">Examples are included in the following section.</span><span class="sxs-lookup"><span data-stu-id="75d7d-177">Examples are included in the following section.</span></span>

## <a name="example"></a><span data-ttu-id="75d7d-178">Example</span><span class="sxs-lookup"><span data-stu-id="75d7d-178">Example</span></span>

<span data-ttu-id="75d7d-179">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span><span class="sxs-lookup"><span data-stu-id="75d7d-179">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="75d7d-180">The code lists the Contact entities in the table and logs the first and last names.</span><span class="sxs-lookup"><span data-stu-id="75d7d-180">The code lists the Contact entities in the table and logs the first and last names.</span></span>

<span data-ttu-id="75d7d-181">Here's the *function.json* file:</span><span class="sxs-lookup"><span data-stu-id="75d7d-181">Here's the *function.json* file:</span></span>

```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="75d7d-182">Here's the C# script code:</span><span class="sxs-lookup"><span data-stu-id="75d7d-182">Here's the C# script code:</span></span>

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retrieve table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

### <a name="sql-server-data-source"></a><span data-ttu-id="75d7d-183">SQL Server data source</span><span class="sxs-lookup"><span data-stu-id="75d7d-183">SQL Server data source</span></span>

<span data-ttu-id="75d7d-184">To create a table in SQL Server to use with this example, here's a script.</span><span class="sxs-lookup"><span data-stu-id="75d7d-184">To create a table in SQL Server to use with this example, here's a script.</span></span> <span data-ttu-id="75d7d-185">`dataSetName` is “default.”</span><span class="sxs-lookup"><span data-stu-id="75d7d-185">`dataSetName` is “default.”</span></span>

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets-data-source"></a><span data-ttu-id="75d7d-186">Google Sheets data source</span><span class="sxs-lookup"><span data-stu-id="75d7d-186">Google Sheets data source</span></span>

<span data-ttu-id="75d7d-187">To create a table to use with this example in Google Docs, create a spreadsheet with a worksheet named `Contact`.</span><span class="sxs-lookup"><span data-stu-id="75d7d-187">To create a table to use with this example in Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="75d7d-188">The connector cannot use the spreadsheet display name.</span><span class="sxs-lookup"><span data-stu-id="75d7d-188">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="75d7d-189">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span><span class="sxs-lookup"><span data-stu-id="75d7d-189">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="75d7d-190">Salesforce</span><span class="sxs-lookup"><span data-stu-id="75d7d-190">Salesforce</span></span>

<span data-ttu-id="75d7d-191">To use this example with Salesforce, `dataSetName` is “default.”</span><span class="sxs-lookup"><span data-stu-id="75d7d-191">To use this example with Salesforce, `dataSetName` is “default.”</span></span>

## <a name="configuration"></a><span data-ttu-id="75d7d-192">Configuration</span><span class="sxs-lookup"><span data-stu-id="75d7d-192">Configuration</span></span>

<span data-ttu-id="75d7d-193">The following table explains the binding configuration properties that you set in the *function.json* file.</span><span class="sxs-lookup"><span data-stu-id="75d7d-193">The following table explains the binding configuration properties that you set in the *function.json* file.</span></span>

|<span data-ttu-id="75d7d-194">function.json property</span><span class="sxs-lookup"><span data-stu-id="75d7d-194">function.json property</span></span> | <span data-ttu-id="75d7d-195">Description</span><span class="sxs-lookup"><span data-stu-id="75d7d-195">Description</span></span>|
|---------|----------------------|
|<span data-ttu-id="75d7d-196">**type**</span><span class="sxs-lookup"><span data-stu-id="75d7d-196">**type**</span></span> | <span data-ttu-id="75d7d-197">Must be set to `apiHubTable`.</span><span class="sxs-lookup"><span data-stu-id="75d7d-197">Must be set to `apiHubTable`.</span></span> <span data-ttu-id="75d7d-198">This property is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75d7d-198">This property is set automatically when you create the trigger in the Azure portal.</span></span>|
|<span data-ttu-id="75d7d-199">**direction**</span><span class="sxs-lookup"><span data-stu-id="75d7d-199">**direction**</span></span> | <span data-ttu-id="75d7d-200">Must be set to `in`.</span><span class="sxs-lookup"><span data-stu-id="75d7d-200">Must be set to `in`.</span></span> <span data-ttu-id="75d7d-201">This property is set automatically when you create the trigger in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75d7d-201">This property is set automatically when you create the trigger in the Azure portal.</span></span> |
|<span data-ttu-id="75d7d-202">**name**</span><span class="sxs-lookup"><span data-stu-id="75d7d-202">**name**</span></span> | <span data-ttu-id="75d7d-203">The name of the variable that represents the event item in function code.</span><span class="sxs-lookup"><span data-stu-id="75d7d-203">The name of the variable that represents the event item in function code.</span></span> | 
|<span data-ttu-id="75d7d-204">**connection**</span><span class="sxs-lookup"><span data-stu-id="75d7d-204">**connection**</span></span>| <span data-ttu-id="75d7d-205">Identifies the app setting that stores the API connection string.</span><span class="sxs-lookup"><span data-stu-id="75d7d-205">Identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="75d7d-206">The app setting is created automatically when you add an API connection in the integrate UI.</span><span class="sxs-lookup"><span data-stu-id="75d7d-206">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>|
|<span data-ttu-id="75d7d-207">**dataSetName**</span><span class="sxs-lookup"><span data-stu-id="75d7d-207">**dataSetName**</span></span>|<span data-ttu-id="75d7d-208">The name of the dataset that contains the table to read.</span><span class="sxs-lookup"><span data-stu-id="75d7d-208">The name of the dataset that contains the table to read.</span></span>|
|<span data-ttu-id="75d7d-209">**tableName**</span><span class="sxs-lookup"><span data-stu-id="75d7d-209">**tableName**</span></span>|<span data-ttu-id="75d7d-210">The name of the table</span><span class="sxs-lookup"><span data-stu-id="75d7d-210">The name of the table</span></span>|
|<span data-ttu-id="75d7d-211">**entityId**</span><span class="sxs-lookup"><span data-stu-id="75d7d-211">**entityId**</span></span>|<span data-ttu-id="75d7d-212">Must be empty for table bindings.</span><span class="sxs-lookup"><span data-stu-id="75d7d-212">Must be empty for table bindings.</span></span>

<span data-ttu-id="75d7d-213">A tabular connector provides data sets, and each data set contains tables.</span><span class="sxs-lookup"><span data-stu-id="75d7d-213">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="75d7d-214">The name of the default data set is “default.”</span><span class="sxs-lookup"><span data-stu-id="75d7d-214">The name of the default data set is “default.”</span></span> <span data-ttu-id="75d7d-215">The titles for a dataset and a table in various SaaS providers are listed below:</span><span class="sxs-lookup"><span data-stu-id="75d7d-215">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="75d7d-216">Connector</span><span class="sxs-lookup"><span data-stu-id="75d7d-216">Connector</span></span>|<span data-ttu-id="75d7d-217">Dataset</span><span class="sxs-lookup"><span data-stu-id="75d7d-217">Dataset</span></span>|<span data-ttu-id="75d7d-218">Table</span><span class="sxs-lookup"><span data-stu-id="75d7d-218">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="75d7d-219">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="75d7d-219">**SharePoint**</span></span>|<span data-ttu-id="75d7d-220">Site</span><span class="sxs-lookup"><span data-stu-id="75d7d-220">Site</span></span>|<span data-ttu-id="75d7d-221">SharePoint List</span><span class="sxs-lookup"><span data-stu-id="75d7d-221">SharePoint List</span></span>
|<span data-ttu-id="75d7d-222">**SQL**</span><span class="sxs-lookup"><span data-stu-id="75d7d-222">**SQL**</span></span>|<span data-ttu-id="75d7d-223">Database</span><span class="sxs-lookup"><span data-stu-id="75d7d-223">Database</span></span>|<span data-ttu-id="75d7d-224">Table</span><span class="sxs-lookup"><span data-stu-id="75d7d-224">Table</span></span> 
|<span data-ttu-id="75d7d-225">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="75d7d-225">**Google Sheet**</span></span>|<span data-ttu-id="75d7d-226">Spreadsheet</span><span class="sxs-lookup"><span data-stu-id="75d7d-226">Spreadsheet</span></span>|<span data-ttu-id="75d7d-227">Worksheet</span><span class="sxs-lookup"><span data-stu-id="75d7d-227">Worksheet</span></span> 
|<span data-ttu-id="75d7d-228">**Excel**</span><span class="sxs-lookup"><span data-stu-id="75d7d-228">**Excel**</span></span>|<span data-ttu-id="75d7d-229">Excel file</span><span class="sxs-lookup"><span data-stu-id="75d7d-229">Excel file</span></span>|<span data-ttu-id="75d7d-230">Sheet</span><span class="sxs-lookup"><span data-stu-id="75d7d-230">Sheet</span></span> 

## <a name="next-steps"></a><span data-ttu-id="75d7d-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="75d7d-231">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75d7d-232">Learn more about Azure functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="75d7d-232">Learn more about Azure functions triggers and bindings</span></span>](functions-triggers-bindings.md)
