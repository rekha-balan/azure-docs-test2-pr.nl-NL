### <a name="type-conversion-sample"></a><span data-ttu-id="9d933-101">Type conversion sample</span><span class="sxs-lookup"><span data-stu-id="9d933-101">Type conversion sample</span></span>
<span data-ttu-id="9d933-102">The following sample is for copying data from a Blob to Azure SQL with type conversions.</span><span class="sxs-lookup"><span data-stu-id="9d933-102">The following sample is for copying data from a Blob to Azure SQL with type conversions.</span></span>

<span data-ttu-id="9d933-103">Suppose the Blob dataset is in CSV format and contains 3 columns.</span><span class="sxs-lookup"><span data-stu-id="9d933-103">Suppose the Blob dataset is in CSV format and contains 3 columns.</span></span> <span data-ttu-id="9d933-104">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span><span class="sxs-lookup"><span data-stu-id="9d933-104">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="9d933-105">You will define the Blob Source dataset as follows along with type definitions for the columns.</span><span class="sxs-lookup"><span data-stu-id="9d933-105">You will define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```json
{
    "name": "AzureBlobTypeSystemInput",
    "properties":
    {
         "structure": 
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
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
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        },
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
<span data-ttu-id="9d933-106">Given the SQL type to .NET type mapping table above you would define the Azure SQL table with the following schema.</span><span class="sxs-lookup"><span data-stu-id="9d933-106">Given the SQL type to .NET type mapping table above you would define the Azure SQL table with the following schema.</span></span>

| <span data-ttu-id="9d933-107">Column Name</span><span class="sxs-lookup"><span data-stu-id="9d933-107">Column Name</span></span> | <span data-ttu-id="9d933-108">SQL Type</span><span class="sxs-lookup"><span data-stu-id="9d933-108">SQL Type</span></span> |
| --- | --- |
| <span data-ttu-id="9d933-109">userid</span><span class="sxs-lookup"><span data-stu-id="9d933-109">userid</span></span> |<span data-ttu-id="9d933-110">bigint</span><span class="sxs-lookup"><span data-stu-id="9d933-110">bigint</span></span> |
| <span data-ttu-id="9d933-111">name</span><span class="sxs-lookup"><span data-stu-id="9d933-111">name</span></span> |<span data-ttu-id="9d933-112">text</span><span class="sxs-lookup"><span data-stu-id="9d933-112">text</span></span> |
| <span data-ttu-id="9d933-113">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="9d933-113">lastlogindate</span></span> |<span data-ttu-id="9d933-114">datetime</span><span class="sxs-lookup"><span data-stu-id="9d933-114">datetime</span></span> |

<span data-ttu-id="9d933-115">Next you will define the Azure SQL dataset as follows.</span><span class="sxs-lookup"><span data-stu-id="9d933-115">Next you will define the Azure SQL dataset as follows.</span></span> 

> [!NOTE]
> <span data-ttu-id="9d933-116">You do not need to specify the **structure** section with type information as the type information is already specified in the underlying data store.</span><span class="sxs-lookup"><span data-stu-id="9d933-116">You do not need to specify the **structure** section with type information as the type information is already specified in the underlying data store.</span></span>

```json
{
    "name": "AzureSQLOutput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9d933-117">In this case data factory will automatically do the type conversions including the Datetime field with the custom datetime format using the fr-fr culture when moving data from Blob to Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9d933-117">In this case data factory will automatically do the type conversions including the Datetime field with the custom datetime format using the fr-fr culture when moving data from Blob to Azure SQL.</span></span>

