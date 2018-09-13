<!--created by Robin Shahan to go in the articles for table storage w/powershell.
    There is one for Azure Table Storage and one for Azure Cosmos DB Table API -->

## <a name="managing-table-entities"></a><span data-ttu-id="fcbac-101">Managing table entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-101">Managing table entities</span></span>

<span data-ttu-id="fcbac-102">Now that you have a table, let's look at how to manage entities, or rows, in the table.</span><span class="sxs-lookup"><span data-stu-id="fcbac-102">Now that you have a table, let's look at how to manage entities, or rows, in the table.</span></span> 

<span data-ttu-id="fcbac-103">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-103">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="fcbac-104">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-104">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="fcbac-105">The server manages the value of **Timestamp**, which cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="fcbac-105">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="fcbac-106">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span><span class="sxs-lookup"><span data-stu-id="fcbac-106">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="fcbac-107">**PartitionKey**: Determines the partition that the entity is stored in.</span><span class="sxs-lookup"><span data-stu-id="fcbac-107">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="fcbac-108">**RowKey**: Uniquely identifies the entity within the partition.</span><span class="sxs-lookup"><span data-stu-id="fcbac-108">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="fcbac-109">You may define up to 252 custom properties for an entity.</span><span class="sxs-lookup"><span data-stu-id="fcbac-109">You may define up to 252 custom properties for an entity.</span></span> 

### <a name="add-table-entities"></a><span data-ttu-id="fcbac-110">Add table entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-110">Add table entities</span></span>

<span data-ttu-id="fcbac-111">Add entities to a table using **Add-StorageTableRow**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-111">Add entities to a table using **Add-StorageTableRow**.</span></span> <span data-ttu-id="fcbac-112">These examples use partition keys with values "partition1" and "partition2", and row keys equal to state abbreviations.</span><span class="sxs-lookup"><span data-stu-id="fcbac-112">These examples use partition keys with values "partition1" and "partition2", and row keys equal to state abbreviations.</span></span> <span data-ttu-id="fcbac-113">The properties in each entity are username and userid.</span><span class="sxs-lookup"><span data-stu-id="fcbac-113">The properties in each entity are username and userid.</span></span> 

```powershell
$partitionKey1 = "partition1"
$partitionKey2 = "partition2"

# add four rows 
Add-StorageTableRow `
    -table $storageTable `
    -partitionKey $partitionKey1 `
    -rowKey ("CA") -property @{"username"="Chris";"userid"=1}

Add-StorageTableRow `
    -table $storageTable `
    -partitionKey $partitionKey2 `
    -rowKey ("NM") -property @{"username"="Jessie";"userid"=2}

Add-StorageTableRow `
    -table $storageTable `
    -partitionKey $partitionKey1 `
    -rowKey ("WA") -property @{"username"="Christine";"userid"=3}

Add-StorageTableRow `
    -table $storageTable `
    -partitionKey $partitionKey2 `
    -rowKey ("TX") -property @{"username"="Steven";"userid"=4}
```

### <a name="query-the-table-entities"></a><span data-ttu-id="fcbac-114">Query the table entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-114">Query the table entities</span></span>

<span data-ttu-id="fcbac-115">There are several different ways to query the entities in a table.</span><span class="sxs-lookup"><span data-stu-id="fcbac-115">There are several different ways to query the entities in a table.</span></span>

#### <a name="retrieve-all-entities"></a><span data-ttu-id="fcbac-116">Retrieve all entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-116">Retrieve all entities</span></span>

<span data-ttu-id="fcbac-117">To retrieve all entities, use **Get-AzureStorageTableRowAll**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-117">To retrieve all entities, use **Get-AzureStorageTableRowAll**.</span></span>

```powershell
Get-AzureStorageTableRowAll -table $storageTable | ft
```

<span data-ttu-id="fcbac-118">This command yields results similar to the following table:</span><span class="sxs-lookup"><span data-stu-id="fcbac-118">This command yields results similar to the following table:</span></span>

| <span data-ttu-id="fcbac-119">userid</span><span class="sxs-lookup"><span data-stu-id="fcbac-119">userid</span></span> | <span data-ttu-id="fcbac-120">username</span><span class="sxs-lookup"><span data-stu-id="fcbac-120">username</span></span> | <span data-ttu-id="fcbac-121">partition</span><span class="sxs-lookup"><span data-stu-id="fcbac-121">partition</span></span> | <span data-ttu-id="fcbac-122">rowkey</span><span class="sxs-lookup"><span data-stu-id="fcbac-122">rowkey</span></span> |
|----|---------|---------------|----|
| <span data-ttu-id="fcbac-123">1</span><span class="sxs-lookup"><span data-stu-id="fcbac-123">1</span></span> | <span data-ttu-id="fcbac-124">Chris</span><span class="sxs-lookup"><span data-stu-id="fcbac-124">Chris</span></span> | <span data-ttu-id="fcbac-125">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-125">partition1</span></span> | <span data-ttu-id="fcbac-126">CA</span><span class="sxs-lookup"><span data-stu-id="fcbac-126">CA</span></span> |
| <span data-ttu-id="fcbac-127">3</span><span class="sxs-lookup"><span data-stu-id="fcbac-127">3</span></span> | <span data-ttu-id="fcbac-128">Christine</span><span class="sxs-lookup"><span data-stu-id="fcbac-128">Christine</span></span> | <span data-ttu-id="fcbac-129">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-129">partition1</span></span> | <span data-ttu-id="fcbac-130">WA</span><span class="sxs-lookup"><span data-stu-id="fcbac-130">WA</span></span> |
| <span data-ttu-id="fcbac-131">2</span><span class="sxs-lookup"><span data-stu-id="fcbac-131">2</span></span> | <span data-ttu-id="fcbac-132">Jessie</span><span class="sxs-lookup"><span data-stu-id="fcbac-132">Jessie</span></span> | <span data-ttu-id="fcbac-133">partition2</span><span class="sxs-lookup"><span data-stu-id="fcbac-133">partition2</span></span> | <span data-ttu-id="fcbac-134">NM</span><span class="sxs-lookup"><span data-stu-id="fcbac-134">NM</span></span> |
| <span data-ttu-id="fcbac-135">4</span><span class="sxs-lookup"><span data-stu-id="fcbac-135">4</span></span> | <span data-ttu-id="fcbac-136">Steven</span><span class="sxs-lookup"><span data-stu-id="fcbac-136">Steven</span></span> | <span data-ttu-id="fcbac-137">partition2</span><span class="sxs-lookup"><span data-stu-id="fcbac-137">partition2</span></span> | <span data-ttu-id="fcbac-138">TX</span><span class="sxs-lookup"><span data-stu-id="fcbac-138">TX</span></span> |

#### <a name="retrieve-entities-for-a-specific-partition"></a><span data-ttu-id="fcbac-139">Retrieve entities for a specific partition</span><span class="sxs-lookup"><span data-stu-id="fcbac-139">Retrieve entities for a specific partition</span></span>

<span data-ttu-id="fcbac-140">To retrieve all entities in a specific partition, use **Get-AzureStorageTableRowByPartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-140">To retrieve all entities in a specific partition, use **Get-AzureStorageTableRowByPartitionKey**.</span></span>

```powershell
Get-AzureStorageTableRowByPartitionKey -table $storageTable -partitionKey $partitionKey1 | ft
```
<span data-ttu-id="fcbac-141">The results look similar to the following table:</span><span class="sxs-lookup"><span data-stu-id="fcbac-141">The results look similar to the following table:</span></span>

| <span data-ttu-id="fcbac-142">userid</span><span class="sxs-lookup"><span data-stu-id="fcbac-142">userid</span></span> | <span data-ttu-id="fcbac-143">username</span><span class="sxs-lookup"><span data-stu-id="fcbac-143">username</span></span> | <span data-ttu-id="fcbac-144">partition</span><span class="sxs-lookup"><span data-stu-id="fcbac-144">partition</span></span> | <span data-ttu-id="fcbac-145">rowkey</span><span class="sxs-lookup"><span data-stu-id="fcbac-145">rowkey</span></span> |
|----|---------|---------------|----|
| <span data-ttu-id="fcbac-146">1</span><span class="sxs-lookup"><span data-stu-id="fcbac-146">1</span></span> | <span data-ttu-id="fcbac-147">Chris</span><span class="sxs-lookup"><span data-stu-id="fcbac-147">Chris</span></span> | <span data-ttu-id="fcbac-148">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-148">partition1</span></span> | <span data-ttu-id="fcbac-149">CA</span><span class="sxs-lookup"><span data-stu-id="fcbac-149">CA</span></span> |
| <span data-ttu-id="fcbac-150">3</span><span class="sxs-lookup"><span data-stu-id="fcbac-150">3</span></span> | <span data-ttu-id="fcbac-151">Christine</span><span class="sxs-lookup"><span data-stu-id="fcbac-151">Christine</span></span> | <span data-ttu-id="fcbac-152">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-152">partition1</span></span> | <span data-ttu-id="fcbac-153">WA</span><span class="sxs-lookup"><span data-stu-id="fcbac-153">WA</span></span> |

#### <a name="retrieve-entities-for-a-specific-value-in-a-specific-column"></a><span data-ttu-id="fcbac-154">Retrieve entities for a specific value in a specific column</span><span class="sxs-lookup"><span data-stu-id="fcbac-154">Retrieve entities for a specific value in a specific column</span></span>

<span data-ttu-id="fcbac-155">To retrieve entities where the value in a specific column equals a particular value, use **Get-AzureStorageTableRowByColumnName**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-155">To retrieve entities where the value in a specific column equals a particular value, use **Get-AzureStorageTableRowByColumnName**.</span></span>

```powershell
Get-AzureStorageTableRowByColumnName -table $storageTable `
    -columnName "username" `
    -value "Chris" `
    -operator Equal
```

<span data-ttu-id="fcbac-156">This query retrieves one record.</span><span class="sxs-lookup"><span data-stu-id="fcbac-156">This query retrieves one record.</span></span>

|<span data-ttu-id="fcbac-157">field</span><span class="sxs-lookup"><span data-stu-id="fcbac-157">field</span></span>|<span data-ttu-id="fcbac-158">value</span><span class="sxs-lookup"><span data-stu-id="fcbac-158">value</span></span>|
|----|----|
| <span data-ttu-id="fcbac-159">userid</span><span class="sxs-lookup"><span data-stu-id="fcbac-159">userid</span></span> | <span data-ttu-id="fcbac-160">1</span><span class="sxs-lookup"><span data-stu-id="fcbac-160">1</span></span> |
| <span data-ttu-id="fcbac-161">username</span><span class="sxs-lookup"><span data-stu-id="fcbac-161">username</span></span> | <span data-ttu-id="fcbac-162">Chris</span><span class="sxs-lookup"><span data-stu-id="fcbac-162">Chris</span></span> |
| <span data-ttu-id="fcbac-163">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-163">PartitionKey</span></span> | <span data-ttu-id="fcbac-164">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-164">partition1</span></span> |
| <span data-ttu-id="fcbac-165">RowKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-165">RowKey</span></span>      | <span data-ttu-id="fcbac-166">CA</span><span class="sxs-lookup"><span data-stu-id="fcbac-166">CA</span></span> |

#### <a name="retrieve-entities-using-a-custom-filter"></a><span data-ttu-id="fcbac-167">Retrieve entities using a custom filter</span><span class="sxs-lookup"><span data-stu-id="fcbac-167">Retrieve entities using a custom filter</span></span> 

<span data-ttu-id="fcbac-168">To retrieve entities using a custom filter, use **Get-AzureStorageTableRowByCustomFilter**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-168">To retrieve entities using a custom filter, use **Get-AzureStorageTableRowByCustomFilter**.</span></span>

```powershell
Get-AzureStorageTableRowByCustomFilter `
    -table $storageTable `
    -customFilter "(userid eq 1)"
```

<span data-ttu-id="fcbac-169">This query retrieves one record.</span><span class="sxs-lookup"><span data-stu-id="fcbac-169">This query retrieves one record.</span></span>

|<span data-ttu-id="fcbac-170">field</span><span class="sxs-lookup"><span data-stu-id="fcbac-170">field</span></span>|<span data-ttu-id="fcbac-171">value</span><span class="sxs-lookup"><span data-stu-id="fcbac-171">value</span></span>|
|----|----|
| <span data-ttu-id="fcbac-172">userid</span><span class="sxs-lookup"><span data-stu-id="fcbac-172">userid</span></span> | <span data-ttu-id="fcbac-173">1</span><span class="sxs-lookup"><span data-stu-id="fcbac-173">1</span></span> |
| <span data-ttu-id="fcbac-174">username</span><span class="sxs-lookup"><span data-stu-id="fcbac-174">username</span></span> | <span data-ttu-id="fcbac-175">Chris</span><span class="sxs-lookup"><span data-stu-id="fcbac-175">Chris</span></span> |
| <span data-ttu-id="fcbac-176">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-176">PartitionKey</span></span> | <span data-ttu-id="fcbac-177">partition1</span><span class="sxs-lookup"><span data-stu-id="fcbac-177">partition1</span></span> |
| <span data-ttu-id="fcbac-178">RowKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-178">RowKey</span></span>      | <span data-ttu-id="fcbac-179">CA</span><span class="sxs-lookup"><span data-stu-id="fcbac-179">CA</span></span> |

### <a name="updating-entities"></a><span data-ttu-id="fcbac-180">Updating entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-180">Updating entities</span></span> 

<span data-ttu-id="fcbac-181">There are three steps for updating entities.</span><span class="sxs-lookup"><span data-stu-id="fcbac-181">There are three steps for updating entities.</span></span> <span data-ttu-id="fcbac-182">First, retrieve the entity to change.</span><span class="sxs-lookup"><span data-stu-id="fcbac-182">First, retrieve the entity to change.</span></span> <span data-ttu-id="fcbac-183">Second, make the change.</span><span class="sxs-lookup"><span data-stu-id="fcbac-183">Second, make the change.</span></span> <span data-ttu-id="fcbac-184">Third, commit the change using **Update-AzureStorageTableRow**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-184">Third, commit the change using **Update-AzureStorageTableRow**.</span></span>

<span data-ttu-id="fcbac-185">Update the entity with username = 'Jessie' to have username = 'Jessie2'.</span><span class="sxs-lookup"><span data-stu-id="fcbac-185">Update the entity with username = 'Jessie' to have username = 'Jessie2'.</span></span> <span data-ttu-id="fcbac-186">This example also shows another way to create a custom filter using .NET types.</span><span class="sxs-lookup"><span data-stu-id="fcbac-186">This example also shows another way to create a custom filter using .NET types.</span></span> 

```powershell
# Create a filter and get the entity to be updated.
[string]$filter = `
    [Microsoft.WindowsAzure.Storage.Table.TableQuery]::GenerateFilterCondition("username",`
    [Microsoft.WindowsAzure.Storage.Table.QueryComparisons]::Equal,"Jessie")
$user = Get-AzureStorageTableRowByCustomFilter `
    -table $storageTable `
    -customFilter $filter

# Change the entity.
$user.username = "Jessie2" 

# To commit the change, pipe the updated record into the update cmdlet.
$user | Update-AzureStorageTableRow -table $storageTable 

# To see the new record, query the table.
Get-AzureStorageTableRowByCustomFilter -table $storageTable `
    -customFilter "(username eq 'Jessie2')"
```

<span data-ttu-id="fcbac-187">The results show the Jessie2 record.</span><span class="sxs-lookup"><span data-stu-id="fcbac-187">The results show the Jessie2 record.</span></span>

|<span data-ttu-id="fcbac-188">field</span><span class="sxs-lookup"><span data-stu-id="fcbac-188">field</span></span>|<span data-ttu-id="fcbac-189">value</span><span class="sxs-lookup"><span data-stu-id="fcbac-189">value</span></span>|
|----|----|
| <span data-ttu-id="fcbac-190">userid</span><span class="sxs-lookup"><span data-stu-id="fcbac-190">userid</span></span> | <span data-ttu-id="fcbac-191">2</span><span class="sxs-lookup"><span data-stu-id="fcbac-191">2</span></span> |
| <span data-ttu-id="fcbac-192">username</span><span class="sxs-lookup"><span data-stu-id="fcbac-192">username</span></span> | <span data-ttu-id="fcbac-193">Jessie2</span><span class="sxs-lookup"><span data-stu-id="fcbac-193">Jessie2</span></span> |
| <span data-ttu-id="fcbac-194">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-194">PartitionKey</span></span> | <span data-ttu-id="fcbac-195">partition2</span><span class="sxs-lookup"><span data-stu-id="fcbac-195">partition2</span></span> |
| <span data-ttu-id="fcbac-196">RowKey</span><span class="sxs-lookup"><span data-stu-id="fcbac-196">RowKey</span></span>      | <span data-ttu-id="fcbac-197">NM</span><span class="sxs-lookup"><span data-stu-id="fcbac-197">NM</span></span> |

### <a name="deleting-table-entities"></a><span data-ttu-id="fcbac-198">Deleting table entities</span><span class="sxs-lookup"><span data-stu-id="fcbac-198">Deleting table entities</span></span>

<span data-ttu-id="fcbac-199">You can delete one entity or all entities in the table.</span><span class="sxs-lookup"><span data-stu-id="fcbac-199">You can delete one entity or all entities in the table.</span></span>

#### <a name="deleting-one-entity"></a><span data-ttu-id="fcbac-200">Deleting one entity</span><span class="sxs-lookup"><span data-stu-id="fcbac-200">Deleting one entity</span></span>

<span data-ttu-id="fcbac-201">To delete a single entity, get a reference to that entity and pipe it into **Remove-AzureStorageTableRow**.</span><span class="sxs-lookup"><span data-stu-id="fcbac-201">To delete a single entity, get a reference to that entity and pipe it into **Remove-AzureStorageTableRow**.</span></span>

```powershell
# Set filter.
[string]$filter = `
  [Microsoft.WindowsAzure.Storage.Table.TableQuery]::GenerateFilterCondition("username",`
  [Microsoft.WindowsAzure.Storage.Table.QueryComparisons]::Equal,"Jessie2")

# Retrieve entity to be deleted, then pipe it into the remove cmdlet.
$userToDelete = Get-AzureStorageTableRowByCustomFilter `
    -table $storageTable `
    -customFilter $filter
$userToDelete | Remove-AzureStorageTableRow -table $storageTable 

# Retrieve entities from table and see that Jessie2 has been deleted.
Get-AzureStorageTableRowAll -table $storageTable | ft
```

#### <a name="delete-all-entities-in-the-table"></a><span data-ttu-id="fcbac-202">Delete all entities in the table</span><span class="sxs-lookup"><span data-stu-id="fcbac-202">Delete all entities in the table</span></span> 

<span data-ttu-id="fcbac-203">To delete all entities in the table, you retrieve them and pipe the results into the remove cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fcbac-203">To delete all entities in the table, you retrieve them and pipe the results into the remove cmdlet.</span></span> 

```powershell
# Get all rows and pipe the result into the remove cmdlet.
Get-AzureStorageTableRowAll `
    -table $storageTable | Remove-AzureStorageTableRow -table $storageTable 

# List entities in the table (there won't be any).
Get-AzureStorageTableRowAll -table $storageTable | ft
```
