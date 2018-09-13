---
title: Constructing filter strings for the table designer | Microsoft Docs
description: Constructing filter strings for the table designer
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: fb2fa8e147ad32ba01db67a79526c9b500564a21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670753"
---
# <a name="constructing-filter-strings-for-the-table-designer"></a><span data-ttu-id="fb1ca-103">Constructing Filter Strings for the Table Designer</span><span class="sxs-lookup"><span data-stu-id="fb1ca-103">Constructing Filter Strings for the Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="fb1ca-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fb1ca-104">Overview</span></span>
<span data-ttu-id="fb1ca-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span></span> <span data-ttu-id="fb1ca-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span></span> <span data-ttu-id="fb1ca-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span></span> <span data-ttu-id="fb1ca-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="fb1ca-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="fb1ca-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="fb1ca-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="fb1ca-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="fb1ca-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="fb1ca-111">Comparison Operators</span><span class="sxs-lookup"><span data-stu-id="fb1ca-111">Comparison Operators</span></span>
<span data-ttu-id="fb1ca-112">The following logical operators are supported for all property types:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-112">The following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="fb1ca-113">Logical operator</span><span class="sxs-lookup"><span data-stu-id="fb1ca-113">Logical operator</span></span> | <span data-ttu-id="fb1ca-114">Description</span><span class="sxs-lookup"><span data-stu-id="fb1ca-114">Description</span></span> | <span data-ttu-id="fb1ca-115">Example filter string</span><span class="sxs-lookup"><span data-stu-id="fb1ca-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb1ca-116">eq</span><span class="sxs-lookup"><span data-stu-id="fb1ca-116">eq</span></span> |<span data-ttu-id="fb1ca-117">Equal</span><span class="sxs-lookup"><span data-stu-id="fb1ca-117">Equal</span></span> |<span data-ttu-id="fb1ca-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="fb1ca-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="fb1ca-119">gt</span><span class="sxs-lookup"><span data-stu-id="fb1ca-119">gt</span></span> |<span data-ttu-id="fb1ca-120">Greater than</span><span class="sxs-lookup"><span data-stu-id="fb1ca-120">Greater than</span></span> |<span data-ttu-id="fb1ca-121">Price gt 20</span><span class="sxs-lookup"><span data-stu-id="fb1ca-121">Price gt 20</span></span> |
| <span data-ttu-id="fb1ca-122">ge</span><span class="sxs-lookup"><span data-stu-id="fb1ca-122">ge</span></span> |<span data-ttu-id="fb1ca-123">Greater than or equal to</span><span class="sxs-lookup"><span data-stu-id="fb1ca-123">Greater than or equal to</span></span> |<span data-ttu-id="fb1ca-124">Price ge 10</span><span class="sxs-lookup"><span data-stu-id="fb1ca-124">Price ge 10</span></span> |
| <span data-ttu-id="fb1ca-125">lt</span><span class="sxs-lookup"><span data-stu-id="fb1ca-125">lt</span></span> |<span data-ttu-id="fb1ca-126">Less than</span><span class="sxs-lookup"><span data-stu-id="fb1ca-126">Less than</span></span> |<span data-ttu-id="fb1ca-127">Price lt 20</span><span class="sxs-lookup"><span data-stu-id="fb1ca-127">Price lt 20</span></span> |
| <span data-ttu-id="fb1ca-128">le</span><span class="sxs-lookup"><span data-stu-id="fb1ca-128">le</span></span> |<span data-ttu-id="fb1ca-129">Less than or equal</span><span class="sxs-lookup"><span data-stu-id="fb1ca-129">Less than or equal</span></span> |<span data-ttu-id="fb1ca-130">Price le 100</span><span class="sxs-lookup"><span data-stu-id="fb1ca-130">Price le 100</span></span> |
| <span data-ttu-id="fb1ca-131">ne</span><span class="sxs-lookup"><span data-stu-id="fb1ca-131">ne</span></span> |<span data-ttu-id="fb1ca-132">Not equal</span><span class="sxs-lookup"><span data-stu-id="fb1ca-132">Not equal</span></span> |<span data-ttu-id="fb1ca-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="fb1ca-133">City ne 'London'</span></span> |
| <span data-ttu-id="fb1ca-134">and</span><span class="sxs-lookup"><span data-stu-id="fb1ca-134">and</span></span> |<span data-ttu-id="fb1ca-135">And</span><span class="sxs-lookup"><span data-stu-id="fb1ca-135">And</span></span> |<span data-ttu-id="fb1ca-136">Price le 200 and Price gt 3.5</span><span class="sxs-lookup"><span data-stu-id="fb1ca-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="fb1ca-137">or</span><span class="sxs-lookup"><span data-stu-id="fb1ca-137">or</span></span> |<span data-ttu-id="fb1ca-138">Or</span><span class="sxs-lookup"><span data-stu-id="fb1ca-138">Or</span></span> |<span data-ttu-id="fb1ca-139">Price le 3.5 or Price gt 200</span><span class="sxs-lookup"><span data-stu-id="fb1ca-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="fb1ca-140">not</span><span class="sxs-lookup"><span data-stu-id="fb1ca-140">not</span></span> |<span data-ttu-id="fb1ca-141">Not</span><span class="sxs-lookup"><span data-stu-id="fb1ca-141">Not</span></span> |<span data-ttu-id="fb1ca-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="fb1ca-142">not isAvailable</span></span> |

<span data-ttu-id="fb1ca-143">When constructing a filter string, the following rules are important:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-143">When constructing a filter string, the following rules are important:</span></span>

* <span data-ttu-id="fb1ca-144">Use the logical operators to compare a property to a value.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-144">Use the logical operators to compare a property to a value.</span></span> <span data-ttu-id="fb1ca-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span></span>
* <span data-ttu-id="fb1ca-146">All parts of the filter string are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-146">All parts of the filter string are case-sensitive.</span></span>
* <span data-ttu-id="fb1ca-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="fb1ca-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="fb1ca-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="fb1ca-149">Filtering on String Properties</span><span class="sxs-lookup"><span data-stu-id="fb1ca-149">Filtering on String Properties</span></span>
<span data-ttu-id="fb1ca-150">When you filter on string properties, enclose the string constant in single quotation marks.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-150">When you filter on string properties, enclose the string constant in single quotation marks.</span></span>

<span data-ttu-id="fb1ca-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="fb1ca-152">You can enclose each filter expression in parentheses, although it is not required:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="fb1ca-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span></span> <span data-ttu-id="fb1ca-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span></span> <span data-ttu-id="fb1ca-155">The following example returns entities with a LastName property beginning with the letter 'A':</span><span class="sxs-lookup"><span data-stu-id="fb1ca-155">The following example returns entities with a LastName property beginning with the letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="fb1ca-156">Filtering on Numeric Properties</span><span class="sxs-lookup"><span data-stu-id="fb1ca-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="fb1ca-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span></span>

<span data-ttu-id="fb1ca-158">This example returns all entities with an Age property whose value is greater than 30:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="fb1ca-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="fb1ca-160">Filtering on Boolean Properties</span><span class="sxs-lookup"><span data-stu-id="fb1ca-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="fb1ca-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="fb1ca-162">The following example returns all entities where the IsActive property is set to **true**:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-162">The following example returns all entities where the IsActive property is set to **true**:</span></span>

    IsActive eq true

<span data-ttu-id="fb1ca-163">You can also write this filter expression without the logical operator.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-163">You can also write this filter expression without the logical operator.</span></span> <span data-ttu-id="fb1ca-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="fb1ca-165">To return all entities where IsActive is false, you can use the not operator:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-165">To return all entities where IsActive is false, you can use the not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="fb1ca-166">Filtering on DateTime Properties</span><span class="sxs-lookup"><span data-stu-id="fb1ca-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="fb1ca-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span><span class="sxs-lookup"><span data-stu-id="fb1ca-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span></span> <span data-ttu-id="fb1ca-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="fb1ca-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="fb1ca-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="fb1ca-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
