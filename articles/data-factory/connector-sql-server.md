---
title: Copy data to/from SQL Server using Azure Data Factory | Microsoft Docs
description: Learn about how to move data to/from SQL Server database that is on-premises or in an Azure VM using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: 4a0800dccca3a43d49204dfbcc32e7778449ae6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855658"
---
# <a name="copy-data-to-and-from-sql-server-using-azure-data-factory"></a><span data-ttu-id="d4198-103">Copy data to and from SQL Server using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d4198-103">Copy data to and from SQL Server using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-sqlserver-connector.md)
> * [Current version](connector-sql-server.md)

<span data-ttu-id="d4198-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to an SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d4198-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to an SQL Server database.</span></span> <span data-ttu-id="d4198-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="d4198-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="d4198-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="d4198-108">Supported capabilities</span></span>

<span data-ttu-id="d4198-109">You can copy data from/to SQL Server database to any supported sink data store, or copy data from any supported source data store to SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d4198-109">You can copy data from/to SQL Server database to any supported sink data store, or copy data from any supported source data store to SQL Server database.</span></span> <span data-ttu-id="d4198-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="d4198-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="d4198-111">Specifically, this SQL Server connector supports:</span><span class="sxs-lookup"><span data-stu-id="d4198-111">Specifically, this SQL Server connector supports:</span></span>

- <span data-ttu-id="d4198-112">SQL Server version 2016, 2014, 2012, 2008 R2, 2008, and 2005</span><span class="sxs-lookup"><span data-stu-id="d4198-112">SQL Server version 2016, 2014, 2012, 2008 R2, 2008, and 2005</span></span>
- <span data-ttu-id="d4198-113">Copying data using **SQL** or **Windows** authentication.</span><span class="sxs-lookup"><span data-stu-id="d4198-113">Copying data using **SQL** or **Windows** authentication.</span></span>
- <span data-ttu-id="d4198-114">As source, retrieving data using SQL query or stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4198-114">As source, retrieving data using SQL query or stored procedure.</span></span>
- <span data-ttu-id="d4198-115">As sink, appending data to destination table or invoking a stored procedure with custom logic during copy.</span><span class="sxs-lookup"><span data-stu-id="d4198-115">As sink, appending data to destination table or invoking a stored procedure with custom logic during copy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4198-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d4198-116">Prerequisites</span></span>

<span data-ttu-id="d4198-117">To use copy data from a SQL Server database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d4198-117">To use copy data from a SQL Server database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="d4198-118">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="d4198-118">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span> <span data-ttu-id="d4198-119">The Integration Runtime provides a built-in SQL Server database driver, therefore you don't need to manually install any driver when copying data from/to SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d4198-119">The Integration Runtime provides a built-in SQL Server database driver, therefore you don't need to manually install any driver when copying data from/to SQL Server database.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d4198-120">Getting started</span><span class="sxs-lookup"><span data-stu-id="d4198-120">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="d4198-121">The following sections provide details about properties that are used to define Data Factory entities specific to SQL Server database connector.</span><span class="sxs-lookup"><span data-stu-id="d4198-121">The following sections provide details about properties that are used to define Data Factory entities specific to SQL Server database connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d4198-122">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="d4198-122">Linked service properties</span></span>

<span data-ttu-id="d4198-123">The following properties are supported for SQL Server linked service:</span><span class="sxs-lookup"><span data-stu-id="d4198-123">The following properties are supported for SQL Server linked service:</span></span>

| <span data-ttu-id="d4198-124">Property</span><span class="sxs-lookup"><span data-stu-id="d4198-124">Property</span></span> | <span data-ttu-id="d4198-125">Description</span><span class="sxs-lookup"><span data-stu-id="d4198-125">Description</span></span> | <span data-ttu-id="d4198-126">Required</span><span class="sxs-lookup"><span data-stu-id="d4198-126">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4198-127">type</span><span class="sxs-lookup"><span data-stu-id="d4198-127">type</span></span> | <span data-ttu-id="d4198-128">The type property must be set to: **SqlServer**</span><span class="sxs-lookup"><span data-stu-id="d4198-128">The type property must be set to: **SqlServer**</span></span> | <span data-ttu-id="d4198-129">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-129">Yes</span></span> |
| <span data-ttu-id="d4198-130">connectionString</span><span class="sxs-lookup"><span data-stu-id="d4198-130">connectionString</span></span> |<span data-ttu-id="d4198-131">Specify connectionString information needed to connect to the SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="d4198-131">Specify connectionString information needed to connect to the SQL Server database using either SQL authentication or Windows authentication.</span></span> <span data-ttu-id="d4198-132">Refer to the following sample.</span><span class="sxs-lookup"><span data-stu-id="d4198-132">Refer to the following sample.</span></span> <span data-ttu-id="d4198-133">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d4198-133">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="d4198-134">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-134">Yes</span></span> |
| <span data-ttu-id="d4198-135">userName</span><span class="sxs-lookup"><span data-stu-id="d4198-135">userName</span></span> |<span data-ttu-id="d4198-136">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="d4198-136">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="d4198-137">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="d4198-137">Example: **domainname\\username**.</span></span> |<span data-ttu-id="d4198-138">No</span><span class="sxs-lookup"><span data-stu-id="d4198-138">No</span></span> |
| <span data-ttu-id="d4198-139">password</span><span class="sxs-lookup"><span data-stu-id="d4198-139">password</span></span> |<span data-ttu-id="d4198-140">Specify password for the user account you specified for the userName.</span><span class="sxs-lookup"><span data-stu-id="d4198-140">Specify password for the user account you specified for the userName.</span></span> <span data-ttu-id="d4198-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d4198-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="d4198-142">No</span><span class="sxs-lookup"><span data-stu-id="d4198-142">No</span></span> |
| <span data-ttu-id="d4198-143">connectVia</span><span class="sxs-lookup"><span data-stu-id="d4198-143">connectVia</span></span> | <span data-ttu-id="d4198-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="d4198-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="d4198-145">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="d4198-145">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="d4198-146">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="d4198-146">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="d4198-147">No</span><span class="sxs-lookup"><span data-stu-id="d4198-147">No</span></span> |

>[!TIP]
>If you hit error with error code as "UserErrorFailedToConnectToSqlServer" and message like "The session limit for the database is XXX and has been reached.", add `Pooling=false` to your connection string and try again.

<span data-ttu-id="d4198-149">**Example 1: using SQL authentication**</span><span class="sxs-lookup"><span data-stu-id="d4198-149">**Example 1: using SQL authentication**</span></span>

```json
{
    "name": "SqlServerLinkedService",
    "properties": {
        "type": "SqlServer",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Data Source=<servername>\\<instance name if using named instance>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="d4198-150">**Example 2: using Windows authentication**</span><span class="sxs-lookup"><span data-stu-id="d4198-150">**Example 2: using Windows authentication**</span></span>

```json
{
    "name": "SqlServerLinkedService",
    "properties": {
        "type": "SqlServer",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Data Source=<servername>\\<instance name if using named instance>;Initial Catalog=<databasename>;Integrated Security=True;"
            },
             "userName": "<domain\\username>",
             "password": {
                "type": "SecureString",
                "value": "<password>"
             }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d4198-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="d4198-151">Dataset properties</span></span>

<span data-ttu-id="d4198-152">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="d4198-152">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="d4198-153">This section provides a list of properties supported by SQL Server dataset.</span><span class="sxs-lookup"><span data-stu-id="d4198-153">This section provides a list of properties supported by SQL Server dataset.</span></span>

<span data-ttu-id="d4198-154">To copy data from/to SQL Server database, set the type property of the dataset to **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="d4198-154">To copy data from/to SQL Server database, set the type property of the dataset to **SqlServerTable**.</span></span> <span data-ttu-id="d4198-155">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="d4198-155">The following properties are supported:</span></span>

| <span data-ttu-id="d4198-156">Property</span><span class="sxs-lookup"><span data-stu-id="d4198-156">Property</span></span> | <span data-ttu-id="d4198-157">Description</span><span class="sxs-lookup"><span data-stu-id="d4198-157">Description</span></span> | <span data-ttu-id="d4198-158">Required</span><span class="sxs-lookup"><span data-stu-id="d4198-158">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4198-159">type</span><span class="sxs-lookup"><span data-stu-id="d4198-159">type</span></span> | <span data-ttu-id="d4198-160">The type property of the dataset must be set to: **SqlServerTable**</span><span class="sxs-lookup"><span data-stu-id="d4198-160">The type property of the dataset must be set to: **SqlServerTable**</span></span> | <span data-ttu-id="d4198-161">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-161">Yes</span></span> |
| <span data-ttu-id="d4198-162">tableName</span><span class="sxs-lookup"><span data-stu-id="d4198-162">tableName</span></span> |<span data-ttu-id="d4198-163">Name of the table or view in the SQL Server database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="d4198-163">Name of the table or view in the SQL Server database instance that linked service refers to.</span></span> | <span data-ttu-id="d4198-164">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-164">Yes</span></span> |

<span data-ttu-id="d4198-165">**Example:**</span><span class="sxs-lookup"><span data-stu-id="d4198-165">**Example:**</span></span>

```json
{
    "name": "SQLServerDataset",
    "properties":
    {
        "type": "SqlServerTable",
        "linkedServiceName": {
            "referenceName": "<SQL Server linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="d4198-166">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="d4198-166">Copy activity properties</span></span>

<span data-ttu-id="d4198-167">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="d4198-167">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="d4198-168">This section provides a list of properties supported by SQL Server source and sink.</span><span class="sxs-lookup"><span data-stu-id="d4198-168">This section provides a list of properties supported by SQL Server source and sink.</span></span>

### <a name="sql-server-as-source"></a><span data-ttu-id="d4198-169">SQL Server as source</span><span class="sxs-lookup"><span data-stu-id="d4198-169">SQL Server as source</span></span>

<span data-ttu-id="d4198-170">To copy data from SQL Server, set the source type in the copy activity to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="d4198-170">To copy data from SQL Server, set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="d4198-171">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="d4198-171">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="d4198-172">Property</span><span class="sxs-lookup"><span data-stu-id="d4198-172">Property</span></span> | <span data-ttu-id="d4198-173">Description</span><span class="sxs-lookup"><span data-stu-id="d4198-173">Description</span></span> | <span data-ttu-id="d4198-174">Required</span><span class="sxs-lookup"><span data-stu-id="d4198-174">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4198-175">type</span><span class="sxs-lookup"><span data-stu-id="d4198-175">type</span></span> | <span data-ttu-id="d4198-176">The type property of the copy activity source must be set to: **SqlSource**</span><span class="sxs-lookup"><span data-stu-id="d4198-176">The type property of the copy activity source must be set to: **SqlSource**</span></span> | <span data-ttu-id="d4198-177">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-177">Yes</span></span> |
| <span data-ttu-id="d4198-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d4198-178">sqlReaderQuery</span></span> |<span data-ttu-id="d4198-179">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="d4198-179">Use the custom SQL query to read data.</span></span> <span data-ttu-id="d4198-180">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d4198-180">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="d4198-181">No</span><span class="sxs-lookup"><span data-stu-id="d4198-181">No</span></span> |
| <span data-ttu-id="d4198-182">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d4198-182">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d4198-183">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="d4198-183">Name of the stored procedure that reads data from the source table.</span></span> <span data-ttu-id="d4198-184">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4198-184">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="d4198-185">No</span><span class="sxs-lookup"><span data-stu-id="d4198-185">No</span></span> |
| <span data-ttu-id="d4198-186">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d4198-186">storedProcedureParameters</span></span> |<span data-ttu-id="d4198-187">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4198-187">Parameters for the stored procedure.</span></span><br/><span data-ttu-id="d4198-188">Allowed values are: name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="d4198-188">Allowed values are: name/value pairs.</span></span> <span data-ttu-id="d4198-189">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="d4198-189">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="d4198-190">No</span><span class="sxs-lookup"><span data-stu-id="d4198-190">No</span></span> |

<span data-ttu-id="d4198-191">**Points to note:**</span><span class="sxs-lookup"><span data-stu-id="d4198-191">**Points to note:**</span></span>

- <span data-ttu-id="d4198-192">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server source to get the data.</span><span class="sxs-lookup"><span data-stu-id="d4198-192">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server source to get the data.</span></span> <span data-ttu-id="d4198-193">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="d4198-193">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
- <span data-ttu-id="d4198-194">If you do not specify either "sqlReaderQuery" or "sqlReaderStoredProcedureName", the columns defined in the "structure" section of the dataset JSON are used to construct a query (`select column1, column2 from mytable`) to run against the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4198-194">If you do not specify either "sqlReaderQuery" or "sqlReaderStoredProcedureName", the columns defined in the "structure" section of the dataset JSON are used to construct a query (`select column1, column2 from mytable`) to run against the SQL Server.</span></span> <span data-ttu-id="d4198-195">If the dataset definition does not have the "structure", all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="d4198-195">If the dataset definition does not have the "structure", all columns are selected from the table.</span></span>
- <span data-ttu-id="d4198-196">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="d4198-196">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span></span>

<span data-ttu-id="d4198-197">**Example: using SQL query**</span><span class="sxs-lookup"><span data-stu-id="d4198-197">**Example: using SQL query**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSQLServer",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SQL Server input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
                "sqlReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

<span data-ttu-id="d4198-198">**Example: using stored procedure**</span><span class="sxs-lookup"><span data-stu-id="d4198-198">**Example: using stored procedure**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSQLServer",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SQL Server input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
                "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
                "storedProcedureParameters": {
                    "stringData": { "value": "str3" },
                    "identifier": { "value": "$$Text.Format('{0:yyyy}', <datetime parameter>)", "type": "Int"}
                }
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

<span data-ttu-id="d4198-199">**The stored procedure definition:**</span><span class="sxs-lookup"><span data-stu-id="d4198-199">**The stored procedure definition:**</span></span>

```sql
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sql-server-as-sink"></a><span data-ttu-id="d4198-200">SQL Server as sink</span><span class="sxs-lookup"><span data-stu-id="d4198-200">SQL Server as sink</span></span>

<span data-ttu-id="d4198-201">To copy data to SQL Server, set the sink type in the copy activity to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="d4198-201">To copy data to SQL Server, set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="d4198-202">The following properties are supported in the copy activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="d4198-202">The following properties are supported in the copy activity **sink** section:</span></span>

| <span data-ttu-id="d4198-203">Property</span><span class="sxs-lookup"><span data-stu-id="d4198-203">Property</span></span> | <span data-ttu-id="d4198-204">Description</span><span class="sxs-lookup"><span data-stu-id="d4198-204">Description</span></span> | <span data-ttu-id="d4198-205">Required</span><span class="sxs-lookup"><span data-stu-id="d4198-205">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4198-206">type</span><span class="sxs-lookup"><span data-stu-id="d4198-206">type</span></span> | <span data-ttu-id="d4198-207">The type property of the copy activity sink must be set to: **SqlSink**</span><span class="sxs-lookup"><span data-stu-id="d4198-207">The type property of the copy activity sink must be set to: **SqlSink**</span></span> | <span data-ttu-id="d4198-208">Yes</span><span class="sxs-lookup"><span data-stu-id="d4198-208">Yes</span></span> |
| <span data-ttu-id="d4198-209">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d4198-209">writeBatchSize</span></span> |<span data-ttu-id="d4198-210">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="d4198-210">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span><br/><span data-ttu-id="d4198-211">Allowed values are: integer (number of rows).</span><span class="sxs-lookup"><span data-stu-id="d4198-211">Allowed values are: integer (number of rows).</span></span> |<span data-ttu-id="d4198-212">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="d4198-212">No (default: 10000)</span></span> |
| <span data-ttu-id="d4198-213">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d4198-213">writeBatchTimeout</span></span> |<span data-ttu-id="d4198-214">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="d4198-214">Wait time for the batch insert operation to complete before it times out.</span></span><br/><span data-ttu-id="d4198-215">Allowed values are: timespan.</span><span class="sxs-lookup"><span data-stu-id="d4198-215">Allowed values are: timespan.</span></span> <span data-ttu-id="d4198-216">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="d4198-216">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d4198-217">No</span><span class="sxs-lookup"><span data-stu-id="d4198-217">No</span></span> |
| <span data-ttu-id="d4198-218">preCopyScript</span><span class="sxs-lookup"><span data-stu-id="d4198-218">preCopyScript</span></span> |<span data-ttu-id="d4198-219">Specify a SQL query for Copy Activity to execute before writing data into SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4198-219">Specify a SQL query for Copy Activity to execute before writing data into SQL Server.</span></span> <span data-ttu-id="d4198-220">It will only be invoked once per copy run.</span><span class="sxs-lookup"><span data-stu-id="d4198-220">It will only be invoked once per copy run.</span></span> <span data-ttu-id="d4198-221">You can use this property to clean up the pre-loaded data.</span><span class="sxs-lookup"><span data-stu-id="d4198-221">You can use this property to clean up the pre-loaded data.</span></span> |<span data-ttu-id="d4198-222">No</span><span class="sxs-lookup"><span data-stu-id="d4198-222">No</span></span> |
| <span data-ttu-id="d4198-223">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d4198-223">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="d4198-224">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span><span class="sxs-lookup"><span data-stu-id="d4198-224">Name of the stored procedure that defines how to apply source data into target table, e.g. to do upserts or transform using your own business logic.</span></span> <br/><br/><span data-ttu-id="d4198-225">Note this stored procedure will be **invoked per batch**.</span><span class="sxs-lookup"><span data-stu-id="d4198-225">Note this stored procedure will be **invoked per batch**.</span></span> <span data-ttu-id="d4198-226">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `preCopyScript` property.</span><span class="sxs-lookup"><span data-stu-id="d4198-226">If you want to do operation that only runs once and has nothing to do with source data e.g. delete/truncate, use `preCopyScript` property.</span></span> |<span data-ttu-id="d4198-227">No</span><span class="sxs-lookup"><span data-stu-id="d4198-227">No</span></span> |
| <span data-ttu-id="d4198-228">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d4198-228">storedProcedureParameters</span></span> |<span data-ttu-id="d4198-229">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4198-229">Parameters for the stored procedure.</span></span><br/><span data-ttu-id="d4198-230">Allowed values are: name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="d4198-230">Allowed values are: name/value pairs.</span></span> <span data-ttu-id="d4198-231">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="d4198-231">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="d4198-232">No</span><span class="sxs-lookup"><span data-stu-id="d4198-232">No</span></span> |
| <span data-ttu-id="d4198-233">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="d4198-233">sqlWriterTableType</span></span> |<span data-ttu-id="d4198-234">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d4198-234">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="d4198-235">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="d4198-235">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="d4198-236">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="d4198-236">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="d4198-237">No</span><span class="sxs-lookup"><span data-stu-id="d4198-237">No</span></span> |

> [!TIP]
> When copying data to SQL Server, the copy activity appends data to the sink table by default. To perform an UPSERT or additional business logic, use the stored procedure in SqlSink. Learn more details from [Invoking stored procedure for SQL Sink](#invoking-stored-procedure-for-sql-sink).

<span data-ttu-id="d4198-241">**Example 1: appending data**</span><span class="sxs-lookup"><span data-stu-id="d4198-241">**Example 1: appending data**</span></span>

```json
"activities":[
    {
        "name": "CopyToSQLServer",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<SQL Server output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "writeBatchSize": 100000
            }
        }
    }
]
```

<span data-ttu-id="d4198-242">**Example 2: invoking a stored procedure during copy for upsert**</span><span class="sxs-lookup"><span data-stu-id="d4198-242">**Example 2: invoking a stored procedure during copy for upsert**</span></span>

<span data-ttu-id="d4198-243">Learn more details from [Invoking stored procedure for SQL Sink](#invoking-stored-procedure-for-sql-sink).</span><span class="sxs-lookup"><span data-stu-id="d4198-243">Learn more details from [Invoking stored procedure for SQL Sink](#invoking-stored-procedure-for-sql-sink).</span></span>

```json
"activities":[
    {
        "name": "CopyToSQLServer",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<SQL Server output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
                "sqlWriterTableType": "CopyTestTableType",
                "storedProcedureParameters": {
                    "identifier": { "value": "1", "type": "Int" },
                    "stringData": { "value": "str1" }
                }
            }
        }
    }
]
```

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="d4198-244">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="d4198-244">Identity columns in the target database</span></span>

<span data-ttu-id="d4198-245">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="d4198-245">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="d4198-246">**Source table:**</span><span class="sxs-lookup"><span data-stu-id="d4198-246">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```

<span data-ttu-id="d4198-247">**Destination table:**</span><span class="sxs-lookup"><span data-stu-id="d4198-247">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="d4198-248">Notice that the target table has an identity column.</span><span class="sxs-lookup"><span data-stu-id="d4198-248">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="d4198-249">**Source dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="d4198-249">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "SourceTbl"
        }
    }
}
```

<span data-ttu-id="d4198-250">**Destination dataset JSON definition**</span><span class="sxs-lookup"><span data-stu-id="d4198-250">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "SqlServerTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "TargetTbl"
        }
    }
}
```

<span data-ttu-id="d4198-251">Notice that as your source and target table have different schema (target has an additional column with identity).</span><span class="sxs-lookup"><span data-stu-id="d4198-251">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="d4198-252">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="d4198-252">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoking-stored-procedure-for-sql-sink"></a> <span data-ttu-id="d4198-253">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="d4198-253">Invoke stored procedure from SQL sink</span></span>

<span data-ttu-id="d4198-254">When copying data into SQL Server database, a user specified stored procedure could be configured and invoked with additional parameters.</span><span class="sxs-lookup"><span data-stu-id="d4198-254">When copying data into SQL Server database, a user specified stored procedure could be configured and invoked with additional parameters.</span></span>

<span data-ttu-id="d4198-255">A stored procedure can be used when built-in copy mechanisms do not serve the purpose.</span><span class="sxs-lookup"><span data-stu-id="d4198-255">A stored procedure can be used when built-in copy mechanisms do not serve the purpose.</span></span> <span data-ttu-id="d4198-256">It is typically used when upsert (insert + update) or extra processing (merging columns, looking up additional values, insertion into multiple tables, etc.) needs to be done before the final insertion of source data in the destination table.</span><span class="sxs-lookup"><span data-stu-id="d4198-256">It is typically used when upsert (insert + update) or extra processing (merging columns, looking up additional values, insertion into multiple tables, etc.) needs to be done before the final insertion of source data in the destination table.</span></span>

<span data-ttu-id="d4198-257">The following sample shows how to use a stored procedure to do an upsert into a table in the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d4198-257">The following sample shows how to use a stored procedure to do an upsert into a table in the SQL Server database.</span></span> <span data-ttu-id="d4198-258">Assuming input data and the sink "Marketing" table each has three columns: ProfileID, State, and Category.</span><span class="sxs-lookup"><span data-stu-id="d4198-258">Assuming input data and the sink "Marketing" table each has three columns: ProfileID, State, and Category.</span></span> <span data-ttu-id="d4198-259">Perform upsert based on the “ProfileID” column and only apply for a specific category.</span><span class="sxs-lookup"><span data-stu-id="d4198-259">Perform upsert based on the “ProfileID” column and only apply for a specific category.</span></span>

<span data-ttu-id="d4198-260">**Output dataset**</span><span class="sxs-lookup"><span data-stu-id="d4198-260">**Output dataset**</span></span>

```json
{
    "name": "SQLServerDataset",
    "properties":
    {
        "type": "SqlServerTable",
        "linkedServiceName": {
            "referenceName": "<SQL Server linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "Marketing"
        }
    }
}
```

<span data-ttu-id="d4198-261">Define the SqlSink section in copy activity as follows.</span><span class="sxs-lookup"><span data-stu-id="d4198-261">Define the SqlSink section in copy activity as follows.</span></span>

```json
"sink": {
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing",
    "storedProcedureParameters": {
        "category": {
            "value": "ProductA"
        }
    }
}
```

<span data-ttu-id="d4198-262">In your database, define the stored procedure with the same name as SqlWriterStoredProcedureName.</span><span class="sxs-lookup"><span data-stu-id="d4198-262">In your database, define the stored procedure with the same name as SqlWriterStoredProcedureName.</span></span> <span data-ttu-id="d4198-263">It handles input data from your specified source, and merge into the output table.</span><span class="sxs-lookup"><span data-stu-id="d4198-263">It handles input data from your specified source, and merge into the output table.</span></span> <span data-ttu-id="d4198-264">The parameter name of the table type in the stored procedure should be the same as the "tableName" defined in dataset.</span><span class="sxs-lookup"><span data-stu-id="d4198-264">The parameter name of the table type in the stored procedure should be the same as the "tableName" defined in dataset.</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @category varchar(256)
AS
BEGIN
  MERGE [dbo].[Marketing] AS target
  USING @Marketing AS source
  ON (target.ProfileID = source.ProfileID and target.Category = @category)
  WHEN MATCHED THEN
      UPDATE SET State = source.State
  WHEN NOT MATCHED THEN
      INSERT (ProfileID, State, Category)
      VALUES (source.ProfileID, source.State, source.Category)
END
```

<span data-ttu-id="d4198-265">In your database, define the table type with the same name as sqlWriterTableType.</span><span class="sxs-lookup"><span data-stu-id="d4198-265">In your database, define the table type with the same name as sqlWriterTableType.</span></span> <span data-ttu-id="d4198-266">Notice that the schema of the table type should be same as the schema returned by your input data.</span><span class="sxs-lookup"><span data-stu-id="d4198-266">Notice that the schema of the table type should be same as the schema returned by your input data.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL，
    [Category] [varchar](256) NOT NULL，
)
```

<span data-ttu-id="d4198-267">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4198-267">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span>

## <a name="data-type-mapping-for-sql-server"></a><span data-ttu-id="d4198-268">Data type mapping for SQL server</span><span class="sxs-lookup"><span data-stu-id="d4198-268">Data type mapping for SQL server</span></span>

<span data-ttu-id="d4198-269">When copying data from/to SQL Server, the following mappings are used from SQL Server data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="d4198-269">When copying data from/to SQL Server, the following mappings are used from SQL Server data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="d4198-270">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="d4198-270">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="d4198-271">SQL Server data type</span><span class="sxs-lookup"><span data-stu-id="d4198-271">SQL Server data type</span></span> | <span data-ttu-id="d4198-272">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="d4198-272">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="d4198-273">bigint</span><span class="sxs-lookup"><span data-stu-id="d4198-273">bigint</span></span> |<span data-ttu-id="d4198-274">Int64</span><span class="sxs-lookup"><span data-stu-id="d4198-274">Int64</span></span> |
| <span data-ttu-id="d4198-275">binary</span><span class="sxs-lookup"><span data-stu-id="d4198-275">binary</span></span> |<span data-ttu-id="d4198-276">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-276">Byte[]</span></span> |
| <span data-ttu-id="d4198-277">bit</span><span class="sxs-lookup"><span data-stu-id="d4198-277">bit</span></span> |<span data-ttu-id="d4198-278">Boolean</span><span class="sxs-lookup"><span data-stu-id="d4198-278">Boolean</span></span> |
| <span data-ttu-id="d4198-279">char</span><span class="sxs-lookup"><span data-stu-id="d4198-279">char</span></span> |<span data-ttu-id="d4198-280">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-280">String, Char[]</span></span> |
| <span data-ttu-id="d4198-281">date</span><span class="sxs-lookup"><span data-stu-id="d4198-281">date</span></span> |<span data-ttu-id="d4198-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4198-282">DateTime</span></span> |
| <span data-ttu-id="d4198-283">Datetime</span><span class="sxs-lookup"><span data-stu-id="d4198-283">Datetime</span></span> |<span data-ttu-id="d4198-284">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4198-284">DateTime</span></span> |
| <span data-ttu-id="d4198-285">datetime2</span><span class="sxs-lookup"><span data-stu-id="d4198-285">datetime2</span></span> |<span data-ttu-id="d4198-286">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4198-286">DateTime</span></span> |
| <span data-ttu-id="d4198-287">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d4198-287">Datetimeoffset</span></span> |<span data-ttu-id="d4198-288">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4198-288">DateTimeOffset</span></span> |
| <span data-ttu-id="d4198-289">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4198-289">Decimal</span></span> |<span data-ttu-id="d4198-290">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4198-290">Decimal</span></span> |
| <span data-ttu-id="d4198-291">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="d4198-291">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="d4198-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-292">Byte[]</span></span> |
| <span data-ttu-id="d4198-293">Float</span><span class="sxs-lookup"><span data-stu-id="d4198-293">Float</span></span> |<span data-ttu-id="d4198-294">Double</span><span class="sxs-lookup"><span data-stu-id="d4198-294">Double</span></span> |
| <span data-ttu-id="d4198-295">image</span><span class="sxs-lookup"><span data-stu-id="d4198-295">image</span></span> |<span data-ttu-id="d4198-296">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-296">Byte[]</span></span> |
| <span data-ttu-id="d4198-297">int</span><span class="sxs-lookup"><span data-stu-id="d4198-297">int</span></span> |<span data-ttu-id="d4198-298">Int32</span><span class="sxs-lookup"><span data-stu-id="d4198-298">Int32</span></span> |
| <span data-ttu-id="d4198-299">money</span><span class="sxs-lookup"><span data-stu-id="d4198-299">money</span></span> |<span data-ttu-id="d4198-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4198-300">Decimal</span></span> |
| <span data-ttu-id="d4198-301">nchar</span><span class="sxs-lookup"><span data-stu-id="d4198-301">nchar</span></span> |<span data-ttu-id="d4198-302">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-302">String, Char[]</span></span> |
| <span data-ttu-id="d4198-303">ntext</span><span class="sxs-lookup"><span data-stu-id="d4198-303">ntext</span></span> |<span data-ttu-id="d4198-304">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-304">String, Char[]</span></span> |
| <span data-ttu-id="d4198-305">numeric</span><span class="sxs-lookup"><span data-stu-id="d4198-305">numeric</span></span> |<span data-ttu-id="d4198-306">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4198-306">Decimal</span></span> |
| <span data-ttu-id="d4198-307">nvarchar</span><span class="sxs-lookup"><span data-stu-id="d4198-307">nvarchar</span></span> |<span data-ttu-id="d4198-308">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-308">String, Char[]</span></span> |
| <span data-ttu-id="d4198-309">real</span><span class="sxs-lookup"><span data-stu-id="d4198-309">real</span></span> |<span data-ttu-id="d4198-310">Single</span><span class="sxs-lookup"><span data-stu-id="d4198-310">Single</span></span> |
| <span data-ttu-id="d4198-311">rowversion</span><span class="sxs-lookup"><span data-stu-id="d4198-311">rowversion</span></span> |<span data-ttu-id="d4198-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-312">Byte[]</span></span> |
| <span data-ttu-id="d4198-313">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="d4198-313">smalldatetime</span></span> |<span data-ttu-id="d4198-314">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4198-314">DateTime</span></span> |
| <span data-ttu-id="d4198-315">smallint</span><span class="sxs-lookup"><span data-stu-id="d4198-315">smallint</span></span> |<span data-ttu-id="d4198-316">Int16</span><span class="sxs-lookup"><span data-stu-id="d4198-316">Int16</span></span> |
| <span data-ttu-id="d4198-317">smallmoney</span><span class="sxs-lookup"><span data-stu-id="d4198-317">smallmoney</span></span> |<span data-ttu-id="d4198-318">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4198-318">Decimal</span></span> |
| <span data-ttu-id="d4198-319">sql_variant</span><span class="sxs-lookup"><span data-stu-id="d4198-319">sql_variant</span></span> |<span data-ttu-id="d4198-320">Object \*</span><span class="sxs-lookup"><span data-stu-id="d4198-320">Object \*</span></span> |
| <span data-ttu-id="d4198-321">text</span><span class="sxs-lookup"><span data-stu-id="d4198-321">text</span></span> |<span data-ttu-id="d4198-322">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-322">String, Char[]</span></span> |
| <span data-ttu-id="d4198-323">time</span><span class="sxs-lookup"><span data-stu-id="d4198-323">time</span></span> |<span data-ttu-id="d4198-324">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d4198-324">TimeSpan</span></span> |
| <span data-ttu-id="d4198-325">timestamp</span><span class="sxs-lookup"><span data-stu-id="d4198-325">timestamp</span></span> |<span data-ttu-id="d4198-326">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-326">Byte[]</span></span> |
| <span data-ttu-id="d4198-327">tinyint</span><span class="sxs-lookup"><span data-stu-id="d4198-327">tinyint</span></span> |<span data-ttu-id="d4198-328">Int16</span><span class="sxs-lookup"><span data-stu-id="d4198-328">Int16</span></span> |
| <span data-ttu-id="d4198-329">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="d4198-329">uniqueidentifier</span></span> |<span data-ttu-id="d4198-330">Guid</span><span class="sxs-lookup"><span data-stu-id="d4198-330">Guid</span></span> |
| <span data-ttu-id="d4198-331">varbinary</span><span class="sxs-lookup"><span data-stu-id="d4198-331">varbinary</span></span> |<span data-ttu-id="d4198-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4198-332">Byte[]</span></span> |
| <span data-ttu-id="d4198-333">varchar</span><span class="sxs-lookup"><span data-stu-id="d4198-333">varchar</span></span> |<span data-ttu-id="d4198-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4198-334">String, Char[]</span></span> |
| <span data-ttu-id="d4198-335">xml</span><span class="sxs-lookup"><span data-stu-id="d4198-335">xml</span></span> |<span data-ttu-id="d4198-336">Xml</span><span class="sxs-lookup"><span data-stu-id="d4198-336">Xml</span></span> |

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="d4198-337">Troubleshooting connection issues</span><span class="sxs-lookup"><span data-stu-id="d4198-337">Troubleshooting connection issues</span></span>

1. <span data-ttu-id="d4198-338">Configure your SQL Server to accept remote connections.</span><span class="sxs-lookup"><span data-stu-id="d4198-338">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="d4198-339">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d4198-339">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="d4198-340">Select **Connections** from the list and check **Allow remote connections to the server**.</span><span class="sxs-lookup"><span data-stu-id="d4198-340">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Enable remote connections](media/copy-data-to-from-sql-server/AllowRemoteConnections.png)

    <span data-ttu-id="d4198-342">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="d4198-342">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>

2. <span data-ttu-id="d4198-343">Launch **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="d4198-343">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="d4198-344">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="d4198-344">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="d4198-345">You should see protocols in the right-pane.</span><span class="sxs-lookup"><span data-stu-id="d4198-345">You should see protocols in the right-pane.</span></span> <span data-ttu-id="d4198-346">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span><span class="sxs-lookup"><span data-stu-id="d4198-346">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Enable TCP/IP](./media/copy-data-to-from-sql-server/EnableTCPProptocol.png)

    <span data-ttu-id="d4198-348">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span><span class="sxs-lookup"><span data-stu-id="d4198-348">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>

3. <span data-ttu-id="d4198-349">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span><span class="sxs-lookup"><span data-stu-id="d4198-349">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="d4198-350">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span><span class="sxs-lookup"><span data-stu-id="d4198-350">Switch to the **IP Addresses** tab. Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="d4198-351">Note down the \*\*TCP Port \*\*(default is **1433**).</span><span class="sxs-lookup"><span data-stu-id="d4198-351">Note down the \*\*TCP Port \*\*(default is **1433**).</span></span>
5. <span data-ttu-id="d4198-352">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span><span class="sxs-lookup"><span data-stu-id="d4198-352">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="d4198-353">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span><span class="sxs-lookup"><span data-stu-id="d4198-353">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="d4198-354">For example: `"<machine>.<domain>.corp.<company>.com,1433"`.</span><span class="sxs-lookup"><span data-stu-id="d4198-354">For example: `"<machine>.<domain>.corp.<company>.com,1433"`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d4198-355">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4198-355">Next steps</span></span>
<span data-ttu-id="d4198-356">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d4198-356">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
