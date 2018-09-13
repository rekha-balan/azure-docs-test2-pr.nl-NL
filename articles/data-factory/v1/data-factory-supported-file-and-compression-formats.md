---
title: File and compression formats in Azure Data Factory | Microsoft Docs
description: Learn about the file formats supported by Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 5afc89e774595952adf860fc6bcdc0e2403c617a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868048"
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="d46c8-103">File and compression formats supported by Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d46c8-103">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="d46c8-104">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="d46c8-104">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

> [!NOTE]
> <span data-ttu-id="d46c8-105">This article applies to version 1 of Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d46c8-105">This article applies to version 1 of Azure Data Factory.</span></span> <span data-ttu-id="d46c8-106">If you are using the current version of the Data Factory service, see [supported file formats and compression codecs in Data Factory](../supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="d46c8-106">If you are using the current version of the Data Factory service, see [supported file formats and compression codecs in Data Factory](../supported-file-formats-and-compression-codecs.md).</span></span>

<span data-ttu-id="d46c8-107">Azure Data Factory supports the following file format types:</span><span class="sxs-lookup"><span data-stu-id="d46c8-107">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="d46c8-108">Text format</span><span class="sxs-lookup"><span data-stu-id="d46c8-108">Text format</span></span>](#text-format)
* [<span data-ttu-id="d46c8-109">JSON format</span><span class="sxs-lookup"><span data-stu-id="d46c8-109">JSON format</span></span>](#json-format)
* [<span data-ttu-id="d46c8-110">Avro format</span><span class="sxs-lookup"><span data-stu-id="d46c8-110">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="d46c8-111">ORC format</span><span class="sxs-lookup"><span data-stu-id="d46c8-111">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="d46c8-112">Parquet format</span><span class="sxs-lookup"><span data-stu-id="d46c8-112">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="d46c8-113">Text format</span><span class="sxs-lookup"><span data-stu-id="d46c8-113">Text format</span></span>
<span data-ttu-id="d46c8-114">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-114">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="d46c8-115">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="d46c8-115">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="d46c8-116">See [TextFormat example](#textformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="d46c8-116">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="d46c8-117">Property</span><span class="sxs-lookup"><span data-stu-id="d46c8-117">Property</span></span> | <span data-ttu-id="d46c8-118">Description</span><span class="sxs-lookup"><span data-stu-id="d46c8-118">Description</span></span> | <span data-ttu-id="d46c8-119">Allowed values</span><span class="sxs-lookup"><span data-stu-id="d46c8-119">Allowed values</span></span> | <span data-ttu-id="d46c8-120">Required</span><span class="sxs-lookup"><span data-stu-id="d46c8-120">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d46c8-121">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="d46c8-121">columnDelimiter</span></span> |<span data-ttu-id="d46c8-122">The character used to separate columns in a file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-122">The character used to separate columns in a file.</span></span> <span data-ttu-id="d46c8-123">You can consider to use a rare unprintable char that may not likely exists in your data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-123">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="d46c8-124">For example, specify "\u0001", which represents Start of Heading (SOH).</span><span class="sxs-lookup"><span data-stu-id="d46c8-124">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="d46c8-125">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="d46c8-125">Only one character is allowed.</span></span> <span data-ttu-id="d46c8-126">The **default** value is **comma (',')**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-126">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="d46c8-127">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span><span class="sxs-lookup"><span data-stu-id="d46c8-127">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="d46c8-128">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-128">No</span></span> |
| <span data-ttu-id="d46c8-129">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="d46c8-129">rowDelimiter</span></span> |<span data-ttu-id="d46c8-130">The character used to separate rows in a file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-130">The character used to separate rows in a file.</span></span> |<span data-ttu-id="d46c8-131">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="d46c8-131">Only one character is allowed.</span></span> <span data-ttu-id="d46c8-132">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span><span class="sxs-lookup"><span data-stu-id="d46c8-132">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="d46c8-133">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-133">No</span></span> |
| <span data-ttu-id="d46c8-134">escapeChar</span><span class="sxs-lookup"><span data-stu-id="d46c8-134">escapeChar</span></span> |<span data-ttu-id="d46c8-135">The special character used to escape a column delimiter in the content of input file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-135">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="d46c8-136">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="d46c8-136">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="d46c8-137">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="d46c8-137">Only one character is allowed.</span></span> <span data-ttu-id="d46c8-138">No default value.</span><span class="sxs-lookup"><span data-stu-id="d46c8-138">No default value.</span></span> <br/><br/><span data-ttu-id="d46c8-139">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="d46c8-139">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="d46c8-140">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-140">No</span></span> |
| <span data-ttu-id="d46c8-141">quoteChar</span><span class="sxs-lookup"><span data-stu-id="d46c8-141">quoteChar</span></span> |<span data-ttu-id="d46c8-142">The character used to quote a string value.</span><span class="sxs-lookup"><span data-stu-id="d46c8-142">The character used to quote a string value.</span></span> <span data-ttu-id="d46c8-143">The column and row delimiters inside the quote characters would be treated as part of the string value.</span><span class="sxs-lookup"><span data-stu-id="d46c8-143">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="d46c8-144">This property is applicable to both input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="d46c8-144">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="d46c8-145">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="d46c8-145">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="d46c8-146">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="d46c8-146">Only one character is allowed.</span></span> <span data-ttu-id="d46c8-147">No default value.</span><span class="sxs-lookup"><span data-stu-id="d46c8-147">No default value.</span></span> <br/><br/><span data-ttu-id="d46c8-148">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="d46c8-148">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="d46c8-149">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-149">No</span></span> |
| <span data-ttu-id="d46c8-150">nullValue</span><span class="sxs-lookup"><span data-stu-id="d46c8-150">nullValue</span></span> |<span data-ttu-id="d46c8-151">One or more characters used to represent a null value.</span><span class="sxs-lookup"><span data-stu-id="d46c8-151">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="d46c8-152">One or more characters.</span><span class="sxs-lookup"><span data-stu-id="d46c8-152">One or more characters.</span></span> <span data-ttu-id="d46c8-153">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span><span class="sxs-lookup"><span data-stu-id="d46c8-153">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="d46c8-154">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-154">No</span></span> |
| <span data-ttu-id="d46c8-155">encodingName</span><span class="sxs-lookup"><span data-stu-id="d46c8-155">encodingName</span></span> |<span data-ttu-id="d46c8-156">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="d46c8-156">Specify the encoding name.</span></span> |<span data-ttu-id="d46c8-157">A valid encoding name.</span><span class="sxs-lookup"><span data-stu-id="d46c8-157">A valid encoding name.</span></span> <span data-ttu-id="d46c8-158">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="d46c8-158">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="d46c8-159">Example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="d46c8-159">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="d46c8-160">The **default** value is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-160">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="d46c8-161">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-161">No</span></span> |
| <span data-ttu-id="d46c8-162">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="d46c8-162">firstRowAsHeader</span></span> |<span data-ttu-id="d46c8-163">Specifies whether to consider the first row as a header.</span><span class="sxs-lookup"><span data-stu-id="d46c8-163">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="d46c8-164">For an input dataset, Data Factory reads first row as a header.</span><span class="sxs-lookup"><span data-stu-id="d46c8-164">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="d46c8-165">For an output dataset, Data Factory writes first row as a header.</span><span class="sxs-lookup"><span data-stu-id="d46c8-165">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="d46c8-166">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="d46c8-166">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="d46c8-167">True</span><span class="sxs-lookup"><span data-stu-id="d46c8-167">True</span></span><br/><span data-ttu-id="d46c8-168"><b>False (default)</b></span><span class="sxs-lookup"><span data-stu-id="d46c8-168"><b>False (default)</b></span></span> |<span data-ttu-id="d46c8-169">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-169">No</span></span> |
| <span data-ttu-id="d46c8-170">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="d46c8-170">skipLineCount</span></span> |<span data-ttu-id="d46c8-171">Indicates the number of rows to skip when reading data from input files.</span><span class="sxs-lookup"><span data-stu-id="d46c8-171">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="d46c8-172">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-172">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="d46c8-173">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="d46c8-173">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="d46c8-174">Integer</span><span class="sxs-lookup"><span data-stu-id="d46c8-174">Integer</span></span> |<span data-ttu-id="d46c8-175">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-175">No</span></span> |
| <span data-ttu-id="d46c8-176">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="d46c8-176">treatEmptyAsNull</span></span> |<span data-ttu-id="d46c8-177">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-177">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="d46c8-178">**True (default)**</span><span class="sxs-lookup"><span data-stu-id="d46c8-178">**True (default)**</span></span><br/><span data-ttu-id="d46c8-179">False</span><span class="sxs-lookup"><span data-stu-id="d46c8-179">False</span></span> |<span data-ttu-id="d46c8-180">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-180">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="d46c8-181">TextFormat example</span><span class="sxs-lookup"><span data-stu-id="d46c8-181">TextFormat example</span></span>
<span data-ttu-id="d46c8-182">In the following JSON definition for a dataset, some of the optional properties are specified.</span><span class="sxs-lookup"><span data-stu-id="d46c8-182">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="d46c8-183">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span><span class="sxs-lookup"><span data-stu-id="d46c8-183">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="d46c8-184">Scenarios for using firstRowAsHeader and skipLineCount</span><span class="sxs-lookup"><span data-stu-id="d46c8-184">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="d46c8-185">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span><span class="sxs-lookup"><span data-stu-id="d46c8-185">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="d46c8-186">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span><span class="sxs-lookup"><span data-stu-id="d46c8-186">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="d46c8-187">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span><span class="sxs-lookup"><span data-stu-id="d46c8-187">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="d46c8-188">Specify `firstRowAsHeader` as true in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="d46c8-188">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="d46c8-189">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span><span class="sxs-lookup"><span data-stu-id="d46c8-189">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="d46c8-190">Specify `skipLineCount` to indicate the number of lines to be skipped.</span><span class="sxs-lookup"><span data-stu-id="d46c8-190">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="d46c8-191">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="d46c8-191">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="d46c8-192">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span><span class="sxs-lookup"><span data-stu-id="d46c8-192">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="d46c8-193">JSON format</span><span class="sxs-lookup"><span data-stu-id="d46c8-193">JSON format</span></span>
<span data-ttu-id="d46c8-194">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span><span class="sxs-lookup"><span data-stu-id="d46c8-194">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="d46c8-195">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-195">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="d46c8-196">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="d46c8-196">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="d46c8-197">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="d46c8-197">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="d46c8-198">Property</span><span class="sxs-lookup"><span data-stu-id="d46c8-198">Property</span></span> | <span data-ttu-id="d46c8-199">Description</span><span class="sxs-lookup"><span data-stu-id="d46c8-199">Description</span></span> | <span data-ttu-id="d46c8-200">Required</span><span class="sxs-lookup"><span data-stu-id="d46c8-200">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d46c8-201">filePattern</span><span class="sxs-lookup"><span data-stu-id="d46c8-201">filePattern</span></span> |<span data-ttu-id="d46c8-202">Indicate the pattern of data stored in each JSON file.</span><span class="sxs-lookup"><span data-stu-id="d46c8-202">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="d46c8-203">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-203">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="d46c8-204">The **default** value is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-204">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="d46c8-205">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span><span class="sxs-lookup"><span data-stu-id="d46c8-205">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="d46c8-206">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-206">No</span></span> |
| <span data-ttu-id="d46c8-207">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="d46c8-207">jsonNodeReference</span></span> | <span data-ttu-id="d46c8-208">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span><span class="sxs-lookup"><span data-stu-id="d46c8-208">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="d46c8-209">This property is supported only when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="d46c8-209">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="d46c8-210">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-210">No</span></span> |
| <span data-ttu-id="d46c8-211">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="d46c8-211">jsonPathDefinition</span></span> | <span data-ttu-id="d46c8-212">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span><span class="sxs-lookup"><span data-stu-id="d46c8-212">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="d46c8-213">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span><span class="sxs-lookup"><span data-stu-id="d46c8-213">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="d46c8-214">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span><span class="sxs-lookup"><span data-stu-id="d46c8-214">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="d46c8-215">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="d46c8-215">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="d46c8-216">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-216">No</span></span> |
| <span data-ttu-id="d46c8-217">encodingName</span><span class="sxs-lookup"><span data-stu-id="d46c8-217">encodingName</span></span> |<span data-ttu-id="d46c8-218">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="d46c8-218">Specify the encoding name.</span></span> <span data-ttu-id="d46c8-219">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span><span class="sxs-lookup"><span data-stu-id="d46c8-219">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="d46c8-220">For example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="d46c8-220">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="d46c8-221">The **default** value is: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-221">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="d46c8-222">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-222">No</span></span> |
| <span data-ttu-id="d46c8-223">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="d46c8-223">nestingSeparator</span></span> |<span data-ttu-id="d46c8-224">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="d46c8-224">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="d46c8-225">The default value is '.' (dot).</span><span class="sxs-lookup"><span data-stu-id="d46c8-225">The default value is '.' (dot).</span></span> |<span data-ttu-id="d46c8-226">No</span><span class="sxs-lookup"><span data-stu-id="d46c8-226">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="d46c8-227">JSON file patterns</span><span class="sxs-lookup"><span data-stu-id="d46c8-227">JSON file patterns</span></span>

<span data-ttu-id="d46c8-228">Copy activity can parse the following patterns of JSON files:</span><span class="sxs-lookup"><span data-stu-id="d46c8-228">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="d46c8-229">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="d46c8-229">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="d46c8-230">Each file contains single object, or line-delimited/concatenated multiple objects.</span><span class="sxs-lookup"><span data-stu-id="d46c8-230">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="d46c8-231">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span><span class="sxs-lookup"><span data-stu-id="d46c8-231">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="d46c8-232">**single object JSON example**</span><span class="sxs-lookup"><span data-stu-id="d46c8-232">**single object JSON example**</span></span>

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

    * <span data-ttu-id="d46c8-233">**line-delimited JSON example**</span><span class="sxs-lookup"><span data-stu-id="d46c8-233">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="d46c8-234">**concatenated JSON example**</span><span class="sxs-lookup"><span data-stu-id="d46c8-234">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="d46c8-235">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="d46c8-235">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="d46c8-236">Each file contains an array of objects.</span><span class="sxs-lookup"><span data-stu-id="d46c8-236">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="d46c8-237">JsonFormat example</span><span class="sxs-lookup"><span data-stu-id="d46c8-237">JsonFormat example</span></span>

<span data-ttu-id="d46c8-238">**Case 1: Copying data from JSON files**</span><span class="sxs-lookup"><span data-stu-id="d46c8-238">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="d46c8-239">See the following two samples when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="d46c8-239">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="d46c8-240">The generic points to note:</span><span class="sxs-lookup"><span data-stu-id="d46c8-240">The generic points to note:</span></span>

<span data-ttu-id="d46c8-241">**Sample 1: extract data from object and array**</span><span class="sxs-lookup"><span data-stu-id="d46c8-241">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="d46c8-242">In this sample, you expect one root JSON object maps to single record in tabular result.</span><span class="sxs-lookup"><span data-stu-id="d46c8-242">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="d46c8-243">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="d46c8-243">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="d46c8-244">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span><span class="sxs-lookup"><span data-stu-id="d46c8-244">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="d46c8-245">id</span><span class="sxs-lookup"><span data-stu-id="d46c8-245">id</span></span> | <span data-ttu-id="d46c8-246">deviceType</span><span class="sxs-lookup"><span data-stu-id="d46c8-246">deviceType</span></span> | <span data-ttu-id="d46c8-247">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="d46c8-247">targetResourceType</span></span> | <span data-ttu-id="d46c8-248">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="d46c8-248">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="d46c8-249">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="d46c8-249">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d46c8-250">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="d46c8-250">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="d46c8-251">PC</span><span class="sxs-lookup"><span data-stu-id="d46c8-251">PC</span></span> | <span data-ttu-id="d46c8-252">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="d46c8-252">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="d46c8-253">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="d46c8-253">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="d46c8-254">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="d46c8-254">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="d46c8-255">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="d46c8-255">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="d46c8-256">More specifically:</span><span class="sxs-lookup"><span data-stu-id="d46c8-256">More specifically:</span></span>

- <span data-ttu-id="d46c8-257">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-257">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="d46c8-258">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="d46c8-258">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="d46c8-259">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span><span class="sxs-lookup"><span data-stu-id="d46c8-259">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="d46c8-260">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="d46c8-260">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="d46c8-261">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span><span class="sxs-lookup"><span data-stu-id="d46c8-261">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="d46c8-262">**Sample 2: cross apply multiple objects with the same pattern from array**</span><span class="sxs-lookup"><span data-stu-id="d46c8-262">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="d46c8-263">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span><span class="sxs-lookup"><span data-stu-id="d46c8-263">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="d46c8-264">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="d46c8-264">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="d46c8-265">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span><span class="sxs-lookup"><span data-stu-id="d46c8-265">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="d46c8-266">ordernumber</span><span class="sxs-lookup"><span data-stu-id="d46c8-266">ordernumber</span></span> | <span data-ttu-id="d46c8-267">orderdate</span><span class="sxs-lookup"><span data-stu-id="d46c8-267">orderdate</span></span> | <span data-ttu-id="d46c8-268">order_pd</span><span class="sxs-lookup"><span data-stu-id="d46c8-268">order_pd</span></span> | <span data-ttu-id="d46c8-269">order_price</span><span class="sxs-lookup"><span data-stu-id="d46c8-269">order_price</span></span> | <span data-ttu-id="d46c8-270">city</span><span class="sxs-lookup"><span data-stu-id="d46c8-270">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d46c8-271">01</span><span class="sxs-lookup"><span data-stu-id="d46c8-271">01</span></span> | <span data-ttu-id="d46c8-272">20170122</span><span class="sxs-lookup"><span data-stu-id="d46c8-272">20170122</span></span> | <span data-ttu-id="d46c8-273">P1</span><span class="sxs-lookup"><span data-stu-id="d46c8-273">P1</span></span> | <span data-ttu-id="d46c8-274">23</span><span class="sxs-lookup"><span data-stu-id="d46c8-274">23</span></span> | <span data-ttu-id="d46c8-275">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="d46c8-275">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="d46c8-276">01</span><span class="sxs-lookup"><span data-stu-id="d46c8-276">01</span></span> | <span data-ttu-id="d46c8-277">20170122</span><span class="sxs-lookup"><span data-stu-id="d46c8-277">20170122</span></span> | <span data-ttu-id="d46c8-278">P2</span><span class="sxs-lookup"><span data-stu-id="d46c8-278">P2</span></span> | <span data-ttu-id="d46c8-279">13</span><span class="sxs-lookup"><span data-stu-id="d46c8-279">13</span></span> | <span data-ttu-id="d46c8-280">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="d46c8-280">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="d46c8-281">01</span><span class="sxs-lookup"><span data-stu-id="d46c8-281">01</span></span> | <span data-ttu-id="d46c8-282">20170122</span><span class="sxs-lookup"><span data-stu-id="d46c8-282">20170122</span></span> | <span data-ttu-id="d46c8-283">P3</span><span class="sxs-lookup"><span data-stu-id="d46c8-283">P3</span></span> | <span data-ttu-id="d46c8-284">231</span><span class="sxs-lookup"><span data-stu-id="d46c8-284">231</span></span> | <span data-ttu-id="d46c8-285">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="d46c8-285">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="d46c8-286">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="d46c8-286">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="d46c8-287">More specifically:</span><span class="sxs-lookup"><span data-stu-id="d46c8-287">More specifically:</span></span>

- <span data-ttu-id="d46c8-288">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-288">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="d46c8-289">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="d46c8-289">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="d46c8-290">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span><span class="sxs-lookup"><span data-stu-id="d46c8-290">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="d46c8-291">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span><span class="sxs-lookup"><span data-stu-id="d46c8-291">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="d46c8-292">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="d46c8-292">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="d46c8-293">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span><span class="sxs-lookup"><span data-stu-id="d46c8-293">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="d46c8-294">**Note the following points:**</span><span class="sxs-lookup"><span data-stu-id="d46c8-294">**Note the following points:**</span></span>

* <span data-ttu-id="d46c8-295">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span><span class="sxs-lookup"><span data-stu-id="d46c8-295">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="d46c8-296">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span><span class="sxs-lookup"><span data-stu-id="d46c8-296">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="d46c8-297">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="d46c8-297">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="d46c8-298">If there are duplicate names at the same level, the Copy Activity picks the last one.</span><span class="sxs-lookup"><span data-stu-id="d46c8-298">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="d46c8-299">Property names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="d46c8-299">Property names are case-sensitive.</span></span> <span data-ttu-id="d46c8-300">Two properties with same name but different casings are treated as two separate properties.</span><span class="sxs-lookup"><span data-stu-id="d46c8-300">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="d46c8-301">**Case 2: Writing data to JSON file**</span><span class="sxs-lookup"><span data-stu-id="d46c8-301">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="d46c8-302">If you have the following table in SQL Database:</span><span class="sxs-lookup"><span data-stu-id="d46c8-302">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="d46c8-303">id</span><span class="sxs-lookup"><span data-stu-id="d46c8-303">id</span></span> | <span data-ttu-id="d46c8-304">order_date</span><span class="sxs-lookup"><span data-stu-id="d46c8-304">order_date</span></span> | <span data-ttu-id="d46c8-305">order_price</span><span class="sxs-lookup"><span data-stu-id="d46c8-305">order_price</span></span> | <span data-ttu-id="d46c8-306">order_by</span><span class="sxs-lookup"><span data-stu-id="d46c8-306">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d46c8-307">1</span><span class="sxs-lookup"><span data-stu-id="d46c8-307">1</span></span> | <span data-ttu-id="d46c8-308">20170119</span><span class="sxs-lookup"><span data-stu-id="d46c8-308">20170119</span></span> | <span data-ttu-id="d46c8-309">2000</span><span class="sxs-lookup"><span data-stu-id="d46c8-309">2000</span></span> | <span data-ttu-id="d46c8-310">David</span><span class="sxs-lookup"><span data-stu-id="d46c8-310">David</span></span> |
| <span data-ttu-id="d46c8-311">2</span><span class="sxs-lookup"><span data-stu-id="d46c8-311">2</span></span> | <span data-ttu-id="d46c8-312">20170120</span><span class="sxs-lookup"><span data-stu-id="d46c8-312">20170120</span></span> | <span data-ttu-id="d46c8-313">3500</span><span class="sxs-lookup"><span data-stu-id="d46c8-313">3500</span></span> | <span data-ttu-id="d46c8-314">Patrick</span><span class="sxs-lookup"><span data-stu-id="d46c8-314">Patrick</span></span> |
| <span data-ttu-id="d46c8-315">3</span><span class="sxs-lookup"><span data-stu-id="d46c8-315">3</span></span> | <span data-ttu-id="d46c8-316">20170121</span><span class="sxs-lookup"><span data-stu-id="d46c8-316">20170121</span></span> | <span data-ttu-id="d46c8-317">4000</span><span class="sxs-lookup"><span data-stu-id="d46c8-317">4000</span></span> | <span data-ttu-id="d46c8-318">Jason</span><span class="sxs-lookup"><span data-stu-id="d46c8-318">Jason</span></span> |

<span data-ttu-id="d46c8-319">and for each record, you expect to write to a JSON object in the following format:</span><span class="sxs-lookup"><span data-stu-id="d46c8-319">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="d46c8-320">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="d46c8-320">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="d46c8-321">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span><span class="sxs-lookup"><span data-stu-id="d46c8-321">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="d46c8-322">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span><span class="sxs-lookup"><span data-stu-id="d46c8-322">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="d46c8-323">AVRO format</span><span class="sxs-lookup"><span data-stu-id="d46c8-323">AVRO format</span></span>
<span data-ttu-id="d46c8-324">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-324">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="d46c8-325">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="d46c8-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="d46c8-326">Example:</span><span class="sxs-lookup"><span data-stu-id="d46c8-326">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="d46c8-327">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="d46c8-327">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="d46c8-328">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="d46c8-328">Note the following points:</span></span>  

* <span data-ttu-id="d46c8-329">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span><span class="sxs-lookup"><span data-stu-id="d46c8-329">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="d46c8-330">ORC format</span><span class="sxs-lookup"><span data-stu-id="d46c8-330">ORC format</span></span>
<span data-ttu-id="d46c8-331">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-331">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="d46c8-332">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="d46c8-332">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="d46c8-333">Example:</span><span class="sxs-lookup"><span data-stu-id="d46c8-333">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="d46c8-334">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="d46c8-334">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="d46c8-335">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="d46c8-335">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="d46c8-336">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="d46c8-336">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="d46c8-337">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="d46c8-337">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="d46c8-338">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="d46c8-338">Note the following points:</span></span>

* <span data-ttu-id="d46c8-339">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="d46c8-339">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="d46c8-340">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="d46c8-340">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="d46c8-341">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="d46c8-341">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="d46c8-342">It uses the compression codec is in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-342">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="d46c8-343">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span><span class="sxs-lookup"><span data-stu-id="d46c8-343">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="d46c8-344">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="d46c8-344">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="d46c8-345">Parquet format</span><span class="sxs-lookup"><span data-stu-id="d46c8-345">Parquet format</span></span>
<span data-ttu-id="d46c8-346">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-346">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="d46c8-347">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="d46c8-347">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="d46c8-348">Example:</span><span class="sxs-lookup"><span data-stu-id="d46c8-348">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="d46c8-349">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="d46c8-349">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="d46c8-350">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="d46c8-350">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="d46c8-351">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="d46c8-351">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="d46c8-352">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="d46c8-352">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="d46c8-353">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="d46c8-353">Note the following points:</span></span>

* <span data-ttu-id="d46c8-354">Complex data types are not supported (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="d46c8-354">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="d46c8-355">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span><span class="sxs-lookup"><span data-stu-id="d46c8-355">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="d46c8-356">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="d46c8-356">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="d46c8-357">It uses the compression codec in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-357">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="d46c8-358">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span><span class="sxs-lookup"><span data-stu-id="d46c8-358">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="d46c8-359">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="d46c8-359">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="d46c8-360">Compression support</span><span class="sxs-lookup"><span data-stu-id="d46c8-360">Compression support</span></span>
<span data-ttu-id="d46c8-361">Processing large data sets can cause I/O and network bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="d46c8-361">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="d46c8-362">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span><span class="sxs-lookup"><span data-stu-id="d46c8-362">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="d46c8-363">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span><span class="sxs-lookup"><span data-stu-id="d46c8-363">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="d46c8-364">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span><span class="sxs-lookup"><span data-stu-id="d46c8-364">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="d46c8-365">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d46c8-365">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="d46c8-366">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-366">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="d46c8-367">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span><span class="sxs-lookup"><span data-stu-id="d46c8-367">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="d46c8-368">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span><span class="sxs-lookup"><span data-stu-id="d46c8-368">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="d46c8-369">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="d46c8-369">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="d46c8-370">The **compression** section has two properties:</span><span class="sxs-lookup"><span data-stu-id="d46c8-370">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="d46c8-371">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-371">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="d46c8-372">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d46c8-372">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="d46c8-373">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span><span class="sxs-lookup"><span data-stu-id="d46c8-373">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="d46c8-374">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span><span class="sxs-lookup"><span data-stu-id="d46c8-374">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="d46c8-375">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="d46c8-375">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="d46c8-376">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span><span class="sxs-lookup"><span data-stu-id="d46c8-376">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="d46c8-377">Here are a few sample scenarios:</span><span class="sxs-lookup"><span data-stu-id="d46c8-377">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="d46c8-378">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="d46c8-378">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="d46c8-379">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span><span class="sxs-lookup"><span data-stu-id="d46c8-379">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="d46c8-380">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="d46c8-380">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="d46c8-381">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span><span class="sxs-lookup"><span data-stu-id="d46c8-381">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="d46c8-382">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d46c8-382">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="d46c8-383">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="d46c8-383">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="d46c8-384">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="d46c8-384">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="d46c8-385">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span><span class="sxs-lookup"><span data-stu-id="d46c8-385">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="d46c8-386">Next steps</span><span class="sxs-lookup"><span data-stu-id="d46c8-386">Next steps</span></span>
<span data-ttu-id="d46c8-387">See the following articles for file-based data stores supported by Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d46c8-387">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="d46c8-388">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="d46c8-388">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="d46c8-389">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d46c8-389">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="d46c8-390">FTP</span><span class="sxs-lookup"><span data-stu-id="d46c8-390">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="d46c8-391">HDFS</span><span class="sxs-lookup"><span data-stu-id="d46c8-391">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="d46c8-392">File System</span><span class="sxs-lookup"><span data-stu-id="d46c8-392">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="d46c8-393">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d46c8-393">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
