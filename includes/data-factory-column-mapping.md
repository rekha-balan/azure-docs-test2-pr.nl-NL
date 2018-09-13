## <a name="column-mapping-with-translator-rules"></a><span data-ttu-id="ecf19-101">Column mapping with translator rules</span><span class="sxs-lookup"><span data-stu-id="ecf19-101">Column mapping with translator rules</span></span>
<span data-ttu-id="ecf19-102">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span><span class="sxs-lookup"><span data-stu-id="ecf19-102">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="ecf19-103">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="ecf19-103">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="ecf19-104">Column mapping supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="ecf19-104">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="ecf19-105">All columns in the source table “structure” are mapped to all columns in the sink table “structure”.</span><span class="sxs-lookup"><span data-stu-id="ecf19-105">All columns in the source table “structure” are mapped to all columns in the sink table “structure”.</span></span>
* <span data-ttu-id="ecf19-106">A subset of the columns in the source table “structure” are mapped to all columns in the sink table “structure”.</span><span class="sxs-lookup"><span data-stu-id="ecf19-106">A subset of the columns in the source table “structure” are mapped to all columns in the sink table “structure”.</span></span>

<span data-ttu-id="ecf19-107">The following are error conditions and will result in an exception:</span><span class="sxs-lookup"><span data-stu-id="ecf19-107">The following are error conditions and will result in an exception:</span></span>

* <span data-ttu-id="ecf19-108">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span><span class="sxs-lookup"><span data-stu-id="ecf19-108">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="ecf19-109">Duplicate mapping.</span><span class="sxs-lookup"><span data-stu-id="ecf19-109">Duplicate mapping.</span></span>
* <span data-ttu-id="ecf19-110">SQL query result does not have a column name that is specified in the mapping.</span><span class="sxs-lookup"><span data-stu-id="ecf19-110">SQL query result does not have a column name that is specified in the mapping.</span></span>

## <a name="column-mapping-samples"></a><span data-ttu-id="ecf19-111">Column mapping samples</span><span class="sxs-lookup"><span data-stu-id="ecf19-111">Column mapping samples</span></span>
> [!NOTE]
> <span data-ttu-id="ecf19-112">The samples below are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span><span class="sxs-lookup"><span data-stu-id="ecf19-112">The samples below are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="ecf19-113">You will have to adjust dataset and linked service definitions in examples below to point to data in the relevant data source.</span><span class="sxs-lookup"><span data-stu-id="ecf19-113">You will have to adjust dataset and linked service definitions in examples below to point to data in the relevant data source.</span></span> 
> 
> 

### <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="ecf19-114">Sample 1 – column mapping from Azure SQL to Azure blob</span><span class="sxs-lookup"><span data-stu-id="ecf19-114">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="ecf19-115">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ecf19-115">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="ecf19-116">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ecf19-116">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="ecf19-117">The JSON for the activity is shown below.</span><span class="sxs-lookup"><span data-stu-id="ecf19-117">The JSON for the activity is shown below.</span></span> <span data-ttu-id="ecf19-118">The columns from source mapped to columns in sink (**columnMappings**) by using **Translator** property.</span><span class="sxs-lookup"><span data-stu-id="ecf19-118">The columns from source mapped to columns in sink (**columnMappings**) by using **Translator** property.</span></span>

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="ecf19-119">**Column mapping flow:**</span><span class="sxs-lookup"><span data-stu-id="ecf19-119">**Column mapping flow:**</span></span>

![Column mapping flow](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/data-factory-data-stores-with-rectangular-tables/column-mapping-flow.png)

### <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="ecf19-121">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span><span class="sxs-lookup"><span data-stu-id="ecf19-121">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="ecf19-122">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span><span class="sxs-lookup"><span data-stu-id="ecf19-122">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="ecf19-123">In this case, the query results are first mapped to columns specified in “structure” of source.</span><span class="sxs-lookup"><span data-stu-id="ecf19-123">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="ecf19-124">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span><span class="sxs-lookup"><span data-stu-id="ecf19-124">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="ecf19-125">Suppose the query returns 5 columns, two additional columns then those specified in the “structure” of source.</span><span class="sxs-lookup"><span data-stu-id="ecf19-125">Suppose the query returns 5 columns, two additional columns then those specified in the “structure” of source.</span></span>

<span data-ttu-id="ecf19-126">**Column mapping flow**</span><span class="sxs-lookup"><span data-stu-id="ecf19-126">**Column mapping flow**</span></span>

![Column mapping flow-2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/data-factory-data-stores-with-rectangular-tables/column-mapping-flow-2.png)



