## <a name="repeatability-during-copy"></a><span data-ttu-id="93452-101">Repeatability during Copy</span><span class="sxs-lookup"><span data-stu-id="93452-101">Repeatability during Copy</span></span>
<span data-ttu-id="93452-102">When copying data from and to relational stores, you need to keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="93452-102">When copying data from and to relational stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="93452-103">A slice can be rerun automatically in Azure Data Factory as per the retry policy specified.</span><span class="sxs-lookup"><span data-stu-id="93452-103">A slice can be rerun automatically in Azure Data Factory as per the retry policy specified.</span></span> <span data-ttu-id="93452-104">We recommend that you set a retry policy to guard against transient failures.</span><span class="sxs-lookup"><span data-stu-id="93452-104">We recommend that you set a retry policy to guard against transient failures.</span></span> <span data-ttu-id="93452-105">Hence repeatability is an important aspect to take care of during data movement.</span><span class="sxs-lookup"><span data-stu-id="93452-105">Hence repeatability is an important aspect to take care of during data movement.</span></span> 

<span data-ttu-id="93452-106">**As a source:**</span><span class="sxs-lookup"><span data-stu-id="93452-106">**As a source:**</span></span>

> [!NOTE]
> <span data-ttu-id="93452-107">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span><span class="sxs-lookup"><span data-stu-id="93452-107">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="93452-108">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span><span class="sxs-lookup"><span data-stu-id="93452-108">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   
> 
> 

<span data-ttu-id="93452-109">Usually, when reading from relational stores, you would want to read only the data corresponding to that slice.</span><span class="sxs-lookup"><span data-stu-id="93452-109">Usually, when reading from relational stores, you would want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="93452-110">A way to do so would be by using the WindowStart and WindowEnd variables available in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="93452-110">A way to do so would be by using the WindowStart and WindowEnd variables available in Azure Data Factory.</span></span> <span data-ttu-id="93452-111">Read about the variables and functions in Azure Data Factory here in the [Scheduling and Execution](../articles/data-factory/data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="93452-111">Read about the variables and functions in Azure Data Factory here in the [Scheduling and Execution](../articles/data-factory/data-factory-scheduling-and-execution.md) article.</span></span> <span data-ttu-id="93452-112">Example:</span><span class="sxs-lookup"><span data-stu-id="93452-112">Example:</span></span> 

```json
"source": {
"type": "SqlSource",
"sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="93452-113">This query reads data from ‘MyTable’ that falls in the slice duration range.</span><span class="sxs-lookup"><span data-stu-id="93452-113">This query reads data from ‘MyTable’ that falls in the slice duration range.</span></span> <span data-ttu-id="93452-114">Rerun of this slice would also always ensure this behavior.</span><span class="sxs-lookup"><span data-stu-id="93452-114">Rerun of this slice would also always ensure this behavior.</span></span> 

<span data-ttu-id="93452-115">In other cases, you may wish to read the entire Table (suppose for one time move only) and may define the sqlReaderQuery as follows:</span><span class="sxs-lookup"><span data-stu-id="93452-115">In other cases, you may wish to read the entire Table (suppose for one time move only) and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```
