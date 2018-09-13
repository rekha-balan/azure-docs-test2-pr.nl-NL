## <a name="create-client"></a><span data-ttu-id="406e6-101">Create a client connection</span><span class="sxs-lookup"><span data-stu-id="406e6-101">Create a client connection</span></span>
<span data-ttu-id="406e6-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span><span class="sxs-lookup"><span data-stu-id="406e6-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="406e6-103">Replace `appUrl` with the URL to your Mobile App.</span><span class="sxs-lookup"><span data-stu-id="406e6-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a><span data-ttu-id="406e6-104">Work with tables</span><span class="sxs-lookup"><span data-stu-id="406e6-104">Work with tables</span></span>
<span data-ttu-id="406e6-105">To access or update data, create a reference to the backend table.</span><span class="sxs-lookup"><span data-stu-id="406e6-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="406e6-106">Replace `tableName` with the name of your table</span><span class="sxs-lookup"><span data-stu-id="406e6-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="406e6-107">Once you have a table reference, you can work further with your table:</span><span class="sxs-lookup"><span data-stu-id="406e6-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="406e6-108">Query a Table</span><span class="sxs-lookup"><span data-stu-id="406e6-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="406e6-109">Filtering Data</span><span class="sxs-lookup"><span data-stu-id="406e6-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="406e6-110">Paging through Data</span><span class="sxs-lookup"><span data-stu-id="406e6-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="406e6-111">Sorting Data</span><span class="sxs-lookup"><span data-stu-id="406e6-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="406e6-112">Inserting Data</span><span class="sxs-lookup"><span data-stu-id="406e6-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="406e6-113">Modifying Data</span><span class="sxs-lookup"><span data-stu-id="406e6-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="406e6-114">Deleting Data</span><span class="sxs-lookup"><span data-stu-id="406e6-114">Deleting Data</span></span>](#deleting)

### <a name="querying"></a><span data-ttu-id="406e6-115">How to: Query a table reference</span><span class="sxs-lookup"><span data-stu-id="406e6-115">How to: Query a table reference</span></span>
<span data-ttu-id="406e6-116">Once you have a table reference, you can use it to query for data on the server.</span><span class="sxs-lookup"><span data-stu-id="406e6-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="406e6-117">Queries are made in a "LINQ-like" language.</span><span class="sxs-lookup"><span data-stu-id="406e6-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="406e6-118">To return all data from the table, use the following code:</span><span class="sxs-lookup"><span data-stu-id="406e6-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="406e6-119">The success function is called with the results.</span><span class="sxs-lookup"><span data-stu-id="406e6-119">The success function is called with the results.</span></span>  <span data-ttu-id="406e6-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span><span class="sxs-lookup"><span data-stu-id="406e6-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="406e6-121">For more information on the Query syntax, see the [Query object documentation].</span><span class="sxs-lookup"><span data-stu-id="406e6-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <a name="table-filter"></a><span data-ttu-id="406e6-122">Filtering data on the server</span><span class="sxs-lookup"><span data-stu-id="406e6-122">Filtering data on the server</span></span>
<span data-ttu-id="406e6-123">You can use a `where` clause on the table reference:</span><span class="sxs-lookup"><span data-stu-id="406e6-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="406e6-124">You can also use a function that filters the object.</span><span class="sxs-lookup"><span data-stu-id="406e6-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="406e6-125">In this case, the `this` variable is assigned to the current object being filtered.</span><span class="sxs-lookup"><span data-stu-id="406e6-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="406e6-126">The following code is functionally equivalent to the prior example:</span><span class="sxs-lookup"><span data-stu-id="406e6-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a><span data-ttu-id="406e6-127">Paging through data</span><span class="sxs-lookup"><span data-stu-id="406e6-127">Paging through data</span></span>
<span data-ttu-id="406e6-128">Utilize the `take()` and `skip()` methods.</span><span class="sxs-lookup"><span data-stu-id="406e6-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="406e6-129">For example, if you wish to split the table into 100-row records:</span><span class="sxs-lookup"><span data-stu-id="406e6-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="406e6-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span><span class="sxs-lookup"><span data-stu-id="406e6-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="406e6-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span><span class="sxs-lookup"><span data-stu-id="406e6-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="406e6-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span><span class="sxs-lookup"><span data-stu-id="406e6-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="406e6-133">Implement caching to speed access to records that have already been loaded.</span><span class="sxs-lookup"><span data-stu-id="406e6-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <a name="sorting-data"></a><span data-ttu-id="406e6-134">How to: Return sorted data</span><span class="sxs-lookup"><span data-stu-id="406e6-134">How to: Return sorted data</span></span>
<span data-ttu-id="406e6-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span><span class="sxs-lookup"><span data-stu-id="406e6-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="406e6-136">For more information on the Query object, see the [Query object documentation].</span><span class="sxs-lookup"><span data-stu-id="406e6-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <a name="inserting"></a><span data-ttu-id="406e6-137">How to: Insert data</span><span class="sxs-lookup"><span data-stu-id="406e6-137">How to: Insert data</span></span>
<span data-ttu-id="406e6-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span><span class="sxs-lookup"><span data-stu-id="406e6-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="406e6-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span><span class="sxs-lookup"><span data-stu-id="406e6-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="406e6-140">Update your own cache with this information for later updates.</span><span class="sxs-lookup"><span data-stu-id="406e6-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="406e6-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span><span class="sxs-lookup"><span data-stu-id="406e6-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="406e6-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span><span class="sxs-lookup"><span data-stu-id="406e6-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="406e6-143">We recommend that you turn off dynamic schema before moving your application to production.</span><span class="sxs-lookup"><span data-stu-id="406e6-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <a name="modifying"></a><span data-ttu-id="406e6-144">How to: Modify data</span><span class="sxs-lookup"><span data-stu-id="406e6-144">How to: Modify data</span></span>
<span data-ttu-id="406e6-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span><span class="sxs-lookup"><span data-stu-id="406e6-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="406e6-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="406e6-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a><span data-ttu-id="406e6-147">How to: Delete data</span><span class="sxs-lookup"><span data-stu-id="406e6-147">How to: Delete data</span></span>
<span data-ttu-id="406e6-148">To delete a record, call the `.del()` method.</span><span class="sxs-lookup"><span data-stu-id="406e6-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="406e6-149">Pass the ID in an object reference:</span><span class="sxs-lookup"><span data-stu-id="406e6-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
