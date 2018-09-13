## <a name="repeatability-during-copy"></a><span data-ttu-id="53890-101">Repeatability during Copy</span><span class="sxs-lookup"><span data-stu-id="53890-101">Repeatability during Copy</span></span>
<span data-ttu-id="53890-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="53890-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="53890-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="53890-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="53890-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span><span class="sxs-lookup"><span data-stu-id="53890-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="53890-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span><span class="sxs-lookup"><span data-stu-id="53890-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="53890-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="53890-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="53890-107">The below assumes none of the columns in the table have the primary key constraint.</span><span class="sxs-lookup"><span data-stu-id="53890-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="53890-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span><span class="sxs-lookup"><span data-stu-id="53890-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="53890-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span><span class="sxs-lookup"><span data-stu-id="53890-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="53890-110">Mechanism 1</span><span class="sxs-lookup"><span data-stu-id="53890-110">Mechanism 1</span></span>
<span data-ttu-id="53890-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span><span class="sxs-lookup"><span data-stu-id="53890-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="53890-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span><span class="sxs-lookup"><span data-stu-id="53890-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="53890-113">The activity will subsequently insert the data into the SQL Table.</span><span class="sxs-lookup"><span data-stu-id="53890-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="53890-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span><span class="sxs-lookup"><span data-stu-id="53890-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="53890-115">Suppose the Flat Washer record is removed from the original csv.</span><span class="sxs-lookup"><span data-stu-id="53890-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="53890-116">Then re-running the slice would produce the following result:</span><span class="sxs-lookup"><span data-stu-id="53890-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="53890-117">Nothing new had to be done.</span><span class="sxs-lookup"><span data-stu-id="53890-117">Nothing new had to be done.</span></span> <span data-ttu-id="53890-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span><span class="sxs-lookup"><span data-stu-id="53890-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="53890-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span><span class="sxs-lookup"><span data-stu-id="53890-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="53890-120">Mechanism 2</span><span class="sxs-lookup"><span data-stu-id="53890-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="53890-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span><span class="sxs-lookup"><span data-stu-id="53890-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="53890-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span><span class="sxs-lookup"><span data-stu-id="53890-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="53890-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span><span class="sxs-lookup"><span data-stu-id="53890-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="53890-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span><span class="sxs-lookup"><span data-stu-id="53890-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="53890-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span><span class="sxs-lookup"><span data-stu-id="53890-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="53890-126">Way to use this approach:</span><span class="sxs-lookup"><span data-stu-id="53890-126">Way to use this approach:</span></span>

1. <span data-ttu-id="53890-127">Define a column of type binary (32) in the destination SQL Table.</span><span class="sxs-lookup"><span data-stu-id="53890-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="53890-128">There should be no constraints on this column.</span><span class="sxs-lookup"><span data-stu-id="53890-128">There should be no constraints on this column.</span></span> <span data-ttu-id="53890-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span><span class="sxs-lookup"><span data-stu-id="53890-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="53890-130">Use it in the copy activity as follows:</span><span class="sxs-lookup"><span data-stu-id="53890-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="53890-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span><span class="sxs-lookup"><span data-stu-id="53890-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="53890-132">The values of this column should not be used outside of this context by the user.</span><span class="sxs-lookup"><span data-stu-id="53890-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="53890-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span><span class="sxs-lookup"><span data-stu-id="53890-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

