## <a name="specifying-structure-definition-for-rectangular-datasets"></a><span data-ttu-id="33b9b-101">Specifying structure definition for rectangular datasets</span><span class="sxs-lookup"><span data-stu-id="33b9b-101">Specifying structure definition for rectangular datasets</span></span>
<span data-ttu-id="33b9b-102">The structure section in the datasets JSON is an **optional** section for rectangular tables (with rows & columns) and contains a collection of columns for the table.</span><span class="sxs-lookup"><span data-stu-id="33b9b-102">The structure section in the datasets JSON is an **optional** section for rectangular tables (with rows & columns) and contains a collection of columns for the table.</span></span> <span data-ttu-id="33b9b-103">You will use the structure section for either providing type information for type conversions or doing column mappings.</span><span class="sxs-lookup"><span data-stu-id="33b9b-103">You will use the structure section for either providing type information for type conversions or doing column mappings.</span></span> <span data-ttu-id="33b9b-104">The following sections describe these features in detail.</span><span class="sxs-lookup"><span data-stu-id="33b9b-104">The following sections describe these features in detail.</span></span> 

<span data-ttu-id="33b9b-105">Each column contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="33b9b-105">Each column contains the following properties:</span></span>

| <span data-ttu-id="33b9b-106">Property</span><span class="sxs-lookup"><span data-stu-id="33b9b-106">Property</span></span> | <span data-ttu-id="33b9b-107">Description</span><span class="sxs-lookup"><span data-stu-id="33b9b-107">Description</span></span> | <span data-ttu-id="33b9b-108">Required</span><span class="sxs-lookup"><span data-stu-id="33b9b-108">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33b9b-109">name</span><span class="sxs-lookup"><span data-stu-id="33b9b-109">name</span></span> |<span data-ttu-id="33b9b-110">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="33b9b-110">Name of the column.</span></span> |<span data-ttu-id="33b9b-111">Yes</span><span class="sxs-lookup"><span data-stu-id="33b9b-111">Yes</span></span> |
| <span data-ttu-id="33b9b-112">type</span><span class="sxs-lookup"><span data-stu-id="33b9b-112">type</span></span> |<span data-ttu-id="33b9b-113">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="33b9b-113">Data type of the column.</span></span> <span data-ttu-id="33b9b-114">See type conversions section below for more details regarding when should you specify type information</span><span class="sxs-lookup"><span data-stu-id="33b9b-114">See type conversions section below for more details regarding when should you specify type information</span></span> |<span data-ttu-id="33b9b-115">No</span><span class="sxs-lookup"><span data-stu-id="33b9b-115">No</span></span> |
| <span data-ttu-id="33b9b-116">culture</span><span class="sxs-lookup"><span data-stu-id="33b9b-116">culture</span></span> |<span data-ttu-id="33b9b-117">.NET based culture to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span><span class="sxs-lookup"><span data-stu-id="33b9b-117">.NET based culture to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> <span data-ttu-id="33b9b-118">Default is “en-us”.</span><span class="sxs-lookup"><span data-stu-id="33b9b-118">Default is “en-us”.</span></span> |<span data-ttu-id="33b9b-119">No</span><span class="sxs-lookup"><span data-stu-id="33b9b-119">No</span></span> |
| <span data-ttu-id="33b9b-120">format</span><span class="sxs-lookup"><span data-stu-id="33b9b-120">format</span></span> |<span data-ttu-id="33b9b-121">Format string to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span><span class="sxs-lookup"><span data-stu-id="33b9b-121">Format string to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> |<span data-ttu-id="33b9b-122">No</span><span class="sxs-lookup"><span data-stu-id="33b9b-122">No</span></span> |

<span data-ttu-id="33b9b-123">The following sample shows the structure section JSON for a table that has three columns userid, name, and lastlogindate.</span><span class="sxs-lookup"><span data-stu-id="33b9b-123">The following sample shows the structure section JSON for a table that has three columns userid, name, and lastlogindate.</span></span>

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

<span data-ttu-id="33b9b-124">Please use the following guidelines for when to include “structure” information and what to include in the **structure** section.</span><span class="sxs-lookup"><span data-stu-id="33b9b-124">Please use the following guidelines for when to include “structure” information and what to include in the **structure** section.</span></span>

* <span data-ttu-id="33b9b-125">**For structured data sources** that store data schema and type information along with the data itself (sources like SQL Server, Oracle, Azure table etc.), you should specify the “structure” section only if you want do column mapping of specific source columns to specific columns in sink and their names are not the same (see details in column mapping section below).</span><span class="sxs-lookup"><span data-stu-id="33b9b-125">**For structured data sources** that store data schema and type information along with the data itself (sources like SQL Server, Oracle, Azure table etc.), you should specify the “structure” section only if you want do column mapping of specific source columns to specific columns in sink and their names are not the same (see details in column mapping section below).</span></span> 
  
    <span data-ttu-id="33b9b-126">As mentioned above, the type information is optional in “structure” section.</span><span class="sxs-lookup"><span data-stu-id="33b9b-126">As mentioned above, the type information is optional in “structure” section.</span></span> <span data-ttu-id="33b9b-127">For structured sources, type information is already available as part of dataset definition in the data store, so you should not include type information when you do include the “structure” section.</span><span class="sxs-lookup"><span data-stu-id="33b9b-127">For structured sources, type information is already available as part of dataset definition in the data store, so you should not include type information when you do include the “structure” section.</span></span>
* <span data-ttu-id="33b9b-128">**For schema on read data sources (specifically Azure blob)**  you can choose to store data without storing any schema or type information with the data.</span><span class="sxs-lookup"><span data-stu-id="33b9b-128">**For schema on read data sources (specifically Azure blob)**  you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="33b9b-129">For these types of data sources you should include “structure” in the following 2 cases:</span><span class="sxs-lookup"><span data-stu-id="33b9b-129">For these types of data sources you should include “structure” in the following 2 cases:</span></span>
  * <span data-ttu-id="33b9b-130">You want to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="33b9b-130">You want to do column mapping.</span></span>
  * <span data-ttu-id="33b9b-131">When the dataset is a source in a Copy activity, you can provide type information in “structure” and data factory will use this type information for conversion to native types for the sink.</span><span class="sxs-lookup"><span data-stu-id="33b9b-131">When the dataset is a source in a Copy activity, you can provide type information in “structure” and data factory will use this type information for conversion to native types for the sink.</span></span> <span data-ttu-id="33b9b-132">See [Move data to and from Azure Blob](../articles/data-factory/data-factory-azure-blob-connector.md) article for more information.</span><span class="sxs-lookup"><span data-stu-id="33b9b-132">See [Move data to and from Azure Blob](../articles/data-factory/data-factory-azure-blob-connector.md) article for more information.</span></span>

### <a name="supported-net-based-types"></a><span data-ttu-id="33b9b-133">Supported .NET-based types</span><span class="sxs-lookup"><span data-stu-id="33b9b-133">Supported .NET-based types</span></span>
<span data-ttu-id="33b9b-134">Data factory supports the following CLS compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob.</span><span class="sxs-lookup"><span data-stu-id="33b9b-134">Data factory supports the following CLS compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob.</span></span>

* <span data-ttu-id="33b9b-135">Int16</span><span class="sxs-lookup"><span data-stu-id="33b9b-135">Int16</span></span>
* <span data-ttu-id="33b9b-136">Int32</span><span class="sxs-lookup"><span data-stu-id="33b9b-136">Int32</span></span> 
* <span data-ttu-id="33b9b-137">Int64</span><span class="sxs-lookup"><span data-stu-id="33b9b-137">Int64</span></span>
* <span data-ttu-id="33b9b-138">Single</span><span class="sxs-lookup"><span data-stu-id="33b9b-138">Single</span></span>
* <span data-ttu-id="33b9b-139">Double</span><span class="sxs-lookup"><span data-stu-id="33b9b-139">Double</span></span>
* <span data-ttu-id="33b9b-140">Decimal</span><span class="sxs-lookup"><span data-stu-id="33b9b-140">Decimal</span></span>
* <span data-ttu-id="33b9b-141">Byte[]</span><span class="sxs-lookup"><span data-stu-id="33b9b-141">Byte[]</span></span>
* <span data-ttu-id="33b9b-142">Bool</span><span class="sxs-lookup"><span data-stu-id="33b9b-142">Bool</span></span>
* <span data-ttu-id="33b9b-143">String</span><span class="sxs-lookup"><span data-stu-id="33b9b-143">String</span></span> 
* <span data-ttu-id="33b9b-144">Guid</span><span class="sxs-lookup"><span data-stu-id="33b9b-144">Guid</span></span>
* <span data-ttu-id="33b9b-145">Datetime</span><span class="sxs-lookup"><span data-stu-id="33b9b-145">Datetime</span></span>
* <span data-ttu-id="33b9b-146">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="33b9b-146">Datetimeoffset</span></span>
* <span data-ttu-id="33b9b-147">Timespan</span><span class="sxs-lookup"><span data-stu-id="33b9b-147">Timespan</span></span> 

<span data-ttu-id="33b9b-148">For Datetime & Datetimeoffset you can also optionally specify “culture” & “format” string to facilitate parsing of your custom Datetime string.</span><span class="sxs-lookup"><span data-stu-id="33b9b-148">For Datetime & Datetimeoffset you can also optionally specify “culture” & “format” string to facilitate parsing of your custom Datetime string.</span></span> <span data-ttu-id="33b9b-149">See sample for type conversion below.</span><span class="sxs-lookup"><span data-stu-id="33b9b-149">See sample for type conversion below.</span></span>
