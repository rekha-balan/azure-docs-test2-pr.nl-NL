---
title: U-SQL programmability guide for Azure Data Lake | Microsoft Docs
description: Learn about the set of services in Azure Data Lake that enable you to create a cloud-based big data platform.
services: data-lake-analytics
documentationcenter: ''
author: MikeRys
manager: arindamc
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: mrys
ms.openlocfilehash: 55af8efb79f7e270377aca3b2372c12b9df380a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563985"
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="e05cc-103">U-SQL programmability guide</span><span class="sxs-lookup"><span data-stu-id="e05cc-103">U-SQL programmability guide</span></span>
## <a name="azure-data-lake"></a><span data-ttu-id="e05cc-104">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e05cc-104">Azure Data Lake</span></span>
<span data-ttu-id="e05cc-105">Azure Data Lake includes capabilities that make it easy for developers, data scientists, and analysts to store data of any size, shape, and speed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-105">Azure Data Lake includes capabilities that make it easy for developers, data scientists, and analysts to store data of any size, shape, and speed.</span></span> <span data-ttu-id="e05cc-106">It also enables developers to use many types of processing and analytics across platforms and languages.</span><span class="sxs-lookup"><span data-stu-id="e05cc-106">It also enables developers to use many types of processing and analytics across platforms and languages.</span></span> <span data-ttu-id="e05cc-107">It removes the complexities of ingesting and storing all your data while making it faster to use batches, streaming, and interactive analytics.</span><span class="sxs-lookup"><span data-stu-id="e05cc-107">It removes the complexities of ingesting and storing all your data while making it faster to use batches, streaming, and interactive analytics.</span></span>

<span data-ttu-id="e05cc-108">Azure Data Lake is a set of services that work together to provide a cloud-based big data platform.</span><span class="sxs-lookup"><span data-stu-id="e05cc-108">Azure Data Lake is a set of services that work together to provide a cloud-based big data platform.</span></span> <span data-ttu-id="e05cc-109">These services include:</span><span class="sxs-lookup"><span data-stu-id="e05cc-109">These services include:</span></span>

- <span data-ttu-id="e05cc-110">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e05cc-110">Azure HDInsight</span></span>
- <span data-ttu-id="e05cc-111">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e05cc-111">Azure Data Lake Store</span></span>
- <span data-ttu-id="e05cc-112">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e05cc-112">Azure Data Lake Analytics</span></span>

<span data-ttu-id="e05cc-113">U-SQL is a query language that's designed for big data-type of workloads.</span><span class="sxs-lookup"><span data-stu-id="e05cc-113">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="e05cc-114">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span><span class="sxs-lookup"><span data-stu-id="e05cc-114">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="e05cc-115">It also provides the ability to access and manipulate schema metadata, and to create custom components such as data processors and reducers.</span><span class="sxs-lookup"><span data-stu-id="e05cc-115">It also provides the ability to access and manipulate schema metadata, and to create custom components such as data processors and reducers.</span></span>

<span data-ttu-id="e05cc-116">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span><span class="sxs-lookup"><span data-stu-id="e05cc-116">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="e05cc-117">Requirements</span><span class="sxs-lookup"><span data-stu-id="e05cc-117">Requirements</span></span>
<span data-ttu-id="e05cc-118">To begin with Azure Data Lake development, you need to download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="e05cc-118">To begin with Azure Data Lake development, you need to download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="e05cc-119">Get started with U-SQL</span><span class="sxs-lookup"><span data-stu-id="e05cc-119">Get started with U-SQL</span></span>  
<span data-ttu-id="e05cc-120">The description of U-SQL language is outside the scope of this document.</span><span class="sxs-lookup"><span data-stu-id="e05cc-120">The description of U-SQL language is outside the scope of this document.</span></span> <span data-ttu-id="e05cc-121">However, we describe basic U-SQL constructs to gradually introduce U-SQL programmability features.</span><span class="sxs-lookup"><span data-stu-id="e05cc-121">However, we describe basic U-SQL constructs to gradually introduce U-SQL programmability features.</span></span> <span data-ttu-id="e05cc-122">For more information, see the [U-SQL Language Reference](http://aka.ms/usql_reference) guide.</span><span class="sxs-lookup"><span data-stu-id="e05cc-122">For more information, see the [U-SQL Language Reference](http://aka.ms/usql_reference) guide.</span></span>

<span data-ttu-id="e05cc-123">Let’s look at the following example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-123">Let’s look at the following example:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-124">In this example, we have an **Input File**: file input_file.tsv, defined by **Local Variable** @input_file.</span><span class="sxs-lookup"><span data-stu-id="e05cc-124">In this example, we have an **Input File**: file input_file.tsv, defined by **Local Variable** @input_file.</span></span>

<span data-ttu-id="e05cc-125">The following actions are performed by the U-SQL script show in this example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-125">The following actions are performed by the U-SQL script show in this example:</span></span>

* <span data-ttu-id="e05cc-126">The initial **EXTRACT** statement loads data to memory by converting Input File to the **Memory RowSet**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-126">The initial **EXTRACT** statement loads data to memory by converting Input File to the **Memory RowSet**.</span></span>
* <span data-ttu-id="e05cc-127">**SELECT** operates on data rowset to aggregate data and prepare for exporting.</span><span class="sxs-lookup"><span data-stu-id="e05cc-127">**SELECT** operates on data rowset to aggregate data and prepare for exporting.</span></span>
* <span data-ttu-id="e05cc-128">**OUTPUT** exports data rowset to **Output File**, which is an external file.</span><span class="sxs-lookup"><span data-stu-id="e05cc-128">**OUTPUT** exports data rowset to **Output File**, which is an external file.</span></span>

<span data-ttu-id="e05cc-129">First, let’s look at some options for using a C# expression directly in a U-SQL Script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-129">First, let’s look at some options for using a C# expression directly in a U-SQL Script.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="e05cc-130">C# types and expressions in U-SQL script</span><span class="sxs-lookup"><span data-stu-id="e05cc-130">C# types and expressions in U-SQL script</span></span>
<span data-ttu-id="e05cc-131">A U-SQL C# expression, similar to an expression in general C#, is a sequence of one or more operators that can be evaluated to a single value, object, method, or namespace.</span><span class="sxs-lookup"><span data-stu-id="e05cc-131">A U-SQL C# expression, similar to an expression in general C#, is a sequence of one or more operators that can be evaluated to a single value, object, method, or namespace.</span></span> <span data-ttu-id="e05cc-132">Expressions can consist of a literal value, a method invocation, an operator, or a simple name.</span><span class="sxs-lookup"><span data-stu-id="e05cc-132">Expressions can consist of a literal value, a method invocation, an operator, or a simple name.</span></span> <span data-ttu-id="e05cc-133">Simple names can be the name of a variable, type member, method parameter, namespace, or type.</span><span class="sxs-lookup"><span data-stu-id="e05cc-133">Simple names can be the name of a variable, type member, method parameter, namespace, or type.</span></span>

<span data-ttu-id="e05cc-134">When we talk about U-SQL C# expressions, we specifically refer to the U-SQL base script C# expressions.</span><span class="sxs-lookup"><span data-stu-id="e05cc-134">When we talk about U-SQL C# expressions, we specifically refer to the U-SQL base script C# expressions.</span></span> <span data-ttu-id="e05cc-135">The underlying C# code-behind section, discussed later in this document, can also contain C# expressions as regular C# code-based elements.</span><span class="sxs-lookup"><span data-stu-id="e05cc-135">The underlying C# code-behind section, discussed later in this document, can also contain C# expressions as regular C# code-based elements.</span></span>

<span data-ttu-id="e05cc-136">Expressions can use operators that use other expressions as parameters.</span><span class="sxs-lookup"><span data-stu-id="e05cc-136">Expressions can use operators that use other expressions as parameters.</span></span> <span data-ttu-id="e05cc-137">They can also use method calls with parameters that are other method calls.</span><span class="sxs-lookup"><span data-stu-id="e05cc-137">They can also use method calls with parameters that are other method calls.</span></span> <span data-ttu-id="e05cc-138">Following are examples of an expression:</span><span class="sxs-lookup"><span data-stu-id="e05cc-138">Following are examples of an expression:</span></span>  

```c#
    Convert.ToDateTime(Convert.ToDateTime(dt).ToString("yyyy-MM-dd"))
```

<span data-ttu-id="e05cc-139">U-SQL language enables the usage of standard C# expressions from built-in namespaces.</span><span class="sxs-lookup"><span data-stu-id="e05cc-139">U-SQL language enables the usage of standard C# expressions from built-in namespaces.</span></span>  

```c#
    Microsoft.Analytics.Interfaces;  
    Microsoft.Analytics.Types.Sql;  
    System;  
    System.Collections.Generic;  
    System.Linq;  
    System.Text;  
```

<span data-ttu-id="e05cc-140">General C# expressions can be used in U-SQL SELECT, EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="e05cc-140">General C# expressions can be used in U-SQL SELECT, EXTRACT.</span></span>

<span data-ttu-id="e05cc-141">The C# expressions can also be used in DECLARE or IF statements.</span><span class="sxs-lookup"><span data-stu-id="e05cc-141">The C# expressions can also be used in DECLARE or IF statements.</span></span> <span data-ttu-id="e05cc-142">An example of this type of expression is as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-142">An example of this type of expression is as follows:</span></span>   

```c#
    DateTime.Today.Day   
    Convert.ToDateTime
```

<span data-ttu-id="e05cc-143">U-SQL-based script example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-143">U-SQL-based script example:</span></span>  

```sql
    DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");
```

<span data-ttu-id="e05cc-144">C# expressions can provide extended functionality when you're manipulating columns as part of a rowset.</span><span class="sxs-lookup"><span data-stu-id="e05cc-144">C# expressions can provide extended functionality when you're manipulating columns as part of a rowset.</span></span> <span data-ttu-id="e05cc-145">For example, if you want to convert a datetime column to the date with zero hours, you can use the following SELECT part of a U-SQL-based script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-145">For example, if you want to convert a datetime column to the date with zero hours, you can use the following SELECT part of a U-SQL-based script:</span></span>

```sql
@rs1 =
    SELECT
        MAX(guid) AS start_id,
     MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt).ToString("yyyy-MM-dd")))
AS start_zero_time,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```

<span data-ttu-id="e05cc-146">As you can see, we use `System.Convert.ToDateTime` method to run through the conversion.</span><span class="sxs-lookup"><span data-stu-id="e05cc-146">As you can see, we use `System.Convert.ToDateTime` method to run through the conversion.</span></span>

<span data-ttu-id="e05cc-147">Following is a slightly more complicated scenario that demonstrates the use of some basic C# operators:</span><span class="sxs-lookup"><span data-stu-id="e05cc-147">Following is a slightly more complicated scenario that demonstrates the use of some basic C# operators:</span></span>

```sql
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
          MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```

<span data-ttu-id="e05cc-148">This shows an example of a C# conditional operator expression.</span><span class="sxs-lookup"><span data-stu-id="e05cc-148">This shows an example of a C# conditional operator expression.</span></span>

<span data-ttu-id="e05cc-149">The previous examples demonstrate the use of C# expressions in the base U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-149">The previous examples demonstrate the use of C# expressions in the base U-SQL script.</span></span> <span data-ttu-id="e05cc-150">However, U-SQL enables more extensible programmability features that are covered later in this document.</span><span class="sxs-lookup"><span data-stu-id="e05cc-150">However, U-SQL enables more extensible programmability features that are covered later in this document.</span></span>  

<span data-ttu-id="e05cc-151">Full script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-151">Full script:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="e05cc-152">Use C# expressions for data type conversions</span><span class="sxs-lookup"><span data-stu-id="e05cc-152">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="e05cc-153">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span><span class="sxs-lookup"><span data-stu-id="e05cc-153">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="e05cc-154">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span><span class="sxs-lookup"><span data-stu-id="e05cc-154">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```sql
DECLARE @dt String = "2016-07-06 10:23:15";
@rs1 =
    SELECT Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
           dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="e05cc-155">Use C# expressions for today’s date</span><span class="sxs-lookup"><span data-stu-id="e05cc-155">Use C# expressions for today’s date</span></span>
<span data-ttu-id="e05cc-156">To pull today’s date, we can use the following C# expression:</span><span class="sxs-lookup"><span data-stu-id="e05cc-156">To pull today’s date, we can use the following C# expression:</span></span>

```c#
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="e05cc-157">Here's an example of how to use this expression in a script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-157">Here's an example of how to use this expression in a script:</span></span>

```sql
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```

## <a name="use-inline-c-function-expressions"></a><span data-ttu-id="e05cc-158">Use inline C# function expressions</span><span class="sxs-lookup"><span data-stu-id="e05cc-158">Use inline C# function expressions</span></span>
<span data-ttu-id="e05cc-159">U-SQL allows the use of inline function expressions definition as part of C# expressions.</span><span class="sxs-lookup"><span data-stu-id="e05cc-159">U-SQL allows the use of inline function expressions definition as part of C# expressions.</span></span> <span data-ttu-id="e05cc-160">This creates additional possibilities for using C# functions with output reference parameters.</span><span class="sxs-lookup"><span data-stu-id="e05cc-160">This creates additional possibilities for using C# functions with output reference parameters.</span></span>

<span data-ttu-id="e05cc-161">Following is an example of a general inline function expression definition:</span><span class="sxs-lookup"><span data-stu-id="e05cc-161">Following is an example of a general inline function expression definition:</span></span>

```c#
    (Func<type of param1, type of param2>)
    (param1 =>
         { … return param2}
    ) (Rowset Column)
```

<span data-ttu-id="e05cc-162">Example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-162">Example:</span></span>

```c#
    (Func<string, DateTime?>)
    (input_p =>
         {
            DateTime dt_result;
            return DateTime.TryParse(input_p, out dt_result)
                   ? (DateTime?) dt_result : (DateTime?) null;
         }
    )
    ) (dt)
```

<span data-ttu-id="e05cc-163">In this example, we define an inline function with the string input parameter input_p.</span><span class="sxs-lookup"><span data-stu-id="e05cc-163">In this example, we define an inline function with the string input parameter input_p.</span></span> <span data-ttu-id="e05cc-164">Inside this function, we verify if input string is a valid datetime value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-164">Inside this function, we verify if input string is a valid datetime value.</span></span> <span data-ttu-id="e05cc-165">If it is, return it, otherwise return null.</span><span class="sxs-lookup"><span data-stu-id="e05cc-165">If it is, return it, otherwise return null.</span></span>

<span data-ttu-id="e05cc-166">The inline function is needed in this scenario because the DateTime.TryParse function contains the output parameter `out dt_result`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-166">The inline function is needed in this scenario because the DateTime.TryParse function contains the output parameter `out dt_result`.</span></span> <span data-ttu-id="e05cc-167">We define it as the `DateTime dt_result;`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-167">We define it as the `DateTime dt_result;`.</span></span>


## <a name="verify-data-type-values"></a><span data-ttu-id="e05cc-168">Verify data type values</span><span class="sxs-lookup"><span data-stu-id="e05cc-168">Verify data type values</span></span>
<span data-ttu-id="e05cc-169">Some C# functions cannot be used directly in base U-SQL scripts as C# expressions.</span><span class="sxs-lookup"><span data-stu-id="e05cc-169">Some C# functions cannot be used directly in base U-SQL scripts as C# expressions.</span></span> <span data-ttu-id="e05cc-170">Specifically, the functions that can't be used directly are those that require an output reference parameter.</span><span class="sxs-lookup"><span data-stu-id="e05cc-170">Specifically, the functions that can't be used directly are those that require an output reference parameter.</span></span> <span data-ttu-id="e05cc-171">However, these functions can be defined and used as part of an inline function expression, as discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="e05cc-171">However, these functions can be defined and used as part of an inline function expression, as discussed earlier.</span></span>

### <a name="use-inline-function-expressions"></a><span data-ttu-id="e05cc-172">Use inline function expressions</span><span class="sxs-lookup"><span data-stu-id="e05cc-172">Use inline function expressions</span></span>
<span data-ttu-id="e05cc-173">To verify if DateTime value is valid, we can use `DateTime.TryParse`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-173">To verify if DateTime value is valid, we can use `DateTime.TryParse`.</span></span>

<span data-ttu-id="e05cc-174">Here is a complete example that shows how to use an inline function expression to verify data type value with `DateTime.TryParse`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-174">Here is a complete example that shows how to use an inline function expression to verify data type value with `DateTime.TryParse`.</span></span>

<span data-ttu-id="e05cc-175">In this scenario, we verify DateTime data type value:</span><span class="sxs-lookup"><span data-stu-id="e05cc-175">In this scenario, we verify DateTime data type value:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt string,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN((
             (Func<string, DateTime?>)
             (input_parameter =>
                { DateTime dt_result;
                  return
                     DateTime.TryParse(input_parameter, out dt_result)
                       ?(DateTime?) dt_result : (DateTime?) null;
                }
             )
             ) (dt)) AS start_time,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-code-behind"></a><span data-ttu-id="e05cc-176">Use code-behind</span><span class="sxs-lookup"><span data-stu-id="e05cc-176">Use code-behind</span></span>
<span data-ttu-id="e05cc-177">To use the same functionality in the code-behind section of the U-SQL program, we define the C# function ToDateTime.</span><span class="sxs-lookup"><span data-stu-id="e05cc-177">To use the same functionality in the code-behind section of the U-SQL program, we define the C# function ToDateTime.</span></span>

<span data-ttu-id="e05cc-178">Here is the section of base U-SQL script in which we made the necessary changes:</span><span class="sxs-lookup"><span data-stu-id="e05cc-178">Here is the section of base U-SQL script in which we made the necessary changes:</span></span>

```sql
     @rs1 =
        SELECT
          MAX(guid) AS start_id,
          MIN(USQL_Programmability.CustomFunctions.ToDateTime(dt)) AS start_time,
          DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
          user,
          des
          FROM @rs0
        GROUP BY user, des;
```

<span data-ttu-id="e05cc-179">Here is the code-behind function:</span><span class="sxs-lookup"><span data-stu-id="e05cc-179">Here is the code-behind function:</span></span>

```c#
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }
```

## <a name="use-code-behind"></a><span data-ttu-id="e05cc-180">Use code-behind</span><span class="sxs-lookup"><span data-stu-id="e05cc-180">Use code-behind</span></span>
<span data-ttu-id="e05cc-181">Code-behind is a C# programmability section of the U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="e05cc-181">Code-behind is a C# programmability section of the U-SQL project.</span></span> <span data-ttu-id="e05cc-182">Conceptually, code-behind is a compiled assembly (DLL) that's referenced in U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-182">Conceptually, code-behind is a compiled assembly (DLL) that's referenced in U-SQL script.</span></span> <span data-ttu-id="e05cc-183">Visual Studio Tools enables you to manage and debug a C# programmability section as part of a U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="e05cc-183">Visual Studio Tools enables you to manage and debug a C# programmability section as part of a U-SQL project.</span></span>

<span data-ttu-id="e05cc-184">When a typical U-SQL project is created in Visual Studio, there are two parts of the project: base script and a file with the extension **.usql**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-184">When a typical U-SQL project is created in Visual Studio, there are two parts of the project: base script and a file with the extension **.usql**.</span></span>

![Base script file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/base-script-file.png)


<span data-ttu-id="e05cc-186">Typical solution project:</span><span class="sxs-lookup"><span data-stu-id="e05cc-186">Typical solution project:</span></span>   
![Typical solution project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/typical-solution-project.png)


<span data-ttu-id="e05cc-188">In the second part of the project, we call a code-behind file: Script.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="e05cc-188">In the second part of the project, we call a code-behind file: Script.usql.cs.</span></span>  
![Code-behind](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/code-behind.png)

<span data-ttu-id="e05cc-190">This file contains a default namespace definition for programmability objects.</span><span class="sxs-lookup"><span data-stu-id="e05cc-190">This file contains a default namespace definition for programmability objects.</span></span>

```c#
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{

}
```

<span data-ttu-id="e05cc-191">The preview code-behind template is generated automatically.</span><span class="sxs-lookup"><span data-stu-id="e05cc-191">The preview code-behind template is generated automatically.</span></span> <span data-ttu-id="e05cc-192">This file contains a default namespace definition for programmability objects.</span><span class="sxs-lookup"><span data-stu-id="e05cc-192">This file contains a default namespace definition for programmability objects.</span></span> <span data-ttu-id="e05cc-193">During project execution, it gets compiled and referenced in base U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-193">During project execution, it gets compiled and referenced in base U-SQL script.</span></span>

<span data-ttu-id="e05cc-194">To start developing programmability objects, we need to create a **public** class.</span><span class="sxs-lookup"><span data-stu-id="e05cc-194">To start developing programmability objects, we need to create a **public** class.</span></span>

```c#
namespace USQL_Programmability
{
    public class MyClass
    {
        public static string MyFunction(string param1)
        {
            return "my result";
        }

    }

}
```

<span data-ttu-id="e05cc-195">The programmability objects can be user-defined functions, UDF, User-Defined Types, UDT, PROCESS, or REDUCER, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-195">The programmability objects can be user-defined functions, UDF, User-Defined Types, UDT, PROCESS, or REDUCER, and so on.</span></span>

## <a name="register-u-sql-assemblies"></a><span data-ttu-id="e05cc-196">Register U-SQL assemblies</span><span class="sxs-lookup"><span data-stu-id="e05cc-196">Register U-SQL assemblies</span></span>
<span data-ttu-id="e05cc-197">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span><span class="sxs-lookup"><span data-stu-id="e05cc-197">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="e05cc-198">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span><span class="sxs-lookup"><span data-stu-id="e05cc-198">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="e05cc-199">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span><span class="sxs-lookup"><span data-stu-id="e05cc-199">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span>

<span data-ttu-id="e05cc-200">You can even deploy your own runtime for other languages, but you still need to provide the interoperability through a .NET layer yourself.</span><span class="sxs-lookup"><span data-stu-id="e05cc-200">You can even deploy your own runtime for other languages, but you still need to provide the interoperability through a .NET layer yourself.</span></span> <span data-ttu-id="e05cc-201">If you want us to support a specific language, file a feature request or leave a comment at http://aka.ms/adlfeedback.</span><span class="sxs-lookup"><span data-stu-id="e05cc-201">If you want us to support a specific language, file a feature request or leave a comment at http://aka.ms/adlfeedback.</span></span>

### <a name="learn-the-difference-between-code-behind-and-assembly-registration-through-azure-data-lake-tools-in-visual-studio"></a><span data-ttu-id="e05cc-202">Learn the difference between code-behind and assembly registration through Azure Data Lake Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e05cc-202">Learn the difference between code-behind and assembly registration through Azure Data Lake Tools in Visual Studio</span></span>
<span data-ttu-id="e05cc-203">The easiest way to use custom code is to use the Azure Data Lake Tools for Visual Studio’s code-behind capabilities.</span><span class="sxs-lookup"><span data-stu-id="e05cc-203">The easiest way to use custom code is to use the Azure Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span>

<span data-ttu-id="e05cc-204">As we mentioned earlier, you fill in the custom code for the script (for example, Script.usql) into its code-behind file (for example, Script.usql.cs).</span><span class="sxs-lookup"><span data-stu-id="e05cc-204">As we mentioned earlier, you fill in the custom code for the script (for example, Script.usql) into its code-behind file (for example, Script.usql.cs).</span></span>

<span data-ttu-id="e05cc-205">![Code-behind example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/code-behind-example.jpg)
**Figure 1**: Code-behind example in Azure Data Lake Tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e05cc-205">![Code-behind example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/code-behind-example.jpg)
**Figure 1**: Code-behind example in Azure Data Lake Tools in Visual Studio.</span></span> <span data-ttu-id="e05cc-206">(Click the image to enlarge it.</span><span class="sxs-lookup"><span data-stu-id="e05cc-206">(Click the image to enlarge it.</span></span> <span data-ttu-id="e05cc-207">[Sample code](https://github.com/Azure/usql/tree/master/Examples/TweetAnalysis) is available.)</span><span class="sxs-lookup"><span data-stu-id="e05cc-207">[Sample code](https://github.com/Azure/usql/tree/master/Examples/TweetAnalysis) is available.)</span></span>


<span data-ttu-id="e05cc-208">The advantage of code-behind is that the tooling takes care of the following steps for you when you submit your script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-208">The advantage of code-behind is that the tooling takes care of the following steps for you when you submit your script:</span></span>  

1. <span data-ttu-id="e05cc-209">It builds the assembly for the code-behind file.</span><span class="sxs-lookup"><span data-stu-id="e05cc-209">It builds the assembly for the code-behind file.</span></span>  

2. <span data-ttu-id="e05cc-210">It adds a prologue to the script that uses the [CREATE ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763293.aspx) statement to register the assembly file.</span><span class="sxs-lookup"><span data-stu-id="e05cc-210">It adds a prologue to the script that uses the [CREATE ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763293.aspx) statement to register the assembly file.</span></span> <span data-ttu-id="e05cc-211">It also uses [REFERENCE ASSEMBLY]  (https://msdn.microsoft.com/library/azure/mt763294.aspx) to load the assembly into the script’s context.</span><span class="sxs-lookup"><span data-stu-id="e05cc-211">It also uses [REFERENCE ASSEMBLY]  (https://msdn.microsoft.com/library/azure/mt763294.aspx) to load the assembly into the script’s context.</span></span>

3. <span data-ttu-id="e05cc-212">It adds an epilogue to the script, which uses [DROP ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763295.aspx) to remove the temporarily registered assembly again.</span><span class="sxs-lookup"><span data-stu-id="e05cc-212">It adds an epilogue to the script, which uses [DROP ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763295.aspx) to remove the temporarily registered assembly again.</span></span>

<span data-ttu-id="e05cc-213">You can see the generated prologue and epilogue when you open the script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-213">You can see the generated prologue and epilogue when you open the script:</span></span>

![Generated prologue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/generated-prologue.png)

<span data-ttu-id="e05cc-215">**Figure 2**: Auto-generated prologue and epilogue for code-behind</span><span class="sxs-lookup"><span data-stu-id="e05cc-215">**Figure 2**: Auto-generated prologue and epilogue for code-behind</span></span>
<br />

<span data-ttu-id="e05cc-216">The following are some of the drawbacks of code-behind:</span><span class="sxs-lookup"><span data-stu-id="e05cc-216">The following are some of the drawbacks of code-behind:</span></span>

* <span data-ttu-id="e05cc-217">The code gets uploaded for every script submission.</span><span class="sxs-lookup"><span data-stu-id="e05cc-217">The code gets uploaded for every script submission.</span></span>
* <span data-ttu-id="e05cc-218">The functionality cannot be shared with others.</span><span class="sxs-lookup"><span data-stu-id="e05cc-218">The functionality cannot be shared with others.</span></span>

<span data-ttu-id="e05cc-219">Thus, you can add a separate C# Class Library (for U-SQL) to your solution (see Figure 3), develop the code, or copy existing code-behind code (no changes in the C# code required, as shown in Figure 4).</span><span class="sxs-lookup"><span data-stu-id="e05cc-219">Thus, you can add a separate C# Class Library (for U-SQL) to your solution (see Figure 3), develop the code, or copy existing code-behind code (no changes in the C# code required, as shown in Figure 4).</span></span> <span data-ttu-id="e05cc-220">Then use the **Register Assembly** menu option on the project to register the assembly (as shown in Step 1 of Figure 5).</span><span class="sxs-lookup"><span data-stu-id="e05cc-220">Then use the **Register Assembly** menu option on the project to register the assembly (as shown in Step 1 of Figure 5).</span></span>

<span data-ttu-id="e05cc-221">![Creating project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/creating-project.png)
**Figure 3**: Creating a U-SQL C# code project</span><span class="sxs-lookup"><span data-stu-id="e05cc-221">![Creating project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/creating-project.png)
**Figure 3**: Creating a U-SQL C# code project</span></span>  
<br />

<span data-ttu-id="e05cc-222">![Class library](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/class-library.png)
**Figure 4**: The U-SQL C# class library next to the code-behind file</span><span class="sxs-lookup"><span data-stu-id="e05cc-222">![Class library](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/class-library.png)
**Figure 4**: The U-SQL C# class library next to the code-behind file</span></span>
<br />

<span data-ttu-id="e05cc-223">![Register code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/register-code.png)
**Figure 5**: How to register the U-SQL C# code project</span><span class="sxs-lookup"><span data-stu-id="e05cc-223">![Register code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/register-code.png)
**Figure 5**: How to register the U-SQL C# code project</span></span>
<br />

<span data-ttu-id="e05cc-224">The registration dialog box (see Step 2 of Figure 5) gives you the options for how to register the assembly (for example, which Data Lake Analytics account to use, which database to use).</span><span class="sxs-lookup"><span data-stu-id="e05cc-224">The registration dialog box (see Step 2 of Figure 5) gives you the options for how to register the assembly (for example, which Data Lake Analytics account to use, which database to use).</span></span> <span data-ttu-id="e05cc-225">It also gives you information about how to name the assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-225">It also gives you information about how to name the assembly.</span></span> <span data-ttu-id="e05cc-226">(The local assembly path gets filled in by the tool.) In addition, it provides an option to re-register an already registered assembly, and two options for adding additional dependencies:</span><span class="sxs-lookup"><span data-stu-id="e05cc-226">(The local assembly path gets filled in by the tool.) In addition, it provides an option to re-register an already registered assembly, and two options for adding additional dependencies:</span></span>

<span data-ttu-id="e05cc-227">**Managed dependencies**: Shows the managed assemblies that are needed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-227">**Managed dependencies**: Shows the managed assemblies that are needed.</span></span> <span data-ttu-id="e05cc-228">Each selected assembly is registered individually and becomes referenceable in scripts.</span><span class="sxs-lookup"><span data-stu-id="e05cc-228">Each selected assembly is registered individually and becomes referenceable in scripts.</span></span> <span data-ttu-id="e05cc-229">You use this for other .NET assemblies.</span><span class="sxs-lookup"><span data-stu-id="e05cc-229">You use this for other .NET assemblies.</span></span>

<span data-ttu-id="e05cc-230">**Additional files**: Enables you to add additional resource files that are needed by the assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-230">**Additional files**: Enables you to add additional resource files that are needed by the assembly.</span></span> <span data-ttu-id="e05cc-231">They are registered together with the assembly and automatically loaded when the assembly gets referenced.</span><span class="sxs-lookup"><span data-stu-id="e05cc-231">They are registered together with the assembly and automatically loaded when the assembly gets referenced.</span></span> <span data-ttu-id="e05cc-232">You use this for config files, native assemblies, other language runtimes, their resources, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-232">You use this for config files, native assemblies, other language runtimes, their resources, and so on.</span></span>

<span data-ttu-id="e05cc-233">We use both of these options in the following examples.</span><span class="sxs-lookup"><span data-stu-id="e05cc-233">We use both of these options in the following examples.</span></span> <span data-ttu-id="e05cc-234">The [recent blog post about image processing](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/18/introducing-image-processing-in-u-sql/) is another example that shows the use of a predefined assembly that can use these options for registration.</span><span class="sxs-lookup"><span data-stu-id="e05cc-234">The [recent blog post about image processing](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/18/introducing-image-processing-in-u-sql/) is another example that shows the use of a predefined assembly that can use these options for registration.</span></span>

<span data-ttu-id="e05cc-235">Now you can refer to the registered assemblies from any U-SQL script that has permissions for the database of the registered assemblies.</span><span class="sxs-lookup"><span data-stu-id="e05cc-235">Now you can refer to the registered assemblies from any U-SQL script that has permissions for the database of the registered assemblies.</span></span> <span data-ttu-id="e05cc-236">(For more information, see the code in the U-SQL script in Figure 4.) You have to add a reference for every assembly that's registered separately.</span><span class="sxs-lookup"><span data-stu-id="e05cc-236">(For more information, see the code in the U-SQL script in Figure 4.) You have to add a reference for every assembly that's registered separately.</span></span> <span data-ttu-id="e05cc-237">The additional resource files are automatically deployed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-237">The additional resource files are automatically deployed.</span></span> <span data-ttu-id="e05cc-238">That script should not have a code-behind file for the code that's in the referenced assemblies anymore, but the code-behind file can still provide other code.</span><span class="sxs-lookup"><span data-stu-id="e05cc-238">That script should not have a code-behind file for the code that's in the referenced assemblies anymore, but the code-behind file can still provide other code.</span></span>

### <a name="register-assemblies-via-azure-data-lake-tools-in-visual-studio-and-in-u-sql-scripts"></a><span data-ttu-id="e05cc-239">Register assemblies via Azure Data Lake Tools in Visual Studio and in U-SQL scripts</span><span class="sxs-lookup"><span data-stu-id="e05cc-239">Register assemblies via Azure Data Lake Tools in Visual Studio and in U-SQL scripts</span></span>
<span data-ttu-id="e05cc-240">While the Azure Data Lake Tools in Visual Studio make it easy to register an assembly, you can also do it with a script (in the same way that the tools do it for you) if you are (for example) developing on a different platform or have already compiled assemblies that you want to upload and register.</span><span class="sxs-lookup"><span data-stu-id="e05cc-240">While the Azure Data Lake Tools in Visual Studio make it easy to register an assembly, you can also do it with a script (in the same way that the tools do it for you) if you are (for example) developing on a different platform or have already compiled assemblies that you want to upload and register.</span></span> <span data-ttu-id="e05cc-241">You take the following steps:</span><span class="sxs-lookup"><span data-stu-id="e05cc-241">You take the following steps:</span></span>

1. <span data-ttu-id="e05cc-242">Upload your assembly DLL and also all required non-system DLLs and resource files into a location that you choose.</span><span class="sxs-lookup"><span data-stu-id="e05cc-242">Upload your assembly DLL and also all required non-system DLLs and resource files into a location that you choose.</span></span> <span data-ttu-id="e05cc-243">You can also upload it to your Azure Data Lake storage account or even a Microsoft Azure Blob storage account that's linked to your Azure Data Lake account.</span><span class="sxs-lookup"><span data-stu-id="e05cc-243">You can also upload it to your Azure Data Lake storage account or even a Microsoft Azure Blob storage account that's linked to your Azure Data Lake account.</span></span> <span data-ttu-id="e05cc-244">You can use any of the upload tools that are available to you (for example, Windows PowerShell commands, Visual Studio’s Azure Data Lake Tool Data Lake Explorer upload, your favorite SDK’s upload command, or tools that you access through the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="e05cc-244">You can use any of the upload tools that are available to you (for example, Windows PowerShell commands, Visual Studio’s Azure Data Lake Tool Data Lake Explorer upload, your favorite SDK’s upload command, or tools that you access through the Azure portal).</span></span>

1. <span data-ttu-id="e05cc-245">After you have uploaded the DLLs, use the [CREATE ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763293.aspx) statements to register them.</span><span class="sxs-lookup"><span data-stu-id="e05cc-245">After you have uploaded the DLLs, use the [CREATE ASSEMBLY](https://msdn.microsoft.com/library/azure/mt763293.aspx) statements to register them.</span></span>

<span data-ttu-id="e05cc-246">We use this approach in the following spatial example.</span><span class="sxs-lookup"><span data-stu-id="e05cc-246">We use this approach in the following spatial example.</span></span>

### <a name="register-assemblies-that-use-other-net-assemblies-based-on-the-json-and-xml-sample-library"></a><span data-ttu-id="e05cc-247">Register assemblies that use other .NET assemblies (based on the JSON and XML sample library)</span><span class="sxs-lookup"><span data-stu-id="e05cc-247">Register assemblies that use other .NET assemblies (based on the JSON and XML sample library)</span></span>
<span data-ttu-id="e05cc-248">Our [U-SQL GitHub site](https://github.com/Azure/usql/) offers a set of shared example assemblies for you to use.</span><span class="sxs-lookup"><span data-stu-id="e05cc-248">Our [U-SQL GitHub site](https://github.com/Azure/usql/) offers a set of shared example assemblies for you to use.</span></span> <span data-ttu-id="e05cc-249">One of the assemblies, called [Microsoft.Analytics.Samples.Formats](https://github.com/Azure/usql/tree/master/Examples/DataFormats), provides extractors, functions, and outputters to handle both JSON and XML documents.</span><span class="sxs-lookup"><span data-stu-id="e05cc-249">One of the assemblies, called [Microsoft.Analytics.Samples.Formats](https://github.com/Azure/usql/tree/master/Examples/DataFormats), provides extractors, functions, and outputters to handle both JSON and XML documents.</span></span> <span data-ttu-id="e05cc-250">The Microsoft.Analytics.Samples.Formats assembly depends on two existing domain-specific assemblies to do the processing of the JSON and XML respectively.</span><span class="sxs-lookup"><span data-stu-id="e05cc-250">The Microsoft.Analytics.Samples.Formats assembly depends on two existing domain-specific assemblies to do the processing of the JSON and XML respectively.</span></span> <span data-ttu-id="e05cc-251">It uses the [Newtonsoft Json.Net](http://www.newtonsoft.com/) library for processing the JSON documents and the [System.Xml](https://msdn.microsoft.com/data/bb291078.aspx) assembly for processing XML.</span><span class="sxs-lookup"><span data-stu-id="e05cc-251">It uses the [Newtonsoft Json.Net](http://www.newtonsoft.com/) library for processing the JSON documents and the [System.Xml](https://msdn.microsoft.com/data/bb291078.aspx) assembly for processing XML.</span></span> <span data-ttu-id="e05cc-252">We use it to show how to register them and use the assemblies in our scripts.</span><span class="sxs-lookup"><span data-stu-id="e05cc-252">We use it to show how to register them and use the assemblies in our scripts.</span></span>

<span data-ttu-id="e05cc-253">First we download the [Visual Studio project](https://github.com/Azure/usql/tree/master/Examples/DataFormats) to our local development environment (for example, by making a local copy with the GitHub tool for Windows).</span><span class="sxs-lookup"><span data-stu-id="e05cc-253">First we download the [Visual Studio project](https://github.com/Azure/usql/tree/master/Examples/DataFormats) to our local development environment (for example, by making a local copy with the GitHub tool for Windows).</span></span> <span data-ttu-id="e05cc-254">Then we open the solution in Visual Studio and right-click the project (as explained previously) to register the assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-254">Then we open the solution in Visual Studio and right-click the project (as explained previously) to register the assembly.</span></span>

<span data-ttu-id="e05cc-255">Though this assembly has two dependencies, we only have to include the Newtonsoft dependency because System.Xml is available in Azure Data Lake already (it has to be explicitly referenced, however).</span><span class="sxs-lookup"><span data-stu-id="e05cc-255">Though this assembly has two dependencies, we only have to include the Newtonsoft dependency because System.Xml is available in Azure Data Lake already (it has to be explicitly referenced, however).</span></span> <span data-ttu-id="e05cc-256">Figure 6 shows how we name the assembly (note that you can choose a different name without dots as well) and add the Newtonsoft DLL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-256">Figure 6 shows how we name the assembly (note that you can choose a different name without dots as well) and add the Newtonsoft DLL.</span></span> <span data-ttu-id="e05cc-257">Each of the two assemblies is individually registered in the specified database (for example, JSONBlog).</span><span class="sxs-lookup"><span data-stu-id="e05cc-257">Each of the two assemblies is individually registered in the specified database (for example, JSONBlog).</span></span>

![Register assembly](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-u-sql-programmability-guide/register-assembly.png)

<span data-ttu-id="e05cc-259">**Figure 6**: How to register the Microsoft.Analytics.Samples.Formats assembly from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e05cc-259">**Figure 6**: How to register the Microsoft.Analytics.Samples.Formats assembly from Visual Studio</span></span>
<br />

<span data-ttu-id="e05cc-260">If you or others (with whom you shared the registered assemblies by giving them read access to the database) now want to use the JSON capability in your scripts, add the following two references to your script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-260">If you or others (with whom you shared the registered assemblies by giving them read access to the database) now want to use the JSON capability in your scripts, add the following two references to your script:</span></span>

```
REFERENCE ASSEMBLY JSONBlog.[NewtonSoft.Json];
REFERENCE ASSEMBLY JSONBlog.[Microsoft.Analytics.Samples.Formats];
```

<span data-ttu-id="e05cc-261">And if you want to use the XML functionality, add a system assembly reference and a reference to the registered assembly:</span><span class="sxs-lookup"><span data-stu-id="e05cc-261">And if you want to use the XML functionality, add a system assembly reference and a reference to the registered assembly:</span></span>

```
REFERENCE SYSTEM ASSEMBLY [System.Xml];
REFERENCE ASSEMBLY JSONBlog.[Microsoft.Analytics.Samples.Formats];
```

<span data-ttu-id="e05cc-262">For more information about how to use the JSON functionality, see [this blog post](https://blogs.msdn.microsoft.com/mrys/?p=755).</span><span class="sxs-lookup"><span data-stu-id="e05cc-262">For more information about how to use the JSON functionality, see [this blog post](https://blogs.msdn.microsoft.com/mrys/?p=755).</span></span>

### <a name="register-assemblies-that-use-native-c-assemblies-using-the-sql-server-2016-spatial-type-assembly-from-the-feature-pack"></a><span data-ttu-id="e05cc-263">Register assemblies that use native C++ assemblies (using the SQL Server 2016 spatial type assembly from the feature pack)</span><span class="sxs-lookup"><span data-stu-id="e05cc-263">Register assemblies that use native C++ assemblies (using the SQL Server 2016 spatial type assembly from the feature pack)</span></span>
<span data-ttu-id="e05cc-264">Now let’s look at a slightly different scenario.</span><span class="sxs-lookup"><span data-stu-id="e05cc-264">Now let’s look at a slightly different scenario.</span></span> <span data-ttu-id="e05cc-265">Let’s assume the assembly that we want to use has a dependency on code that is not .NET based.</span><span class="sxs-lookup"><span data-stu-id="e05cc-265">Let’s assume the assembly that we want to use has a dependency on code that is not .NET based.</span></span> <span data-ttu-id="e05cc-266">More specifically, the assembly has a dependency on a native C++ assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-266">More specifically, the assembly has a dependency on a native C++ assembly.</span></span> <span data-ttu-id="e05cc-267">An example of such an assembly is the SQL Server type assembly [Microsoft.SqlServer.Types.dll](https://www.microsoft.com/download/details.aspx?id=52676).</span><span class="sxs-lookup"><span data-stu-id="e05cc-267">An example of such an assembly is the SQL Server type assembly [Microsoft.SqlServer.Types.dll](https://www.microsoft.com/download/details.aspx?id=52676).</span></span> <span data-ttu-id="e05cc-268">It provides .NET-based implementations of the SQL Server hierarchyID, geometry, and geography types to be used by SQL Server client-side applications for handling the SQL Server types.</span><span class="sxs-lookup"><span data-stu-id="e05cc-268">It provides .NET-based implementations of the SQL Server hierarchyID, geometry, and geography types to be used by SQL Server client-side applications for handling the SQL Server types.</span></span> <span data-ttu-id="e05cc-269">(It was also originally the assembly that provided the implementation for the SQL Server spatial types before the SQL Server 2016 release.)</span><span class="sxs-lookup"><span data-stu-id="e05cc-269">(It was also originally the assembly that provided the implementation for the SQL Server spatial types before the SQL Server 2016 release.)</span></span>

<span data-ttu-id="e05cc-270">Let’s look at how to register this assembly in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-270">Let’s look at how to register this assembly in U-SQL.</span></span>

<span data-ttu-id="e05cc-271">First we download and install the assembly from the [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=52676).</span><span class="sxs-lookup"><span data-stu-id="e05cc-271">First we download and install the assembly from the [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=52676).</span></span> <span data-ttu-id="e05cc-272">To ensure that you have the 64-bit version of the libraries, select the 64-bit version of the installer (ENU\x64\SQLSysClrTypes.msi).</span><span class="sxs-lookup"><span data-stu-id="e05cc-272">To ensure that you have the 64-bit version of the libraries, select the 64-bit version of the installer (ENU\x64\SQLSysClrTypes.msi).</span></span>

<span data-ttu-id="e05cc-273">The installer installs the managed assembly Microsoft.SqlServer.Types.dll into C:\Program Files (x86)\Microsoft SQL Server\130\SDK\Assemblies and the native assembly SqlServerSpatial130.dll into \Windows\System32\.</span><span class="sxs-lookup"><span data-stu-id="e05cc-273">The installer installs the managed assembly Microsoft.SqlServer.Types.dll into C:\Program Files (x86)\Microsoft SQL Server\130\SDK\Assemblies and the native assembly SqlServerSpatial130.dll into \Windows\System32\.</span></span> <span data-ttu-id="e05cc-274">Now we upload the assemblies into our Azure Data Lake Store (for example, into a folder called /upload/asm/spatial).</span><span class="sxs-lookup"><span data-stu-id="e05cc-274">Now we upload the assemblies into our Azure Data Lake Store (for example, into a folder called /upload/asm/spatial).</span></span>

<span data-ttu-id="e05cc-275">Because the installer has installed the native library into the system folder c:\Windows\System32, we have to make sure that we either copy SqlServerSpatial130.dll out from that folder before uploading it, or that the tool we use does not perform the [file system redirection](https://msdn.microsoft.com/library/windows/desktop/aa384187(v=vs.85).aspx) of system folders.</span><span class="sxs-lookup"><span data-stu-id="e05cc-275">Because the installer has installed the native library into the system folder c:\Windows\System32, we have to make sure that we either copy SqlServerSpatial130.dll out from that folder before uploading it, or that the tool we use does not perform the [file system redirection](https://msdn.microsoft.com/library/windows/desktop/aa384187(v=vs.85).aspx) of system folders.</span></span>

<span data-ttu-id="e05cc-276">For example, if you want to upload it with the current Visual Studio Azure Data Lake File Explorer, you have to copy the file into another directory first.</span><span class="sxs-lookup"><span data-stu-id="e05cc-276">For example, if you want to upload it with the current Visual Studio Azure Data Lake File Explorer, you have to copy the file into another directory first.</span></span> <span data-ttu-id="e05cc-277">Otherwise--as of the time of the writing of this article--you upload the 32-bit version.</span><span class="sxs-lookup"><span data-stu-id="e05cc-277">Otherwise--as of the time of the writing of this article--you upload the 32-bit version.</span></span> <span data-ttu-id="e05cc-278">The reason for this is that Visual Studio is a 32-bit application, which does File System Redirection in its Azure Data Lake upload file selection window.</span><span class="sxs-lookup"><span data-stu-id="e05cc-278">The reason for this is that Visual Studio is a 32-bit application, which does File System Redirection in its Azure Data Lake upload file selection window.</span></span> <span data-ttu-id="e05cc-279">Then, when you run a U-SQL script that calls into the native assembly, you get the following (inner) error at runtime:</span><span class="sxs-lookup"><span data-stu-id="e05cc-279">Then, when you run a U-SQL script that calls into the native assembly, you get the following (inner) error at runtime:</span></span>

<span data-ttu-id="e05cc-280">**Inner exception from user expression: An attempt was made to load a program with an incorrect format. (Exception from HRESULT: 0x8007000B)**</span><span class="sxs-lookup"><span data-stu-id="e05cc-280">**Inner exception from user expression: An attempt was made to load a program with an incorrect format. (Exception from HRESULT: 0x8007000B)**</span></span>

<span data-ttu-id="e05cc-281">After uploading the two assembly files, we now register them in the database SQLSpatial with the following script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-281">After uploading the two assembly files, we now register them in the database SQLSpatial with the following script:</span></span>

```sql
DECLARE @ASSEMBLY_PATH string = "/upload/asm/spatial/";
DECLARE @SPATIAL_ASM string = @ASSEMBLY_PATH+"Microsoft.SqlServer.Types.dll";
DECLARE @SPATIAL_NATIVEDLL string = @ASSEMBLY_PATH+"SqlServerSpatial130.dll";

CREATE DATABASE IF NOT EXISTS SQLSpatial;
USE DATABASE SQLSpatial;

DROP ASSEMBLY IF EXISTS SqlSpatial;
CREATE ASSEMBLY SqlSpatial
FROM @SPATIAL_ASM
WITH ADDITIONAL_FILES =
     (
         @SPATIAL_NATIVEDLL
     );
```

<span data-ttu-id="e05cc-282">In this case, we only register one U-SQL assembly and include the native assembly as a string dependency to the U-SQL assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-282">In this case, we only register one U-SQL assembly and include the native assembly as a string dependency to the U-SQL assembly.</span></span> <span data-ttu-id="e05cc-283">To use the spatial assemblies, we only need to reference the U-SQL assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-283">To use the spatial assemblies, we only need to reference the U-SQL assembly.</span></span> <span data-ttu-id="e05cc-284">The additional file is automatically made available for the assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-284">The additional file is automatically made available for the assembly.</span></span> <span data-ttu-id="e05cc-285">Here's a simple sample script that uses the spatial assembly:</span><span class="sxs-lookup"><span data-stu-id="e05cc-285">Here's a simple sample script that uses the spatial assembly:</span></span>

```sql
REFERENCE SYSTEM ASSEMBLY [System.Xml];
REFERENCE ASSEMBLY SQLSpatial.SqlSpatial;

USING Geometry = Microsoft.SqlServer.Types.SqlGeometry;
USING Geography = Microsoft.SqlServer.Types.SqlGeography;
USING SqlChars = System.Data.SqlTypes.SqlChars;

@spatial =
    SELECT * FROM (VALUES
                   // The following expression is not using the native DDL
                   ( Geometry.Point(1.0,1.0,0).ToString()),    
                   // The following expression is using the native DDL
                   ( Geometry.STGeomFromText(new SqlChars("LINESTRING (100 100, 20 180, 180 180)"), 0).ToString())
                  ) AS T(geom);

OUTPUT @spatial
TO "/output/spatial.csv"
USING Outputters.Csv();
```

<span data-ttu-id="e05cc-286">The SQL Types library has a dependency on the System.XML assembly, so we need to reference it.</span><span class="sxs-lookup"><span data-stu-id="e05cc-286">The SQL Types library has a dependency on the System.XML assembly, so we need to reference it.</span></span> <span data-ttu-id="e05cc-287">Also, some of the methods use the System.Data.SqlTypes types instead of the built-in C# types.</span><span class="sxs-lookup"><span data-stu-id="e05cc-287">Also, some of the methods use the System.Data.SqlTypes types instead of the built-in C# types.</span></span> <span data-ttu-id="e05cc-288">Because System.Data is already included by default, we can reference the needed SQL type.</span><span class="sxs-lookup"><span data-stu-id="e05cc-288">Because System.Data is already included by default, we can reference the needed SQL type.</span></span> <span data-ttu-id="e05cc-289">The previous code is available on our [GitHub site](https://github.com/Azure/usql/tree/master/Examples/SQLSpatialExample).</span><span class="sxs-lookup"><span data-stu-id="e05cc-289">The previous code is available on our [GitHub site](https://github.com/Azure/usql/tree/master/Examples/SQLSpatialExample).</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="e05cc-290">Use assembly versioning</span><span class="sxs-lookup"><span data-stu-id="e05cc-290">Use assembly versioning</span></span>
<span data-ttu-id="e05cc-291">Currently, U-SQL uses the .NET Framework version 4.5.</span><span class="sxs-lookup"><span data-stu-id="e05cc-291">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="e05cc-292">So ensure that your own assemblies are compatible with that version of the runtime.</span><span class="sxs-lookup"><span data-stu-id="e05cc-292">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="e05cc-293">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span><span class="sxs-lookup"><span data-stu-id="e05cc-293">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="e05cc-294">So make sure that your code is compiled to run on x64.</span><span class="sxs-lookup"><span data-stu-id="e05cc-294">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="e05cc-295">Otherwise you get the incorrect format error shown earlier.</span><span class="sxs-lookup"><span data-stu-id="e05cc-295">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="e05cc-296">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span><span class="sxs-lookup"><span data-stu-id="e05cc-296">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="e05cc-297">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span><span class="sxs-lookup"><span data-stu-id="e05cc-297">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="e05cc-298">Finally, note that each U-SQL database can only contain one version of any given assembly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-298">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="e05cc-299">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span><span class="sxs-lookup"><span data-stu-id="e05cc-299">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="e05cc-300">Furthermore, each script can only refer to one version of a given assembly DLL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-300">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="e05cc-301">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span><span class="sxs-lookup"><span data-stu-id="e05cc-301">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="e05cc-302">Use user-defined functions: UDF</span><span class="sxs-lookup"><span data-stu-id="e05cc-302">Use user-defined functions: UDF</span></span>
<span data-ttu-id="e05cc-303">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-303">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="e05cc-304">The return value of UDF can only be a single scalar.</span><span class="sxs-lookup"><span data-stu-id="e05cc-304">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="e05cc-305">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span><span class="sxs-lookup"><span data-stu-id="e05cc-305">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="e05cc-306">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-306">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```c#
        public static string MyFunction(string param1)
        {
            return "my result";
        }
```

<span data-ttu-id="e05cc-307">First let’s look at the simple example of creating a UDF.</span><span class="sxs-lookup"><span data-stu-id="e05cc-307">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="e05cc-308">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span><span class="sxs-lookup"><span data-stu-id="e05cc-308">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="e05cc-309">The first fiscal month of the year in our scenario is June.</span><span class="sxs-lookup"><span data-stu-id="e05cc-309">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="e05cc-310">To calculate fiscal period, we introduce the following C# function:</span><span class="sxs-lookup"><span data-stu-id="e05cc-310">To calculate fiscal period, we introduce the following C# function:</span></span>

```c#
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
        }
```

<span data-ttu-id="e05cc-311">It simply calculates fiscal month and quarter and returns a string value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-311">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="e05cc-312">For June, the first month of the first fiscal quarter, we use “Q1:P1”.</span><span class="sxs-lookup"><span data-stu-id="e05cc-312">For June, the first month of the first fiscal quarter, we use “Q1:P1”.</span></span> <span data-ttu-id="e05cc-313">For July, we use “Q1:P2”, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-313">For July, we use “Q1:P2”, and so on.</span></span>

<span data-ttu-id="e05cc-314">This is a regular C# function that we are going to use in our U-SQL project.</span><span class="sxs-lookup"><span data-stu-id="e05cc-314">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="e05cc-315">Here is how the code-behind section looks in this scenario:</span><span class="sxs-lookup"><span data-stu-id="e05cc-315">Here is how the code-behind section looks in this scenario:</span></span>

```c#
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="e05cc-316">Now we are going to call this function from the base U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-316">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="e05cc-317">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="e05cc-317">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```sql
    USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="e05cc-318">Following is the actual U-SQL base script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-318">Following is the actual U-SQL base script:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-319">Following is the output file of the script execution:</span><span class="sxs-lookup"><span data-stu-id="e05cc-319">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="e05cc-320">This example demonstrates a simple usage of inline UDF in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-320">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="e05cc-321">Keep state between UDF invocations</span><span class="sxs-lookup"><span data-stu-id="e05cc-321">Keep state between UDF invocations</span></span>
<span data-ttu-id="e05cc-322">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span><span class="sxs-lookup"><span data-stu-id="e05cc-322">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="e05cc-323">Let’s look at the following business use-case scenario.</span><span class="sxs-lookup"><span data-stu-id="e05cc-323">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="e05cc-324">In large organizations, users can switch between varieties of internal applications.</span><span class="sxs-lookup"><span data-stu-id="e05cc-324">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="e05cc-325">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-325">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="e05cc-326">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-326">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="e05cc-327">The goal for the business is to optimize application usage.</span><span class="sxs-lookup"><span data-stu-id="e05cc-327">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="e05cc-328">They also might want to combine different applications or specific sign-on routines.</span><span class="sxs-lookup"><span data-stu-id="e05cc-328">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="e05cc-329">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span><span class="sxs-lookup"><span data-stu-id="e05cc-329">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="e05cc-330">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span><span class="sxs-lookup"><span data-stu-id="e05cc-330">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="e05cc-331">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span><span class="sxs-lookup"><span data-stu-id="e05cc-331">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="e05cc-332">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span><span class="sxs-lookup"><span data-stu-id="e05cc-332">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="e05cc-333">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-333">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="e05cc-334">This global variable is applied to the entire rowset during our script execution.</span><span class="sxs-lookup"><span data-stu-id="e05cc-334">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="e05cc-335">Here is the code-behind section of our U-SQL program:</span><span class="sxs-lookup"><span data-stu-id="e05cc-335">Here is the code-behind section of our U-SQL program:</span></span>

```c#
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60)
                    return Session;
                else
                    return Guid.NewGuid().ToString();
            }
            else
                return Guid.NewGuid().ToString();

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session))
            {
                globalSession = Session;
            }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="e05cc-336">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-336">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="e05cc-337">The U-SQL base script is as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-337">The U-SQL base script is as follows:</span></span>

```sql
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT EventDateTime,
           UserName,
LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
           string.IsNullOrEmpty(LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
           USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           )
           AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT EventDateTime,
           UserName,
           LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
           string.IsNullOrEmpty(LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
           USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
TO @out2
ORDER BY UserName, EventDateTime ASC
USING Outputters.Csv();
```

<span data-ttu-id="e05cc-338">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span><span class="sxs-lookup"><span data-stu-id="e05cc-338">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="e05cc-339">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-339">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="e05cc-340">The output file is as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-340">The output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="e05cc-341">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span><span class="sxs-lookup"><span data-stu-id="e05cc-341">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="e05cc-342">Use user-defined types: UDT</span><span class="sxs-lookup"><span data-stu-id="e05cc-342">Use user-defined types: UDT</span></span>
<span data-ttu-id="e05cc-343">User-defined types, or UDT, is another programmability feature of U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-343">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="e05cc-344">U-SQL UDT acts like a regular C# user-defined type.</span><span class="sxs-lookup"><span data-stu-id="e05cc-344">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="e05cc-345">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span><span class="sxs-lookup"><span data-stu-id="e05cc-345">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="e05cc-346">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span><span class="sxs-lookup"><span data-stu-id="e05cc-346">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="e05cc-347">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-347">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="e05cc-348">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span><span class="sxs-lookup"><span data-stu-id="e05cc-348">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="e05cc-349">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span><span class="sxs-lookup"><span data-stu-id="e05cc-349">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="e05cc-350">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span><span class="sxs-lookup"><span data-stu-id="e05cc-350">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="e05cc-351">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span><span class="sxs-lookup"><span data-stu-id="e05cc-351">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="e05cc-352">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span><span class="sxs-lookup"><span data-stu-id="e05cc-352">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="e05cc-353">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span><span class="sxs-lookup"><span data-stu-id="e05cc-353">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```sql
@rs1 =
    SELECT MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-354">We receive the following error:</span><span class="sxs-lookup"><span data-stu-id="e05cc-354">We receive the following error:</span></span>

```
    Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
    MyNameSpace.Myfunction_Returning_UDT.

    Description:

    Outputters.Text only supports built-in types.

    Resolution:

    Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
    the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
    USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="e05cc-355">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span><span class="sxs-lookup"><span data-stu-id="e05cc-355">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="e05cc-356">UDTs currently cannot be used in GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="e05cc-356">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="e05cc-357">If UDT is used in GROUP BY, the following error is thrown:</span><span class="sxs-lookup"><span data-stu-id="e05cc-357">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
    Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
    for column myfield

    Description:

    GROUP BY doesn't support UDT or Complex types.

    Resolution:

    Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
    C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
    62  5   USQL-Programmability
```

<span data-ttu-id="e05cc-358">To define a UDT, we have to:</span><span class="sxs-lookup"><span data-stu-id="e05cc-358">To define a UDT, we have to:</span></span>

* <span data-ttu-id="e05cc-359">Add the following namespaces:</span><span class="sxs-lookup"><span data-stu-id="e05cc-359">Add the following namespaces:</span></span>

```c#
    using Microsoft.Analytics.Interfaces
    using System.IO;
```

* <span data-ttu-id="e05cc-360">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span><span class="sxs-lookup"><span data-stu-id="e05cc-360">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="e05cc-361">In addition, `System.IO` might be needed to define the IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-361">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="e05cc-362">Define a used-defined type with SqlUserDefinedType attribute.</span><span class="sxs-lookup"><span data-stu-id="e05cc-362">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="e05cc-363">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-363">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="e05cc-364">The properties on the attribute reflect the physical characteristics of the UDT.</span><span class="sxs-lookup"><span data-stu-id="e05cc-364">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="e05cc-365">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-365">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-366">SqlUserDefinedType is a required attribute for UDT definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-366">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="e05cc-367">The constructor of the class:</span><span class="sxs-lookup"><span data-stu-id="e05cc-367">The constructor of the class:</span></span>  

* <span data-ttu-id="e05cc-368">SqlUserDefinedTypeAttribute (type formatter)</span><span class="sxs-lookup"><span data-stu-id="e05cc-368">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="e05cc-369">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span><span class="sxs-lookup"><span data-stu-id="e05cc-369">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```c#
    [SqlUserDefinedType(typeof(MyTypeFormatter))]
      public class MyType
           {
             …
           }
```

* <span data-ttu-id="e05cc-370">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-370">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```c#
       public class MyTypeFormatter : IFormatter<MyType>
        {
            public void Serialize(MyType instance, IColumnWriter writer,
                           ISerializationContext context)
            {
        …
            }

            public MyType Deserialize(IColumnReader reader,
                                  ISerializationContext context)
            {
        …
            }
        }
```

<span data-ttu-id="e05cc-371">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span><span class="sxs-lookup"><span data-stu-id="e05cc-371">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="e05cc-372">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span><span class="sxs-lookup"><span data-stu-id="e05cc-372">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="e05cc-373">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span><span class="sxs-lookup"><span data-stu-id="e05cc-373">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="e05cc-374">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span><span class="sxs-lookup"><span data-stu-id="e05cc-374">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="e05cc-375">`MyType` instance: Instance of the type.</span><span class="sxs-lookup"><span data-stu-id="e05cc-375">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="e05cc-376">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span><span class="sxs-lookup"><span data-stu-id="e05cc-376">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="e05cc-377">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span><span class="sxs-lookup"><span data-stu-id="e05cc-377">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

   * <span data-ttu-id="e05cc-378">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span><span class="sxs-lookup"><span data-stu-id="e05cc-378">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

   * <span data-ttu-id="e05cc-379">**Persistence**: Specifies that the source or destination context is a persisted store.</span><span class="sxs-lookup"><span data-stu-id="e05cc-379">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="e05cc-380">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="e05cc-380">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="e05cc-381">It can also include static methods.</span><span class="sxs-lookup"><span data-stu-id="e05cc-381">It can also include static methods.</span></span> <span data-ttu-id="e05cc-382">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span><span class="sxs-lookup"><span data-stu-id="e05cc-382">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="e05cc-383">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="e05cc-383">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="e05cc-384">The following example shows how to define a custom type for fiscal period values.</span><span class="sxs-lookup"><span data-stu-id="e05cc-384">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="e05cc-385">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span><span class="sxs-lookup"><span data-stu-id="e05cc-385">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```c#
        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
```

<span data-ttu-id="e05cc-386">The defined type includes two numbers: quarter and month.</span><span class="sxs-lookup"><span data-stu-id="e05cc-386">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="e05cc-387">Operators ==/!=/>/< and static method ToString() are defined here.</span><span class="sxs-lookup"><span data-stu-id="e05cc-387">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="e05cc-388">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span><span class="sxs-lookup"><span data-stu-id="e05cc-388">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="e05cc-389">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span><span class="sxs-lookup"><span data-stu-id="e05cc-389">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="e05cc-390">Now let’s discuss usage of UDT.</span><span class="sxs-lookup"><span data-stu-id="e05cc-390">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="e05cc-391">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span><span class="sxs-lookup"><span data-stu-id="e05cc-391">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

```c#
        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }
```

<span data-ttu-id="e05cc-392">As you can see, it returns the value of our FiscalPeriod type.</span><span class="sxs-lookup"><span data-stu-id="e05cc-392">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="e05cc-393">Here we provide an example of how to use it further in U-SQL base script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-393">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="e05cc-394">This example demonstrates different forms of UDT invocation from U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-394">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```sql
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT guid AS start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs0;

@rs2 =
    SELECT start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-395">Here's an example of a full code-behind section:</span><span class="sxs-lookup"><span data-stu-id="e05cc-395">Here's an example of a full code-behind section:</span></span>

```c#
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }

    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="e05cc-396">Use user-defined aggregates: UDAGG</span><span class="sxs-lookup"><span data-stu-id="e05cc-396">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="e05cc-397">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e05cc-397">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="e05cc-398">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span><span class="sxs-lookup"><span data-stu-id="e05cc-398">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="e05cc-399">The user-defined aggregate base class definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-399">The user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="e05cc-400">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span><span class="sxs-lookup"><span data-stu-id="e05cc-400">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="e05cc-401">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-401">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-402">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-402">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="e05cc-403">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span><span class="sxs-lookup"><span data-stu-id="e05cc-403">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="e05cc-404">The data types are variable and should be defined during class inheritance.</span><span class="sxs-lookup"><span data-stu-id="e05cc-404">The data types are variable and should be defined during class inheritance.</span></span>

```c#
    public class GuidAggregate : IAggregate<string, string, string>
    {
        string guid_agg;

        public override void Init()
        {
        …
        }

        public override void Accumulate(string guid, string user)
        {
        …
        }

        public override string Terminate()
        {
        …
        }

    }
```

* <span data-ttu-id="e05cc-405">**Init** invokes once for each group during computation.</span><span class="sxs-lookup"><span data-stu-id="e05cc-405">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="e05cc-406">It provides an initialization routine for each aggregation group.</span><span class="sxs-lookup"><span data-stu-id="e05cc-406">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="e05cc-407">**Accumulate** is executed once for each value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-407">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="e05cc-408">It provides the main functionality for the aggregation algorithm.</span><span class="sxs-lookup"><span data-stu-id="e05cc-408">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="e05cc-409">It can be used to aggregate values with various data types that are defined during class inheritance.</span><span class="sxs-lookup"><span data-stu-id="e05cc-409">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="e05cc-410">It can accept two parameters of variable data types.</span><span class="sxs-lookup"><span data-stu-id="e05cc-410">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="e05cc-411">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span><span class="sxs-lookup"><span data-stu-id="e05cc-411">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="e05cc-412">To declare correct input and output data types, use the class definition as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-412">To declare correct input and output data types, use the class definition as follows:</span></span>

```c#
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="e05cc-413">T1: First parameter to accumulate</span><span class="sxs-lookup"><span data-stu-id="e05cc-413">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="e05cc-414">T2: First parameter to accumulate</span><span class="sxs-lookup"><span data-stu-id="e05cc-414">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="e05cc-415">TResult: Return type of terminate</span><span class="sxs-lookup"><span data-stu-id="e05cc-415">TResult: Return type of terminate</span></span>

<span data-ttu-id="e05cc-416">For example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-416">For example:</span></span>

```c#
    public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="e05cc-417">or</span><span class="sxs-lookup"><span data-stu-id="e05cc-417">or</span></span>

```c#
    public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="e05cc-418">Use UDAGG in U-SQL</span><span class="sxs-lookup"><span data-stu-id="e05cc-418">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="e05cc-419">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="e05cc-419">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="e05cc-420">Then use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="e05cc-420">Then use the following syntax:</span></span>

```c#
    AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="e05cc-421">Here is an example of UDAGG:</span><span class="sxs-lookup"><span data-stu-id="e05cc-421">Here is an example of UDAGG:</span></span>

```c#
    public class GuidAggregate : IAggregate<string, string, string>
    {
        string guid_agg;

        public override void Init()
        {
            guid_agg = "";
        }

        public override void Accumulate(string guid, string user)
        {
            if (user.ToUpper()== "USER1")
            {
                guid_agg += "{" + guid + "}";
            }
        }

        public override string Terminate()
        {
            return guid_agg;
        }

    }
```

<span data-ttu-id="e05cc-422">And base U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-422">And base U-SQL script:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-423">In this use-case scenario, we concatenate class GUIDs for the specific users.</span><span class="sxs-lookup"><span data-stu-id="e05cc-423">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="e05cc-424">Use user-defined objects: UDO</span><span class="sxs-lookup"><span data-stu-id="e05cc-424">Use user-defined objects: UDO</span></span>
<span data-ttu-id="e05cc-425">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span><span class="sxs-lookup"><span data-stu-id="e05cc-425">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="e05cc-426">The following is a list of UDO in U-SQL:</span><span class="sxs-lookup"><span data-stu-id="e05cc-426">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="e05cc-427">User-defined extractors</span><span class="sxs-lookup"><span data-stu-id="e05cc-427">User-defined extractors</span></span>
    * <span data-ttu-id="e05cc-428">Extract row by row</span><span class="sxs-lookup"><span data-stu-id="e05cc-428">Extract row by row</span></span>
    * <span data-ttu-id="e05cc-429">Used to implement data extraction from custom structured files</span><span class="sxs-lookup"><span data-stu-id="e05cc-429">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="e05cc-430">User-defined outputters</span><span class="sxs-lookup"><span data-stu-id="e05cc-430">User-defined outputters</span></span>
    * <span data-ttu-id="e05cc-431">Output row by row</span><span class="sxs-lookup"><span data-stu-id="e05cc-431">Output row by row</span></span>
    * <span data-ttu-id="e05cc-432">Used to output custom data types or custom file formats</span><span class="sxs-lookup"><span data-stu-id="e05cc-432">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="e05cc-433">User-defined processors</span><span class="sxs-lookup"><span data-stu-id="e05cc-433">User-defined processors</span></span>
    * <span data-ttu-id="e05cc-434">Take one row and produce one row</span><span class="sxs-lookup"><span data-stu-id="e05cc-434">Take one row and produce one row</span></span>
    * <span data-ttu-id="e05cc-435">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span><span class="sxs-lookup"><span data-stu-id="e05cc-435">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="e05cc-436">User-defined appliers</span><span class="sxs-lookup"><span data-stu-id="e05cc-436">User-defined appliers</span></span>
    * <span data-ttu-id="e05cc-437">Take one row and produce 0 to n rows</span><span class="sxs-lookup"><span data-stu-id="e05cc-437">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="e05cc-438">Used with OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="e05cc-438">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="e05cc-439">User-defined combiners</span><span class="sxs-lookup"><span data-stu-id="e05cc-439">User-defined combiners</span></span>
    * <span data-ttu-id="e05cc-440">Combines rowsets--user-defined JOINs</span><span class="sxs-lookup"><span data-stu-id="e05cc-440">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="e05cc-441">User-defined reducers</span><span class="sxs-lookup"><span data-stu-id="e05cc-441">User-defined reducers</span></span>
    * <span data-ttu-id="e05cc-442">Take n rows and produce one row</span><span class="sxs-lookup"><span data-stu-id="e05cc-442">Take n rows and produce one row</span></span>
    * <span data-ttu-id="e05cc-443">Used to reduce the number of rows</span><span class="sxs-lookup"><span data-stu-id="e05cc-443">Used to reduce the number of rows</span></span>

<span data-ttu-id="e05cc-444">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span><span class="sxs-lookup"><span data-stu-id="e05cc-444">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="e05cc-445">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="e05cc-445">EXTRACT</span></span>
* <span data-ttu-id="e05cc-446">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="e05cc-446">OUTPUT</span></span>
* <span data-ttu-id="e05cc-447">PROCESS</span><span class="sxs-lookup"><span data-stu-id="e05cc-447">PROCESS</span></span>
* <span data-ttu-id="e05cc-448">COMBINE</span><span class="sxs-lookup"><span data-stu-id="e05cc-448">COMBINE</span></span>
* <span data-ttu-id="e05cc-449">REDUCE</span><span class="sxs-lookup"><span data-stu-id="e05cc-449">REDUCE</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="e05cc-450">Use user-defined extractors</span><span class="sxs-lookup"><span data-stu-id="e05cc-450">Use user-defined extractors</span></span>
<span data-ttu-id="e05cc-451">U-SQL allows you to import external data by using an EXTRACT statement.</span><span class="sxs-lookup"><span data-stu-id="e05cc-451">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="e05cc-452">An EXTRACT statement can use built-in UDO extractors:</span><span class="sxs-lookup"><span data-stu-id="e05cc-452">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="e05cc-453">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-453">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="e05cc-454">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-454">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="e05cc-455">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-455">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="e05cc-456">It can be useful to develop a custom extractor.</span><span class="sxs-lookup"><span data-stu-id="e05cc-456">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="e05cc-457">This can be helpful during data import if we want to do any of the following tasks:</span><span class="sxs-lookup"><span data-stu-id="e05cc-457">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="e05cc-458">Modify input data by splitting columns and modifying individual values.</span><span class="sxs-lookup"><span data-stu-id="e05cc-458">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="e05cc-459">The PROCESSOR functionality is better for combining columns.</span><span class="sxs-lookup"><span data-stu-id="e05cc-459">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="e05cc-460">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="e05cc-460">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="e05cc-461">Parse data in unsupported encoding.</span><span class="sxs-lookup"><span data-stu-id="e05cc-461">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="e05cc-462">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-462">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="e05cc-463">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span><span class="sxs-lookup"><span data-stu-id="e05cc-463">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="e05cc-464">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-464">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

```c#
     [SqlUserDefinedExtractor]
     public class SampleExtractor : IExtractor
     {
         public SampleExtractor(string row_delimiter, char col_delimiter)
         {
            …

         }

         public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
         {
             …
         }
     }
```

<span data-ttu-id="e05cc-465">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span><span class="sxs-lookup"><span data-stu-id="e05cc-465">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="e05cc-466">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-466">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-467">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-467">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="e05cc-468">It used to define AtomicFileProcessing property for the UDE object.</span><span class="sxs-lookup"><span data-stu-id="e05cc-468">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="e05cc-469">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="e05cc-469">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="e05cc-470">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="e05cc-470">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="e05cc-471">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="e05cc-471">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="e05cc-472">The main UDE programmability objects are **input** and **output**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-472">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e05cc-473">The input object is used to enumerate input data as `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-473">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="e05cc-474">The output object is used to set output data as a result of the extractor activity.</span><span class="sxs-lookup"><span data-stu-id="e05cc-474">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="e05cc-475">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-475">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="e05cc-476">For input columns enumeration, we first split the input stream by using a row delimiter.</span><span class="sxs-lookup"><span data-stu-id="e05cc-476">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```c#
    foreach (Stream current in input.Split(my_row_delimiter))
    {
    …
    }
```

<span data-ttu-id="e05cc-477">Then, further split input row into column parts.</span><span class="sxs-lookup"><span data-stu-id="e05cc-477">Then, further split input row into column parts.</span></span>

```c#
    foreach (Stream current in input.Split(my_row_delimiter))
    {
    …
        string[] parts = line.Split(my_column_delimiter);
            foreach (string part in parts)
        {
        …
        }
    }
```

<span data-ttu-id="e05cc-478">To set output data, we use the `output.Set` method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-478">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="e05cc-479">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span><span class="sxs-lookup"><span data-stu-id="e05cc-479">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="e05cc-480">Set method call.</span><span class="sxs-lookup"><span data-stu-id="e05cc-480">Set method call.</span></span>

```c#
    output.Set<string>(count, part);
```

<span data-ttu-id="e05cc-481">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-481">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e05cc-482">Following is the extractor example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-482">Following is the extractor example:</span></span>

```c#
    [SqlUserDefinedExtractor(AtomicFileProcessing = true)]
    public class FullDescriptionExtractor : IExtractor
    {
         private Encoding _encoding;
         private byte[] _row_delim;
         private char _col_delim;

        public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
        {
             this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
             this._row_delim = this._encoding.GetBytes(row_delim);
             this._col_delim = col_delim;

        }

        public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
        {
             string line;
             //Read the input line by line
             foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
             {
                using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
                 {
                     line = streamReader.ReadToEnd().Trim();
                     //Split the input by the column delimiter
                     string[] parts = line.Split(this._col_delim);
                     int count = 0; // start with first column
                     foreach (string part in parts)
                     {
    if (count == 0)
                         {  // for column “guid”, re-generated guid
                             Guid new_guid = Guid.NewGuid();
                             output.Set<Guid>(count, new_guid);
                         }
                         else if (count == 2)
                         {
                             // for column “user”, convert to UPPER case
                             output.Set<string>(count, part.ToUpper());

                         }
                         else
                         {
                             // keep the rest of the columns as-is
                             output.Set<string>(count, part);
                         }
                         count += 1;
                     }

                 }
                 yield return output.AsReadOnly();
             }
             yield break;
         }
     }
```

<span data-ttu-id="e05cc-483">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span><span class="sxs-lookup"><span data-stu-id="e05cc-483">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="e05cc-484">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span><span class="sxs-lookup"><span data-stu-id="e05cc-484">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="e05cc-485">Following is base U-SQL script that uses a custom extractor:</span><span class="sxs-lookup"><span data-stu-id="e05cc-485">Following is base U-SQL script that uses a custom extractor:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt String,
        user String,
        des String
    FROM @input_file
    USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="e05cc-486">Use user-defined outputters</span><span class="sxs-lookup"><span data-stu-id="e05cc-486">Use user-defined outputters</span></span>
<span data-ttu-id="e05cc-487">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span><span class="sxs-lookup"><span data-stu-id="e05cc-487">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="e05cc-488">Similar to the extractor, there are several built-in outputters.</span><span class="sxs-lookup"><span data-stu-id="e05cc-488">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="e05cc-489">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-489">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="e05cc-490">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-490">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="e05cc-491">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-491">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="e05cc-492">Custom outputter allows you to write data in a custom defined format.</span><span class="sxs-lookup"><span data-stu-id="e05cc-492">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="e05cc-493">This can be useful for the following tasks:</span><span class="sxs-lookup"><span data-stu-id="e05cc-493">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="e05cc-494">Writing data to semi-structured or unstructured files.</span><span class="sxs-lookup"><span data-stu-id="e05cc-494">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="e05cc-495">Writing data not supported encodings.</span><span class="sxs-lookup"><span data-stu-id="e05cc-495">Writing data not supported encodings.</span></span>
* <span data-ttu-id="e05cc-496">Modifying output data or adding custom attributes.</span><span class="sxs-lookup"><span data-stu-id="e05cc-496">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="e05cc-497">To define user-defined outputter, we need to create the `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-497">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="e05cc-498">Following is the base `IOutputter` class implementation:</span><span class="sxs-lookup"><span data-stu-id="e05cc-498">Following is the base `IOutputter` class implementation:</span></span>

```c#
    public abstract class IOutputter : IUserDefinedOperator
    {
        protected IOutputter();

        public virtual void Close();
        public abstract void Output(IRow input, IUnstructuredWriter output);
    }
```

<span data-ttu-id="e05cc-499">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span><span class="sxs-lookup"><span data-stu-id="e05cc-499">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="e05cc-500">The `IOutputter` interface should also contain a definition for `void Output` override.</span><span class="sxs-lookup"><span data-stu-id="e05cc-500">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="e05cc-501">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span><span class="sxs-lookup"><span data-stu-id="e05cc-501">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="e05cc-502">For more information, see the following details.</span><span class="sxs-lookup"><span data-stu-id="e05cc-502">For more information, see the following details.</span></span>

```c#
        [SqlUserDefinedOutputter(AtomicFileProcessing = true)]
        public class MyOutputter : IOutputter
        {

            public MyOutputter(myparam1, myparam2)
            {
              …
            }

            public override void Close()
            {
              …
            }

            public override void Output(IRow row, IUnstructuredWriter output)
            {
              …
            }
        }
```

* <span data-ttu-id="e05cc-503">`Output` is called for each input row.</span><span class="sxs-lookup"><span data-stu-id="e05cc-503">`Output` is called for each input row.</span></span> <span data-ttu-id="e05cc-504">It returns the `IUnstructuredWriter output` rowset.</span><span class="sxs-lookup"><span data-stu-id="e05cc-504">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="e05cc-505">The Constructor class is used to pass parameters to the user-defined outputter.</span><span class="sxs-lookup"><span data-stu-id="e05cc-505">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="e05cc-506">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span><span class="sxs-lookup"><span data-stu-id="e05cc-506">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="e05cc-507">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span><span class="sxs-lookup"><span data-stu-id="e05cc-507">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="e05cc-508">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-508">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-509">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-509">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="e05cc-510">It's used to define the AtomicFileProcessing property.</span><span class="sxs-lookup"><span data-stu-id="e05cc-510">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="e05cc-511">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="e05cc-511">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="e05cc-512">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="e05cc-512">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="e05cc-513">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="e05cc-513">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="e05cc-514">The main programmability objects are **row** and **output**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-514">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="e05cc-515">The **row** object is used to enumerate output data as `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-515">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="e05cc-516">**Output** is used to set output data to the target file.</span><span class="sxs-lookup"><span data-stu-id="e05cc-516">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="e05cc-517">The output data is accessed through the `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-517">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="e05cc-518">Output data is passed a row at a time.</span><span class="sxs-lookup"><span data-stu-id="e05cc-518">Output data is passed a row at a time.</span></span>

<span data-ttu-id="e05cc-519">The individual values are enumerated by calling the Get method of the IRow interface:</span><span class="sxs-lookup"><span data-stu-id="e05cc-519">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```c#
    row.Get<string>("column_name")
```

<span data-ttu-id="e05cc-520">Individual column names can be determined by calling `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="e05cc-520">Individual column names can be determined by calling `row.Schema`:</span></span>

```c#
    ISchema schema = row.Schema;
    var col = schema[i];
    string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e05cc-521">This approach enables you to build a flexible outputter for any metadata schema.</span><span class="sxs-lookup"><span data-stu-id="e05cc-521">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="e05cc-522">The output data is written to file by using `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-522">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="e05cc-523">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-523">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="e05cc-524">Note that it's important to flush the data buffer to the file after each row iteration.</span><span class="sxs-lookup"><span data-stu-id="e05cc-524">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="e05cc-525">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span><span class="sxs-lookup"><span data-stu-id="e05cc-525">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```c#
    using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
            {
        …
            }
```

<span data-ttu-id="e05cc-526">Otherwise, call Flush() method explicitly after each iteration.</span><span class="sxs-lookup"><span data-stu-id="e05cc-526">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="e05cc-527">We show this in the following example.</span><span class="sxs-lookup"><span data-stu-id="e05cc-527">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="e05cc-528">Set headers and footers for user-defined outputter</span><span class="sxs-lookup"><span data-stu-id="e05cc-528">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="e05cc-529">To set a header, use single iteration execution flow.</span><span class="sxs-lookup"><span data-stu-id="e05cc-529">To set a header, use single iteration execution flow.</span></span>

```c#
            public override void Output(IRow row, IUnstructuredWriter output)
            {
             …
                if (isHeaderRow)
                {
                    …                
                }

             …
                if (isHeaderRow)
                {
                    isHeaderRow = false;
                }
             …
            }
        }
```

<span data-ttu-id="e05cc-530">The code in the first `if (isHeaderRow)` block is executed only once.</span><span class="sxs-lookup"><span data-stu-id="e05cc-530">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="e05cc-531">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="e05cc-531">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="e05cc-532">Write the footer in the Close() method of the `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-532">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="e05cc-533">(For more information, see the following example.)</span><span class="sxs-lookup"><span data-stu-id="e05cc-533">(For more information, see the following example.)</span></span>

<span data-ttu-id="e05cc-534">Following is an example of a user-defined outputter:</span><span class="sxs-lookup"><span data-stu-id="e05cc-534">Following is an example of a user-defined outputter:</span></span>

```c#
        [SqlUserDefinedOutputter(AtomicFileProcessing = true)]
        public class HTMLOutputter : IOutputter
        {
            // Local variables initialization
            private string row_delimiter;
            private char col_delimiter;
            private bool isHeaderRow;
            private Encoding encoding;
            private bool IsTableHeader = true;
            private Stream g_writer;

            // Parameters definition            
            public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                this.isHeaderRow = isHeader;
                this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
            }

            // The Close method is used to write the footer to the file. It's executed only once, after all rows
            public override void Close().
            {
                //Reference to IO.Stream object - g_writer
                StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
                streamWriter.Write("</table>");
                streamWriter.Flush();
                streamWriter.Close();
            }

            public override void Output(IRow row, IUnstructuredWriter output)
            {
                System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

                // Metadata schema initialization to enumerate column names
                ISchema schema = row.Schema;

                // This is a data-independent header--HTML table definition
                if (IsTableHeader)
                {
                    streamWriter.Write("<table border=1>");
                    IsTableHeader = false;
                }

                // HTML table attributes
                string header_wrapper_on = "<th>";
                string header_wrapper_off = "</th>";
                string data_wrapper_on = "<td>";
                string data_wrapper_off = "</td>";

                // Header row output--runs only once
                if (isHeaderRow)
                {
                    streamWriter.Write("<tr>");
                    for (int i = 0; i < schema.Count(); i++)
                    {
                        var col = schema[i];
                        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
                    }
                    streamWriter.Write("</tr>");
                }

                // Data row output
                streamWriter.Write("<tr>");                
                for (int i = 0; i < schema.Count(); i++)
                {
                    var col = schema[i];
                    string val = "";
                    try
                    {
                        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
                        switch (col.Type.Name.ToString().ToLower())
                        {
                            case "string": val = row.Get<string>(col.Name).ToString(); break;
                            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
                            default: break;
                        }
                    }
                    // Handling NULL values--keeping them empty
                    catch (System.NullReferenceException)
                    {
                    }
                    streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
                }
                streamWriter.Write("</tr>");

                if (isHeaderRow)
                {
                    isHeaderRow = false;
                }
                // Reference to the instance of the IO.Stream object for footer generation
                g_writer = output.BaseStream;
                streamWriter.Flush();
            }
        }

        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="e05cc-535">And U-SQL base script:</span><span class="sxs-lookup"><span data-stu-id="e05cc-535">And U-SQL base script:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
        guid Guid,
        dt String,
        user String,
        des String
    FROM @input_file
    USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="e05cc-536">This is an HTML outputter, which creates an HTML file with table data.</span><span class="sxs-lookup"><span data-stu-id="e05cc-536">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="e05cc-537">Call outputter from U-SQL base script</span><span class="sxs-lookup"><span data-stu-id="e05cc-537">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="e05cc-538">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span><span class="sxs-lookup"><span data-stu-id="e05cc-538">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="e05cc-539">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-539">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="e05cc-540">In this case, the original call looks like the following:</span><span class="sxs-lookup"><span data-stu-id="e05cc-540">In this case, the original call looks like the following:</span></span>

```sql
OUTPUT @rs0 TO @output_file USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="e05cc-541">Use user-defined processors</span><span class="sxs-lookup"><span data-stu-id="e05cc-541">Use user-defined processors</span></span>
<span data-ttu-id="e05cc-542">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span><span class="sxs-lookup"><span data-stu-id="e05cc-542">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="e05cc-543">UDP enables you to combine columns, modify values, and add new columns if necessary.</span><span class="sxs-lookup"><span data-stu-id="e05cc-543">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="e05cc-544">Basically, it helps to process a rowset to produce required data elements.</span><span class="sxs-lookup"><span data-stu-id="e05cc-544">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="e05cc-545">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span><span class="sxs-lookup"><span data-stu-id="e05cc-545">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="e05cc-546">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-546">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

```c#
    [SqlUserDefinedProcessor]
     public class MyProcessor: IProcessor
     {
        public override IRow Process(IRow input, IUpdatableRow output)
         {
            …
         }
     }
```

<span data-ttu-id="e05cc-547">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span><span class="sxs-lookup"><span data-stu-id="e05cc-547">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="e05cc-548">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-548">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-549">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-549">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="e05cc-550">The main programmability objects are **input** and **output**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-550">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e05cc-551">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span><span class="sxs-lookup"><span data-stu-id="e05cc-551">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="e05cc-552">For input columns enumeration, we use the `input.Get` method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-552">For input columns enumeration, we use the `input.Get` method.</span></span>

```c#
    string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="e05cc-553">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-553">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="e05cc-554">We need to use the correct data type here.</span><span class="sxs-lookup"><span data-stu-id="e05cc-554">We need to use the correct data type here.</span></span>

<span data-ttu-id="e05cc-555">For output, use the `output.Set` method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-555">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="e05cc-556">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span><span class="sxs-lookup"><span data-stu-id="e05cc-556">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```c#
    output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="e05cc-557">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-557">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e05cc-558">Following is a processor example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-558">Following is a processor example:</span></span>

```c#
     [SqlUserDefinedProcessor]
     public class FullDescriptionProcessor : IProcessor
     {
        public override IRow Process(IRow input, IUpdatableRow output)
         {
             string user = input.Get<string>("user");
             string des = input.Get<string>("des");
             string full_description = user.ToUpper() + "=>" + des;
             output.Set<string>("dt", input.Get<string>("dt"));
             output.Set<string>("full_description", full_description);
             output.Set<Guid>("new_guid", Guid.NewGuid());
             output.Set<Guid>("guid", input.Get<Guid>("guid"));
             return output.AsReadOnly();
         }
     }
```

<span data-ttu-id="e05cc-559">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span><span class="sxs-lookup"><span data-stu-id="e05cc-559">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="e05cc-560">It also regenerates a GUID and returns the original and new GUID values.</span><span class="sxs-lookup"><span data-stu-id="e05cc-560">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="e05cc-561">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span><span class="sxs-lookup"><span data-stu-id="e05cc-561">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="e05cc-562">Following is an example of base U-SQL script that uses a custom processor:</span><span class="sxs-lookup"><span data-stu-id="e05cc-562">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid Guid,
        dt String,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="e05cc-563">Use user-defined appliers</span><span class="sxs-lookup"><span data-stu-id="e05cc-563">Use user-defined appliers</span></span>
<span data-ttu-id="e05cc-564">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span><span class="sxs-lookup"><span data-stu-id="e05cc-564">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="e05cc-565">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span><span class="sxs-lookup"><span data-stu-id="e05cc-565">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="e05cc-566">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span><span class="sxs-lookup"><span data-stu-id="e05cc-566">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="e05cc-567">User-defined applier is being invoked as part of the USQL SELECT expression.</span><span class="sxs-lookup"><span data-stu-id="e05cc-567">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="e05cc-568">The typical call to the user-defined applier looks like the following:</span><span class="sxs-lookup"><span data-stu-id="e05cc-568">The typical call to the user-defined applier looks like the following:</span></span>

```sql
    SELECT …
    FROM …
    CROSS APPLYis used to pass parameters
    new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="e05cc-569">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="e05cc-569">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="e05cc-570">The user-defined applier base class definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-570">The user-defined applier base class definition is as follows:</span></span>

```c#
    public abstract class IApplier : IUserDefinedOperator
    {
        protected IApplier();

        public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
    }
```

<span data-ttu-id="e05cc-571">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-571">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```c#
    [SqlUserDefinedApplier]
    public class ParserApplier : IApplier
    {

        public ParserApplier()
        {
        …
        }

        public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
        {
        …
        }
    }
```

* <span data-ttu-id="e05cc-572">Apply is called for each row of the outer table.</span><span class="sxs-lookup"><span data-stu-id="e05cc-572">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="e05cc-573">It returns the `IUpdatableRow` output rowset.</span><span class="sxs-lookup"><span data-stu-id="e05cc-573">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="e05cc-574">The Constructor class is used to pass parameters to the user-defined applier.</span><span class="sxs-lookup"><span data-stu-id="e05cc-574">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="e05cc-575">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span><span class="sxs-lookup"><span data-stu-id="e05cc-575">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="e05cc-576">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-576">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-577">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-577">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="e05cc-578">The main programmability objects are as follows:</span><span class="sxs-lookup"><span data-stu-id="e05cc-578">The main programmability objects are as follows:</span></span>

```c#
        public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="e05cc-579">Input rowsets are passed as `IRow` input.</span><span class="sxs-lookup"><span data-stu-id="e05cc-579">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="e05cc-580">The output rows are generated as `IUpdatableRow` output interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-580">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="e05cc-581">Individual column names can be determined by calling the `IRow` Schema method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-581">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```c#
    ISchema schema = row.Schema;
    var col = schema[i];
    string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e05cc-582">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-582">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```c#
    mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="e05cc-583">Or we use the schema column name:</span><span class="sxs-lookup"><span data-stu-id="e05cc-583">Or we use the schema column name:</span></span>

```c#
    row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="e05cc-584">The output values must be set with `IUpdatableRow` output:</span><span class="sxs-lookup"><span data-stu-id="e05cc-584">The output values must be set with `IUpdatableRow` output:</span></span>

```c#
    output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="e05cc-585">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span><span class="sxs-lookup"><span data-stu-id="e05cc-585">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="e05cc-586">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-586">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e05cc-587">The user-defined applier parameters can be passed to the constructor.</span><span class="sxs-lookup"><span data-stu-id="e05cc-587">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="e05cc-588">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-588">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```c#
  new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="e05cc-589">Here is the user-defined applier example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-589">Here is the user-defined applier example:</span></span>

```c#
   [SqlUserDefinedApplier]
    public class ParserApplier : IApplier
    {
        private string parsingPart;

        public ParserApplier(string parsingPart)
        {
            if (parsingPart.ToUpper().Contains("ALL")
                || parsingPart.ToUpper().Contains("MAKE")
                || parsingPart.ToUpper().Contains("MODEL")
                || parsingPart.ToUpper().Contains("YEAR")
                || parsingPart.ToUpper().Contains("TYPE")
                || parsingPart.ToUpper().Contains("MILLAGE")
                )
            {
                this.parsingPart = parsingPart;
            }
            else
            {
                throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
            }
        }

        public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
        {

            string[] properties = input.Get<string>("properties").Split(',');

            //  only process with correct number of properties
            if (properties.Count() == 5)
            {

                string make = properties[0];
                string model = properties[1];
                string year = properties[2];
                string type = properties[3];
                int millage = -1;

                // Only return millage if it is number, otherwise, -1
                if (!int.TryParse(properties[4], out millage))
                {
                    millage = -1;
                }

                if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
                if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
                if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
                if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
                if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
            }
            yield return output.AsReadOnly();            
        }
    }
```

<span data-ttu-id="e05cc-590">Following is the base U-SQL script for this user-defined applier:</span><span class="sxs-lookup"><span data-stu-id="e05cc-590">Following is the base U-SQL script for this user-defined applier:</span></span>

```sql
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="e05cc-591">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span><span class="sxs-lookup"><span data-stu-id="e05cc-591">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="e05cc-592">The input file rows look like the following:</span><span class="sxs-lookup"><span data-stu-id="e05cc-592">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="e05cc-593">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span><span class="sxs-lookup"><span data-stu-id="e05cc-593">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="e05cc-594">Those properties must be parsed to the table columns.</span><span class="sxs-lookup"><span data-stu-id="e05cc-594">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="e05cc-595">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span><span class="sxs-lookup"><span data-stu-id="e05cc-595">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="e05cc-596">You can generate either all properties or a specific set of properties only.</span><span class="sxs-lookup"><span data-stu-id="e05cc-596">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="e05cc-597">The user-defined applier can be called as a new instance of applier object:</span><span class="sxs-lookup"><span data-stu-id="e05cc-597">The user-defined applier can be called as a new instance of applier object:</span></span>

```c#
    CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="e05cc-598">Or with the invocation of a wrapper factory method:</span><span class="sxs-lookup"><span data-stu-id="e05cc-598">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="e05cc-599">Use user-defined combiners</span><span class="sxs-lookup"><span data-stu-id="e05cc-599">Use user-defined combiners</span></span>
<span data-ttu-id="e05cc-600">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span><span class="sxs-lookup"><span data-stu-id="e05cc-600">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="e05cc-601">User-defined combiner is used with COMBINE expression.</span><span class="sxs-lookup"><span data-stu-id="e05cc-601">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="e05cc-602">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span><span class="sxs-lookup"><span data-stu-id="e05cc-602">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="e05cc-603">To call a combiner in a base U-SQL script, we use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="e05cc-603">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

```sql
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="e05cc-604">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="e05cc-604">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="e05cc-605">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-605">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="e05cc-606">Base `ICombiner` class definition:</span><span class="sxs-lookup"><span data-stu-id="e05cc-606">Base `ICombiner` class definition:</span></span>

```c#
    public abstract class ICombiner : IUserDefinedOperator
    {
        protected ICombiner();
        public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
               IUpdatableRow output);
        public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
               IUpdatableRow output);
    }
```

<span data-ttu-id="e05cc-607">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span><span class="sxs-lookup"><span data-stu-id="e05cc-607">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

```c#
    [SqlUserDefinedCombiner]
    public class MyCombiner : ICombiner
    {

        public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output)
        {
        …
        }
    }
```

<span data-ttu-id="e05cc-608">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span><span class="sxs-lookup"><span data-stu-id="e05cc-608">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="e05cc-609">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-609">This class cannot be inherited.</span></span>

<span data-ttu-id="e05cc-610">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span><span class="sxs-lookup"><span data-stu-id="e05cc-610">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="e05cc-611">It is an optional attribute for a user-defined combiner definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-611">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="e05cc-612">CombinerMode     Mode</span><span class="sxs-lookup"><span data-stu-id="e05cc-612">CombinerMode     Mode</span></span>

<span data-ttu-id="e05cc-613">CombinerMode enum can take the following values:</span><span class="sxs-lookup"><span data-stu-id="e05cc-613">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="e05cc-614">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-614">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="e05cc-615">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span><span class="sxs-lookup"><span data-stu-id="e05cc-615">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="e05cc-616">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span><span class="sxs-lookup"><span data-stu-id="e05cc-616">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="e05cc-617">Inner (3) Every output row depends on a single input row from left and right with the same value.</span><span class="sxs-lookup"><span data-stu-id="e05cc-617">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="e05cc-618">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="e05cc-618">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="e05cc-619">The main programmability objects are:</span><span class="sxs-lookup"><span data-stu-id="e05cc-619">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="e05cc-620">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-620">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="e05cc-621">Both rowsets must be enumerated for processing.</span><span class="sxs-lookup"><span data-stu-id="e05cc-621">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="e05cc-622">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span><span class="sxs-lookup"><span data-stu-id="e05cc-622">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="e05cc-623">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="e05cc-623">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="e05cc-624">The anonymous data type can be used during enumeration as well.</span><span class="sxs-lookup"><span data-stu-id="e05cc-624">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="e05cc-625">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-625">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="e05cc-626">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-626">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```c#
    mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="e05cc-627">Individual column names can be determined by calling the `IRow` Schema method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-627">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```c#
    ISchema schema = row.Schema;
    var col = schema[i];
    string val = row.Get<string>(col.Name)
```

<span data-ttu-id="e05cc-628">Or by using the schema column name:</span><span class="sxs-lookup"><span data-stu-id="e05cc-628">Or by using the schema column name:</span></span>

```
    c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="e05cc-629">The general enumeration with LINQ looks like the following:</span><span class="sxs-lookup"><span data-stu-id="e05cc-629">The general enumeration with LINQ looks like the following:</span></span>

```c#
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="e05cc-630">After enumerating both rowsets, we are going to loop through all rows.</span><span class="sxs-lookup"><span data-stu-id="e05cc-630">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="e05cc-631">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span><span class="sxs-lookup"><span data-stu-id="e05cc-631">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="e05cc-632">The output values must be set with `IUpdatableRow` output.</span><span class="sxs-lookup"><span data-stu-id="e05cc-632">The output values must be set with `IUpdatableRow` output.</span></span>

```c#
    output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="e05cc-633">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-633">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e05cc-634">Following is a combiner example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-634">Following is a combiner example:</span></span>

```c#
    [SqlUserDefinedCombiner]
    public class CombineSales : ICombiner
    {

        public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output)
        {
            var internetSales =
            (from row in left.Rows
                          select new
                          {
                              ProductKey = row.Get<int>("ProductKey"),
                              OrderDateKey = row.Get<int>("OrderDateKey"),
                              SalesAmount = row.Get<decimal>("SalesAmount"),
                              TaxAmt = row.Get<decimal>("TaxAmt")
                          }).ToList();

            var resellerSales =
            (from row in right.Rows
             select new
             {
                 ProductKey = row.Get<int>("ProductKey"),
                 OrderDateKey = row.Get<int>("OrderDateKey"),
                 SalesAmount = row.Get<decimal>("SalesAmount"),
                 TaxAmt = row.Get<decimal>("TaxAmt")
             }).ToList();

            foreach (var row_i in internetSales)
            {
                foreach (var row_r in resellerSales)
                {

                    if (
                        row_i.OrderDateKey > 0
                        && row_i.OrderDateKey < row_r.OrderDateKey
                        && row_i.OrderDateKey == 20010701
                        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
                    {
                        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
                        output.Set<int>("ProductKey", row_i.ProductKey);
                        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
                        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
                    }

                }
            }
            yield return output.AsReadOnly();
        }
    }
```

<span data-ttu-id="e05cc-635">In this use-case scenario, we are building an analytics report for the retailer.</span><span class="sxs-lookup"><span data-stu-id="e05cc-635">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="e05cc-636">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span><span class="sxs-lookup"><span data-stu-id="e05cc-636">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="e05cc-637">Here is the base U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-637">Here is the base U-SQL script.</span></span> <span data-ttu-id="e05cc-638">You can compare the logic between a regular JOIN and a combiner:</span><span class="sxs-lookup"><span data-stu-id="e05cc-638">You can compare the logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="e05cc-639">A user-defined combiner can be called as a new instance of the applier object:</span><span class="sxs-lookup"><span data-stu-id="e05cc-639">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```c#
    USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="e05cc-640">Or with the invocation of a wrapper factory method:</span><span class="sxs-lookup"><span data-stu-id="e05cc-640">Or with the invocation of a wrapper factory method:</span></span>

```c#
    USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="e05cc-641">Use user-defined reducers</span><span class="sxs-lookup"><span data-stu-id="e05cc-641">Use user-defined reducers</span></span>
<span data-ttu-id="e05cc-642">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span><span class="sxs-lookup"><span data-stu-id="e05cc-642">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="e05cc-643">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span><span class="sxs-lookup"><span data-stu-id="e05cc-643">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="e05cc-644">It also can be used to manipulate and evaluate rows and columns.</span><span class="sxs-lookup"><span data-stu-id="e05cc-644">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="e05cc-645">Based on programmability logic, it can also define which rows need to be extracted.</span><span class="sxs-lookup"><span data-stu-id="e05cc-645">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="e05cc-646">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span><span class="sxs-lookup"><span data-stu-id="e05cc-646">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="e05cc-647">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span><span class="sxs-lookup"><span data-stu-id="e05cc-647">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

```c#
        [SqlUserDefinedReducer]
        public class EmptyUserReducer : IReducer
        {

            public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
            {
            …
            }

        }
```

<span data-ttu-id="e05cc-648">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span><span class="sxs-lookup"><span data-stu-id="e05cc-648">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="e05cc-649">This class cannot be inherited.</span><span class="sxs-lookup"><span data-stu-id="e05cc-649">This class cannot be inherited.</span></span>
<span data-ttu-id="e05cc-650">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span><span class="sxs-lookup"><span data-stu-id="e05cc-650">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="e05cc-651">It's used to define IsRecursive property.</span><span class="sxs-lookup"><span data-stu-id="e05cc-651">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="e05cc-652">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="e05cc-652">bool     IsRecursive</span></span>    
* <span data-ttu-id="e05cc-653">**true**  = Indicates whether this Reducer is idempotent</span><span class="sxs-lookup"><span data-stu-id="e05cc-653">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="e05cc-654">The main programmability objects are **input** and **output**.</span><span class="sxs-lookup"><span data-stu-id="e05cc-654">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="e05cc-655">The input object is used to enumerate input rows.</span><span class="sxs-lookup"><span data-stu-id="e05cc-655">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="e05cc-656">Output is used to set output rows as a result of reducing activity.</span><span class="sxs-lookup"><span data-stu-id="e05cc-656">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="e05cc-657">For input rows enumeration, we use the `Row.Get` method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-657">For input rows enumeration, we use the `Row.Get` method.</span></span>

```c#
            foreach (IRow row in input.Rows)
            {
                        row.Get<string>("mycolumn");
            }
```

<span data-ttu-id="e05cc-658">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span><span class="sxs-lookup"><span data-stu-id="e05cc-658">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="e05cc-659">We need to use the correct data type here as well.</span><span class="sxs-lookup"><span data-stu-id="e05cc-659">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="e05cc-660">For output, use the `output.Set` method.</span><span class="sxs-lookup"><span data-stu-id="e05cc-660">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="e05cc-661">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span><span class="sxs-lookup"><span data-stu-id="e05cc-661">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```c#
    output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="e05cc-662">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="e05cc-662">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="e05cc-663">Following is a reducer example:</span><span class="sxs-lookup"><span data-stu-id="e05cc-663">Following is a reducer example:</span></span>

```c#
        [SqlUserDefinedReducer]
        public class EmptyUserReducer : IReducer
        {

            public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
            {
                string guid;
                DateTime dt;
                string user;
                string des;

                foreach (IRow row in input.Rows)
                {
                    guid = row.Get<string>("guid");
                    dt = row.Get<DateTime>("dt");
                    user = row.Get<string>("user");
                    des = row.Get<string>("des");

                    if (user.Length > 0)
                    {
                        output.Set<string>("guid", guid);
                        output.Set<DateTime>("dt", dt);
                        output.Set<string>("user", user);
                        output.Set<string>("des", des);

                        yield return output.AsReadOnly();
                    }
                }
            }

        }
```

<span data-ttu-id="e05cc-664">In this use-case scenario, the reducer is skipping rows with an empty user name.</span><span class="sxs-lookup"><span data-stu-id="e05cc-664">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="e05cc-665">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span><span class="sxs-lookup"><span data-stu-id="e05cc-665">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="e05cc-666">It outputs the actual row only if user name value length is more than 0.</span><span class="sxs-lookup"><span data-stu-id="e05cc-666">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="e05cc-667">Following is base U-SQL script that uses a custom reducer:</span><span class="sxs-lookup"><span data-stu-id="e05cc-667">Following is base U-SQL script that uses a custom reducer:</span></span>

```sql
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 TO @output_file USING Outputters.Text();
```









