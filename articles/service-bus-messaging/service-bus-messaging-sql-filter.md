---
title: Azure Service Bus SQLFilter syntax reference | Microsoft Docs
description: Details about SQLFilter grammar.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: sethm
ms.openlocfilehash: c5127a457e99772a52b76e28e7fd3a3e4dd861b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556278"
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="29940-103">SQLFilter syntax</span><span class="sxs-lookup"><span data-stu-id="29940-103">SQLFilter syntax</span></span>

<span data-ttu-id="29940-104">A *SqlFilter* is an instance of the [SqlFilter Class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="29940-104">A *SqlFilter* is an instance of the [SqlFilter Class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="29940-105">A SqlFilter supports a subset of the SQL-92 standard.</span><span class="sxs-lookup"><span data-stu-id="29940-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="29940-106">This topic lists details about SqlFilter grammar.</span><span class="sxs-lookup"><span data-stu-id="29940-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a><span data-ttu-id="29940-107">Arguments</span><span class="sxs-lookup"><span data-stu-id="29940-107">Arguments</span></span>  
  
-   <span data-ttu-id="29940-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="29940-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="29940-109">Valid values are `sys` or `user`.</span><span class="sxs-lookup"><span data-stu-id="29940-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="29940-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="29940-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="29940-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span><span class="sxs-lookup"><span data-stu-id="29940-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="29940-112">`user` scope is the default scope if `<scope>` is not specified.</span><span class="sxs-lookup"><span data-stu-id="29940-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="29940-113">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-113">Remarks</span></span>

<span data-ttu-id="29940-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span><span class="sxs-lookup"><span data-stu-id="29940-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="29940-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span><span class="sxs-lookup"><span data-stu-id="29940-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="29940-116">An unknown value is treated specially during operator evaluation.</span><span class="sxs-lookup"><span data-stu-id="29940-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="29940-117">property_name</span><span class="sxs-lookup"><span data-stu-id="29940-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="29940-118">Arguments</span><span class="sxs-lookup"><span data-stu-id="29940-118">Arguments</span></span>  

 <span data-ttu-id="29940-119">`<regular_identifier>` is a string represented by the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="29940-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="29940-120">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span><span class="sxs-lookup"><span data-stu-id="29940-120">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="29940-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span><span class="sxs-lookup"><span data-stu-id="29940-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="29940-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span><span class="sxs-lookup"><span data-stu-id="29940-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="29940-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span><span class="sxs-lookup"><span data-stu-id="29940-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="29940-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span><span class="sxs-lookup"><span data-stu-id="29940-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="29940-125">A `<regular_identifier>` cannot be a reserved keyword.</span><span class="sxs-lookup"><span data-stu-id="29940-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="29940-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span><span class="sxs-lookup"><span data-stu-id="29940-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="29940-127">A right square bracket is represented as two right square brackets.</span><span class="sxs-lookup"><span data-stu-id="29940-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="29940-128">The following are examples of `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="29940-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="29940-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span><span class="sxs-lookup"><span data-stu-id="29940-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="29940-130">A double quotation mark in identifier is represented as two double quotation marks.</span><span class="sxs-lookup"><span data-stu-id="29940-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="29940-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span><span class="sxs-lookup"><span data-stu-id="29940-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="29940-132">Use a delimited identifier if possible.</span><span class="sxs-lookup"><span data-stu-id="29940-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="29940-133">The following is an example of `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="29940-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="29940-134">pattern</span><span class="sxs-lookup"><span data-stu-id="29940-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="29940-135">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-135">Remarks</span></span>
  
<span data-ttu-id="29940-136">`<pattern>` must be an expression that is evaluated as a string.</span><span class="sxs-lookup"><span data-stu-id="29940-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="29940-137">It is used as a pattern for the LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="29940-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="29940-138">It can contain the following wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="29940-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="29940-139">`%`:  Any string of zero or more characters.</span><span class="sxs-lookup"><span data-stu-id="29940-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="29940-140">`_`: Any single character.</span><span class="sxs-lookup"><span data-stu-id="29940-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="29940-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="29940-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="29940-142">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-142">Remarks</span></span>  

<span data-ttu-id="29940-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span><span class="sxs-lookup"><span data-stu-id="29940-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="29940-144">It is used as an escape character for the LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="29940-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="29940-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span><span class="sxs-lookup"><span data-stu-id="29940-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="29940-146">constant</span><span class="sxs-lookup"><span data-stu-id="29940-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="29940-147">Arguments</span><span class="sxs-lookup"><span data-stu-id="29940-147">Arguments</span></span>  
  
-   <span data-ttu-id="29940-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span><span class="sxs-lookup"><span data-stu-id="29940-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="29940-149">The values are stored as `System.Int64` internally, and follow the same range.</span><span class="sxs-lookup"><span data-stu-id="29940-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="29940-150">The following are examples of long constants:</span><span class="sxs-lookup"><span data-stu-id="29940-150">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="29940-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span><span class="sxs-lookup"><span data-stu-id="29940-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="29940-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span><span class="sxs-lookup"><span data-stu-id="29940-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="29940-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="29940-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="29940-154">The following are examples of decimal constants:</span><span class="sxs-lookup"><span data-stu-id="29940-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="29940-155">`<approximate_number_constant>` is a number written in scientific notation.</span><span class="sxs-lookup"><span data-stu-id="29940-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="29940-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span><span class="sxs-lookup"><span data-stu-id="29940-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="29940-157">The following are examples of approximate number constants:</span><span class="sxs-lookup"><span data-stu-id="29940-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="29940-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="29940-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="29940-159">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-159">Remarks</span></span>  

<span data-ttu-id="29940-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="29940-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="29940-161">The values are stored as `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="29940-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="29940-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="29940-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="29940-163">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-163">Remarks</span></span>  

<span data-ttu-id="29940-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span><span class="sxs-lookup"><span data-stu-id="29940-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="29940-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span><span class="sxs-lookup"><span data-stu-id="29940-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="29940-166">function</span><span class="sxs-lookup"><span data-stu-id="29940-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="29940-167">Remarks</span><span class="sxs-lookup"><span data-stu-id="29940-167">Remarks</span></span>
  
<span data-ttu-id="29940-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span><span class="sxs-lookup"><span data-stu-id="29940-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="29940-169">The `property(name)` function returns the value of the property referenced by `name`.</span><span class="sxs-lookup"><span data-stu-id="29940-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="29940-170">The `name` value can be any valid expression that returns a string value.</span><span class="sxs-lookup"><span data-stu-id="29940-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="29940-171">Considerations</span><span class="sxs-lookup"><span data-stu-id="29940-171">Considerations</span></span>
  
<span data-ttu-id="29940-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span><span class="sxs-lookup"><span data-stu-id="29940-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="29940-173">Property names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="29940-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="29940-174">Operators follow C# implicit conversion semantics whenever possible.</span><span class="sxs-lookup"><span data-stu-id="29940-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="29940-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span><span class="sxs-lookup"><span data-stu-id="29940-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="29940-176">Consider the following `IS [NOT] NULL` semantics:</span><span class="sxs-lookup"><span data-stu-id="29940-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="29940-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span><span class="sxs-lookup"><span data-stu-id="29940-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="29940-178">Property evaluation semantics</span><span class="sxs-lookup"><span data-stu-id="29940-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="29940-179">An attempt to evaluate a non-existent system property will throw a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span><span class="sxs-lookup"><span data-stu-id="29940-179">An attempt to evaluate a non-existent system property will throw a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="29940-180">A property that does not exist is internally evaluated as **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="29940-181">Unknown evaluation in arithmetic operators:</span><span class="sxs-lookup"><span data-stu-id="29940-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="29940-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="29940-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="29940-184">Unknown evaluation in binary comparison operators:</span><span class="sxs-lookup"><span data-stu-id="29940-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="29940-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="29940-186">Unknown evaluation in `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="29940-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="29940-187">If any operand is evaluated as **unknown** then the result is **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-187">If any operand is evaluated as **unknown** then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="29940-188">Unknown evaluation in `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="29940-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="29940-189">If the left operand is evaluated as **unknown** then the result is **unknown**.</span><span class="sxs-lookup"><span data-stu-id="29940-189">If the left operand is evaluated as **unknown** then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="29940-190">Unknown evaluation in **AND** operator:</span><span class="sxs-lookup"><span data-stu-id="29940-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="29940-191">Unknown evaluation in **OR** operator:</span><span class="sxs-lookup"><span data-stu-id="29940-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="29940-192">Operator binding semantics</span><span class="sxs-lookup"><span data-stu-id="29940-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="29940-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span><span class="sxs-lookup"><span data-stu-id="29940-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="29940-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span><span class="sxs-lookup"><span data-stu-id="29940-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29940-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="29940-195">Next steps</span></span>

- [<span data-ttu-id="29940-196">SQLFilter class</span><span class="sxs-lookup"><span data-stu-id="29940-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="29940-197">SQLRuleAction class</span><span class="sxs-lookup"><span data-stu-id="29940-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)