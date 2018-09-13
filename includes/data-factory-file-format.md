## <a name="specifying-formats"></a><span data-ttu-id="05f44-101">Specifying formats</span><span class="sxs-lookup"><span data-stu-id="05f44-101">Specifying formats</span></span>
<span data-ttu-id="05f44-102">Azure Data Factory supports the following format types:</span><span class="sxs-lookup"><span data-stu-id="05f44-102">Azure Data Factory supports the following format types:</span></span>

* [<span data-ttu-id="05f44-103">Text Format</span><span class="sxs-lookup"><span data-stu-id="05f44-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="05f44-104">JSON Format</span><span class="sxs-lookup"><span data-stu-id="05f44-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="05f44-105">Avro Format</span><span class="sxs-lookup"><span data-stu-id="05f44-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="05f44-106">ORC Format</span><span class="sxs-lookup"><span data-stu-id="05f44-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="05f44-107">Parquet Format</span><span class="sxs-lookup"><span data-stu-id="05f44-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="05f44-108">Specifying TextFormat</span><span class="sxs-lookup"><span data-stu-id="05f44-108">Specifying TextFormat</span></span>
<span data-ttu-id="05f44-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="05f44-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="05f44-110">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="05f44-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="05f44-111">See [TextFormat example](#textformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="05f44-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="05f44-112">Property</span><span class="sxs-lookup"><span data-stu-id="05f44-112">Property</span></span> | <span data-ttu-id="05f44-113">Description</span><span class="sxs-lookup"><span data-stu-id="05f44-113">Description</span></span> | <span data-ttu-id="05f44-114">Allowed values</span><span class="sxs-lookup"><span data-stu-id="05f44-114">Allowed values</span></span> | <span data-ttu-id="05f44-115">Required</span><span class="sxs-lookup"><span data-stu-id="05f44-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="05f44-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="05f44-116">columnDelimiter</span></span> |<span data-ttu-id="05f44-117">The character used to separate columns in a file.</span><span class="sxs-lookup"><span data-stu-id="05f44-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="05f44-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span><span class="sxs-lookup"><span data-stu-id="05f44-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="05f44-119">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="05f44-119">Only one character is allowed.</span></span> <span data-ttu-id="05f44-120">The **default** value is **comma (',')**.</span><span class="sxs-lookup"><span data-stu-id="05f44-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="05f44-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span><span class="sxs-lookup"><span data-stu-id="05f44-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="05f44-122">No</span><span class="sxs-lookup"><span data-stu-id="05f44-122">No</span></span> |
| <span data-ttu-id="05f44-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="05f44-123">rowDelimiter</span></span> |<span data-ttu-id="05f44-124">The character used to separate rows in a file.</span><span class="sxs-lookup"><span data-stu-id="05f44-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="05f44-125">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="05f44-125">Only one character is allowed.</span></span> <span data-ttu-id="05f44-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span><span class="sxs-lookup"><span data-stu-id="05f44-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="05f44-127">No</span><span class="sxs-lookup"><span data-stu-id="05f44-127">No</span></span> |
| <span data-ttu-id="05f44-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="05f44-128">escapeChar</span></span> |<span data-ttu-id="05f44-129">The special character used to escape a column delimiter in the content of input file.</span><span class="sxs-lookup"><span data-stu-id="05f44-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="05f44-130">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="05f44-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="05f44-131">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="05f44-131">Only one character is allowed.</span></span> <span data-ttu-id="05f44-132">No default value.</span><span class="sxs-lookup"><span data-stu-id="05f44-132">No default value.</span></span> <br/><br/><span data-ttu-id="05f44-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="05f44-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="05f44-134">No</span><span class="sxs-lookup"><span data-stu-id="05f44-134">No</span></span> |
| <span data-ttu-id="05f44-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="05f44-135">quoteChar</span></span> |<span data-ttu-id="05f44-136">The character used to quote a string value.</span><span class="sxs-lookup"><span data-stu-id="05f44-136">The character used to quote a string value.</span></span> <span data-ttu-id="05f44-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span><span class="sxs-lookup"><span data-stu-id="05f44-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="05f44-138">This property is applicable to both input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="05f44-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="05f44-139">You cannot specify both escapeChar and quoteChar for a table.</span><span class="sxs-lookup"><span data-stu-id="05f44-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="05f44-140">Only one character is allowed.</span><span class="sxs-lookup"><span data-stu-id="05f44-140">Only one character is allowed.</span></span> <span data-ttu-id="05f44-141">No default value.</span><span class="sxs-lookup"><span data-stu-id="05f44-141">No default value.</span></span> <br/><br/><span data-ttu-id="05f44-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span><span class="sxs-lookup"><span data-stu-id="05f44-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="05f44-143">No</span><span class="sxs-lookup"><span data-stu-id="05f44-143">No</span></span> |
| <span data-ttu-id="05f44-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="05f44-144">nullValue</span></span> |<span data-ttu-id="05f44-145">One or more characters used to represent a null value.</span><span class="sxs-lookup"><span data-stu-id="05f44-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="05f44-146">One or more characters.</span><span class="sxs-lookup"><span data-stu-id="05f44-146">One or more characters.</span></span> <span data-ttu-id="05f44-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span><span class="sxs-lookup"><span data-stu-id="05f44-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="05f44-148">No</span><span class="sxs-lookup"><span data-stu-id="05f44-148">No</span></span> |
| <span data-ttu-id="05f44-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="05f44-149">encodingName</span></span> |<span data-ttu-id="05f44-150">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="05f44-150">Specify the encoding name.</span></span> |<span data-ttu-id="05f44-151">A valid encoding name.</span><span class="sxs-lookup"><span data-stu-id="05f44-151">A valid encoding name.</span></span> <span data-ttu-id="05f44-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="05f44-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="05f44-153">Example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="05f44-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="05f44-154">The **default** value is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="05f44-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="05f44-155">No</span><span class="sxs-lookup"><span data-stu-id="05f44-155">No</span></span> |
| <span data-ttu-id="05f44-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="05f44-156">firstRowAsHeader</span></span> |<span data-ttu-id="05f44-157">Specifies whether to consider the first row as a header.</span><span class="sxs-lookup"><span data-stu-id="05f44-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="05f44-158">For an input dataset, Data Factory reads first row as a header.</span><span class="sxs-lookup"><span data-stu-id="05f44-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="05f44-159">For an output dataset, Data Factory writes first row as a header.</span><span class="sxs-lookup"><span data-stu-id="05f44-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="05f44-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="05f44-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="05f44-161">True</span><span class="sxs-lookup"><span data-stu-id="05f44-161">True</span></span><br/><span data-ttu-id="05f44-162">**False (default)**</span><span class="sxs-lookup"><span data-stu-id="05f44-162">**False (default)**</span></span> |<span data-ttu-id="05f44-163">No</span><span class="sxs-lookup"><span data-stu-id="05f44-163">No</span></span> |
| <span data-ttu-id="05f44-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="05f44-164">skipLineCount</span></span> |<span data-ttu-id="05f44-165">Indicates the number of rows to skip when reading data from input files.</span><span class="sxs-lookup"><span data-stu-id="05f44-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="05f44-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span><span class="sxs-lookup"><span data-stu-id="05f44-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="05f44-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span><span class="sxs-lookup"><span data-stu-id="05f44-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="05f44-168">Integer</span><span class="sxs-lookup"><span data-stu-id="05f44-168">Integer</span></span> |<span data-ttu-id="05f44-169">No</span><span class="sxs-lookup"><span data-stu-id="05f44-169">No</span></span> |
| <span data-ttu-id="05f44-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="05f44-170">treatEmptyAsNull</span></span> |<span data-ttu-id="05f44-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span><span class="sxs-lookup"><span data-stu-id="05f44-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="05f44-172">**True (default)**</span><span class="sxs-lookup"><span data-stu-id="05f44-172">**True (default)**</span></span><br/><span data-ttu-id="05f44-173">False</span><span class="sxs-lookup"><span data-stu-id="05f44-173">False</span></span> |<span data-ttu-id="05f44-174">No</span><span class="sxs-lookup"><span data-stu-id="05f44-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="05f44-175">TextFormat example</span><span class="sxs-lookup"><span data-stu-id="05f44-175">TextFormat example</span></span>
<span data-ttu-id="05f44-176">The following sample shows some of the format properties for TextFormat.</span><span class="sxs-lookup"><span data-stu-id="05f44-176">The following sample shows some of the format properties for TextFormat.</span></span>

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

<span data-ttu-id="05f44-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span><span class="sxs-lookup"><span data-stu-id="05f44-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="05f44-178">Scenarios for using firstRowAsHeader and skipLineCount</span><span class="sxs-lookup"><span data-stu-id="05f44-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="05f44-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span><span class="sxs-lookup"><span data-stu-id="05f44-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="05f44-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span><span class="sxs-lookup"><span data-stu-id="05f44-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="05f44-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span><span class="sxs-lookup"><span data-stu-id="05f44-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="05f44-182">Specify `firstRowAsHeader` as true in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="05f44-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="05f44-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span><span class="sxs-lookup"><span data-stu-id="05f44-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="05f44-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span><span class="sxs-lookup"><span data-stu-id="05f44-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="05f44-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="05f44-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="05f44-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span><span class="sxs-lookup"><span data-stu-id="05f44-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="05f44-187">Specifying JsonFormat</span><span class="sxs-lookup"><span data-stu-id="05f44-187">Specifying JsonFormat</span></span>
<span data-ttu-id="05f44-188">To **import/export JSON files as-is into/from DocumentDB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in DocumentDB connector with details.</span><span class="sxs-lookup"><span data-stu-id="05f44-188">To **import/export JSON files as-is into/from DocumentDB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in DocumentDB connector with details.</span></span>

<span data-ttu-id="05f44-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="05f44-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="05f44-190">You can also specify the following **optional** properties in the `format` section.</span><span class="sxs-lookup"><span data-stu-id="05f44-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="05f44-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="05f44-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="05f44-192">Property</span><span class="sxs-lookup"><span data-stu-id="05f44-192">Property</span></span> | <span data-ttu-id="05f44-193">Description</span><span class="sxs-lookup"><span data-stu-id="05f44-193">Description</span></span> | <span data-ttu-id="05f44-194">Required</span><span class="sxs-lookup"><span data-stu-id="05f44-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05f44-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="05f44-195">filePattern</span></span> |<span data-ttu-id="05f44-196">Indicate the pattern of data stored in each JSON file.</span><span class="sxs-lookup"><span data-stu-id="05f44-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="05f44-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="05f44-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="05f44-198">The **default** value is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="05f44-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="05f44-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span><span class="sxs-lookup"><span data-stu-id="05f44-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="05f44-200">No</span><span class="sxs-lookup"><span data-stu-id="05f44-200">No</span></span> |
| <span data-ttu-id="05f44-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="05f44-201">jsonNodeReference</span></span> | <span data-ttu-id="05f44-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span><span class="sxs-lookup"><span data-stu-id="05f44-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="05f44-203">This property is supported only when copying data from JSON files.</span><span class="sxs-lookup"><span data-stu-id="05f44-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="05f44-204">No</span><span class="sxs-lookup"><span data-stu-id="05f44-204">No</span></span> |
| <span data-ttu-id="05f44-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="05f44-205">jsonPathDefinition</span></span> | <span data-ttu-id="05f44-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span><span class="sxs-lookup"><span data-stu-id="05f44-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="05f44-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span><span class="sxs-lookup"><span data-stu-id="05f44-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="05f44-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span><span class="sxs-lookup"><span data-stu-id="05f44-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="05f44-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span><span class="sxs-lookup"><span data-stu-id="05f44-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="05f44-210">No</span><span class="sxs-lookup"><span data-stu-id="05f44-210">No</span></span> |
| <span data-ttu-id="05f44-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="05f44-211">encodingName</span></span> |<span data-ttu-id="05f44-212">Specify the encoding name.</span><span class="sxs-lookup"><span data-stu-id="05f44-212">Specify the encoding name.</span></span> <span data-ttu-id="05f44-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span><span class="sxs-lookup"><span data-stu-id="05f44-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="05f44-214">For example: windows-1250 or shift_jis.</span><span class="sxs-lookup"><span data-stu-id="05f44-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="05f44-215">The **default** value is: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="05f44-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="05f44-216">No</span><span class="sxs-lookup"><span data-stu-id="05f44-216">No</span></span> |
| <span data-ttu-id="05f44-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="05f44-217">nestingSeparator</span></span> |<span data-ttu-id="05f44-218">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="05f44-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="05f44-219">The default value is '.' (dot).</span><span class="sxs-lookup"><span data-stu-id="05f44-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="05f44-220">No</span><span class="sxs-lookup"><span data-stu-id="05f44-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="05f44-221">JSON file patterns</span><span class="sxs-lookup"><span data-stu-id="05f44-221">JSON file patterns</span></span>

<span data-ttu-id="05f44-222">Copy activity can parse below patterns of JSON files:</span><span class="sxs-lookup"><span data-stu-id="05f44-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="05f44-223">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="05f44-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="05f44-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span><span class="sxs-lookup"><span data-stu-id="05f44-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="05f44-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span><span class="sxs-lookup"><span data-stu-id="05f44-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="05f44-226">**single object JSON example**</span><span class="sxs-lookup"><span data-stu-id="05f44-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="05f44-227">**line-delimited JSON example**</span><span class="sxs-lookup"><span data-stu-id="05f44-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="05f44-228">**concatenated JSON example**</span><span class="sxs-lookup"><span data-stu-id="05f44-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="05f44-229">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="05f44-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="05f44-230">Each file contains an array of objects.</span><span class="sxs-lookup"><span data-stu-id="05f44-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="05f44-231">JsonFormat example</span><span class="sxs-lookup"><span data-stu-id="05f44-231">JsonFormat example</span></span>

<span data-ttu-id="05f44-232">**Case 1: Copying data from JSON files**</span><span class="sxs-lookup"><span data-stu-id="05f44-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="05f44-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span><span class="sxs-lookup"><span data-stu-id="05f44-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="05f44-234">**Sample 1: extract data from object and array**</span><span class="sxs-lookup"><span data-stu-id="05f44-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="05f44-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span><span class="sxs-lookup"><span data-stu-id="05f44-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="05f44-236">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="05f44-236">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="05f44-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span><span class="sxs-lookup"><span data-stu-id="05f44-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="05f44-238">id</span><span class="sxs-lookup"><span data-stu-id="05f44-238">id</span></span> | <span data-ttu-id="05f44-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="05f44-239">deviceType</span></span> | <span data-ttu-id="05f44-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="05f44-240">targetResourceType</span></span> | <span data-ttu-id="05f44-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="05f44-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="05f44-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="05f44-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="05f44-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="05f44-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="05f44-244">PC</span><span class="sxs-lookup"><span data-stu-id="05f44-244">PC</span></span> | <span data-ttu-id="05f44-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="05f44-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="05f44-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="05f44-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="05f44-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="05f44-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="05f44-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="05f44-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="05f44-249">More specifically:</span><span class="sxs-lookup"><span data-stu-id="05f44-249">More specifically:</span></span>

- <span data-ttu-id="05f44-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="05f44-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="05f44-251">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="05f44-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="05f44-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span><span class="sxs-lookup"><span data-stu-id="05f44-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="05f44-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="05f44-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="05f44-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span><span class="sxs-lookup"><span data-stu-id="05f44-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[\*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="05f44-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span><span class="sxs-lookup"><span data-stu-id="05f44-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="05f44-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span><span class="sxs-lookup"><span data-stu-id="05f44-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="05f44-257">If you have a JSON file with the following content:</span><span class="sxs-lookup"><span data-stu-id="05f44-257">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="05f44-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span><span class="sxs-lookup"><span data-stu-id="05f44-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="05f44-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="05f44-259">ordernumber</span></span> | <span data-ttu-id="05f44-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="05f44-260">orderdate</span></span> | <span data-ttu-id="05f44-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="05f44-261">order_pd</span></span> | <span data-ttu-id="05f44-262">order_price</span><span class="sxs-lookup"><span data-stu-id="05f44-262">order_price</span></span> | <span data-ttu-id="05f44-263">city</span><span class="sxs-lookup"><span data-stu-id="05f44-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="05f44-264">01</span><span class="sxs-lookup"><span data-stu-id="05f44-264">01</span></span> | <span data-ttu-id="05f44-265">20170122</span><span class="sxs-lookup"><span data-stu-id="05f44-265">20170122</span></span> | <span data-ttu-id="05f44-266">P1</span><span class="sxs-lookup"><span data-stu-id="05f44-266">P1</span></span> | <span data-ttu-id="05f44-267">23</span><span class="sxs-lookup"><span data-stu-id="05f44-267">23</span></span> | <span data-ttu-id="05f44-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="05f44-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="05f44-269">01</span><span class="sxs-lookup"><span data-stu-id="05f44-269">01</span></span> | <span data-ttu-id="05f44-270">20170122</span><span class="sxs-lookup"><span data-stu-id="05f44-270">20170122</span></span> | <span data-ttu-id="05f44-271">P2</span><span class="sxs-lookup"><span data-stu-id="05f44-271">P2</span></span> | <span data-ttu-id="05f44-272">13</span><span class="sxs-lookup"><span data-stu-id="05f44-272">13</span></span> | <span data-ttu-id="05f44-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="05f44-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="05f44-274">01</span><span class="sxs-lookup"><span data-stu-id="05f44-274">01</span></span> | <span data-ttu-id="05f44-275">20170122</span><span class="sxs-lookup"><span data-stu-id="05f44-275">20170122</span></span> | <span data-ttu-id="05f44-276">P3</span><span class="sxs-lookup"><span data-stu-id="05f44-276">P3</span></span> | <span data-ttu-id="05f44-277">231</span><span class="sxs-lookup"><span data-stu-id="05f44-277">231</span></span> | <span data-ttu-id="05f44-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="05f44-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="05f44-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="05f44-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="05f44-280">More specifically:</span><span class="sxs-lookup"><span data-stu-id="05f44-280">More specifically:</span></span>

- <span data-ttu-id="05f44-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span><span class="sxs-lookup"><span data-stu-id="05f44-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="05f44-282">This section is **optional** unless you need to do column mapping.</span><span class="sxs-lookup"><span data-stu-id="05f44-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="05f44-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span><span class="sxs-lookup"><span data-stu-id="05f44-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="05f44-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span><span class="sxs-lookup"><span data-stu-id="05f44-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="05f44-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span><span class="sxs-lookup"><span data-stu-id="05f44-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="05f44-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span><span class="sxs-lookup"><span data-stu-id="05f44-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="05f44-287">**Note the following points:**</span><span class="sxs-lookup"><span data-stu-id="05f44-287">**Note the following points:**</span></span>

* <span data-ttu-id="05f44-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span><span class="sxs-lookup"><span data-stu-id="05f44-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="05f44-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span><span class="sxs-lookup"><span data-stu-id="05f44-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="05f44-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="05f44-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="05f44-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span><span class="sxs-lookup"><span data-stu-id="05f44-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="05f44-292">Property names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="05f44-292">Property names are case-sensitive.</span></span> <span data-ttu-id="05f44-293">Two properties with same name but different casings are treated as two separate properties.</span><span class="sxs-lookup"><span data-stu-id="05f44-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="05f44-294">**Case 2: Writing data to JSON file**</span><span class="sxs-lookup"><span data-stu-id="05f44-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="05f44-295">If you have below table in SQL Database:</span><span class="sxs-lookup"><span data-stu-id="05f44-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="05f44-296">id</span><span class="sxs-lookup"><span data-stu-id="05f44-296">id</span></span> | <span data-ttu-id="05f44-297">order_date</span><span class="sxs-lookup"><span data-stu-id="05f44-297">order_date</span></span> | <span data-ttu-id="05f44-298">order_price</span><span class="sxs-lookup"><span data-stu-id="05f44-298">order_price</span></span> | <span data-ttu-id="05f44-299">order_by</span><span class="sxs-lookup"><span data-stu-id="05f44-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="05f44-300">1</span><span class="sxs-lookup"><span data-stu-id="05f44-300">1</span></span> | <span data-ttu-id="05f44-301">20170119</span><span class="sxs-lookup"><span data-stu-id="05f44-301">20170119</span></span> | <span data-ttu-id="05f44-302">2000</span><span class="sxs-lookup"><span data-stu-id="05f44-302">2000</span></span> | <span data-ttu-id="05f44-303">David</span><span class="sxs-lookup"><span data-stu-id="05f44-303">David</span></span> |
| <span data-ttu-id="05f44-304">2</span><span class="sxs-lookup"><span data-stu-id="05f44-304">2</span></span> | <span data-ttu-id="05f44-305">20170120</span><span class="sxs-lookup"><span data-stu-id="05f44-305">20170120</span></span> | <span data-ttu-id="05f44-306">3500</span><span class="sxs-lookup"><span data-stu-id="05f44-306">3500</span></span> | <span data-ttu-id="05f44-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="05f44-307">Patrick</span></span> |
| <span data-ttu-id="05f44-308">3</span><span class="sxs-lookup"><span data-stu-id="05f44-308">3</span></span> | <span data-ttu-id="05f44-309">20170121</span><span class="sxs-lookup"><span data-stu-id="05f44-309">20170121</span></span> | <span data-ttu-id="05f44-310">4000</span><span class="sxs-lookup"><span data-stu-id="05f44-310">4000</span></span> | <span data-ttu-id="05f44-311">Jason</span><span class="sxs-lookup"><span data-stu-id="05f44-311">Jason</span></span> |

<span data-ttu-id="05f44-312">and for each record, you expect to write to a JSON object in below format:</span><span class="sxs-lookup"><span data-stu-id="05f44-312">and for each record, you expect to write to a JSON object in below format:</span></span>
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

<span data-ttu-id="05f44-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span><span class="sxs-lookup"><span data-stu-id="05f44-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="05f44-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span><span class="sxs-lookup"><span data-stu-id="05f44-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="05f44-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span><span class="sxs-lookup"><span data-stu-id="05f44-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="05f44-316">Specifying AvroFormat</span><span class="sxs-lookup"><span data-stu-id="05f44-316">Specifying AvroFormat</span></span>
<span data-ttu-id="05f44-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="05f44-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="05f44-318">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="05f44-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="05f44-319">Example:</span><span class="sxs-lookup"><span data-stu-id="05f44-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="05f44-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="05f44-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="05f44-321">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="05f44-321">Note the following points:</span></span>  

* <span data-ttu-id="05f44-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span><span class="sxs-lookup"><span data-stu-id="05f44-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="05f44-323">Specifying OrcFormat</span><span class="sxs-lookup"><span data-stu-id="05f44-323">Specifying OrcFormat</span></span>
<span data-ttu-id="05f44-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="05f44-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="05f44-325">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="05f44-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="05f44-326">Example:</span><span class="sxs-lookup"><span data-stu-id="05f44-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="05f44-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="05f44-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="05f44-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="05f44-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="05f44-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="05f44-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="05f44-330">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="05f44-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="05f44-331">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="05f44-331">Note the following points:</span></span>

* <span data-ttu-id="05f44-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="05f44-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="05f44-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="05f44-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="05f44-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="05f44-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="05f44-335">It uses the compression codec is in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="05f44-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="05f44-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span><span class="sxs-lookup"><span data-stu-id="05f44-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="05f44-337">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="05f44-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="05f44-338">Specifying ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="05f44-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="05f44-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="05f44-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="05f44-340">You do not need to specify any properties in the Format section within the typeProperties section.</span><span class="sxs-lookup"><span data-stu-id="05f44-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="05f44-341">Example:</span><span class="sxs-lookup"><span data-stu-id="05f44-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="05f44-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="05f44-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="05f44-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span><span class="sxs-lookup"><span data-stu-id="05f44-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="05f44-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="05f44-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="05f44-345">Choose the appropriate one.</span><span class="sxs-lookup"><span data-stu-id="05f44-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="05f44-346">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="05f44-346">Note the following points:</span></span>

* <span data-ttu-id="05f44-347">Complex data types are not supported (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="05f44-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="05f44-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span><span class="sxs-lookup"><span data-stu-id="05f44-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="05f44-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span><span class="sxs-lookup"><span data-stu-id="05f44-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="05f44-350">It uses the compression codec in the metadata to read the data.</span><span class="sxs-lookup"><span data-stu-id="05f44-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="05f44-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span><span class="sxs-lookup"><span data-stu-id="05f44-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="05f44-352">Currently, there is no option to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="05f44-352">Currently, there is no option to override this behavior.</span></span>
