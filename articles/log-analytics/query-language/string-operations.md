---
title: Working with strings in Azure Log Analytics queries | Microsoft Docs
description: This article provides a tutorial for using the Analytics portal to write queries in Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/16/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: de1ba8b8560e65586ac59f9a04165a93492f3e05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870441"
---
# <a name="working-with-strings-in-log-analytics-queries"></a><span data-ttu-id="3ee7a-103">Working with strings in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="3ee7a-103">Working with strings in Log Analytics queries</span></span>


> [!NOTE]
> <span data-ttu-id="3ee7a-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this tutorial.</span></span>

<span data-ttu-id="3ee7a-105">This article describes how to edit, compare, search in and perform a variety of other operations on strings.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-105">This article describes how to edit, compare, search in and perform a variety of other operations on strings.</span></span> 

<span data-ttu-id="3ee7a-106">Each character in a string has an index number, according to its location.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-106">Each character in a string has an index number, according to its location.</span></span> <span data-ttu-id="3ee7a-107">The first character is at index 0, the next character is 1, and so one.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-107">The first character is at index 0, the next character is 1, and so one.</span></span> <span data-ttu-id="3ee7a-108">Different string functions use index numbers as shown in the following sections.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-108">Different string functions use index numbers as shown in the following sections.</span></span> <span data-ttu-id="3ee7a-109">Many of the following examples use the **print** command for to demonstrate string manipulation without using a specific data source.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-109">Many of the following examples use the **print** command for to demonstrate string manipulation without using a specific data source.</span></span>


## <a name="strings-and-escaping-them"></a><span data-ttu-id="3ee7a-110">Strings and escaping them</span><span class="sxs-lookup"><span data-stu-id="3ee7a-110">Strings and escaping them</span></span>
<span data-ttu-id="3ee7a-111">String values are wrapped with either with single or double quote characters.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-111">String values are wrapped with either with single or double quote characters.</span></span> <span data-ttu-id="3ee7a-112">Backslash (\) is used to escape characters to the character following it, such as \t for tab, \n for newline, and \" the quote character itself.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-112">Backslash (\) is used to escape characters to the character following it, such as \t for tab, \n for newline, and \" the quote character itself.</span></span>

```OQL
print "this is a 'string' literal in double \" quotes"
```

<span data-ttu-id="3ee7a-113">To prevent "\\" from acting as an escape character, add "@" as a prefix to the string:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-113">To prevent "\\" from acting as an escape character, add "@" as a prefix to the string:</span></span>

```OQL
print @"C:\backslash\not\escaped\with @ prefix"
```


## <a name="string-comparisons"></a><span data-ttu-id="3ee7a-114">String comparisons</span><span class="sxs-lookup"><span data-stu-id="3ee7a-114">String comparisons</span></span>

<span data-ttu-id="3ee7a-115">Operator</span><span class="sxs-lookup"><span data-stu-id="3ee7a-115">Operator</span></span>       |<span data-ttu-id="3ee7a-116">Description</span><span class="sxs-lookup"><span data-stu-id="3ee7a-116">Description</span></span>                         |<span data-ttu-id="3ee7a-117">Case-Sensitive</span><span class="sxs-lookup"><span data-stu-id="3ee7a-117">Case-Sensitive</span></span>|<span data-ttu-id="3ee7a-118">Example (yields `true`)</span><span class="sxs-lookup"><span data-stu-id="3ee7a-118">Example (yields `true`)</span></span>
---------------|------------------------------------|--------------|-----------------------
`==`           |<span data-ttu-id="3ee7a-119">Equals</span><span class="sxs-lookup"><span data-stu-id="3ee7a-119">Equals</span></span>                              |<span data-ttu-id="3ee7a-120">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-120">Yes</span></span>           |`"aBc" == "aBc"`
`!=`           |<span data-ttu-id="3ee7a-121">Not equals</span><span class="sxs-lookup"><span data-stu-id="3ee7a-121">Not equals</span></span>                          |<span data-ttu-id="3ee7a-122">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-122">Yes</span></span>           |`"abc" != "ABC"`
`=~`           |<span data-ttu-id="3ee7a-123">Equals</span><span class="sxs-lookup"><span data-stu-id="3ee7a-123">Equals</span></span>                              |<span data-ttu-id="3ee7a-124">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-124">No</span></span>            |`"abc" =~ "ABC"`
`!~`           |<span data-ttu-id="3ee7a-125">Not equals</span><span class="sxs-lookup"><span data-stu-id="3ee7a-125">Not equals</span></span>                          |<span data-ttu-id="3ee7a-126">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-126">No</span></span>            |`"aBc" !~ "xyz"`
`has`          |<span data-ttu-id="3ee7a-127">Right-hand-side is a whole term in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-127">Right-hand-side is a whole term in left-hand-side</span></span> |<span data-ttu-id="3ee7a-128">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-128">No</span></span>|`"North America" has "america"`
`!has`         |<span data-ttu-id="3ee7a-129">Right-hand-side isn't a full term in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-129">Right-hand-side isn't a full term in left-hand-side</span></span>       |<span data-ttu-id="3ee7a-130">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-130">No</span></span>            |`"North America" !has "amer"` 
`has_cs`       |<span data-ttu-id="3ee7a-131">Right-hand-side is a whole term in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-131">Right-hand-side is a whole term in left-hand-side</span></span> |<span data-ttu-id="3ee7a-132">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-132">Yes</span></span>|`"North America" has_cs "America"`
`!has_cs`      |<span data-ttu-id="3ee7a-133">Right-hand-side isn't a full term in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-133">Right-hand-side isn't a full term in left-hand-side</span></span>       |<span data-ttu-id="3ee7a-134">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-134">Yes</span></span>            |`"North America" !has_cs "amer"` 
`hasprefix`    |<span data-ttu-id="3ee7a-135">Right-hand-side is a term prefix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-135">Right-hand-side is a term prefix in left-hand-side</span></span>         |<span data-ttu-id="3ee7a-136">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-136">No</span></span>            |`"North America" hasprefix "ame"`
`!hasprefix`   |<span data-ttu-id="3ee7a-137">Right-hand-side isn't a term prefix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-137">Right-hand-side isn't a term prefix in left-hand-side</span></span>     |<span data-ttu-id="3ee7a-138">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-138">No</span></span>            |`"North America" !hasprefix "mer"` 
`hasprefix_cs`    |<span data-ttu-id="3ee7a-139">Right-hand-side is a term prefix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-139">Right-hand-side is a term prefix in left-hand-side</span></span>         |<span data-ttu-id="3ee7a-140">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-140">Yes</span></span>            |`"North America" hasprefix_cs "Ame"`
`!hasprefix_cs`   |<span data-ttu-id="3ee7a-141">Right-hand-side isn't a term prefix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-141">Right-hand-side isn't a term prefix in left-hand-side</span></span>     |<span data-ttu-id="3ee7a-142">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-142">Yes</span></span>            |`"North America" !hasprefix_cs "CA"` 
`hassuffix`    |<span data-ttu-id="3ee7a-143">Right-hand-side is a term suffix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-143">Right-hand-side is a term suffix in left-hand-side</span></span>         |<span data-ttu-id="3ee7a-144">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-144">No</span></span>            |`"North America" hassuffix "ica"`
`!hassuffix`   |<span data-ttu-id="3ee7a-145">Right-hand-side isn't a term suffix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-145">Right-hand-side isn't a term suffix in left-hand-side</span></span>     |<span data-ttu-id="3ee7a-146">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-146">No</span></span>            |<span data-ttu-id="3ee7a-147">\`"North America" !hassuffix "americ"</span><span class="sxs-lookup"><span data-stu-id="3ee7a-147">\`"North America" !hassuffix "americ"</span></span>
`hassuffix_cs`    |<span data-ttu-id="3ee7a-148">Right-hand-side is a term suffix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-148">Right-hand-side is a term suffix in left-hand-side</span></span>         |<span data-ttu-id="3ee7a-149">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-149">Yes</span></span>            |`"North America" hassuffix_cs "ica"`
`!hassuffix_cs`   |<span data-ttu-id="3ee7a-150">Right-hand-side isn't a term suffix in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-150">Right-hand-side isn't a term suffix in left-hand-side</span></span>     |<span data-ttu-id="3ee7a-151">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-151">Yes</span></span>            |<span data-ttu-id="3ee7a-152">\`"North America" !hassuffix_cs "icA"</span><span class="sxs-lookup"><span data-stu-id="3ee7a-152">\`"North America" !hassuffix_cs "icA"</span></span>
`contains`     |<span data-ttu-id="3ee7a-153">Right-hand-side occurs as a subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-153">Right-hand-side occurs as a subsequence of left-hand-side</span></span>  |<span data-ttu-id="3ee7a-154">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-154">No</span></span>            |`"FabriKam" contains "BRik"`
`!contains`    |<span data-ttu-id="3ee7a-155">Right-hand-side doesn't occur in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-155">Right-hand-side doesn't occur in left-hand-side</span></span>           |<span data-ttu-id="3ee7a-156">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-156">No</span></span>            |`"Fabrikam" !contains "xyz"`
`contains_cs`   |<span data-ttu-id="3ee7a-157">Right-hand-side occurs as a subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-157">Right-hand-side occurs as a subsequence of left-hand-side</span></span>  |<span data-ttu-id="3ee7a-158">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-158">Yes</span></span>           |`"FabriKam" contains_cs "Kam"`
`!contains_cs`  |<span data-ttu-id="3ee7a-159">Right-hand-side doesn't occur in left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-159">Right-hand-side doesn't occur in left-hand-side</span></span>           |<span data-ttu-id="3ee7a-160">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-160">Yes</span></span>           |`"Fabrikam" !contains_cs "Kam"`
`startswith`   |<span data-ttu-id="3ee7a-161">Right-hand-side is an initial subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-161">Right-hand-side is an initial subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-162">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-162">No</span></span>            |`"Fabrikam" startswith "fab"`
`!startswith`  |<span data-ttu-id="3ee7a-163">Right-hand-side isn't an initial subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-163">Right-hand-side isn't an initial subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-164">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-164">No</span></span>        |`"Fabrikam" !startswith "kam"`
`startswith_cs`   |<span data-ttu-id="3ee7a-165">Right-hand-side is an initial subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-165">Right-hand-side is an initial subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-166">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-166">Yes</span></span>            |`"Fabrikam" startswith_cs "Fab"`
`!startswith_cs`  |<span data-ttu-id="3ee7a-167">Right-hand-side isn't an initial subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-167">Right-hand-side isn't an initial subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-168">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-168">Yes</span></span>        |`"Fabrikam" !startswith_cs "fab"`
`endswith`     |<span data-ttu-id="3ee7a-169">Right-hand-side is a closing subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-169">Right-hand-side is a closing subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-170">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-170">No</span></span>             |`"Fabrikam" endswith "Kam"`
`!endswith`    |<span data-ttu-id="3ee7a-171">Right-hand-side isn't a closing subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-171">Right-hand-side isn't a closing subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-172">No</span><span class="sxs-lookup"><span data-stu-id="3ee7a-172">No</span></span>         |`"Fabrikam" !endswith "brik"`
`endswith_cs`     |<span data-ttu-id="3ee7a-173">Right-hand-side is a closing subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-173">Right-hand-side is a closing subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-174">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-174">Yes</span></span>             |`"Fabrikam" endswith "Kam"`
`!endswith_cs`    |<span data-ttu-id="3ee7a-175">Right-hand-side isn't a closing subsequence of left-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-175">Right-hand-side isn't a closing subsequence of left-hand-side</span></span>|<span data-ttu-id="3ee7a-176">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-176">Yes</span></span>         |`"Fabrikam" !endswith "brik"`
`matches regex`|<span data-ttu-id="3ee7a-177">left-hand-side contains a match for Right-hand-side</span><span class="sxs-lookup"><span data-stu-id="3ee7a-177">left-hand-side contains a match for Right-hand-side</span></span>        |<span data-ttu-id="3ee7a-178">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-178">Yes</span></span>           |`"Fabrikam" matches regex "b.*k"`
`in`           |<span data-ttu-id="3ee7a-179">Equals to one of the elements</span><span class="sxs-lookup"><span data-stu-id="3ee7a-179">Equals to one of the elements</span></span>       |<span data-ttu-id="3ee7a-180">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-180">Yes</span></span>           |`"abc" in ("123", "345", "abc")`
`!in`          |<span data-ttu-id="3ee7a-181">Not equals to any of the elements</span><span class="sxs-lookup"><span data-stu-id="3ee7a-181">Not equals to any of the elements</span></span>   |<span data-ttu-id="3ee7a-182">Yes</span><span class="sxs-lookup"><span data-stu-id="3ee7a-182">Yes</span></span>           |`"bca" !in ("123", "345", "abc")`


## <a name="countof"></a><span data-ttu-id="3ee7a-183">countof</span><span class="sxs-lookup"><span data-stu-id="3ee7a-183">countof</span></span>

<span data-ttu-id="3ee7a-184">Counts occurrences of a substring in a string.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-184">Counts occurrences of a substring in a string.</span></span> <span data-ttu-id="3ee7a-185">Can match plain strings or use regex.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-185">Can match plain strings or use regex.</span></span> <span data-ttu-id="3ee7a-186">Plain string matches may overlap while regex matches don't.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-186">Plain string matches may overlap while regex matches don't.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-187">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-187">Syntax</span></span>
```
countof(text, search [, kind])
```

### <a name="arguments"></a><span data-ttu-id="3ee7a-188">Arguments:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-188">Arguments:</span></span>
- <span data-ttu-id="3ee7a-189">`text` - The input string</span><span class="sxs-lookup"><span data-stu-id="3ee7a-189">`text` - The input string</span></span> 
- <span data-ttu-id="3ee7a-190">`search` - Plain string or regular expression to match inside text.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-190">`search` - Plain string or regular expression to match inside text.</span></span>
- <span data-ttu-id="3ee7a-191">`kind` - _normal_ | _regex_ (default: normal).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-191">`kind` - _normal_ | _regex_ (default: normal).</span></span>

### <a name="returns"></a><span data-ttu-id="3ee7a-192">Returns</span><span class="sxs-lookup"><span data-stu-id="3ee7a-192">Returns</span></span>

<span data-ttu-id="3ee7a-193">The number of times that the search string can be matched in the container.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-193">The number of times that the search string can be matched in the container.</span></span> <span data-ttu-id="3ee7a-194">Plain string matches may overlap while regex matches do not.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-194">Plain string matches may overlap while regex matches do not.</span></span>

### <a name="examples"></a><span data-ttu-id="3ee7a-195">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-195">Examples</span></span>

#### <a name="plain-string-matches"></a><span data-ttu-id="3ee7a-196">Plain string matches</span><span class="sxs-lookup"><span data-stu-id="3ee7a-196">Plain string matches</span></span>

```OQL
print countof("The cat sat on the mat", "at");  //result: 3
print countof("aaa", "a");  //result: 3
print countof("aaaa", "aa");  //result: 3 (not 2!)
print countof("ababa", "ab", "normal");  //result: 2
print countof("ababa", "aba");  //result: 2
```

#### <a name="regex-matches"></a><span data-ttu-id="3ee7a-197">Regex matches</span><span class="sxs-lookup"><span data-stu-id="3ee7a-197">Regex matches</span></span>

```OQL
print countof("The cat sat on the mat", @"\b.at\b", "regex");  //result: 3
print countof("ababa", "aba", "regex");  //result: 1
print countof("abcabc", "a.c", "regex");  // result: 2
```


## <a name="extract"></a><span data-ttu-id="3ee7a-198">extract</span><span class="sxs-lookup"><span data-stu-id="3ee7a-198">extract</span></span>

<span data-ttu-id="3ee7a-199">Gets a match for a regular expression from a given string.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-199">Gets a match for a regular expression from a given string.</span></span> <span data-ttu-id="3ee7a-200">Optionally also converts the extracted substring the specified type.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-200">Optionally also converts the extracted substring the specified type.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-201">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-201">Syntax</span></span>

```OQL
extract(regex, captureGroup, text [, typeLiteral])
```

### <a name="arguments"></a><span data-ttu-id="3ee7a-202">Arguments</span><span class="sxs-lookup"><span data-stu-id="3ee7a-202">Arguments</span></span>

- <span data-ttu-id="3ee7a-203">`regex` - A regular expression.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-203">`regex` - A regular expression.</span></span>
- <span data-ttu-id="3ee7a-204">`captureGroup` - A positive integer constant indicating the capture group to extract.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-204">`captureGroup` - A positive integer constant indicating the capture group to extract.</span></span> <span data-ttu-id="3ee7a-205">0 for the entire match, 1 for the value matched by the first '('parenthesis')' in the regular expression, 2 or more for subsequent parentheses.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-205">0 for the entire match, 1 for the value matched by the first '('parenthesis')' in the regular expression, 2 or more for subsequent parentheses.</span></span>
- <span data-ttu-id="3ee7a-206">`text` - A string to search.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-206">`text` - A string to search.</span></span>
- <span data-ttu-id="3ee7a-207">`typeLiteral` - An optional type literal (for example, typeof(long)).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-207">`typeLiteral` - An optional type literal (for example, typeof(long)).</span></span> <span data-ttu-id="3ee7a-208">If provided, the extracted substring is converted to this type.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-208">If provided, the extracted substring is converted to this type.</span></span>

### <a name="returns"></a><span data-ttu-id="3ee7a-209">Returns</span><span class="sxs-lookup"><span data-stu-id="3ee7a-209">Returns</span></span>
<span data-ttu-id="3ee7a-210">The substring matched against the indicated capture group captureGroup, optionally converted to typeLiteral.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-210">The substring matched against the indicated capture group captureGroup, optionally converted to typeLiteral.</span></span>
<span data-ttu-id="3ee7a-211">If there's no match, or the type conversion fails, return null.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-211">If there's no match, or the type conversion fails, return null.</span></span>

### <a name="examples"></a><span data-ttu-id="3ee7a-212">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-212">Examples</span></span>

<span data-ttu-id="3ee7a-213">The following example extracts the last octet of *ComputerIP* from a heartbeat record:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-213">The following example extracts the last octet of *ComputerIP* from a heartbeat record:</span></span>
```OQL
Heartbeat
| where ComputerIP != "" 
| take 1
| project ComputerIP, last_octet=extract("([0-9]*$)", 1, ComputerIP) 
```

<span data-ttu-id="3ee7a-214">The following example extracts the last octet, casts it to a *real* type (number) and calculates the next IP value</span><span class="sxs-lookup"><span data-stu-id="3ee7a-214">The following example extracts the last octet, casts it to a *real* type (number) and calculates the next IP value</span></span>
```OQL
Heartbeat
| where ComputerIP != "" 
| take 1
| extend last_octet=extract("([0-9]*$)", 1, ComputerIP, typeof(real)) 
| extend next_ip=(last_octet+1)%255
| project ComputerIP, last_octet, next_ip
```

<span data-ttu-id="3ee7a-215">In the example below, the string *Trace* is searched for a definition of "Duration".</span><span class="sxs-lookup"><span data-stu-id="3ee7a-215">In the example below, the string *Trace* is searched for a definition of "Duration".</span></span> <span data-ttu-id="3ee7a-216">The match is cast to *real* and multiplied by a time constant (1 s) *which casts Duration to type timespan*.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-216">The match is cast to *real* and multiplied by a time constant (1 s) *which casts Duration to type timespan*.</span></span>
```OQL
let Trace="A=12, B=34, Duration=567, ...";
print Duration = extract("Duration=([0-9.]+)", 1, Trace, typeof(real));  //result: 567
print Duration_seconds =  extract("Duration=([0-9.]+)", 1, Trace, typeof(real)) * time(1s);  //result: 00:09:27
```


## <a name="isempty-isnotempty-notempty"></a><span data-ttu-id="3ee7a-217">isempty, isnotempty, notempty</span><span class="sxs-lookup"><span data-stu-id="3ee7a-217">isempty, isnotempty, notempty</span></span>

- <span data-ttu-id="3ee7a-218">*isempty* returns true if the argument is an empty string or null (see also *isnull*).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-218">*isempty* returns true if the argument is an empty string or null (see also *isnull*).</span></span>
- <span data-ttu-id="3ee7a-219">*isnotempty* returns true if the argument isn't an empty string or a null (see also *isnotnull*).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-219">*isnotempty* returns true if the argument isn't an empty string or a null (see also *isnotnull*).</span></span> <span data-ttu-id="3ee7a-220">alias: *notempty*.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-220">alias: *notempty*.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-221">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-221">Syntax</span></span>

```
isempty(value)
isnotempty(value)
```

### <a name="examples"></a><span data-ttu-id="3ee7a-222">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-222">Examples</span></span>

```OQL
print isempty("");  // result: true

print isempty("0");  // result: false

print isempty(0);  // result: false

print isempty(5);  // result: false

Heartbeat | where isnotempty(ComputerIP) | take 1  // return 1 Heartbeat record in which ComputerIP isn't empty
```


## <a name="parseurl"></a><span data-ttu-id="3ee7a-223">parseurl</span><span class="sxs-lookup"><span data-stu-id="3ee7a-223">parseurl</span></span>

<span data-ttu-id="3ee7a-224">Splits a URL into its parts (protocol, host, port, etc.), and returns a dictionary object containing the parts as strings.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-224">Splits a URL into its parts (protocol, host, port, etc.), and returns a dictionary object containing the parts as strings.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-225">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-225">Syntax</span></span>

```
parseurl(urlstring)
```

### <a name="examples"></a><span data-ttu-id="3ee7a-226">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-226">Examples</span></span>

```OQL
print parseurl("http://user:pass@contoso.com/icecream/buy.aspx?a=1&b=2#tag")
```

<span data-ttu-id="3ee7a-227">The outcome will be:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-227">The outcome will be:</span></span>
```
{
    "Scheme" : "http",
    "Host" : "contoso.com",
    "Port" : "80",
    "Path" : "/icecream/buy.aspx",
    "Username" : "user",
    "Password" : "pass",
    "Query Parameters" : {"a":"1","b":"2"},
    "Fragment" : "tag"
}
```


## <a name="replace"></a><span data-ttu-id="3ee7a-228">replace</span><span class="sxs-lookup"><span data-stu-id="3ee7a-228">replace</span></span>

<span data-ttu-id="3ee7a-229">Replaces all regex matches with another string.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-229">Replaces all regex matches with another string.</span></span> 

### <a name="syntax"></a><span data-ttu-id="3ee7a-230">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-230">Syntax</span></span>

```
replace(regex, rewrite, input_text)
```

### <a name="arguments"></a><span data-ttu-id="3ee7a-231">Arguments</span><span class="sxs-lookup"><span data-stu-id="3ee7a-231">Arguments</span></span>

- <span data-ttu-id="3ee7a-232">`regex` - The regular expression to match by.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-232">`regex` - The regular expression to match by.</span></span> <span data-ttu-id="3ee7a-233">It can contain capture groups in '('parentheses')'.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-233">It can contain capture groups in '('parentheses')'.</span></span>
- <span data-ttu-id="3ee7a-234">`rewrite` - The replacement regex for any match made by matching regex.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-234">`rewrite` - The replacement regex for any match made by matching regex.</span></span> <span data-ttu-id="3ee7a-235">Use \0 to refer to the whole match, \1 for the first capture group, \2, and so on for subsequent capture groups.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-235">Use \0 to refer to the whole match, \1 for the first capture group, \2, and so on for subsequent capture groups.</span></span>
- <span data-ttu-id="3ee7a-236">`input_text` - The input string to search in.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-236">`input_text` - The input string to search in.</span></span>

### <a name="returns"></a><span data-ttu-id="3ee7a-237">Returns</span><span class="sxs-lookup"><span data-stu-id="3ee7a-237">Returns</span></span>
<span data-ttu-id="3ee7a-238">The text after replacing all matches of regex with evaluations of rewrite.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-238">The text after replacing all matches of regex with evaluations of rewrite.</span></span> <span data-ttu-id="3ee7a-239">Matches don't overlap.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-239">Matches don't overlap.</span></span>

### <a name="examples"></a><span data-ttu-id="3ee7a-240">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-240">Examples</span></span>

```OQL
SecurityEvent
| take 1
| project Activity 
| extend replaced = replace(@"(\d+) -", @"Activity ID \1: ", Activity) 
```

<span data-ttu-id="3ee7a-241">Can have the following results:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-241">Can have the following results:</span></span>
<span data-ttu-id="3ee7a-242">Activity</span><span class="sxs-lookup"><span data-stu-id="3ee7a-242">Activity</span></span>                                        |<span data-ttu-id="3ee7a-243">replaced</span><span class="sxs-lookup"><span data-stu-id="3ee7a-243">replaced</span></span>
------------------------------------------------|----------------------------------------------------------
<span data-ttu-id="3ee7a-244">4663 - An attempt was made to access an object</span><span class="sxs-lookup"><span data-stu-id="3ee7a-244">4663 - An attempt was made to access an object</span></span>  |<span data-ttu-id="3ee7a-245">Activity ID 4663: An attempt was made to access an object.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-245">Activity ID 4663: An attempt was made to access an object.</span></span>


## <a name="split"></a><span data-ttu-id="3ee7a-246">split</span><span class="sxs-lookup"><span data-stu-id="3ee7a-246">split</span></span>

<span data-ttu-id="3ee7a-247">Splits a given string according to a specified delimiter, and returns an array of the resulting substrings.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-247">Splits a given string according to a specified delimiter, and returns an array of the resulting substrings.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-248">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-248">Syntax</span></span>
```
split(source, delimiter [, requestedIndex])
```

### <a name="arguments"></a><span data-ttu-id="3ee7a-249">Arguments:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-249">Arguments:</span></span>

- <span data-ttu-id="3ee7a-250">`source` - The string to be split according to the specified delimiter.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-250">`source` - The string to be split according to the specified delimiter.</span></span>
- <span data-ttu-id="3ee7a-251">`delimiter` - The delimiter that will be used in order to split the source string.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-251">`delimiter` - The delimiter that will be used in order to split the source string.</span></span>
- <span data-ttu-id="3ee7a-252">`requestedIndex` - An optional zero-based index.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-252">`requestedIndex` - An optional zero-based index.</span></span> <span data-ttu-id="3ee7a-253">If provided, the returned string array will hold only that item (if exists).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-253">If provided, the returned string array will hold only that item (if exists).</span></span>


### <a name="examples"></a><span data-ttu-id="3ee7a-254">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-254">Examples</span></span>

```OQL
print split("aaa_bbb_ccc", "_");    // result: ["aaa","bbb","ccc"]
print split("aa_bb", "_");          // result: ["aa","bb"]
print split("aaa_bbb_ccc", "_", 1); // result: ["bbb"]
print split("", "_");               // result: [""]
print split("a__b", "_");           // result: ["a","","b"]
print split("aabbcc", "bb");        // result: ["aa","cc"]
```

## <a name="strcat"></a><span data-ttu-id="3ee7a-255">strcat</span><span class="sxs-lookup"><span data-stu-id="3ee7a-255">strcat</span></span>

<span data-ttu-id="3ee7a-256">Concatenates string arguments (supports 1-16 arguments).</span><span class="sxs-lookup"><span data-stu-id="3ee7a-256">Concatenates string arguments (supports 1-16 arguments).</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-257">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-257">Syntax</span></span>
```
strcat("string1", "string2", "string3")
```

### <a name="examples"></a><span data-ttu-id="3ee7a-258">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-258">Examples</span></span>
```OQL
print strcat("hello", " ", "world") // result: "hello world"
```


## <a name="strlen"></a><span data-ttu-id="3ee7a-259">strlen</span><span class="sxs-lookup"><span data-stu-id="3ee7a-259">strlen</span></span>

<span data-ttu-id="3ee7a-260">Returns the length of a string.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-260">Returns the length of a string.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-261">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-261">Syntax</span></span>
```
strlen("text_to_evaluate")
```

### <a name="examples"></a><span data-ttu-id="3ee7a-262">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-262">Examples</span></span>
```OQL
print strlen("hello")   // result: 5
```


## <a name="substring"></a><span data-ttu-id="3ee7a-263">substring</span><span class="sxs-lookup"><span data-stu-id="3ee7a-263">substring</span></span>

<span data-ttu-id="3ee7a-264">Extracts a substring from a given source string, starting at the specified index.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-264">Extracts a substring from a given source string, starting at the specified index.</span></span> <span data-ttu-id="3ee7a-265">Optionally, the length of the requested substring can be specified.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-265">Optionally, the length of the requested substring can be specified.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-266">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-266">Syntax</span></span>
```
substring(source, startingIndex [, length])
```

### <a name="arguments"></a><span data-ttu-id="3ee7a-267">Arguments:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-267">Arguments:</span></span>

- <span data-ttu-id="3ee7a-268">`source` - The source string that the substring will be taken from.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-268">`source` - The source string that the substring will be taken from.</span></span>
- <span data-ttu-id="3ee7a-269">`startingIndex` - The zero-based starting character position of the requested substring.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-269">`startingIndex` - The zero-based starting character position of the requested substring.</span></span>
- <span data-ttu-id="3ee7a-270">`length` - An optional parameter that can be used to specify the requested length of the returned substring.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-270">`length` - An optional parameter that can be used to specify the requested length of the returned substring.</span></span>

### <a name="examples"></a><span data-ttu-id="3ee7a-271">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-271">Examples</span></span>
```OQL
print substring("abcdefg", 1, 2);   // result: "bc"
print substring("123456", 1);       // result: "23456"
print substring("123456", 2, 2);    // result: "34"
print substring("ABCD", 0, 2);  // result: "AB"
```


## <a name="tolower-toupper"></a><span data-ttu-id="3ee7a-272">tolower, toupper</span><span class="sxs-lookup"><span data-stu-id="3ee7a-272">tolower, toupper</span></span>

<span data-ttu-id="3ee7a-273">Converts a given string to all lower or upper case.</span><span class="sxs-lookup"><span data-stu-id="3ee7a-273">Converts a given string to all lower or upper case.</span></span>

### <a name="syntax"></a><span data-ttu-id="3ee7a-274">Syntax</span><span class="sxs-lookup"><span data-stu-id="3ee7a-274">Syntax</span></span>
```
tolower("value")
toupper("value")
```

### <a name="examples"></a><span data-ttu-id="3ee7a-275">Examples</span><span class="sxs-lookup"><span data-stu-id="3ee7a-275">Examples</span></span>
```OQL
print tolower("HELLO"); // result: "hello"
print toupper("hello"); // result: "HELLO"
```



## <a name="next-steps"></a><span data-ttu-id="3ee7a-276">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ee7a-276">Next steps</span></span>
<span data-ttu-id="3ee7a-277">Continue with the advanced tutorials:</span><span class="sxs-lookup"><span data-stu-id="3ee7a-277">Continue with the advanced tutorials:</span></span>
* [<span data-ttu-id="3ee7a-278">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="3ee7a-278">Aggregation functions</span></span>](aggregations.md)
* [<span data-ttu-id="3ee7a-279">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="3ee7a-279">Advanced aggregations</span></span>](advanced-aggregations.md)
* [<span data-ttu-id="3ee7a-280">Charts and diagrams</span><span class="sxs-lookup"><span data-stu-id="3ee7a-280">Charts and diagrams</span></span>](charts.md)
* [<span data-ttu-id="3ee7a-281">Working with JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="3ee7a-281">Working with JSON and data structures</span></span>](json-data-structures.md)
* [<span data-ttu-id="3ee7a-282">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="3ee7a-282">Advanced query writing</span></span>](advanced-query-writing.md)
* [<span data-ttu-id="3ee7a-283">Joins - cross analysis</span><span class="sxs-lookup"><span data-stu-id="3ee7a-283">Joins - cross analysis</span></span>](joins.md)