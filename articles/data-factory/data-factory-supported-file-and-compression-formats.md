---
title: File and compression formats in Azure Data Factory | Microsoft Docs
description: Learn about the file formats supported by Azure Data Factory.
keywords: blob data, azure blob copy
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jingwang
ms.openlocfilehash: 06f7b38f5d08f2182f08d38a11dec526042c1828
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555810"
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="15610-104">File and compression formats supported by Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="15610-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="15610-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="15610-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="15610-106">Azure Data Factory supports the following file format types:</span><span class="sxs-lookup"><span data-stu-id="15610-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="15610-107">Text format</span><span class="sxs-lookup"><span data-stu-id="15610-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="15610-108">JSON format</span><span class="sxs-lookup"><span data-stu-id="15610-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="15610-109">Avro format</span><span class="sxs-lookup"><span data-stu-id="15610-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="15610-110">ORC format</span><span class="sxs-lookup"><span data-stu-id="15610-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="15610-111">Parquet format</span><span class="sxs-lookup"><span data-stu-id="15610-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="15610-112">Text format</span><span class="sxs-lookup"><span data-stu-id="15610-112">Text format</span></span>
<span data-ttu-id="15610-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="15610-114">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="15610-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="15610-115">See [TextFormat example](#textformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="15610-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="15610-116">Property</span><span class="sxs-lookup"><span data-stu-id="15610-116">Property</span></span> | <span data-ttu-id="15610-117">Description</span><span class="sxs-lookup"><span data-stu-id="15610-117">Description</span></span> | <span data-ttu-id="15610-118">Allowed values</span><span class="sxs-lookup"><span data-stu-id="15610-118">Allowed values</span></span> | <span data-ttu-id="15610-119">Required</span><span class="sxs-lookup"><span data-stu-id="15610-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="15610-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="15610-120">columnDelimiter</span></span> |<span data-ttu-id="15610-121">The character used to separate columns in a file.</span><span class="sxs-lookup"><span data-stu-id="15610-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="15610-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span><span class="sxs-lookup"><span data-stu-id="15610-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="15610-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span><span class="sxs-lookup"><span data-stu-id="15610-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="15610-124">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="15610-124">Only one character is allowed.</span></span> <span data-ttu-id="15610-125">The **default** value is **comma (',')**.</span><span class="sxs-lookup"><span data-stu-id="15610-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="15610-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span><span class="sxs-lookup"><span data-stu-id="15610-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="15610-127">No</span><span class="sxs-lookup"><span data-stu-id="15610-127">No</span></span> |
| <span data-ttu-id="15610-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="15610-128">rowDelimiter</span></span> |<span data-ttu-id="15610-129">The character used to separate rows in a file.</span><span class="sxs-lookup"><span data-stu-id="15610-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="15610-130">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="15610-130">Only one character is allowed.</span></span> <span data-ttu-id="15610-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span><span class="sxs-lookup"><span data-stu-id="15610-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="15610-132">No</span><span class="sxs-lookup"><span data-stu-id="15610-132">No</span></span> |
| <span data-ttu-id="15610-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="15610-133">escapeChar</span></span> |<span data-ttu-id="15610-134">The special character used to escape a column delimiter in the content of input file.</span><span class="sxs-lookup"><span data-stu-id="15610-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="15610-135">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="15610-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="15610-136">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="15610-136">Only one character is allowed.</span></span> <span data-ttu-id="15610-137">No default value.</span><span class="sxs-lookup"><span data-stu-id="15610-137">No default value.</span></span> <br/><br/><span data-ttu-id="15610-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="15610-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="15610-139">No</span><span class="sxs-lookup"><span data-stu-id="15610-139">No</span></span> |
| <span data-ttu-id="15610-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="15610-140">quoteChar</span></span> |<span data-ttu-id="15610-141">The character used to quote a string value.</span><span class="sxs-lookup"><span data-stu-id="15610-141">The character used to quote a string value.</span></span> <span data-ttu-id="15610-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span><span class="sxs-lookup"><span data-stu-id="15610-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="15610-143">This property is applicable to both input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="15610-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="15610-144">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="15610-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="15610-145">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="15610-145">Only one character is allowed.</span></span> <span data-ttu-id="15610-146">No default value.</span><span class="sxs-lookup"><span data-stu-id="15610-146">No default value.</span></span> <br/><br/><span data-ttu-id="15610-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="15610-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="15610-148">No</span><span class="sxs-lookup"><span data-stu-id="15610-148">No</span></span> |
| <span data-ttu-id="15610-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="15610-149">nullValue</span></span> |<span data-ttu-id="15610-150">One or more characters used to represent a null value.</span><span class="sxs-lookup"><span data-stu-id="15610-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="15610-151">One or more characters.</span><span class="sxs-lookup"><span data-stu-id="15610-151">One or more characters.</span></span> <span data-ttu-id="15610-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span><span class="sxs-lookup"><span data-stu-id="15610-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="15610-153">No</span><span class="sxs-lookup"><span data-stu-id="15610-153">No</span></span> |
| <span data-ttu-id="15610-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="15610-154">encodingName</span></span> |<span data-ttu-id="15610-155">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="15610-155">Specify the encoding name.</span></span> |<span data-ttu-id="15610-156">A valid encoding name.</span><span class="sxs-lookup"><span data-stu-id="15610-156">A valid encoding name.</span></span> <span data-ttu-id="15610-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="15610-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="15610-158">Example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="15610-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="15610-159">The **default** value is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="15610-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="15610-160">No</span><span class="sxs-lookup"><span data-stu-id="15610-160">No</span></span> |
| <span data-ttu-id="15610-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="15610-161">firstRowAsHeader</span></span> |<span data-ttu-id="15610-162">Specifies whether to consider the first row as a header.</span><span class="sxs-lookup"><span data-stu-id="15610-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="15610-163">For an input dataset, Data Factory reads first row as a header.</span><span class="sxs-lookup"><span data-stu-id="15610-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="15610-164">For an output dataset, Data Factory writes first row as a header.</span><span class="sxs-lookup"><span data-stu-id="15610-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="15610-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="15610-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="15610-166">True</span><span class="sxs-lookup"><span data-stu-id="15610-166">True</span></span><br/><span data-ttu-id="15610-167"><b>False (default)</b></span><span class="sxs-lookup"><span data-stu-id="15610-167"><b>False (default)</b></span></span> |<span data-ttu-id="15610-168">No</span><span class="sxs-lookup"><span data-stu-id="15610-168">No</span></span> |
| <span data-ttu-id="15610-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="15610-169">skipLineCount</span></span> |<span data-ttu-id="15610-170">Indicates the number of rows to skip when reading data from input files.</span><span class="sxs-lookup"><span data-stu-id="15610-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="15610-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span><span class="sxs-lookup"><span data-stu-id="15610-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="15610-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="15610-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="15610-173">Integer</span><span class="sxs-lookup"><span data-stu-id="15610-173">Integer</span></span> |<span data-ttu-id="15610-174">No</span><span class="sxs-lookup"><span data-stu-id="15610-174">No</span></span> |
| <span data-ttu-id="15610-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="15610-175">treatEmptyAsNull</span></span> |<span data-ttu-id="15610-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span><span class="sxs-lookup"><span data-stu-id="15610-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="15610-177">**True (default)**</span><span class="sxs-lookup"><span data-stu-id="15610-177">**True (default)**</span></span><br/><span data-ttu-id="15610-178">False</span><span class="sxs-lookup"><span data-stu-id="15610-178">False</span></span> |<span data-ttu-id="15610-179">No</span><span class="sxs-lookup"><span data-stu-id="15610-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="15610-180">TextFormat example</span><span class="sxs-lookup"><span data-stu-id="15610-180">TextFormat example</span></span>
<span data-ttu-id="15610-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span><span class="sxs-lookup"><span data-stu-id="15610-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="15610-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span><span class="sxs-lookup"><span data-stu-id="15610-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="15610-183">Scenarios for using firstRowAsHeader and skipLineCount</span><span class="sxs-lookup"><span data-stu-id="15610-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="15610-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span><span class="sxs-lookup"><span data-stu-id="15610-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="15610-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span><span class="sxs-lookup"><span data-stu-id="15610-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="15610-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span><span class="sxs-lookup"><span data-stu-id="15610-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="15610-187">Specify `firstRowAsHeader` as true in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="15610-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="15610-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span><span class="sxs-lookup"><span data-stu-id="15610-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="15610-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span><span class="sxs-lookup"><span data-stu-id="15610-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="15610-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="15610-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="15610-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span><span class="sxs-lookup"><span data-stu-id="15610-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="15610-192">JSON format</span><span class="sxs-lookup"><span data-stu-id="15610-192">JSON format</span></span>
<span data-ttu-id="15610-193">To **import/export a JSON file as-is into/from DocumentDB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure DocumentDB](data-factory-azure-documentdb-connector.md) article.</span><span class="sxs-lookup"><span data-stu-id="15610-193">To **import/export a JSON file as-is into/from DocumentDB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure DocumentDB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="15610-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="15610-195">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="15610-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="15610-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="15610-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="15610-197">Property</span><span class="sxs-lookup"><span data-stu-id="15610-197">Property</span></span> | <span data-ttu-id="15610-198">Description</span><span class="sxs-lookup"><span data-stu-id="15610-198">Description</span></span> | <span data-ttu-id="15610-199">Required</span><span class="sxs-lookup"><span data-stu-id="15610-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15610-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="15610-200">filePattern</span></span> |<span data-ttu-id="15610-201">Indicate the pattern of data stored in each JSON file.</span><span class="sxs-lookup"><span data-stu-id="15610-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="15610-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="15610-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="15610-203">The **default** value is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="15610-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="15610-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span><span class="sxs-lookup"><span data-stu-id="15610-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="15610-205">No</span><span class="sxs-lookup"><span data-stu-id="15610-205">No</span></span> |
| <span data-ttu-id="15610-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="15610-206">jsonNodeReference</span></span> | <span data-ttu-id="15610-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span><span class="sxs-lookup"><span data-stu-id="15610-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="15610-208">This property is supported only when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="15610-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="15610-209">No</span><span class="sxs-lookup"><span data-stu-id="15610-209">No</span></span> |
| <span data-ttu-id="15610-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="15610-210">jsonPathDefinition</span></span> | <span data-ttu-id="15610-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span><span class="sxs-lookup"><span data-stu-id="15610-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="15610-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span><span class="sxs-lookup"><span data-stu-id="15610-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="15610-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span><span class="sxs-lookup"><span data-stu-id="15610-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="15610-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="15610-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="15610-215">No</span><span class="sxs-lookup"><span data-stu-id="15610-215">No</span></span> |
| <span data-ttu-id="15610-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="15610-216">encodingName</span></span> |<span data-ttu-id="15610-217">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="15610-217">Specify the encoding name.</span></span> <span data-ttu-id="15610-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span><span class="sxs-lookup"><span data-stu-id="15610-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="15610-219">For example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="15610-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="15610-220">The **default** value is: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="15610-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="15610-221">No</span><span class="sxs-lookup"><span data-stu-id="15610-221">No</span></span> |
| <span data-ttu-id="15610-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="15610-222">nestingSeparator</span></span> |<span data-ttu-id="15610-223">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="15610-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="15610-224">The default value is '.' (dot).</span><span class="sxs-lookup"><span data-stu-id="15610-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="15610-225">No</span><span class="sxs-lookup"><span data-stu-id="15610-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="15610-226">JSON file patterns</span><span class="sxs-lookup"><span data-stu-id="15610-226">JSON file patterns</span></span>

<span data-ttu-id="15610-227">Copy activity can parse the following patterns of JSON files:</span><span class="sxs-lookup"><span data-stu-id="15610-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="15610-228">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="15610-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="15610-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span><span class="sxs-lookup"><span data-stu-id="15610-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="15610-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span><span class="sxs-lookup"><span data-stu-id="15610-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="15610-231">**single object JSON example**</span><span class="sxs-lookup"><span data-stu-id="15610-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="15610-232">**line-delimited JSON example**</span><span class="sxs-lookup"><span data-stu-id="15610-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="15610-233">**concatenated JSON example**</span><span class="sxs-lookup"><span data-stu-id="15610-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="15610-234">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="15610-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="15610-235">Each file contains an array of objects.</span><span class="sxs-lookup"><span data-stu-id="15610-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="15610-236">JsonFormat example</span><span class="sxs-lookup"><span data-stu-id="15610-236">JsonFormat example</span></span>

<span data-ttu-id="15610-237">**Case 1: Copying data from JSON files**</span><span class="sxs-lookup"><span data-stu-id="15610-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="15610-238">See the following two samples when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="15610-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="15610-239">The generic points to note:</span><span class="sxs-lookup"><span data-stu-id="15610-239">The generic points to note:</span></span>

<span data-ttu-id="15610-240">**Sample 1: extract data from object and array**</span><span class="sxs-lookup"><span data-stu-id="15610-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="15610-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span><span class="sxs-lookup"><span data-stu-id="15610-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="15610-242">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="15610-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="15610-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span><span class="sxs-lookup"><span data-stu-id="15610-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="15610-244">id</span><span class="sxs-lookup"><span data-stu-id="15610-244">id</span></span> | <span data-ttu-id="15610-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="15610-245">deviceType</span></span> | <span data-ttu-id="15610-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="15610-246">targetResourceType</span></span> | <span data-ttu-id="15610-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="15610-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="15610-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="15610-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="15610-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="15610-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="15610-250">PC</span><span class="sxs-lookup"><span data-stu-id="15610-250">PC</span></span> | <span data-ttu-id="15610-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="15610-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="15610-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="15610-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="15610-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="15610-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="15610-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="15610-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="15610-255">More specifically:</span><span class="sxs-lookup"><span data-stu-id="15610-255">More specifically:</span></span>

- <span data-ttu-id="15610-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="15610-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="15610-257">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="15610-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="15610-258">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span><span class="sxs-lookup"><span data-stu-id="15610-258">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="15610-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="15610-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="15610-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span><span class="sxs-lookup"><span data-stu-id="15610-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="15610-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span><span class="sxs-lookup"><span data-stu-id="15610-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="15610-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span><span class="sxs-lookup"><span data-stu-id="15610-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="15610-263">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="15610-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="15610-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span><span class="sxs-lookup"><span data-stu-id="15610-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="15610-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="15610-265">ordernumber</span></span> | <span data-ttu-id="15610-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="15610-266">orderdate</span></span> | <span data-ttu-id="15610-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="15610-267">order_pd</span></span> | <span data-ttu-id="15610-268">order_price</span><span class="sxs-lookup"><span data-stu-id="15610-268">order_price</span></span> | <span data-ttu-id="15610-269">city</span><span class="sxs-lookup"><span data-stu-id="15610-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="15610-270">01</span><span class="sxs-lookup"><span data-stu-id="15610-270">01</span></span> | <span data-ttu-id="15610-271">20170122</span><span class="sxs-lookup"><span data-stu-id="15610-271">20170122</span></span> | <span data-ttu-id="15610-272">P1</span><span class="sxs-lookup"><span data-stu-id="15610-272">P1</span></span> | <span data-ttu-id="15610-273">23</span><span class="sxs-lookup"><span data-stu-id="15610-273">23</span></span> | <span data-ttu-id="15610-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="15610-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="15610-275">01</span><span class="sxs-lookup"><span data-stu-id="15610-275">01</span></span> | <span data-ttu-id="15610-276">20170122</span><span class="sxs-lookup"><span data-stu-id="15610-276">20170122</span></span> | <span data-ttu-id="15610-277">P2</span><span class="sxs-lookup"><span data-stu-id="15610-277">P2</span></span> | <span data-ttu-id="15610-278">13</span><span class="sxs-lookup"><span data-stu-id="15610-278">13</span></span> | <span data-ttu-id="15610-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="15610-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="15610-280">01</span><span class="sxs-lookup"><span data-stu-id="15610-280">01</span></span> | <span data-ttu-id="15610-281">20170122</span><span class="sxs-lookup"><span data-stu-id="15610-281">20170122</span></span> | <span data-ttu-id="15610-282">P3</span><span class="sxs-lookup"><span data-stu-id="15610-282">P3</span></span> | <span data-ttu-id="15610-283">231</span><span class="sxs-lookup"><span data-stu-id="15610-283">231</span></span> | <span data-ttu-id="15610-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="15610-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="15610-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="15610-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="15610-286">More specifically:</span><span class="sxs-lookup"><span data-stu-id="15610-286">More specifically:</span></span>

- <span data-ttu-id="15610-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="15610-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="15610-288">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="15610-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="15610-289">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span><span class="sxs-lookup"><span data-stu-id="15610-289">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="15610-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span><span class="sxs-lookup"><span data-stu-id="15610-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="15610-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="15610-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="15610-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span><span class="sxs-lookup"><span data-stu-id="15610-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="15610-293">**Note the following points:**</span><span class="sxs-lookup"><span data-stu-id="15610-293">**Note the following points:**</span></span>

* <span data-ttu-id="15610-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span><span class="sxs-lookup"><span data-stu-id="15610-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="15610-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span><span class="sxs-lookup"><span data-stu-id="15610-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="15610-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="15610-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="15610-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span><span class="sxs-lookup"><span data-stu-id="15610-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="15610-298">Property names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="15610-298">Property names are case-sensitive.</span></span> <span data-ttu-id="15610-299">Two properties with same name but different casings are treated as two separate properties.</span><span class="sxs-lookup"><span data-stu-id="15610-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="15610-300">**Case 2: Writing data to JSON file**</span><span class="sxs-lookup"><span data-stu-id="15610-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="15610-301">If you have the following table in SQL Database:</span><span class="sxs-lookup"><span data-stu-id="15610-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="15610-302">id</span><span class="sxs-lookup"><span data-stu-id="15610-302">id</span></span> | <span data-ttu-id="15610-303">order_date</span><span class="sxs-lookup"><span data-stu-id="15610-303">order_date</span></span> | <span data-ttu-id="15610-304">order_price</span><span class="sxs-lookup"><span data-stu-id="15610-304">order_price</span></span> | <span data-ttu-id="15610-305">order_by</span><span class="sxs-lookup"><span data-stu-id="15610-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="15610-306">1</span><span class="sxs-lookup"><span data-stu-id="15610-306">1</span></span> | <span data-ttu-id="15610-307">20170119</span><span class="sxs-lookup"><span data-stu-id="15610-307">20170119</span></span> | <span data-ttu-id="15610-308">2000</span><span class="sxs-lookup"><span data-stu-id="15610-308">2000</span></span> | <span data-ttu-id="15610-309">David</span><span class="sxs-lookup"><span data-stu-id="15610-309">David</span></span> |
| <span data-ttu-id="15610-310">2</span><span class="sxs-lookup"><span data-stu-id="15610-310">2</span></span> | <span data-ttu-id="15610-311">20170120</span><span class="sxs-lookup"><span data-stu-id="15610-311">20170120</span></span> | <span data-ttu-id="15610-312">3500</span><span class="sxs-lookup"><span data-stu-id="15610-312">3500</span></span> | <span data-ttu-id="15610-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="15610-313">Patrick</span></span> |
| <span data-ttu-id="15610-314">3</span><span class="sxs-lookup"><span data-stu-id="15610-314">3</span></span> | <span data-ttu-id="15610-315">20170121</span><span class="sxs-lookup"><span data-stu-id="15610-315">20170121</span></span> | <span data-ttu-id="15610-316">4000</span><span class="sxs-lookup"><span data-stu-id="15610-316">4000</span></span> | <span data-ttu-id="15610-317">Jason</span><span class="sxs-lookup"><span data-stu-id="15610-317">Jason</span></span> |

<span data-ttu-id="15610-318">and for each record, you expect to write to a JSON object in the following format:</span><span class="sxs-lookup"><span data-stu-id="15610-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="15610-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="15610-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="15610-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span><span class="sxs-lookup"><span data-stu-id="15610-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="15610-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span><span class="sxs-lookup"><span data-stu-id="15610-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="15610-322">AVRO format</span><span class="sxs-lookup"><span data-stu-id="15610-322">AVRO format</span></span>
<span data-ttu-id="15610-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="15610-324">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="15610-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="15610-325">Example:</span><span class="sxs-lookup"><span data-stu-id="15610-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="15610-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="15610-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="15610-327">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="15610-327">Note the following points:</span></span>  

* <span data-ttu-id="15610-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span><span class="sxs-lookup"><span data-stu-id="15610-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="15610-329">ORC format</span><span class="sxs-lookup"><span data-stu-id="15610-329">ORC format</span></span>
<span data-ttu-id="15610-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="15610-331">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="15610-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="15610-332">Example:</span><span class="sxs-lookup"><span data-stu-id="15610-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="15610-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="15610-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="15610-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="15610-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="15610-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="15610-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="15610-336">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="15610-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="15610-337">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="15610-337">Note the following points:</span></span>

* <span data-ttu-id="15610-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="15610-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="15610-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="15610-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="15610-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="15610-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="15610-341">It uses the compression codec is in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="15610-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="15610-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span><span class="sxs-lookup"><span data-stu-id="15610-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="15610-343">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="15610-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="15610-344">Parquet format</span><span class="sxs-lookup"><span data-stu-id="15610-344">Parquet format</span></span>
<span data-ttu-id="15610-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="15610-346">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="15610-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="15610-347">Example:</span><span class="sxs-lookup"><span data-stu-id="15610-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="15610-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="15610-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="15610-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="15610-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="15610-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="15610-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="15610-351">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="15610-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="15610-352">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="15610-352">Note the following points:</span></span>

* <span data-ttu-id="15610-353">Complex data types are not supported (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="15610-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="15610-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span><span class="sxs-lookup"><span data-stu-id="15610-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="15610-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="15610-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="15610-356">It uses the compression codec in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="15610-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="15610-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span><span class="sxs-lookup"><span data-stu-id="15610-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="15610-358">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="15610-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="15610-359">Compression support</span><span class="sxs-lookup"><span data-stu-id="15610-359">Compression support</span></span>
<span data-ttu-id="15610-360">Processing large data sets can cause I/O and network bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="15610-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="15610-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span><span class="sxs-lookup"><span data-stu-id="15610-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="15610-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span><span class="sxs-lookup"><span data-stu-id="15610-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="15610-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span><span class="sxs-lookup"><span data-stu-id="15610-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="15610-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="15610-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="15610-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="15610-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="15610-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span><span class="sxs-lookup"><span data-stu-id="15610-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="15610-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span><span class="sxs-lookup"><span data-stu-id="15610-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="15610-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="15610-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="15610-369">The **compression** section has two properties:</span><span class="sxs-lookup"><span data-stu-id="15610-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="15610-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="15610-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="15610-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="15610-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="15610-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span><span class="sxs-lookup"><span data-stu-id="15610-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="15610-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span><span class="sxs-lookup"><span data-stu-id="15610-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="15610-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="15610-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="15610-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span><span class="sxs-lookup"><span data-stu-id="15610-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="15610-376">Here are a few sample scenarios:</span><span class="sxs-lookup"><span data-stu-id="15610-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="15610-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="15610-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="15610-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span><span class="sxs-lookup"><span data-stu-id="15610-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="15610-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="15610-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="15610-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span><span class="sxs-lookup"><span data-stu-id="15610-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="15610-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="15610-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="15610-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="15610-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="15610-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="15610-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="15610-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span><span class="sxs-lookup"><span data-stu-id="15610-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="15610-385">Next steps</span><span class="sxs-lookup"><span data-stu-id="15610-385">Next steps</span></span>
<span data-ttu-id="15610-386">See the following articles for file-based data stores supported by Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="15610-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="15610-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="15610-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="15610-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="15610-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="15610-389">FTP</span><span class="sxs-lookup"><span data-stu-id="15610-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="15610-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="15610-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="15610-391">File System</span><span class="sxs-lookup"><span data-stu-id="15610-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="15610-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="15610-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
