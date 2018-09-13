---
title: Supported file formats in Azure Data Factory | Microsoft Docs
description: This topic describes the file formats and compression codes that are supported by file-based connectors in Azure Data Factory.
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: jingwang
ms.openlocfilehash: 844440d22bc0a524e9e61bde457ee9f43fd367b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870695"
---
# <a name="supported-file-formats-and-compression-codecs-in-azure-data-factory"></a><span data-ttu-id="e2e24-103">Supported file formats and compression codecs in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2e24-103">Supported file formats and compression codecs in Azure Data Factory</span></span>

<span data-ttu-id="e2e24-104">*This topic applies to the following connectors: [Amazon S3](connector-amazon-simple-storage-service.md), [Azure Blob](connector-azure-blob-storage.md), [Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md), [Azure Data Lake Storage Gen2](connector-azure-data-lake-storage.md), [Azure File Storage](connector-azure-file-storage.md), [File System](connector-file-system.md), [FTP](connector-ftp.md), [HDFS](connector-hdfs.md), [HTTP](connector-http.md), and [SFTP](connector-sftp.md).*</span><span class="sxs-lookup"><span data-stu-id="e2e24-104">*This topic applies to the following connectors: [Amazon S3](connector-amazon-simple-storage-service.md), [Azure Blob](connector-azure-blob-storage.md), [Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md), [Azure Data Lake Storage Gen2](connector-azure-data-lake-storage.md), [Azure File Storage](connector-azure-file-storage.md), [File System](connector-file-system.md), [FTP](connector-ftp.md), [HDFS](connector-hdfs.md), [HTTP](connector-http.md), and [SFTP](connector-sftp.md).*</span></span>

<span data-ttu-id="e2e24-105">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="e2e24-105">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> <span data-ttu-id="e2e24-106">If you want to **parse or generate files with a specific format**, Azure Data Factory supports the following file format types:</span><span class="sxs-lookup"><span data-stu-id="e2e24-106">If you want to **parse or generate files with a specific format**, Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="e2e24-107">Text format</span><span class="sxs-lookup"><span data-stu-id="e2e24-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="e2e24-108">JSON format</span><span class="sxs-lookup"><span data-stu-id="e2e24-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="e2e24-109">Avro format</span><span class="sxs-lookup"><span data-stu-id="e2e24-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="e2e24-110">ORC format</span><span class="sxs-lookup"><span data-stu-id="e2e24-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="e2e24-111">Parquet format</span><span class="sxs-lookup"><span data-stu-id="e2e24-111">Parquet format</span></span>](#parquet-format)

> [!TIP]
> <span data-ttu-id="e2e24-112">Learn how copy activity maps your source data to sink from [Schema mapping in copy activity](copy-activity-schema-and-type-mapping.md), including how the metadata is determined based on your file format settings and tips on when to specify the [dataset `structure`](concepts-datasets-linked-services.md#dataset-structure) section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-112">Learn how copy activity maps your source data to sink from [Schema mapping in copy activity](copy-activity-schema-and-type-mapping.md), including how the metadata is determined based on your file format settings and tips on when to specify the [dataset `structure`](concepts-datasets-linked-services.md#dataset-structure) section.</span></span>

## <a name="text-format"></a><span data-ttu-id="e2e24-113">Text format</span><span class="sxs-lookup"><span data-stu-id="e2e24-113">Text format</span></span>

<span data-ttu-id="e2e24-114">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-114">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="e2e24-115">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-115">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="e2e24-116">See [TextFormat example](#textformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="e2e24-116">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="e2e24-117">Property</span><span class="sxs-lookup"><span data-stu-id="e2e24-117">Property</span></span> | <span data-ttu-id="e2e24-118">Description</span><span class="sxs-lookup"><span data-stu-id="e2e24-118">Description</span></span> | <span data-ttu-id="e2e24-119">Allowed values</span><span class="sxs-lookup"><span data-stu-id="e2e24-119">Allowed values</span></span> | <span data-ttu-id="e2e24-120">Required</span><span class="sxs-lookup"><span data-stu-id="e2e24-120">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2e24-121">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="e2e24-121">columnDelimiter</span></span> |<span data-ttu-id="e2e24-122">The character used to separate columns in a file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-122">The character used to separate columns in a file.</span></span> <span data-ttu-id="e2e24-123">You can consider to use a rare unprintable character that may not  exist in your data.</span><span class="sxs-lookup"><span data-stu-id="e2e24-123">You can consider to use a rare unprintable character that may not  exist in your data.</span></span> <span data-ttu-id="e2e24-124">For example, specify "\u0001", which represents Start of Heading (SOH).</span><span class="sxs-lookup"><span data-stu-id="e2e24-124">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="e2e24-125">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="e2e24-125">Only one character is allowed.</span></span> <span data-ttu-id="e2e24-126">The **default** value is **comma (',')**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-126">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="e2e24-127">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span><span class="sxs-lookup"><span data-stu-id="e2e24-127">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="e2e24-128">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-128">No</span></span> |
| <span data-ttu-id="e2e24-129">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="e2e24-129">rowDelimiter</span></span> |<span data-ttu-id="e2e24-130">The character used to separate rows in a file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-130">The character used to separate rows in a file.</span></span> |<span data-ttu-id="e2e24-131">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="e2e24-131">Only one character is allowed.</span></span> <span data-ttu-id="e2e24-132">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span><span class="sxs-lookup"><span data-stu-id="e2e24-132">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="e2e24-133">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-133">No</span></span> |
| <span data-ttu-id="e2e24-134">escapeChar</span><span class="sxs-lookup"><span data-stu-id="e2e24-134">escapeChar</span></span> |<span data-ttu-id="e2e24-135">The special character used to escape a column delimiter in the content of input file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-135">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="e2e24-136">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="e2e24-136">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="e2e24-137">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="e2e24-137">Only one character is allowed.</span></span> <span data-ttu-id="e2e24-138">No default value.</span><span class="sxs-lookup"><span data-stu-id="e2e24-138">No default value.</span></span> <br/><br/><span data-ttu-id="e2e24-139">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="e2e24-139">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="e2e24-140">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-140">No</span></span> |
| <span data-ttu-id="e2e24-141">quoteChar</span><span class="sxs-lookup"><span data-stu-id="e2e24-141">quoteChar</span></span> |<span data-ttu-id="e2e24-142">The character used to quote a string value.</span><span class="sxs-lookup"><span data-stu-id="e2e24-142">The character used to quote a string value.</span></span> <span data-ttu-id="e2e24-143">The column and row delimiters inside the quote characters would be treated as part of the string value.</span><span class="sxs-lookup"><span data-stu-id="e2e24-143">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="e2e24-144">This property is applicable to both input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="e2e24-144">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="e2e24-145">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="e2e24-145">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="e2e24-146">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="e2e24-146">Only one character is allowed.</span></span> <span data-ttu-id="e2e24-147">No default value.</span><span class="sxs-lookup"><span data-stu-id="e2e24-147">No default value.</span></span> <br/><br/><span data-ttu-id="e2e24-148">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="e2e24-148">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="e2e24-149">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-149">No</span></span> |
| <span data-ttu-id="e2e24-150">nullValue</span><span class="sxs-lookup"><span data-stu-id="e2e24-150">nullValue</span></span> |<span data-ttu-id="e2e24-151">One or more characters used to represent a null value.</span><span class="sxs-lookup"><span data-stu-id="e2e24-151">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="e2e24-152">One or more characters.</span><span class="sxs-lookup"><span data-stu-id="e2e24-152">One or more characters.</span></span> <span data-ttu-id="e2e24-153">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span><span class="sxs-lookup"><span data-stu-id="e2e24-153">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="e2e24-154">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-154">No</span></span> |
| <span data-ttu-id="e2e24-155">encodingName</span><span class="sxs-lookup"><span data-stu-id="e2e24-155">encodingName</span></span> |<span data-ttu-id="e2e24-156">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="e2e24-156">Specify the encoding name.</span></span> |<span data-ttu-id="e2e24-157">A valid encoding name.</span><span class="sxs-lookup"><span data-stu-id="e2e24-157">A valid encoding name.</span></span> <span data-ttu-id="e2e24-158">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2e24-158">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="e2e24-159">Example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="e2e24-159">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="e2e24-160">The **default** value is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-160">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="e2e24-161">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-161">No</span></span> |
| <span data-ttu-id="e2e24-162">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="e2e24-162">firstRowAsHeader</span></span> |<span data-ttu-id="e2e24-163">Specifies whether to consider the first row as a header.</span><span class="sxs-lookup"><span data-stu-id="e2e24-163">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="e2e24-164">For an input dataset, Data Factory reads first row as a header.</span><span class="sxs-lookup"><span data-stu-id="e2e24-164">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="e2e24-165">For an output dataset, Data Factory writes first row as a header.</span><span class="sxs-lookup"><span data-stu-id="e2e24-165">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="e2e24-166">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="e2e24-166">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="e2e24-167">True</span><span class="sxs-lookup"><span data-stu-id="e2e24-167">True</span></span><br/><span data-ttu-id="e2e24-168"><b>False (default)</b></span><span class="sxs-lookup"><span data-stu-id="e2e24-168"><b>False (default)</b></span></span> |<span data-ttu-id="e2e24-169">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-169">No</span></span> |
| <span data-ttu-id="e2e24-170">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="e2e24-170">skipLineCount</span></span> |<span data-ttu-id="e2e24-171">Indicates the number of rows to skip when reading data from input files.</span><span class="sxs-lookup"><span data-stu-id="e2e24-171">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="e2e24-172">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-172">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="e2e24-173">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="e2e24-173">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="e2e24-174">Integer</span><span class="sxs-lookup"><span data-stu-id="e2e24-174">Integer</span></span> |<span data-ttu-id="e2e24-175">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-175">No</span></span> |
| <span data-ttu-id="e2e24-176">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="e2e24-176">treatEmptyAsNull</span></span> |<span data-ttu-id="e2e24-177">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-177">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="e2e24-178">**True (default)**</span><span class="sxs-lookup"><span data-stu-id="e2e24-178">**True (default)**</span></span><br/><span data-ttu-id="e2e24-179">False</span><span class="sxs-lookup"><span data-stu-id="e2e24-179">False</span></span> |<span data-ttu-id="e2e24-180">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-180">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="e2e24-181">TextFormat example</span><span class="sxs-lookup"><span data-stu-id="e2e24-181">TextFormat example</span></span>

<span data-ttu-id="e2e24-182">In the following JSON definition for a dataset, some of the optional properties are specified.</span><span class="sxs-lookup"><span data-stu-id="e2e24-182">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="e2e24-183">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span><span class="sxs-lookup"><span data-stu-id="e2e24-183">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="e2e24-184">Scenarios for using firstRowAsHeader and skipLineCount</span><span class="sxs-lookup"><span data-stu-id="e2e24-184">Scenarios for using firstRowAsHeader and skipLineCount</span></span>

* <span data-ttu-id="e2e24-185">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span><span class="sxs-lookup"><span data-stu-id="e2e24-185">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="e2e24-186">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span><span class="sxs-lookup"><span data-stu-id="e2e24-186">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="e2e24-187">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span><span class="sxs-lookup"><span data-stu-id="e2e24-187">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="e2e24-188">Specify `firstRowAsHeader` as true in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="e2e24-188">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="e2e24-189">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span><span class="sxs-lookup"><span data-stu-id="e2e24-189">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="e2e24-190">Specify `skipLineCount` to indicate the number of lines to be skipped.</span><span class="sxs-lookup"><span data-stu-id="e2e24-190">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="e2e24-191">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="e2e24-191">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="e2e24-192">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span><span class="sxs-lookup"><span data-stu-id="e2e24-192">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="e2e24-193">JSON format</span><span class="sxs-lookup"><span data-stu-id="e2e24-193">JSON format</span></span>

<span data-ttu-id="e2e24-194">To **import/export a JSON file as-is into/from Azure Cosmos DB**, see Import/export JSON documents section in [Move data to/from Azure Cosmos DB](connector-azure-cosmos-db.md) article.</span><span class="sxs-lookup"><span data-stu-id="e2e24-194">To **import/export a JSON file as-is into/from Azure Cosmos DB**, see Import/export JSON documents section in [Move data to/from Azure Cosmos DB](connector-azure-cosmos-db.md) article.</span></span>

<span data-ttu-id="e2e24-195">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-195">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="e2e24-196">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-196">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="e2e24-197">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="e2e24-197">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="e2e24-198">Property</span><span class="sxs-lookup"><span data-stu-id="e2e24-198">Property</span></span> | <span data-ttu-id="e2e24-199">Description</span><span class="sxs-lookup"><span data-stu-id="e2e24-199">Description</span></span> | <span data-ttu-id="e2e24-200">Required</span><span class="sxs-lookup"><span data-stu-id="e2e24-200">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2e24-201">filePattern</span><span class="sxs-lookup"><span data-stu-id="e2e24-201">filePattern</span></span> |<span data-ttu-id="e2e24-202">Indicate the pattern of data stored in each JSON file.</span><span class="sxs-lookup"><span data-stu-id="e2e24-202">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="e2e24-203">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-203">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="e2e24-204">The **default** value is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-204">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="e2e24-205">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span><span class="sxs-lookup"><span data-stu-id="e2e24-205">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="e2e24-206">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-206">No</span></span> |
| <span data-ttu-id="e2e24-207">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="e2e24-207">jsonNodeReference</span></span> | <span data-ttu-id="e2e24-208">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span><span class="sxs-lookup"><span data-stu-id="e2e24-208">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="e2e24-209">This property is supported only when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="e2e24-209">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="e2e24-210">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-210">No</span></span> |
| <span data-ttu-id="e2e24-211">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="e2e24-211">jsonPathDefinition</span></span> | <span data-ttu-id="e2e24-212">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span><span class="sxs-lookup"><span data-stu-id="e2e24-212">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="e2e24-213">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span><span class="sxs-lookup"><span data-stu-id="e2e24-213">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="e2e24-214">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span><span class="sxs-lookup"><span data-stu-id="e2e24-214">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="e2e24-215">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="e2e24-215">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="e2e24-216">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-216">No</span></span> |
| <span data-ttu-id="e2e24-217">encodingName</span><span class="sxs-lookup"><span data-stu-id="e2e24-217">encodingName</span></span> |<span data-ttu-id="e2e24-218">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="e2e24-218">Specify the encoding name.</span></span> <span data-ttu-id="e2e24-219">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span><span class="sxs-lookup"><span data-stu-id="e2e24-219">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="e2e24-220">For example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="e2e24-220">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="e2e24-221">The **default** value is: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-221">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="e2e24-222">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-222">No</span></span> |
| <span data-ttu-id="e2e24-223">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e2e24-223">nestingSeparator</span></span> |<span data-ttu-id="e2e24-224">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="e2e24-224">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="e2e24-225">The default value is '.' (dot).</span><span class="sxs-lookup"><span data-stu-id="e2e24-225">The default value is '.' (dot).</span></span> |<span data-ttu-id="e2e24-226">No</span><span class="sxs-lookup"><span data-stu-id="e2e24-226">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="e2e24-227">JSON file patterns</span><span class="sxs-lookup"><span data-stu-id="e2e24-227">JSON file patterns</span></span>

<span data-ttu-id="e2e24-228">Copy activity can parse the following patterns of JSON files:</span><span class="sxs-lookup"><span data-stu-id="e2e24-228">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="e2e24-229">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="e2e24-229">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="e2e24-230">Each file contains single object, or line-delimited/concatenated multiple objects.</span><span class="sxs-lookup"><span data-stu-id="e2e24-230">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="e2e24-231">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span><span class="sxs-lookup"><span data-stu-id="e2e24-231">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="e2e24-232">**single object JSON example**</span><span class="sxs-lookup"><span data-stu-id="e2e24-232">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="e2e24-233">**line-delimited JSON example**</span><span class="sxs-lookup"><span data-stu-id="e2e24-233">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="e2e24-234">**concatenated JSON example**</span><span class="sxs-lookup"><span data-stu-id="e2e24-234">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="e2e24-235">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="e2e24-235">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="e2e24-236">Each file contains an array of objects.</span><span class="sxs-lookup"><span data-stu-id="e2e24-236">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="e2e24-237">JsonFormat example</span><span class="sxs-lookup"><span data-stu-id="e2e24-237">JsonFormat example</span></span>

<span data-ttu-id="e2e24-238">**Case 1: Copying data from JSON files**</span><span class="sxs-lookup"><span data-stu-id="e2e24-238">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="e2e24-239">See the following two samples when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="e2e24-239">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="e2e24-240">The generic points to note:</span><span class="sxs-lookup"><span data-stu-id="e2e24-240">The generic points to note:</span></span>

<span data-ttu-id="e2e24-241">**Sample 1: extract data from object and array**</span><span class="sxs-lookup"><span data-stu-id="e2e24-241">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="e2e24-242">In this sample, you expect one root JSON object maps to single record in tabular result.</span><span class="sxs-lookup"><span data-stu-id="e2e24-242">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="e2e24-243">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="e2e24-243">If you have a JSON file with the following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```

<span data-ttu-id="e2e24-244">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span><span class="sxs-lookup"><span data-stu-id="e2e24-244">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="e2e24-245">ID</span><span class="sxs-lookup"><span data-stu-id="e2e24-245">ID</span></span> | <span data-ttu-id="e2e24-246">deviceType</span><span class="sxs-lookup"><span data-stu-id="e2e24-246">deviceType</span></span> | <span data-ttu-id="e2e24-247">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="e2e24-247">targetResourceType</span></span> | <span data-ttu-id="e2e24-248">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="e2e24-248">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="e2e24-249">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="e2e24-249">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e2e24-250">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="e2e24-250">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="e2e24-251">PC</span><span class="sxs-lookup"><span data-stu-id="e2e24-251">PC</span></span> | <span data-ttu-id="e2e24-252">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="e2e24-252">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="e2e24-253">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="e2e24-253">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="e2e24-254">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="e2e24-254">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="e2e24-255">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="e2e24-255">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="e2e24-256">More specifically:</span><span class="sxs-lookup"><span data-stu-id="e2e24-256">More specifically:</span></span>

- <span data-ttu-id="e2e24-257">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="e2e24-257">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="e2e24-258">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="e2e24-258">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="e2e24-259">For more information, see [Map source dataset columns to destination dataset columns](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="e2e24-259">For more information, see [Map source dataset columns to destination dataset columns](copy-activity-schema-and-type-mapping.md).</span></span>
- <span data-ttu-id="e2e24-260">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="e2e24-260">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="e2e24-261">To copy data from array, you can use `array[x].property` to extract value of the given property from the `xth` object, or you can use `array[*].property` to find the value from any object containing such property.</span><span class="sxs-lookup"><span data-stu-id="e2e24-261">To copy data from array, you can use `array[x].property` to extract value of the given property from the `xth` object, or you can use `array[*].property` to find the value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}
        }
    }
}
```

<span data-ttu-id="e2e24-262">**Sample 2: cross apply multiple objects with the same pattern from array**</span><span class="sxs-lookup"><span data-stu-id="e2e24-262">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="e2e24-263">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span><span class="sxs-lookup"><span data-stu-id="e2e24-263">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="e2e24-264">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="e2e24-264">If you have a JSON file with the following content:</span></span>

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```

<span data-ttu-id="e2e24-265">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span><span class="sxs-lookup"><span data-stu-id="e2e24-265">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| `ordernumber` | `orderdate` | `order_pd` | `order_price` | `city` |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e2e24-266">01</span><span class="sxs-lookup"><span data-stu-id="e2e24-266">01</span></span> | <span data-ttu-id="e2e24-267">20170122</span><span class="sxs-lookup"><span data-stu-id="e2e24-267">20170122</span></span> | <span data-ttu-id="e2e24-268">P1</span><span class="sxs-lookup"><span data-stu-id="e2e24-268">P1</span></span> | <span data-ttu-id="e2e24-269">23</span><span class="sxs-lookup"><span data-stu-id="e2e24-269">23</span></span> | `[{"sanmateo":"No 1"}]` |
| <span data-ttu-id="e2e24-270">01</span><span class="sxs-lookup"><span data-stu-id="e2e24-270">01</span></span> | <span data-ttu-id="e2e24-271">20170122</span><span class="sxs-lookup"><span data-stu-id="e2e24-271">20170122</span></span> | <span data-ttu-id="e2e24-272">P2</span><span class="sxs-lookup"><span data-stu-id="e2e24-272">P2</span></span> | <span data-ttu-id="e2e24-273">13</span><span class="sxs-lookup"><span data-stu-id="e2e24-273">13</span></span> | `[{"sanmateo":"No 1"}]` |
| <span data-ttu-id="e2e24-274">01</span><span class="sxs-lookup"><span data-stu-id="e2e24-274">01</span></span> | <span data-ttu-id="e2e24-275">20170122</span><span class="sxs-lookup"><span data-stu-id="e2e24-275">20170122</span></span> | <span data-ttu-id="e2e24-276">P3</span><span class="sxs-lookup"><span data-stu-id="e2e24-276">P3</span></span> | <span data-ttu-id="e2e24-277">231</span><span class="sxs-lookup"><span data-stu-id="e2e24-277">231</span></span> | `[{"sanmateo":"No 1"}]` |


<span data-ttu-id="e2e24-278">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="e2e24-278">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="e2e24-279">More specifically:</span><span class="sxs-lookup"><span data-stu-id="e2e24-279">More specifically:</span></span>

- <span data-ttu-id="e2e24-280">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="e2e24-280">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="e2e24-281">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="e2e24-281">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="e2e24-282">For more information, see [Map source dataset columns to destination dataset columns](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="e2e24-282">For more information, see [Map source dataset columns to destination dataset columns](copy-activity-schema-and-type-mapping.md).</span></span>
- <span data-ttu-id="e2e24-283">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** `orderlines`.</span><span class="sxs-lookup"><span data-stu-id="e2e24-283">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** `orderlines`.</span></span>
- <span data-ttu-id="e2e24-284">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="e2e24-284">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="e2e24-285">In this example, `ordernumber`, `orderdate`, and `city` are under root object with JSON path starting with `$.`, while `order_pd` and `order_price` are defined with path derived from the array element without `$.`.</span><span class="sxs-lookup"><span data-stu-id="e2e24-285">In this example, `ordernumber`, `orderdate`, and `city` are under root object with JSON path starting with `$.`, while `order_pd` and `order_price` are defined with path derived from the array element without `$.`.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}
        }
    }
}
```

<span data-ttu-id="e2e24-286">**Note the following points:**</span><span class="sxs-lookup"><span data-stu-id="e2e24-286">**Note the following points:**</span></span>

* <span data-ttu-id="e2e24-287">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span><span class="sxs-lookup"><span data-stu-id="e2e24-287">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="e2e24-288">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span><span class="sxs-lookup"><span data-stu-id="e2e24-288">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="e2e24-289">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="e2e24-289">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="e2e24-290">If there are duplicate names at the same level, the Copy Activity picks the last one.</span><span class="sxs-lookup"><span data-stu-id="e2e24-290">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="e2e24-291">Property names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e2e24-291">Property names are case-sensitive.</span></span> <span data-ttu-id="e2e24-292">Two properties with same name but different casings are treated as two separate properties.</span><span class="sxs-lookup"><span data-stu-id="e2e24-292">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="e2e24-293">**Case 2: Writing data to JSON file**</span><span class="sxs-lookup"><span data-stu-id="e2e24-293">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="e2e24-294">If you have the following table in SQL Database:</span><span class="sxs-lookup"><span data-stu-id="e2e24-294">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="e2e24-295">ID</span><span class="sxs-lookup"><span data-stu-id="e2e24-295">ID</span></span> | <span data-ttu-id="e2e24-296">order_date</span><span class="sxs-lookup"><span data-stu-id="e2e24-296">order_date</span></span> | <span data-ttu-id="e2e24-297">order_price</span><span class="sxs-lookup"><span data-stu-id="e2e24-297">order_price</span></span> | <span data-ttu-id="e2e24-298">order_by</span><span class="sxs-lookup"><span data-stu-id="e2e24-298">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2e24-299">1</span><span class="sxs-lookup"><span data-stu-id="e2e24-299">1</span></span> | <span data-ttu-id="e2e24-300">20170119</span><span class="sxs-lookup"><span data-stu-id="e2e24-300">20170119</span></span> | <span data-ttu-id="e2e24-301">2000</span><span class="sxs-lookup"><span data-stu-id="e2e24-301">2000</span></span> | <span data-ttu-id="e2e24-302">David</span><span class="sxs-lookup"><span data-stu-id="e2e24-302">David</span></span> |
| <span data-ttu-id="e2e24-303">2</span><span class="sxs-lookup"><span data-stu-id="e2e24-303">2</span></span> | <span data-ttu-id="e2e24-304">20170120</span><span class="sxs-lookup"><span data-stu-id="e2e24-304">20170120</span></span> | <span data-ttu-id="e2e24-305">3500</span><span class="sxs-lookup"><span data-stu-id="e2e24-305">3500</span></span> | <span data-ttu-id="e2e24-306">Patrick</span><span class="sxs-lookup"><span data-stu-id="e2e24-306">Patrick</span></span> |
| <span data-ttu-id="e2e24-307">3</span><span class="sxs-lookup"><span data-stu-id="e2e24-307">3</span></span> | <span data-ttu-id="e2e24-308">20170121</span><span class="sxs-lookup"><span data-stu-id="e2e24-308">20170121</span></span> | <span data-ttu-id="e2e24-309">4000</span><span class="sxs-lookup"><span data-stu-id="e2e24-309">4000</span></span> | <span data-ttu-id="e2e24-310">Jason</span><span class="sxs-lookup"><span data-stu-id="e2e24-310">Jason</span></span> |

<span data-ttu-id="e2e24-311">and for each record, you expect to write to a JSON object in the following format:</span><span class="sxs-lookup"><span data-stu-id="e2e24-311">and for each record, you expect to write to a JSON object in the following format:</span></span>

```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="e2e24-312">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="e2e24-312">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="e2e24-313">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span><span class="sxs-lookup"><span data-stu-id="e2e24-313">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="e2e24-314">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span><span class="sxs-lookup"><span data-stu-id="e2e24-314">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="e2e24-315">AVRO format</span><span class="sxs-lookup"><span data-stu-id="e2e24-315">AVRO format</span></span>

<span data-ttu-id="e2e24-316">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-316">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="e2e24-317">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-317">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="e2e24-318">Example:</span><span class="sxs-lookup"><span data-stu-id="e2e24-318">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="e2e24-319">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="e2e24-319">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="e2e24-320">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e2e24-320">Note the following points:</span></span>

* <span data-ttu-id="e2e24-321">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span><span class="sxs-lookup"><span data-stu-id="e2e24-321">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="e2e24-322">ORC format</span><span class="sxs-lookup"><span data-stu-id="e2e24-322">ORC format</span></span>

<span data-ttu-id="e2e24-323">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-323">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="e2e24-324">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="e2e24-325">Example:</span><span class="sxs-lookup"><span data-stu-id="e2e24-325">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="e2e24-326">For copy empowered by Self-hosted Integration Runtime e.g. between on-premises and cloud data stores, if you are not copying ORC files **as-is**, you need to install the JRE 8 (Java Runtime Environment) on your IR machine.</span><span class="sxs-lookup"><span data-stu-id="e2e24-326">For copy empowered by Self-hosted Integration Runtime e.g. between on-premises and cloud data stores, if you are not copying ORC files **as-is**, you need to install the JRE 8 (Java Runtime Environment) on your IR machine.</span></span> <span data-ttu-id="e2e24-327">A 64-bit IR requires 64-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="e2e24-327">A 64-bit IR requires 64-bit JRE.</span></span> <span data-ttu-id="e2e24-328">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="e2e24-328">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span>
>

<span data-ttu-id="e2e24-329">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e2e24-329">Note the following points:</span></span>

* <span data-ttu-id="e2e24-330">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="e2e24-330">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="e2e24-331">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="e2e24-331">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="e2e24-332">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="e2e24-332">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="e2e24-333">It uses the compression codec is in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="e2e24-333">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="e2e24-334">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span><span class="sxs-lookup"><span data-stu-id="e2e24-334">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="e2e24-335">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="e2e24-335">Currently, there is no option to override this behavior.</span></span>

### <a name="data-type-mapping-for-orc-files"></a><span data-ttu-id="e2e24-336">Data type mapping for ORC files</span><span class="sxs-lookup"><span data-stu-id="e2e24-336">Data type mapping for ORC files</span></span>

| <span data-ttu-id="e2e24-337">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="e2e24-337">Data factory interim data type</span></span> | <span data-ttu-id="e2e24-338">ORC types</span><span class="sxs-lookup"><span data-stu-id="e2e24-338">ORC types</span></span> |
|:--- |:--- |
| <span data-ttu-id="e2e24-339">Boolean</span><span class="sxs-lookup"><span data-stu-id="e2e24-339">Boolean</span></span> | <span data-ttu-id="e2e24-340">Boolean</span><span class="sxs-lookup"><span data-stu-id="e2e24-340">Boolean</span></span> |
| <span data-ttu-id="e2e24-341">SByte</span><span class="sxs-lookup"><span data-stu-id="e2e24-341">SByte</span></span> | <span data-ttu-id="e2e24-342">Byte</span><span class="sxs-lookup"><span data-stu-id="e2e24-342">Byte</span></span> |
| <span data-ttu-id="e2e24-343">Byte</span><span class="sxs-lookup"><span data-stu-id="e2e24-343">Byte</span></span> | <span data-ttu-id="e2e24-344">Short</span><span class="sxs-lookup"><span data-stu-id="e2e24-344">Short</span></span> |
| <span data-ttu-id="e2e24-345">Int16</span><span class="sxs-lookup"><span data-stu-id="e2e24-345">Int16</span></span> | <span data-ttu-id="e2e24-346">Short</span><span class="sxs-lookup"><span data-stu-id="e2e24-346">Short</span></span> |
| <span data-ttu-id="e2e24-347">UInt16</span><span class="sxs-lookup"><span data-stu-id="e2e24-347">UInt16</span></span> | <span data-ttu-id="e2e24-348">Int</span><span class="sxs-lookup"><span data-stu-id="e2e24-348">Int</span></span> |
| <span data-ttu-id="e2e24-349">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-349">Int32</span></span> | <span data-ttu-id="e2e24-350">Int</span><span class="sxs-lookup"><span data-stu-id="e2e24-350">Int</span></span> |
| <span data-ttu-id="e2e24-351">UInt32</span><span class="sxs-lookup"><span data-stu-id="e2e24-351">UInt32</span></span> | <span data-ttu-id="e2e24-352">Long</span><span class="sxs-lookup"><span data-stu-id="e2e24-352">Long</span></span> |
| <span data-ttu-id="e2e24-353">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-353">Int64</span></span> | <span data-ttu-id="e2e24-354">Long</span><span class="sxs-lookup"><span data-stu-id="e2e24-354">Long</span></span> |
| <span data-ttu-id="e2e24-355">UInt64</span><span class="sxs-lookup"><span data-stu-id="e2e24-355">UInt64</span></span> | <span data-ttu-id="e2e24-356">String</span><span class="sxs-lookup"><span data-stu-id="e2e24-356">String</span></span> |
| <span data-ttu-id="e2e24-357">Single</span><span class="sxs-lookup"><span data-stu-id="e2e24-357">Single</span></span> | <span data-ttu-id="e2e24-358">Float</span><span class="sxs-lookup"><span data-stu-id="e2e24-358">Float</span></span> |
| <span data-ttu-id="e2e24-359">Double</span><span class="sxs-lookup"><span data-stu-id="e2e24-359">Double</span></span> | <span data-ttu-id="e2e24-360">Double</span><span class="sxs-lookup"><span data-stu-id="e2e24-360">Double</span></span> |
| <span data-ttu-id="e2e24-361">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-361">Decimal</span></span> | <span data-ttu-id="e2e24-362">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-362">Decimal</span></span> |
| <span data-ttu-id="e2e24-363">String</span><span class="sxs-lookup"><span data-stu-id="e2e24-363">String</span></span> | <span data-ttu-id="e2e24-364">String</span><span class="sxs-lookup"><span data-stu-id="e2e24-364">String</span></span> |
| <span data-ttu-id="e2e24-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="e2e24-365">DateTime</span></span> | <span data-ttu-id="e2e24-366">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e2e24-366">Timestamp</span></span> |
| <span data-ttu-id="e2e24-367">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e2e24-367">DateTimeOffset</span></span> | <span data-ttu-id="e2e24-368">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e2e24-368">Timestamp</span></span> |
| <span data-ttu-id="e2e24-369">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e2e24-369">TimeSpan</span></span> | <span data-ttu-id="e2e24-370">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e2e24-370">Timestamp</span></span> |
| <span data-ttu-id="e2e24-371">ByteArray</span><span class="sxs-lookup"><span data-stu-id="e2e24-371">ByteArray</span></span> | <span data-ttu-id="e2e24-372">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-372">Binary</span></span> |
| <span data-ttu-id="e2e24-373">Guid</span><span class="sxs-lookup"><span data-stu-id="e2e24-373">Guid</span></span> | <span data-ttu-id="e2e24-374">String</span><span class="sxs-lookup"><span data-stu-id="e2e24-374">String</span></span> |
| <span data-ttu-id="e2e24-375">Char</span><span class="sxs-lookup"><span data-stu-id="e2e24-375">Char</span></span> | <span data-ttu-id="e2e24-376">Char(1)</span><span class="sxs-lookup"><span data-stu-id="e2e24-376">Char(1)</span></span> |

## <a name="parquet-format"></a><span data-ttu-id="e2e24-377">Parquet format</span><span class="sxs-lookup"><span data-stu-id="e2e24-377">Parquet format</span></span>

<span data-ttu-id="e2e24-378">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-378">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="e2e24-379">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="e2e24-379">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="e2e24-380">Example:</span><span class="sxs-lookup"><span data-stu-id="e2e24-380">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="e2e24-381">For copy empowered by Self-hosted Integration Runtime e.g. between on-premises and cloud data stores, if you are not copying Parquet files **as-is**, you need to install the JRE 8 (Java Runtime Environment) on your IR machine.</span><span class="sxs-lookup"><span data-stu-id="e2e24-381">For copy empowered by Self-hosted Integration Runtime e.g. between on-premises and cloud data stores, if you are not copying Parquet files **as-is**, you need to install the JRE 8 (Java Runtime Environment) on your IR machine.</span></span> <span data-ttu-id="e2e24-382">A 64-bit IR requires 64-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="e2e24-382">A 64-bit IR requires 64-bit JRE.</span></span> <span data-ttu-id="e2e24-383">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="e2e24-383">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span>
>

<span data-ttu-id="e2e24-384">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="e2e24-384">Note the following points:</span></span>

* <span data-ttu-id="e2e24-385">Complex data types are not supported (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="e2e24-385">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="e2e24-386">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span><span class="sxs-lookup"><span data-stu-id="e2e24-386">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="e2e24-387">Data Factory supports reading data from Parquet file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="e2e24-387">Data Factory supports reading data from Parquet file in any of these compressed formats.</span></span> <span data-ttu-id="e2e24-388">It uses the compression codec in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="e2e24-388">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="e2e24-389">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span><span class="sxs-lookup"><span data-stu-id="e2e24-389">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="e2e24-390">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="e2e24-390">Currently, there is no option to override this behavior.</span></span>

### <a name="data-type-mapping-for-parquet-files"></a><span data-ttu-id="e2e24-391">Data type mapping for Parquet files</span><span class="sxs-lookup"><span data-stu-id="e2e24-391">Data type mapping for Parquet files</span></span>

| <span data-ttu-id="e2e24-392">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="e2e24-392">Data factory interim data type</span></span> | <span data-ttu-id="e2e24-393">Parquet Primitive Type</span><span class="sxs-lookup"><span data-stu-id="e2e24-393">Parquet Primitive Type</span></span> | <span data-ttu-id="e2e24-394">Parquet Original Type (Deserialize)</span><span class="sxs-lookup"><span data-stu-id="e2e24-394">Parquet Original Type (Deserialize)</span></span> | <span data-ttu-id="e2e24-395">Parquet Original Type (Serialize)</span><span class="sxs-lookup"><span data-stu-id="e2e24-395">Parquet Original Type (Serialize)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e2e24-396">Boolean</span><span class="sxs-lookup"><span data-stu-id="e2e24-396">Boolean</span></span> | <span data-ttu-id="e2e24-397">Boolean</span><span class="sxs-lookup"><span data-stu-id="e2e24-397">Boolean</span></span> | <span data-ttu-id="e2e24-398">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-398">N/A</span></span> | <span data-ttu-id="e2e24-399">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-399">N/A</span></span> |
| <span data-ttu-id="e2e24-400">SByte</span><span class="sxs-lookup"><span data-stu-id="e2e24-400">SByte</span></span> | <span data-ttu-id="e2e24-401">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-401">Int32</span></span> | <span data-ttu-id="e2e24-402">Int8</span><span class="sxs-lookup"><span data-stu-id="e2e24-402">Int8</span></span> | <span data-ttu-id="e2e24-403">Int8</span><span class="sxs-lookup"><span data-stu-id="e2e24-403">Int8</span></span> |
| <span data-ttu-id="e2e24-404">Byte</span><span class="sxs-lookup"><span data-stu-id="e2e24-404">Byte</span></span> | <span data-ttu-id="e2e24-405">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-405">Int32</span></span> | <span data-ttu-id="e2e24-406">UInt8</span><span class="sxs-lookup"><span data-stu-id="e2e24-406">UInt8</span></span> | <span data-ttu-id="e2e24-407">Int16</span><span class="sxs-lookup"><span data-stu-id="e2e24-407">Int16</span></span> |
| <span data-ttu-id="e2e24-408">Int16</span><span class="sxs-lookup"><span data-stu-id="e2e24-408">Int16</span></span> | <span data-ttu-id="e2e24-409">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-409">Int32</span></span> | <span data-ttu-id="e2e24-410">Int16</span><span class="sxs-lookup"><span data-stu-id="e2e24-410">Int16</span></span> | <span data-ttu-id="e2e24-411">Int16</span><span class="sxs-lookup"><span data-stu-id="e2e24-411">Int16</span></span> |
| <span data-ttu-id="e2e24-412">UInt16</span><span class="sxs-lookup"><span data-stu-id="e2e24-412">UInt16</span></span> | <span data-ttu-id="e2e24-413">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-413">Int32</span></span> | <span data-ttu-id="e2e24-414">UInt16</span><span class="sxs-lookup"><span data-stu-id="e2e24-414">UInt16</span></span> | <span data-ttu-id="e2e24-415">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-415">Int32</span></span> |
| <span data-ttu-id="e2e24-416">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-416">Int32</span></span> | <span data-ttu-id="e2e24-417">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-417">Int32</span></span> | <span data-ttu-id="e2e24-418">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-418">Int32</span></span> | <span data-ttu-id="e2e24-419">Int32</span><span class="sxs-lookup"><span data-stu-id="e2e24-419">Int32</span></span> |
| <span data-ttu-id="e2e24-420">UInt32</span><span class="sxs-lookup"><span data-stu-id="e2e24-420">UInt32</span></span> | <span data-ttu-id="e2e24-421">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-421">Int64</span></span> | <span data-ttu-id="e2e24-422">UInt32</span><span class="sxs-lookup"><span data-stu-id="e2e24-422">UInt32</span></span> | <span data-ttu-id="e2e24-423">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-423">Int64</span></span> |
| <span data-ttu-id="e2e24-424">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-424">Int64</span></span> | <span data-ttu-id="e2e24-425">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-425">Int64</span></span> | <span data-ttu-id="e2e24-426">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-426">Int64</span></span> | <span data-ttu-id="e2e24-427">Int64</span><span class="sxs-lookup"><span data-stu-id="e2e24-427">Int64</span></span> |
| <span data-ttu-id="e2e24-428">UInt64</span><span class="sxs-lookup"><span data-stu-id="e2e24-428">UInt64</span></span> | <span data-ttu-id="e2e24-429">Int64/Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-429">Int64/Binary</span></span> | <span data-ttu-id="e2e24-430">UInt64</span><span class="sxs-lookup"><span data-stu-id="e2e24-430">UInt64</span></span> | <span data-ttu-id="e2e24-431">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-431">Decimal</span></span> |
| <span data-ttu-id="e2e24-432">Single</span><span class="sxs-lookup"><span data-stu-id="e2e24-432">Single</span></span> | <span data-ttu-id="e2e24-433">Float</span><span class="sxs-lookup"><span data-stu-id="e2e24-433">Float</span></span> | <span data-ttu-id="e2e24-434">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-434">N/A</span></span> | <span data-ttu-id="e2e24-435">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-435">N/A</span></span> |
| <span data-ttu-id="e2e24-436">Double</span><span class="sxs-lookup"><span data-stu-id="e2e24-436">Double</span></span> | <span data-ttu-id="e2e24-437">Double</span><span class="sxs-lookup"><span data-stu-id="e2e24-437">Double</span></span> | <span data-ttu-id="e2e24-438">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-438">N/A</span></span> | <span data-ttu-id="e2e24-439">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-439">N/A</span></span> |
| <span data-ttu-id="e2e24-440">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-440">Decimal</span></span> | <span data-ttu-id="e2e24-441">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-441">Binary</span></span> | <span data-ttu-id="e2e24-442">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-442">Decimal</span></span> | <span data-ttu-id="e2e24-443">Decimal</span><span class="sxs-lookup"><span data-stu-id="e2e24-443">Decimal</span></span> |
| <span data-ttu-id="e2e24-444">String</span><span class="sxs-lookup"><span data-stu-id="e2e24-444">String</span></span> | <span data-ttu-id="e2e24-445">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-445">Binary</span></span> | <span data-ttu-id="e2e24-446">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-446">Utf8</span></span> | <span data-ttu-id="e2e24-447">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-447">Utf8</span></span> |
| <span data-ttu-id="e2e24-448">DateTime</span><span class="sxs-lookup"><span data-stu-id="e2e24-448">DateTime</span></span> | <span data-ttu-id="e2e24-449">Int96</span><span class="sxs-lookup"><span data-stu-id="e2e24-449">Int96</span></span> | <span data-ttu-id="e2e24-450">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-450">N/A</span></span> | <span data-ttu-id="e2e24-451">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-451">N/A</span></span> |
| <span data-ttu-id="e2e24-452">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e2e24-452">TimeSpan</span></span> | <span data-ttu-id="e2e24-453">Int96</span><span class="sxs-lookup"><span data-stu-id="e2e24-453">Int96</span></span> | <span data-ttu-id="e2e24-454">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-454">N/A</span></span> | <span data-ttu-id="e2e24-455">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-455">N/A</span></span> |
| <span data-ttu-id="e2e24-456">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e2e24-456">DateTimeOffset</span></span> | <span data-ttu-id="e2e24-457">Int96</span><span class="sxs-lookup"><span data-stu-id="e2e24-457">Int96</span></span> | <span data-ttu-id="e2e24-458">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-458">N/A</span></span> | <span data-ttu-id="e2e24-459">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-459">N/A</span></span> |
| <span data-ttu-id="e2e24-460">ByteArray</span><span class="sxs-lookup"><span data-stu-id="e2e24-460">ByteArray</span></span> | <span data-ttu-id="e2e24-461">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-461">Binary</span></span> | <span data-ttu-id="e2e24-462">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-462">N/A</span></span> | <span data-ttu-id="e2e24-463">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-463">N/A</span></span> |
| <span data-ttu-id="e2e24-464">Guid</span><span class="sxs-lookup"><span data-stu-id="e2e24-464">Guid</span></span> | <span data-ttu-id="e2e24-465">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-465">Binary</span></span> | <span data-ttu-id="e2e24-466">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-466">Utf8</span></span> | <span data-ttu-id="e2e24-467">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-467">Utf8</span></span> |
| <span data-ttu-id="e2e24-468">Char</span><span class="sxs-lookup"><span data-stu-id="e2e24-468">Char</span></span> | <span data-ttu-id="e2e24-469">Binary</span><span class="sxs-lookup"><span data-stu-id="e2e24-469">Binary</span></span> | <span data-ttu-id="e2e24-470">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-470">Utf8</span></span> | <span data-ttu-id="e2e24-471">Utf8</span><span class="sxs-lookup"><span data-stu-id="e2e24-471">Utf8</span></span> |
| <span data-ttu-id="e2e24-472">CharArray</span><span class="sxs-lookup"><span data-stu-id="e2e24-472">CharArray</span></span> | <span data-ttu-id="e2e24-473">Not supported</span><span class="sxs-lookup"><span data-stu-id="e2e24-473">Not supported</span></span> | <span data-ttu-id="e2e24-474">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-474">N/A</span></span> | <span data-ttu-id="e2e24-475">N/A</span><span class="sxs-lookup"><span data-stu-id="e2e24-475">N/A</span></span> |

## <a name="compression-support"></a><span data-ttu-id="e2e24-476">Compression support</span><span class="sxs-lookup"><span data-stu-id="e2e24-476">Compression support</span></span>

<span data-ttu-id="e2e24-477">Azure Data Factory supports compress/decompress data during copy.</span><span class="sxs-lookup"><span data-stu-id="e2e24-477">Azure Data Factory supports compress/decompress data during copy.</span></span> <span data-ttu-id="e2e24-478">When you specify `compression` property in an input dataset, the copy activity read the compressed data from the source and decompress it; and when you specify the property in an output dataset, the copy activity compress then write data to the sink.</span><span class="sxs-lookup"><span data-stu-id="e2e24-478">When you specify `compression` property in an input dataset, the copy activity read the compressed data from the source and decompress it; and when you specify the property in an output dataset, the copy activity compress then write data to the sink.</span></span> <span data-ttu-id="e2e24-479">Here are a few sample scenarios:</span><span class="sxs-lookup"><span data-stu-id="e2e24-479">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="e2e24-480">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="e2e24-480">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="e2e24-481">You define the input Azure Blob dataset with the `compression` `type` property as GZIP.</span><span class="sxs-lookup"><span data-stu-id="e2e24-481">You define the input Azure Blob dataset with the `compression` `type` property as GZIP.</span></span>
* <span data-ttu-id="e2e24-482">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="e2e24-482">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="e2e24-483">You define an output Azure Blob dataset with the `compression` `type` property as GZip.</span><span class="sxs-lookup"><span data-stu-id="e2e24-483">You define an output Azure Blob dataset with the `compression` `type` property as GZip.</span></span>
* <span data-ttu-id="e2e24-484">Read .zip file from FTP server, decompress it to get the files inside, and land those files in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e2e24-484">Read .zip file from FTP server, decompress it to get the files inside, and land those files in Azure Data Lake Store.</span></span> <span data-ttu-id="e2e24-485">You define an input FTP dataset with the `compression` `type` property as ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="e2e24-485">You define an input FTP dataset with the `compression` `type` property as ZipDeflate.</span></span>
* <span data-ttu-id="e2e24-486">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="e2e24-486">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="e2e24-487">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2.</span><span class="sxs-lookup"><span data-stu-id="e2e24-487">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2.</span></span>

<span data-ttu-id="e2e24-488">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span><span class="sxs-lookup"><span data-stu-id="e2e24-488">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "fileName": "pagecounts.csv.gz",
            "folderPath": "compression/file/",
            "format": {
                "type": "TextFormat"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

<span data-ttu-id="e2e24-489">The **compression** section has two properties:</span><span class="sxs-lookup"><span data-stu-id="e2e24-489">The **compression** section has two properties:</span></span>

* <span data-ttu-id="e2e24-490">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-490">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>
* <span data-ttu-id="e2e24-491">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-491">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="e2e24-492">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span><span class="sxs-lookup"><span data-stu-id="e2e24-492">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="e2e24-493">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span><span class="sxs-lookup"><span data-stu-id="e2e24-493">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="e2e24-494">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="e2e24-494">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e24-495">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="e2e24-495">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="e2e24-496">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span><span class="sxs-lookup"><span data-stu-id="e2e24-496">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="e2e24-497">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span><span class="sxs-lookup"><span data-stu-id="e2e24-497">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="e2e24-498">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="e2e24-498">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e24-499">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2e24-499">Next steps</span></span>

<span data-ttu-id="e2e24-500">See the following articles for file-based data stores supported by Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="e2e24-500">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="e2e24-501">Azure Blob Storage connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-501">Azure Blob Storage connector</span></span>](connector-azure-blob-storage.md)
- [<span data-ttu-id="e2e24-502">Azure Data Lake Store connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-502">Azure Data Lake Store connector</span></span>](connector-azure-data-lake-store.md)
- [<span data-ttu-id="e2e24-503">Amazon S3 connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-503">Amazon S3 connector</span></span>](connector-amazon-simple-storage-service.md)
- [<span data-ttu-id="e2e24-504">File System connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-504">File System connector</span></span>](connector-file-system.md)
- [<span data-ttu-id="e2e24-505">FTP connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-505">FTP connector</span></span>](connector-ftp.md)
- [<span data-ttu-id="e2e24-506">SFTP connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-506">SFTP connector</span></span>](connector-sftp.md)
- [<span data-ttu-id="e2e24-507">HDFS connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-507">HDFS connector</span></span>](connector-hdfs.md)
- [<span data-ttu-id="e2e24-508">HTTP connector</span><span class="sxs-lookup"><span data-stu-id="e2e24-508">HTTP connector</span></span>](connector-http.md)
