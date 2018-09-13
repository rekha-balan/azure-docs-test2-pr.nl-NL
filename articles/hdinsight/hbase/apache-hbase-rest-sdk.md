---
title: Use the HBase .NET SDK - Azure HDInsight
description: Use the HBase .NET SDK to create and delete tables, and to read and write data.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 12/13/2017
ms.author: ashishth
ms.openlocfilehash: af3b87fbe79624143b6c2b7e0a3c50852e532524
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865032"
---
# <a name="use-the-hbase-net-sdk"></a><span data-ttu-id="a9d99-103">Use the HBase .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a9d99-103">Use the HBase .NET SDK</span></span>

<span data-ttu-id="a9d99-104">[HBase](apache-hbase-overview.md) provides two primary choices to work with your data: [Hive queries, and calls to HBase's RESTful API](apache-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a9d99-104">[HBase](apache-hbase-overview.md) provides two primary choices to work with your data: [Hive queries, and calls to HBase's RESTful API](apache-hbase-tutorial-get-started-linux.md).</span></span> <span data-ttu-id="a9d99-105">You can work directly with the REST API using the `curl` command or a similar utility.</span><span class="sxs-lookup"><span data-stu-id="a9d99-105">You can work directly with the REST API using the `curl` command or a similar utility.</span></span>

<span data-ttu-id="a9d99-106">For C# and .NET applications, the [Microsoft HBase REST Client Library for .NET](https://www.nuget.org/packages/Microsoft.HBase.Client/) provides a client library on top of the HBase REST API.</span><span class="sxs-lookup"><span data-stu-id="a9d99-106">For C# and .NET applications, the [Microsoft HBase REST Client Library for .NET](https://www.nuget.org/packages/Microsoft.HBase.Client/) provides a client library on top of the HBase REST API.</span></span>

## <a name="install-the-sdk"></a><span data-ttu-id="a9d99-107">Install the SDK</span><span class="sxs-lookup"><span data-stu-id="a9d99-107">Install the SDK</span></span>

<span data-ttu-id="a9d99-108">The HBase .NET SDK is provided as a NuGet package, which can be installed from the Visual Studio **NuGet Package Manager Console** with the following command:</span><span class="sxs-lookup"><span data-stu-id="a9d99-108">The HBase .NET SDK is provided as a NuGet package, which can be installed from the Visual Studio **NuGet Package Manager Console** with the following command:</span></span>

    Install-Package Microsoft.HBase.Client

## <a name="instantiate-a-new-hbaseclient-object"></a><span data-ttu-id="a9d99-109">Instantiate a new HBaseClient object</span><span class="sxs-lookup"><span data-stu-id="a9d99-109">Instantiate a new HBaseClient object</span></span>

<span data-ttu-id="a9d99-110">To use the SDK, instantiate a new `HBaseClient` object, passing in `ClusterCredentials` composed of the `Uri` to your cluster, and the Hadoop user name and password.</span><span class="sxs-lookup"><span data-stu-id="a9d99-110">To use the SDK, instantiate a new `HBaseClient` object, passing in `ClusterCredentials` composed of the `Uri` to your cluster, and the Hadoop user name and password.</span></span>

```csharp
var credentials = new ClusterCredentials(new Uri("https://CLUSTERNAME.azurehdinsight.net"), "USERNAME", "PASSWORD");
client = new HBaseClient(credentials);
```

<span data-ttu-id="a9d99-111">Replace CLUSTERNAME with your HDInsight HBase cluster name, and USERNAME and PASSWORD with the Hadoop credentials specified on cluster creation.</span><span class="sxs-lookup"><span data-stu-id="a9d99-111">Replace CLUSTERNAME with your HDInsight HBase cluster name, and USERNAME and PASSWORD with the Hadoop credentials specified on cluster creation.</span></span> <span data-ttu-id="a9d99-112">The default Hadoop user name is **admin**.</span><span class="sxs-lookup"><span data-stu-id="a9d99-112">The default Hadoop user name is **admin**.</span></span>

## <a name="create-a-new-table"></a><span data-ttu-id="a9d99-113">Create a new table</span><span class="sxs-lookup"><span data-stu-id="a9d99-113">Create a new table</span></span>

<span data-ttu-id="a9d99-114">HBase stores data in tables.</span><span class="sxs-lookup"><span data-stu-id="a9d99-114">HBase stores data in tables.</span></span> <span data-ttu-id="a9d99-115">A table consists of a *Rowkey*, the primary key, and one or more groups of columns called *column families*.</span><span class="sxs-lookup"><span data-stu-id="a9d99-115">A table consists of a *Rowkey*, the primary key, and one or more groups of columns called *column families*.</span></span> <span data-ttu-id="a9d99-116">The data in each table is horizontally distributed by a Rowkey range into *regions*.</span><span class="sxs-lookup"><span data-stu-id="a9d99-116">The data in each table is horizontally distributed by a Rowkey range into *regions*.</span></span> <span data-ttu-id="a9d99-117">Each region has a start and end key.</span><span class="sxs-lookup"><span data-stu-id="a9d99-117">Each region has a start and end key.</span></span> <span data-ttu-id="a9d99-118">A table can have one or more regions.</span><span class="sxs-lookup"><span data-stu-id="a9d99-118">A table can have one or more regions.</span></span> <span data-ttu-id="a9d99-119">As the data in table grows, HBase splits large regions into smaller regions.</span><span class="sxs-lookup"><span data-stu-id="a9d99-119">As the data in table grows, HBase splits large regions into smaller regions.</span></span> <span data-ttu-id="a9d99-120">Regions are stored in *region servers*, where one region server can store multiple regions.</span><span class="sxs-lookup"><span data-stu-id="a9d99-120">Regions are stored in *region servers*, where one region server can store multiple regions.</span></span>

<span data-ttu-id="a9d99-121">The data is physically stored in *HFiles*.</span><span class="sxs-lookup"><span data-stu-id="a9d99-121">The data is physically stored in *HFiles*.</span></span> <span data-ttu-id="a9d99-122">A single HFile contains data for one table, one region, and one column family.</span><span class="sxs-lookup"><span data-stu-id="a9d99-122">A single HFile contains data for one table, one region, and one column family.</span></span> <span data-ttu-id="a9d99-123">Rows in HFile are stored sorted on Rowkey.</span><span class="sxs-lookup"><span data-stu-id="a9d99-123">Rows in HFile are stored sorted on Rowkey.</span></span> <span data-ttu-id="a9d99-124">Each HFile has a *B+ Tree* index for speedy retrieval of the rows.</span><span class="sxs-lookup"><span data-stu-id="a9d99-124">Each HFile has a *B+ Tree* index for speedy retrieval of the rows.</span></span>

<span data-ttu-id="a9d99-125">To create a new table, specify a `TableSchema` and columns.</span><span class="sxs-lookup"><span data-stu-id="a9d99-125">To create a new table, specify a `TableSchema` and columns.</span></span> <span data-ttu-id="a9d99-126">The following code checks whether the table 'RestSDKTable\` already exists - if not, the table is created.</span><span class="sxs-lookup"><span data-stu-id="a9d99-126">The following code checks whether the table 'RestSDKTable\` already exists - if not, the table is created.</span></span>

```csharp
if (!client.ListTablesAsync().Result.name.Contains("RestSDKTable"))
{
    // Create the table
    var newTableSchema = new TableSchema {name = "RestSDKTable" };
    newTableSchema.columns.Add(new ColumnSchema() {name = "t1"});
    newTableSchema.columns.Add(new ColumnSchema() {name = "t2"});

    await client.CreateTableAsync(newTableSchema);
}
```

<span data-ttu-id="a9d99-127">This new table has two column families, t1 and t2.</span><span class="sxs-lookup"><span data-stu-id="a9d99-127">This new table has two column families, t1 and t2.</span></span> <span data-ttu-id="a9d99-128">Since column families are stored separately in different HFiles, it makes sense to have a separate column family for frequently queried data.</span><span class="sxs-lookup"><span data-stu-id="a9d99-128">Since column families are stored separately in different HFiles, it makes sense to have a separate column family for frequently queried data.</span></span> <span data-ttu-id="a9d99-129">In the following [Insert data](#insert-data) example, columns are added to the t1 column family.</span><span class="sxs-lookup"><span data-stu-id="a9d99-129">In the following [Insert data](#insert-data) example, columns are added to the t1 column family.</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="a9d99-130">Delete a table</span><span class="sxs-lookup"><span data-stu-id="a9d99-130">Delete a table</span></span>

<span data-ttu-id="a9d99-131">To delete a table:</span><span class="sxs-lookup"><span data-stu-id="a9d99-131">To delete a table:</span></span>

```csharp
await client.DeleteTableAsync("RestSDKTable");
```

## <a name="insert-data"></a><span data-ttu-id="a9d99-132">Insert data</span><span class="sxs-lookup"><span data-stu-id="a9d99-132">Insert data</span></span>

<span data-ttu-id="a9d99-133">To insert data, you specify a unique row key as the row identifier.</span><span class="sxs-lookup"><span data-stu-id="a9d99-133">To insert data, you specify a unique row key as the row identifier.</span></span> <span data-ttu-id="a9d99-134">All data is stored in a `byte[]` array.</span><span class="sxs-lookup"><span data-stu-id="a9d99-134">All data is stored in a `byte[]` array.</span></span> <span data-ttu-id="a9d99-135">The following code defines and adds the `title`, `director`, and `release_date` columns to the t1 column family, as these columns are the most frequently accessed.</span><span class="sxs-lookup"><span data-stu-id="a9d99-135">The following code defines and adds the `title`, `director`, and `release_date` columns to the t1 column family, as these columns are the most frequently accessed.</span></span> <span data-ttu-id="a9d99-136">The `description` and `tagline` columns are added to the t2 column family.</span><span class="sxs-lookup"><span data-stu-id="a9d99-136">The `description` and `tagline` columns are added to the t2 column family.</span></span> <span data-ttu-id="a9d99-137">You can partition your data into column families as needed.</span><span class="sxs-lookup"><span data-stu-id="a9d99-137">You can partition your data into column families as needed.</span></span>

```csharp
var key = "fifth_element";
var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };
var value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:title"),
    data = Encoding.UTF8.GetBytes("The Fifth Element")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:director"),
    data = Encoding.UTF8.GetBytes("Luc Besson")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:release_date"),
    data = Encoding.UTF8.GetBytes("1997")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t2:description"),
    data = Encoding.UTF8.GetBytes("In the colorful future, a cab driver unwittingly becomes the central figure in the search for a legendary cosmic weapon to keep Evil and Mr Zorg at bay.")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t2:tagline"),
    data = Encoding.UTF8.GetBytes("The Fifth is life")
};
row.values.Add(value);

var set = new CellSet();
set.rows.Add(row);

await client.StoreCellsAsync("RestSDKTable", set);
```

<span data-ttu-id="a9d99-138">HBase implements BigTable, so the data format looks like the following:</span><span class="sxs-lookup"><span data-stu-id="a9d99-138">HBase implements BigTable, so the data format looks like the following:</span></span>

![User with Cluster User role](./media/apache-hbase-rest-sdk/table.png)

## <a name="select-data"></a><span data-ttu-id="a9d99-140">Select data</span><span class="sxs-lookup"><span data-stu-id="a9d99-140">Select data</span></span>

<span data-ttu-id="a9d99-141">To read data from an HBase table, pass the table name and row key to the `GetCellsAsync` method to return the `CellSet`.</span><span class="sxs-lookup"><span data-stu-id="a9d99-141">To read data from an HBase table, pass the table name and row key to the `GetCellsAsync` method to return the `CellSet`.</span></span>

```csharp
var key = "fifth_element";

var cells = await client.GetCellsAsync("RestSDKTable", key);
// Get the first value from the row.
Console.WriteLine(Encoding.UTF8.GetString(cells.rows[0].values[0].data));
// Get the value for t1:title
Console.WriteLine(Encoding.UTF8.GetString(cells.rows[0].values
    .Find(c => Encoding.UTF8.GetString(c.column) == "t1:title").data));
// With the previous insert, it should yield: "The Fifth Element"
```

<span data-ttu-id="a9d99-142">In this case, the code returns only the first matching row, as there should only be one row for a unique key.</span><span class="sxs-lookup"><span data-stu-id="a9d99-142">In this case, the code returns only the first matching row, as there should only be one row for a unique key.</span></span> <span data-ttu-id="a9d99-143">The returned value is changed into `string` format from the `byte[]` array.</span><span class="sxs-lookup"><span data-stu-id="a9d99-143">The returned value is changed into `string` format from the `byte[]` array.</span></span> <span data-ttu-id="a9d99-144">You can also convert the value to other types, such as an integer for the movie's release date:</span><span class="sxs-lookup"><span data-stu-id="a9d99-144">You can also convert the value to other types, such as an integer for the movie's release date:</span></span>

```csharp
var releaseDateField = cells.rows[0].values
    .Find(c => Encoding.UTF8.GetString(c.column) == "t1:release_date");
int releaseDate = 0;

if (releaseDateField != null)
{
    releaseDate = Convert.ToInt32(Encoding.UTF8.GetString(releaseDateField.data));
}
Console.WriteLine(releaseDate);
// Should return 1997
```

## <a name="scan-over-rows"></a><span data-ttu-id="a9d99-145">Scan over rows</span><span class="sxs-lookup"><span data-stu-id="a9d99-145">Scan over rows</span></span>

<span data-ttu-id="a9d99-146">HBase uses `scan` to retrieve one or more rows.</span><span class="sxs-lookup"><span data-stu-id="a9d99-146">HBase uses `scan` to retrieve one or more rows.</span></span> <span data-ttu-id="a9d99-147">This example requests multiple rows in batches of 10, and retrieves data whose key values are between 25 and 35.</span><span class="sxs-lookup"><span data-stu-id="a9d99-147">This example requests multiple rows in batches of 10, and retrieves data whose key values are between 25 and 35.</span></span> <span data-ttu-id="a9d99-148">After retrieving all rows, delete the scanner to clean up resources.</span><span class="sxs-lookup"><span data-stu-id="a9d99-148">After retrieving all rows, delete the scanner to clean up resources.</span></span>

```csharp
var tableName = "mytablename";

// Assume the table has integer keys and we want data between keys 25 and 35
var scanSettings = new Scanner()
{
    batch = 10,
    startRow = BitConverter.GetBytes(25),
    endRow = BitConverter.GetBytes(35)
};
RequestOptions scanOptions = RequestOptions.GetDefaultOptions();
scanOptions.AlternativeEndpoint = "hbaserest0/";
ScannerInformation scannerInfo = null;
try
{
    scannerInfo = await client.CreateScannerAsync(tableName, scanSettings, scanOptions);
    CellSet next = null;
    while ((next = client.ScannerGetNextAsync(scannerInfo, scanOptions).Result) != null)
    {
        foreach (var row in next.rows)
        {
            // ... read the rows
        }
    }
}
finally
{
    if (scannerInfo != null)
    {
        await client.DeleteScannerAsync(tableName, scannerInfo, scanOptions);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a9d99-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9d99-149">Next steps</span></span>

* [<span data-ttu-id="a9d99-150">Get started with an Apache HBase example in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9d99-150">Get started with an Apache HBase example in HDInsight</span></span>](apache-hbase-tutorial-get-started-linux.md)
* <span data-ttu-id="a9d99-151">Build an end-to-end application with [Analyze real-time Twitter sentiment with HBase](../hdinsight-hbase-analyze-twitter-sentiment.md)</span><span class="sxs-lookup"><span data-stu-id="a9d99-151">Build an end-to-end application with [Analyze real-time Twitter sentiment with HBase](../hdinsight-hbase-analyze-twitter-sentiment.md)</span></span>
