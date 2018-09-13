---
title: SQLRuleAction syntax reference in Azure | Microsoft Docs
description: Details about SQLRuleAction grammar.
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
ms.openlocfilehash: b4cc2ce4d05b035829584a610d52e6079a13a9c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671875"
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="8dab8-103">SQLRuleAction syntax</span><span class="sxs-lookup"><span data-stu-id="8dab8-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="8dab8-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="8dab8-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="8dab8-105">This topic lists details about the SQL rule action grammar.</span><span class="sxs-lookup"><span data-stu-id="8dab8-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="8dab8-106">Arguments</span><span class="sxs-lookup"><span data-stu-id="8dab8-106">Arguments</span></span>  
  
-   <span data-ttu-id="8dab8-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="8dab8-108">Valid values are `sys` or `user`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="8dab8-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="8dab8-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="8dab8-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span><span class="sxs-lookup"><span data-stu-id="8dab8-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="8dab8-111">`user` scope is the default scope if `<scope>` is not specified.</span><span class="sxs-lookup"><span data-stu-id="8dab8-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-112">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-112">Remarks</span></span>  

<span data-ttu-id="8dab8-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span><span class="sxs-lookup"><span data-stu-id="8dab8-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="8dab8-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span><span class="sxs-lookup"><span data-stu-id="8dab8-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="8dab8-115">An unknown value is treated specially during operator evaluation.</span><span class="sxs-lookup"><span data-stu-id="8dab8-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="8dab8-116">property_name</span><span class="sxs-lookup"><span data-stu-id="8dab8-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="8dab8-117">Arguments</span><span class="sxs-lookup"><span data-stu-id="8dab8-117">Arguments</span></span>  
 <span data-ttu-id="8dab8-118">`<regular_identifier>` is a string represented by the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="8dab8-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="8dab8-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span><span class="sxs-lookup"><span data-stu-id="8dab8-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="8dab8-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span><span class="sxs-lookup"><span data-stu-id="8dab8-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="8dab8-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span><span class="sxs-lookup"><span data-stu-id="8dab8-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="8dab8-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span><span class="sxs-lookup"><span data-stu-id="8dab8-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="8dab8-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span><span class="sxs-lookup"><span data-stu-id="8dab8-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="8dab8-124">A `<regular_identifier>` cannot be a reserved keyword.</span><span class="sxs-lookup"><span data-stu-id="8dab8-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="8dab8-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span><span class="sxs-lookup"><span data-stu-id="8dab8-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="8dab8-126">A right square bracket is represented as two right square brackets.</span><span class="sxs-lookup"><span data-stu-id="8dab8-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="8dab8-127">The following are examples of `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="8dab8-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="8dab8-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span><span class="sxs-lookup"><span data-stu-id="8dab8-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="8dab8-129">A double quotation mark in identifier is represented as two double quotation marks.</span><span class="sxs-lookup"><span data-stu-id="8dab8-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="8dab8-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span><span class="sxs-lookup"><span data-stu-id="8dab8-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="8dab8-131">Use a delimited identifier if possible.</span><span class="sxs-lookup"><span data-stu-id="8dab8-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="8dab8-132">The following is an example of `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="8dab8-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="8dab8-133">pattern</span><span class="sxs-lookup"><span data-stu-id="8dab8-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-134">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-134">Remarks</span></span>
  
 <span data-ttu-id="8dab8-135">`<pattern>` must be an expression that is evaluated as a string.</span><span class="sxs-lookup"><span data-stu-id="8dab8-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="8dab8-136">It is used as a pattern for the LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="8dab8-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="8dab8-137">It can contain the following wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="8dab8-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="8dab8-138">`%`:  Any string of zero or more characters.</span><span class="sxs-lookup"><span data-stu-id="8dab8-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="8dab8-139">`_`: Any single character.</span><span class="sxs-lookup"><span data-stu-id="8dab8-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="8dab8-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="8dab8-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-141">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-141">Remarks</span></span>
  
 <span data-ttu-id="8dab8-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span><span class="sxs-lookup"><span data-stu-id="8dab8-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="8dab8-143">It is used as an escape character for the LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="8dab8-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="8dab8-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="8dab8-145">constant</span><span class="sxs-lookup"><span data-stu-id="8dab8-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="8dab8-146">Arguments</span><span class="sxs-lookup"><span data-stu-id="8dab8-146">Arguments</span></span>  
  
-   <span data-ttu-id="8dab8-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span><span class="sxs-lookup"><span data-stu-id="8dab8-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="8dab8-148">The values are stored as `System.Int64` internally, and follow the same range.</span><span class="sxs-lookup"><span data-stu-id="8dab8-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="8dab8-149">The following are examples of long constants:</span><span class="sxs-lookup"><span data-stu-id="8dab8-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="8dab8-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span><span class="sxs-lookup"><span data-stu-id="8dab8-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="8dab8-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span><span class="sxs-lookup"><span data-stu-id="8dab8-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="8dab8-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="8dab8-153">The following are examples of decimal constants:</span><span class="sxs-lookup"><span data-stu-id="8dab8-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="8dab8-154">`<approximate_number_constant>` is a number written in scientific notation.</span><span class="sxs-lookup"><span data-stu-id="8dab8-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="8dab8-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span><span class="sxs-lookup"><span data-stu-id="8dab8-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="8dab8-156">The following are examples of approximate number constants:</span><span class="sxs-lookup"><span data-stu-id="8dab8-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="8dab8-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="8dab8-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-158">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-158">Remarks</span></span>
  
<span data-ttu-id="8dab8-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="8dab8-160">The values are stored as `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="8dab8-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="8dab8-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-162">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-162">Remarks</span></span>
  
<span data-ttu-id="8dab8-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span><span class="sxs-lookup"><span data-stu-id="8dab8-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="8dab8-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span><span class="sxs-lookup"><span data-stu-id="8dab8-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="8dab8-165">function</span><span class="sxs-lookup"><span data-stu-id="8dab8-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="8dab8-166">Remarks</span><span class="sxs-lookup"><span data-stu-id="8dab8-166">Remarks</span></span>  

<span data-ttu-id="8dab8-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span><span class="sxs-lookup"><span data-stu-id="8dab8-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="8dab8-168">The `property(name)` function returns the value of the property referenced by `name`.</span><span class="sxs-lookup"><span data-stu-id="8dab8-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="8dab8-169">The `name` value can be any valid expression that returns a string value.</span><span class="sxs-lookup"><span data-stu-id="8dab8-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="8dab8-170">Considerations</span><span class="sxs-lookup"><span data-stu-id="8dab8-170">Considerations</span></span>

- <span data-ttu-id="8dab8-171">SET is used to create a new property or update the value of an existing property.</span><span class="sxs-lookup"><span data-stu-id="8dab8-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="8dab8-172">REMOVE is used to remove a property.</span><span class="sxs-lookup"><span data-stu-id="8dab8-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="8dab8-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span><span class="sxs-lookup"><span data-stu-id="8dab8-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="8dab8-174">Action fails if non-existent system properties were referenced.</span><span class="sxs-lookup"><span data-stu-id="8dab8-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="8dab8-175">Action does not fail if non-existent user properties were referenced.</span><span class="sxs-lookup"><span data-stu-id="8dab8-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="8dab8-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span><span class="sxs-lookup"><span data-stu-id="8dab8-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dab8-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="8dab8-177">Next steps</span></span>

- [<span data-ttu-id="8dab8-178">SQLRuleAction class</span><span class="sxs-lookup"><span data-stu-id="8dab8-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="8dab8-179">SQLFilter class</span><span class="sxs-lookup"><span data-stu-id="8dab8-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
