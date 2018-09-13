---
title: 'Azure AD Connect sync: Functions Reference | Microsoft Docs'
description: Reference of declarative provisioning expressions in Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: de8190879f37a241a0f030ad61127d8b8dcb1da2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550679"
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="aa1e1-103">Azure AD Connect sync: Functions Reference</span><span class="sxs-lookup"><span data-stu-id="aa1e1-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="aa1e1-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="aa1e1-105">The Syntax of the functions is expressed using the following format:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="aa1e1-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="aa1e1-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="aa1e1-108">If the type does not match, an error is thrown.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="aa1e1-109">The types are expressed with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="aa1e1-110">**bin** – Binary</span><span class="sxs-lookup"><span data-stu-id="aa1e1-110">**bin** – Binary</span></span>
* <span data-ttu-id="aa1e1-111">**bool** – Boolean</span><span class="sxs-lookup"><span data-stu-id="aa1e1-111">**bool** – Boolean</span></span>
* <span data-ttu-id="aa1e1-112">**dt** – UTC Date/Time</span><span class="sxs-lookup"><span data-stu-id="aa1e1-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="aa1e1-113">**enum** – Enumeration of known constants</span><span class="sxs-lookup"><span data-stu-id="aa1e1-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="aa1e1-114">**exp** – Expression, which is expected to evaluate to a Boolean</span><span class="sxs-lookup"><span data-stu-id="aa1e1-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="aa1e1-115">**mvbin** – Multi-Valued Binary</span><span class="sxs-lookup"><span data-stu-id="aa1e1-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="aa1e1-116">**mvstr** – Multi-Valued String</span><span class="sxs-lookup"><span data-stu-id="aa1e1-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="aa1e1-117">**mvref** – Multi-Valued Reference</span><span class="sxs-lookup"><span data-stu-id="aa1e1-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="aa1e1-118">**num** – Numeric</span><span class="sxs-lookup"><span data-stu-id="aa1e1-118">**num** – Numeric</span></span>
* <span data-ttu-id="aa1e1-119">**ref** – Reference</span><span class="sxs-lookup"><span data-stu-id="aa1e1-119">**ref** – Reference</span></span>
* <span data-ttu-id="aa1e1-120">**str** – String</span><span class="sxs-lookup"><span data-stu-id="aa1e1-120">**str** – String</span></span>
* <span data-ttu-id="aa1e1-121">**var** – A variant of (almost) any other type</span><span class="sxs-lookup"><span data-stu-id="aa1e1-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="aa1e1-122">**void** – doesn’t return a value</span><span class="sxs-lookup"><span data-stu-id="aa1e1-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="aa1e1-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="aa1e1-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="aa1e1-125">Functions Reference</span><span class="sxs-lookup"><span data-stu-id="aa1e1-125">Functions Reference</span></span>
| <span data-ttu-id="aa1e1-126">List of functions</span><span class="sxs-lookup"><span data-stu-id="aa1e1-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="aa1e1-127">**Conversion**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-127">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-128">CBool</span><span class="sxs-lookup"><span data-stu-id="aa1e1-128">CBool</span></span>](#cbool) |[<span data-ttu-id="aa1e1-129">CDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-129">CDate</span></span>](#cdate) |[<span data-ttu-id="aa1e1-130">CGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-130">CGuid</span></span>](#cguid) |[<span data-ttu-id="aa1e1-131">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="aa1e1-131">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="aa1e1-132">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="aa1e1-132">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="aa1e1-133">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="aa1e1-133">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="aa1e1-134">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="aa1e1-134">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="aa1e1-135">CNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-135">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="aa1e1-136">CRef</span><span class="sxs-lookup"><span data-stu-id="aa1e1-136">CRef</span></span>](#cref) |[<span data-ttu-id="aa1e1-137">CStr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-137">CStr</span></span>](#cstr) |[<span data-ttu-id="aa1e1-138">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-138">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="aa1e1-139">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-139">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="aa1e1-140">**Date / Time**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-140">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-141">DateAdd</span><span class="sxs-lookup"><span data-stu-id="aa1e1-141">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="aa1e1-142">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-142">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="aa1e1-143">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="aa1e1-143">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="aa1e1-144">Now</span><span class="sxs-lookup"><span data-stu-id="aa1e1-144">Now</span></span>](#now) | |
| [<span data-ttu-id="aa1e1-145">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-145">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="aa1e1-146">**Directory**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-146">**Directory**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-147">DNComponent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-147">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="aa1e1-148">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="aa1e1-148">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="aa1e1-149">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-149">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="aa1e1-150">**Evaluation**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-150">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-151">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="aa1e1-151">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="aa1e1-152">IsDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-152">IsDate</span></span>](#isdate) |[<span data-ttu-id="aa1e1-153">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="aa1e1-153">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="aa1e1-154">IsGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-154">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="aa1e1-155">IsNull</span><span class="sxs-lookup"><span data-stu-id="aa1e1-155">IsNull</span></span>](#isnull) |[<span data-ttu-id="aa1e1-156">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="aa1e1-156">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="aa1e1-157">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="aa1e1-157">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="aa1e1-158">IsPresent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-158">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="aa1e1-159">IsString</span><span class="sxs-lookup"><span data-stu-id="aa1e1-159">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="aa1e1-160">**Math**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-160">**Math**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-161">BitAnd</span><span class="sxs-lookup"><span data-stu-id="aa1e1-161">BitAnd</span></span>](#bitand) |[<span data-ttu-id="aa1e1-162">BitOr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-162">BitOr</span></span>](#bitor) |[<span data-ttu-id="aa1e1-163">RandomNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-163">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="aa1e1-164">**Multi-valued**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-164">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-165">Contains</span><span class="sxs-lookup"><span data-stu-id="aa1e1-165">Contains</span></span>](#contains) |[<span data-ttu-id="aa1e1-166">Count</span><span class="sxs-lookup"><span data-stu-id="aa1e1-166">Count</span></span>](#count) |[<span data-ttu-id="aa1e1-167">Item</span><span class="sxs-lookup"><span data-stu-id="aa1e1-167">Item</span></span>](#item) |[<span data-ttu-id="aa1e1-168">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="aa1e1-168">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="aa1e1-169">Join</span><span class="sxs-lookup"><span data-stu-id="aa1e1-169">Join</span></span>](#join) |[<span data-ttu-id="aa1e1-170">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="aa1e1-170">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="aa1e1-171">Split</span><span class="sxs-lookup"><span data-stu-id="aa1e1-171">Split</span></span>](#split) | | |
| <span data-ttu-id="aa1e1-172">**Program Flow**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-172">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-173">Error</span><span class="sxs-lookup"><span data-stu-id="aa1e1-173">Error</span></span>](#error) |[<span data-ttu-id="aa1e1-174">IIF</span><span class="sxs-lookup"><span data-stu-id="aa1e1-174">IIF</span></span>](#iif) |[<span data-ttu-id="aa1e1-175">Switch</span><span class="sxs-lookup"><span data-stu-id="aa1e1-175">Switch</span></span>](#switch) | | |
| <span data-ttu-id="aa1e1-176">**Text**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-176">**Text**</span></span> | | | | |
| [<span data-ttu-id="aa1e1-177">GUID</span><span class="sxs-lookup"><span data-stu-id="aa1e1-177">GUID</span></span>](#guid) |[<span data-ttu-id="aa1e1-178">InStr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-178">InStr</span></span>](#instr) |[<span data-ttu-id="aa1e1-179">InStrRev</span><span class="sxs-lookup"><span data-stu-id="aa1e1-179">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="aa1e1-180">LCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-180">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="aa1e1-181">Left</span><span class="sxs-lookup"><span data-stu-id="aa1e1-181">Left</span></span>](#left) |[<span data-ttu-id="aa1e1-182">Len</span><span class="sxs-lookup"><span data-stu-id="aa1e1-182">Len</span></span>](#len) |[<span data-ttu-id="aa1e1-183">LTrim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-183">LTrim</span></span>](#ltrim) |[<span data-ttu-id="aa1e1-184">Mid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-184">Mid</span></span>](#mid) | |
| [<span data-ttu-id="aa1e1-185">PadLeft</span><span class="sxs-lookup"><span data-stu-id="aa1e1-185">PadLeft</span></span>](#padleft) |[<span data-ttu-id="aa1e1-186">PadRight</span><span class="sxs-lookup"><span data-stu-id="aa1e1-186">PadRight</span></span>](#padright) |[<span data-ttu-id="aa1e1-187">PCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-187">PCase</span></span>](#pcase) |[<span data-ttu-id="aa1e1-188">Replace</span><span class="sxs-lookup"><span data-stu-id="aa1e1-188">Replace</span></span>](#replace) | |
| [<span data-ttu-id="aa1e1-189">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="aa1e1-189">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="aa1e1-190">Right</span><span class="sxs-lookup"><span data-stu-id="aa1e1-190">Right</span></span>](#right) |[<span data-ttu-id="aa1e1-191">RTrim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-191">RTrim</span></span>](#rtrim) |[<span data-ttu-id="aa1e1-192">Trim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-192">Trim</span></span>](#trim) | |
| [<span data-ttu-id="aa1e1-193">UCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-193">UCase</span></span>](#ucase) |[<span data-ttu-id="aa1e1-194">Word</span><span class="sxs-lookup"><span data-stu-id="aa1e1-194">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="aa1e1-195">BitAnd</span><span class="sxs-lookup"><span data-stu-id="aa1e1-195">BitAnd</span></span>
<span data-ttu-id="aa1e1-196">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-196">**Description:**</span></span>  
<span data-ttu-id="aa1e1-197">The BitAnd function sets specified bits on a value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-197">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="aa1e1-198">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-198">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="aa1e1-199">value1, value2: numeric values that should be AND’ed together</span><span class="sxs-lookup"><span data-stu-id="aa1e1-199">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="aa1e1-200">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-200">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-201">This function converts both parameters to the binary representation and sets a bit to:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-201">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="aa1e1-202">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span><span class="sxs-lookup"><span data-stu-id="aa1e1-202">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="aa1e1-203">1 - if both of the corresponding bits are 1.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-203">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="aa1e1-204">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-204">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="aa1e1-205">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-205">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="aa1e1-206">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-206">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="aa1e1-207">BitOr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-207">BitOr</span></span>
<span data-ttu-id="aa1e1-208">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-208">**Description:**</span></span>  
<span data-ttu-id="aa1e1-209">The BitOr function sets specified bits on a value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-209">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="aa1e1-210">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-210">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="aa1e1-211">value1, value2: numeric values that should be OR’ed together</span><span class="sxs-lookup"><span data-stu-id="aa1e1-211">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="aa1e1-212">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-212">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-213">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-213">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="aa1e1-214">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-214">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="aa1e1-215">CBool</span><span class="sxs-lookup"><span data-stu-id="aa1e1-215">CBool</span></span>
<span data-ttu-id="aa1e1-216">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-216">**Description:**</span></span>  
<span data-ttu-id="aa1e1-217">The CBool function returns a Boolean based on the evaluated expression</span><span class="sxs-lookup"><span data-stu-id="aa1e1-217">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="aa1e1-218">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-218">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="aa1e1-219">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-219">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-220">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-220">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="aa1e1-221">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-221">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="aa1e1-222">Returns True if both attributes have the same value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-222">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="aa1e1-223">CDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-223">CDate</span></span>
<span data-ttu-id="aa1e1-224">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-224">**Description:**</span></span>  
<span data-ttu-id="aa1e1-225">The CDate function returns a UTC DateTime from a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-225">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="aa1e1-226">DateTime is not a native attribute type in Sync but is used by some functions.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-226">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="aa1e1-227">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-227">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="aa1e1-228">Value: A string with a date, time, and optionally time zone</span><span class="sxs-lookup"><span data-stu-id="aa1e1-228">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="aa1e1-229">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-229">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-230">The returned string is always in UTC.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-230">The returned string is always in UTC.</span></span>

<span data-ttu-id="aa1e1-231">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-231">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="aa1e1-232">Returns a DateTime based on the employee’s start time</span><span class="sxs-lookup"><span data-stu-id="aa1e1-232">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="aa1e1-233">Returns a DateTime representing "2013-01-11 12:00 AM"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-233">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="aa1e1-234">CGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-234">CGuid</span></span>
<span data-ttu-id="aa1e1-235">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-235">**Description:**</span></span>  
<span data-ttu-id="aa1e1-236">The CGuid function converts the string representation of a GUID to its binary representation.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-236">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="aa1e1-237">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-237">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="aa1e1-238">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="aa1e1-238">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="aa1e1-239">Contains</span><span class="sxs-lookup"><span data-stu-id="aa1e1-239">Contains</span></span>
<span data-ttu-id="aa1e1-240">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-240">**Description:**</span></span>  
<span data-ttu-id="aa1e1-241">The Contains function finds a string inside a multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-241">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="aa1e1-242">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-242">**Syntax:**</span></span>  
<span data-ttu-id="aa1e1-243">`num Contains (mvstring attribute, str search)` - case-sensitive</span><span class="sxs-lookup"><span data-stu-id="aa1e1-243">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="aa1e1-244">`num Contains (mvref attribute, str search)` - case-sensitive</span><span class="sxs-lookup"><span data-stu-id="aa1e1-244">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="aa1e1-245">attribute: the multi-valued attribute to search.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-245">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="aa1e1-246">search: string to find in the attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-246">search: string to find in the attribute.</span></span>
* <span data-ttu-id="aa1e1-247">Casetype: CaseInsensitive or CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-247">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="aa1e1-248">Returns index in the multi-valued attribute where the string was found.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-248">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="aa1e1-249">0 is returned if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-249">0 is returned if the string is not found.</span></span>

<span data-ttu-id="aa1e1-250">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-250">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-251">For multi-valued string attributes, the search finds substrings in the values.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-251">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="aa1e1-252">For reference attributes, the searched string must exactly match the value to be considered a match.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-252">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="aa1e1-253">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-253">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="aa1e1-254">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-254">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="aa1e1-255">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="aa1e1-255">ConvertFromBase64</span></span>
<span data-ttu-id="aa1e1-256">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-256">**Description:**</span></span>  
<span data-ttu-id="aa1e1-257">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-257">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="aa1e1-258">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-258">**Syntax:**</span></span>  
<span data-ttu-id="aa1e1-259">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span><span class="sxs-lookup"><span data-stu-id="aa1e1-259">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="aa1e1-260">source: Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-260">source: Base64 encoded string</span></span>  
* <span data-ttu-id="aa1e1-261">Encoding: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="aa1e1-261">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="aa1e1-262">**Example**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-262">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="aa1e1-263">Both examples return "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-263">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="aa1e1-264">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="aa1e1-264">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="aa1e1-265">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-265">**Description:**</span></span>  
<span data-ttu-id="aa1e1-266">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-266">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="aa1e1-267">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-267">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="aa1e1-268">source: UTF8 2-byte encoded sting</span><span class="sxs-lookup"><span data-stu-id="aa1e1-268">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="aa1e1-269">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-269">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-270">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-270">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="aa1e1-271">This format is used by Azure Active Directory as DN.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-271">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="aa1e1-272">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-272">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="aa1e1-273">Returns "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-273">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="aa1e1-274">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="aa1e1-274">ConvertToBase64</span></span>
<span data-ttu-id="aa1e1-275">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-275">**Description:**</span></span>  
<span data-ttu-id="aa1e1-276">The ConvertToBase64 function converts a string to a Unicode base64 string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-276">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="aa1e1-277">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-277">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="aa1e1-278">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-278">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="aa1e1-279">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-279">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="aa1e1-280">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-280">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="aa1e1-281">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="aa1e1-281">ConvertToUTF8Hex</span></span>
<span data-ttu-id="aa1e1-282">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-282">**Description:**</span></span>  
<span data-ttu-id="aa1e1-283">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-283">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="aa1e1-284">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-284">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="aa1e1-285">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-285">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-286">The output format of this function is used by Azure Active Directory as DN attribute format.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-286">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="aa1e1-287">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-287">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="aa1e1-288">Returns 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="aa1e1-288">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="aa1e1-289">Count</span><span class="sxs-lookup"><span data-stu-id="aa1e1-289">Count</span></span>
<span data-ttu-id="aa1e1-290">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-290">**Description:**</span></span>  
<span data-ttu-id="aa1e1-291">The Count function returns the number of elements in a multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-291">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="aa1e1-292">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-292">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="aa1e1-293">CNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-293">CNum</span></span>
<span data-ttu-id="aa1e1-294">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-294">**Description:**</span></span>  
<span data-ttu-id="aa1e1-295">The CNum function takes a string and returns a numeric data type.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-295">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="aa1e1-296">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-296">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="aa1e1-297">CRef</span><span class="sxs-lookup"><span data-stu-id="aa1e1-297">CRef</span></span>
<span data-ttu-id="aa1e1-298">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-298">**Description:**</span></span>  
<span data-ttu-id="aa1e1-299">Converts a string to a reference attribute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-299">Converts a string to a reference attribute</span></span>

<span data-ttu-id="aa1e1-300">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-300">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="aa1e1-301">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-301">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="aa1e1-302">CStr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-302">CStr</span></span>
<span data-ttu-id="aa1e1-303">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-303">**Description:**</span></span>  
<span data-ttu-id="aa1e1-304">The CStr function converts to a string data type.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-304">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="aa1e1-305">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-305">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="aa1e1-306">value: Can be a numeric value, reference attribute, or Boolean.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-306">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="aa1e1-307">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-307">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="aa1e1-308">Could return "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-308">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="aa1e1-309">DateAdd</span><span class="sxs-lookup"><span data-stu-id="aa1e1-309">DateAdd</span></span>
<span data-ttu-id="aa1e1-310">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-310">**Description:**</span></span>  
<span data-ttu-id="aa1e1-311">Returns a Date containing a date to which a specified time interval has been added.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-311">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="aa1e1-312">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-312">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="aa1e1-313">interval: String expression that is the interval of time you want to add.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-313">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="aa1e1-314">The string must have one of the following values:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-314">The string must have one of the following values:</span></span>
  * <span data-ttu-id="aa1e1-315">yyyy Year</span><span class="sxs-lookup"><span data-stu-id="aa1e1-315">yyyy Year</span></span>
  * <span data-ttu-id="aa1e1-316">q Quarter</span><span class="sxs-lookup"><span data-stu-id="aa1e1-316">q Quarter</span></span>
  * <span data-ttu-id="aa1e1-317">m Month</span><span class="sxs-lookup"><span data-stu-id="aa1e1-317">m Month</span></span>
  * <span data-ttu-id="aa1e1-318">y Day of year</span><span class="sxs-lookup"><span data-stu-id="aa1e1-318">y Day of year</span></span>
  * <span data-ttu-id="aa1e1-319">d Day</span><span class="sxs-lookup"><span data-stu-id="aa1e1-319">d Day</span></span>
  * <span data-ttu-id="aa1e1-320">w Weekday</span><span class="sxs-lookup"><span data-stu-id="aa1e1-320">w Weekday</span></span>
  * <span data-ttu-id="aa1e1-321">ww Week</span><span class="sxs-lookup"><span data-stu-id="aa1e1-321">ww Week</span></span>
  * <span data-ttu-id="aa1e1-322">h Hour</span><span class="sxs-lookup"><span data-stu-id="aa1e1-322">h Hour</span></span>
  * <span data-ttu-id="aa1e1-323">n Minute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-323">n Minute</span></span>
  * <span data-ttu-id="aa1e1-324">s Second</span><span class="sxs-lookup"><span data-stu-id="aa1e1-324">s Second</span></span>
* <span data-ttu-id="aa1e1-325">value: The number of units you want to add.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-325">value: The number of units you want to add.</span></span> <span data-ttu-id="aa1e1-326">It can be positive (to get dates in the future) or negative (to get dates in the past).</span><span class="sxs-lookup"><span data-stu-id="aa1e1-326">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="aa1e1-327">date: DateTime representing date to which the interval is added.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-327">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="aa1e1-328">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-328">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="aa1e1-329">Adds 3 months and returns a DateTime representing "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-329">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="aa1e1-330">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-330">DateFromNum</span></span>
<span data-ttu-id="aa1e1-331">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-331">**Description:**</span></span>  
<span data-ttu-id="aa1e1-332">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-332">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="aa1e1-333">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-333">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="aa1e1-334">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-334">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="aa1e1-335">Returns a DateTime representing 2012-01-01 23:00:00</span><span class="sxs-lookup"><span data-stu-id="aa1e1-335">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="aa1e1-336">DNComponent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-336">DNComponent</span></span>
<span data-ttu-id="aa1e1-337">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-337">**Description:**</span></span>  
<span data-ttu-id="aa1e1-338">The DNComponent function returns the value of a specified DN component going from left.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-338">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="aa1e1-339">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-339">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="aa1e1-340">dn: the reference attribute to interpret</span><span class="sxs-lookup"><span data-stu-id="aa1e1-340">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="aa1e1-341">ComponentNumber: The component in the DN to return</span><span class="sxs-lookup"><span data-stu-id="aa1e1-341">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="aa1e1-342">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-342">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="aa1e1-343">If dn is "cn=Joe,ou=…," it returns Joe</span><span class="sxs-lookup"><span data-stu-id="aa1e1-343">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="aa1e1-344">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="aa1e1-344">DNComponentRev</span></span>
<span data-ttu-id="aa1e1-345">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-345">**Description:**</span></span>  
<span data-ttu-id="aa1e1-346">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span><span class="sxs-lookup"><span data-stu-id="aa1e1-346">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="aa1e1-347">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-347">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="aa1e1-348">dn: the reference attribute to interpret</span><span class="sxs-lookup"><span data-stu-id="aa1e1-348">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="aa1e1-349">ComponentNumber - The component in the DN to return</span><span class="sxs-lookup"><span data-stu-id="aa1e1-349">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="aa1e1-350">Options: DC – Ignore all components with "dc="</span><span class="sxs-lookup"><span data-stu-id="aa1e1-350">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="aa1e1-351">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-351">**Example:**</span></span>  
<span data-ttu-id="aa1e1-352">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span><span class="sxs-lookup"><span data-stu-id="aa1e1-352">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="aa1e1-353">Both return US.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-353">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="aa1e1-354">Error</span><span class="sxs-lookup"><span data-stu-id="aa1e1-354">Error</span></span>
<span data-ttu-id="aa1e1-355">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-355">**Description:**</span></span>  
<span data-ttu-id="aa1e1-356">The Error function is used to return a custom error.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-356">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="aa1e1-357">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-357">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="aa1e1-358">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-358">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="aa1e1-359">If the attribute accountName is not present, throw an error on the object.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-359">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="aa1e1-360">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-360">EscapeDNComponent</span></span>
<span data-ttu-id="aa1e1-361">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-361">**Description:**</span></span>  
<span data-ttu-id="aa1e1-362">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-362">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="aa1e1-363">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-363">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="aa1e1-364">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-364">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="aa1e1-365">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-365">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="aa1e1-366">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="aa1e1-366">FormatDateTime</span></span>
<span data-ttu-id="aa1e1-367">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-367">**Description:**</span></span>  
<span data-ttu-id="aa1e1-368">The FormatDateTime function is used to format a DateTime to a string with a specified format</span><span class="sxs-lookup"><span data-stu-id="aa1e1-368">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="aa1e1-369">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-369">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="aa1e1-370">value: a value in the DateTime format</span><span class="sxs-lookup"><span data-stu-id="aa1e1-370">value: a value in the DateTime format</span></span>
* <span data-ttu-id="aa1e1-371">format: a string representing the format to convert to.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-371">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="aa1e1-372">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-372">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-373">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="aa1e1-373">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="aa1e1-374">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-374">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="aa1e1-375">Results in "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-375">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="aa1e1-376">Can result in "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-376">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="aa1e1-377">GUID</span><span class="sxs-lookup"><span data-stu-id="aa1e1-377">GUID</span></span>
<span data-ttu-id="aa1e1-378">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-378">**Description:**</span></span>  
<span data-ttu-id="aa1e1-379">The function GUID generates a new random GUID</span><span class="sxs-lookup"><span data-stu-id="aa1e1-379">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="aa1e1-380">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-380">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="aa1e1-381">IIF</span><span class="sxs-lookup"><span data-stu-id="aa1e1-381">IIF</span></span>
<span data-ttu-id="aa1e1-382">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-382">**Description:**</span></span>  
<span data-ttu-id="aa1e1-383">The IIF function returns one of a set of possible values based on a specified condition.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-383">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="aa1e1-384">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-384">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="aa1e1-385">condition: any value or expression that can be evaluated to true or false.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-385">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="aa1e1-386">valueIfTrue: If the condition evaluates to true, the returned value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-386">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="aa1e1-387">valueIfFalse: If the condition evaluates to false, the returned value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-387">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="aa1e1-388">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-388">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="aa1e1-389">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-389">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="aa1e1-390">InStr</span><span class="sxs-lookup"><span data-stu-id="aa1e1-390">InStr</span></span>
<span data-ttu-id="aa1e1-391">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-391">**Description:**</span></span>  
<span data-ttu-id="aa1e1-392">The InStr function finds the first occurrence of a substring in a string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-392">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="aa1e1-393">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-393">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="aa1e1-394">stringcheck: string to be searched</span><span class="sxs-lookup"><span data-stu-id="aa1e1-394">stringcheck: string to be searched</span></span>
* <span data-ttu-id="aa1e1-395">stringmatch: string to be found</span><span class="sxs-lookup"><span data-stu-id="aa1e1-395">stringmatch: string to be found</span></span>
* <span data-ttu-id="aa1e1-396">start: starting position to find the substring</span><span class="sxs-lookup"><span data-stu-id="aa1e1-396">start: starting position to find the substring</span></span>
* <span data-ttu-id="aa1e1-397">compare: vbTextCompare or vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="aa1e1-397">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="aa1e1-398">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-398">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-399">Returns the position where the substring was found or 0 if not found.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-399">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="aa1e1-400">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-400">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="aa1e1-401">Evalues to 5</span><span class="sxs-lookup"><span data-stu-id="aa1e1-401">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="aa1e1-402">Evaluates to 7</span><span class="sxs-lookup"><span data-stu-id="aa1e1-402">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="aa1e1-403">InStrRev</span><span class="sxs-lookup"><span data-stu-id="aa1e1-403">InStrRev</span></span>
<span data-ttu-id="aa1e1-404">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-404">**Description:**</span></span>  
<span data-ttu-id="aa1e1-405">The InStrRev function finds the last occurrence of a substring in a string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-405">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="aa1e1-406">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-406">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="aa1e1-407">stringcheck: string to be searched</span><span class="sxs-lookup"><span data-stu-id="aa1e1-407">stringcheck: string to be searched</span></span>
* <span data-ttu-id="aa1e1-408">stringmatch: string to be found</span><span class="sxs-lookup"><span data-stu-id="aa1e1-408">stringmatch: string to be found</span></span>
* <span data-ttu-id="aa1e1-409">start: starting position to find the substring</span><span class="sxs-lookup"><span data-stu-id="aa1e1-409">start: starting position to find the substring</span></span>
* <span data-ttu-id="aa1e1-410">compare: vbTextCompare or vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="aa1e1-410">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="aa1e1-411">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-411">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-412">Returns the position where the substring was found or 0 if not found.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-412">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="aa1e1-413">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-413">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="aa1e1-414">Returns 7</span><span class="sxs-lookup"><span data-stu-id="aa1e1-414">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="aa1e1-415">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="aa1e1-415">IsBitSet</span></span>
<span data-ttu-id="aa1e1-416">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-416">**Description:**</span></span>  
<span data-ttu-id="aa1e1-417">The function IsBitSet Tests if a bit is set or not</span><span class="sxs-lookup"><span data-stu-id="aa1e1-417">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="aa1e1-418">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-418">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="aa1e1-419">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span><span class="sxs-lookup"><span data-stu-id="aa1e1-419">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="aa1e1-420">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-420">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="aa1e1-421">Returns True because bit "4" is set in the hexadecimal value "F"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-421">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="aa1e1-422">IsDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-422">IsDate</span></span>
<span data-ttu-id="aa1e1-423">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-423">**Description:**</span></span>  
<span data-ttu-id="aa1e1-424">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-424">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="aa1e1-425">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-425">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="aa1e1-426">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-426">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-427">Used to determine if CDate() can be successful.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-427">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="isempty"></a><span data-ttu-id="aa1e1-428">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="aa1e1-428">IsEmpty</span></span>
<span data-ttu-id="aa1e1-429">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-429">**Description:**</span></span>  
<span data-ttu-id="aa1e1-430">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-430">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="aa1e1-431">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-431">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="aa1e1-432">IsGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-432">IsGuid</span></span>
<span data-ttu-id="aa1e1-433">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-433">**Description:**</span></span>  
<span data-ttu-id="aa1e1-434">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-434">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="aa1e1-435">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-435">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="aa1e1-436">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-436">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-437">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="aa1e1-437">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="aa1e1-438">Used to determine if CGuid() can be successful.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-438">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="aa1e1-439">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-439">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="aa1e1-440">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-440">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="aa1e1-441">IsNull</span><span class="sxs-lookup"><span data-stu-id="aa1e1-441">IsNull</span></span>
<span data-ttu-id="aa1e1-442">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-442">**Description:**</span></span>  
<span data-ttu-id="aa1e1-443">If the expression evaluates to Null, then the IsNull function returns true.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-443">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="aa1e1-444">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-444">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="aa1e1-445">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-445">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-446">For an attribute, a Null is expressed by the absence of the attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-446">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="aa1e1-447">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-447">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="aa1e1-448">Returns True if the attribute is not present in the CS or MV.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-448">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="aa1e1-449">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="aa1e1-449">IsNullOrEmpty</span></span>
<span data-ttu-id="aa1e1-450">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-450">**Description:**</span></span>  
<span data-ttu-id="aa1e1-451">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-451">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="aa1e1-452">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-452">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="aa1e1-453">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-453">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-454">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-454">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="aa1e1-455">The inverse of this function is named IsPresent.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-455">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="aa1e1-456">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-456">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="aa1e1-457">Returns True if the attribute is not present or is an empty string in the CS or MV.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-457">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="aa1e1-458">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="aa1e1-458">IsNumeric</span></span>
<span data-ttu-id="aa1e1-459">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-459">**Description:**</span></span>  
<span data-ttu-id="aa1e1-460">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-460">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="aa1e1-461">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-461">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="aa1e1-462">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-462">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-463">Used to determine if CNum() can be successful to parse the expression.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-463">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="aa1e1-464">IsString</span><span class="sxs-lookup"><span data-stu-id="aa1e1-464">IsString</span></span>
<span data-ttu-id="aa1e1-465">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-465">**Description:**</span></span>  
<span data-ttu-id="aa1e1-466">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-466">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="aa1e1-467">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-467">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="aa1e1-468">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-468">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-469">Used to determine if CStr() can be successful to parse the expression.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-469">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="aa1e1-470">IsPresent</span><span class="sxs-lookup"><span data-stu-id="aa1e1-470">IsPresent</span></span>
<span data-ttu-id="aa1e1-471">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-471">**Description:**</span></span>  
<span data-ttu-id="aa1e1-472">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-472">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="aa1e1-473">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-473">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="aa1e1-474">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-474">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-475">The inverse of this function is named IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-475">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="aa1e1-476">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-476">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="aa1e1-477">Item</span><span class="sxs-lookup"><span data-stu-id="aa1e1-477">Item</span></span>
<span data-ttu-id="aa1e1-478">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-478">**Description:**</span></span>  
<span data-ttu-id="aa1e1-479">The Item function returns one item from a multi-valued string/attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-479">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="aa1e1-480">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-480">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="aa1e1-481">attribute: multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-481">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="aa1e1-482">index: index to an item in the multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-482">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="aa1e1-483">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-483">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-484">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-484">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="aa1e1-485">Throws an error if index is out of bounds.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-485">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="aa1e1-486">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-486">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="aa1e1-487">Returns the primary email address.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-487">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="aa1e1-488">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="aa1e1-488">ItemOrNull</span></span>
<span data-ttu-id="aa1e1-489">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-489">**Description:**</span></span>  
<span data-ttu-id="aa1e1-490">The ItemOrNull function returns one item from a multi-valued string/attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-490">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="aa1e1-491">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-491">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="aa1e1-492">attribute: multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="aa1e1-492">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="aa1e1-493">index: index to an item in the multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-493">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="aa1e1-494">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-494">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-495">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-495">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="aa1e1-496">If index is out of bounds, then returns a Null value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-496">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="aa1e1-497">Join</span><span class="sxs-lookup"><span data-stu-id="aa1e1-497">Join</span></span>
<span data-ttu-id="aa1e1-498">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-498">**Description:**</span></span>  
<span data-ttu-id="aa1e1-499">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-499">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="aa1e1-500">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-500">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="aa1e1-501">attribute: Multi-valued attribute containing strings to be joined.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-501">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="aa1e1-502">delimiter: Any string, used to separate the substrings in the returned string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-502">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="aa1e1-503">If omitted, the space character (" ") is used.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-503">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="aa1e1-504">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-504">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="aa1e1-505">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-505">**Remarks**</span></span>  
<span data-ttu-id="aa1e1-506">There is parity between the Join and Split functions.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-506">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="aa1e1-507">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-507">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="aa1e1-508">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-508">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="aa1e1-509">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-509">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="aa1e1-510">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-510">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="aa1e1-511">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-511">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="aa1e1-512">LCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-512">LCase</span></span>
<span data-ttu-id="aa1e1-513">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-513">**Description:**</span></span>  
<span data-ttu-id="aa1e1-514">The LCase function converts all characters in a string to lower case.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-514">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="aa1e1-515">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-515">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="aa1e1-516">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-516">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="aa1e1-517">Returns "test".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-517">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="aa1e1-518">Left</span><span class="sxs-lookup"><span data-stu-id="aa1e1-518">Left</span></span>
<span data-ttu-id="aa1e1-519">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-519">**Description:**</span></span>  
<span data-ttu-id="aa1e1-520">The Left function returns a specified number of characters from the left of a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-520">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="aa1e1-521">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-521">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="aa1e1-522">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="aa1e1-522">string: the string to return characters from</span></span>
* <span data-ttu-id="aa1e1-523">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-523">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="aa1e1-524">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-524">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-525">A string containing the first numChars characters in string:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-525">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="aa1e1-526">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-526">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="aa1e1-527">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-527">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="aa1e1-528">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-528">If string is null, return empty string.</span></span>

<span data-ttu-id="aa1e1-529">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-529">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="aa1e1-530">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-530">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="aa1e1-531">Returns "Joh".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-531">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="aa1e1-532">Len</span><span class="sxs-lookup"><span data-stu-id="aa1e1-532">Len</span></span>
<span data-ttu-id="aa1e1-533">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-533">**Description:**</span></span>  
<span data-ttu-id="aa1e1-534">The Len function returns number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-534">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="aa1e1-535">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-535">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="aa1e1-536">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-536">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="aa1e1-537">Returns 8</span><span class="sxs-lookup"><span data-stu-id="aa1e1-537">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="aa1e1-538">LTrim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-538">LTrim</span></span>
<span data-ttu-id="aa1e1-539">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-539">**Description:**</span></span>  
<span data-ttu-id="aa1e1-540">The LTrim function removes leading white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-540">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="aa1e1-541">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-541">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="aa1e1-542">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-542">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="aa1e1-543">Returns "Test "</span><span class="sxs-lookup"><span data-stu-id="aa1e1-543">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="aa1e1-544">Mid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-544">Mid</span></span>
<span data-ttu-id="aa1e1-545">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-545">**Description:**</span></span>  
<span data-ttu-id="aa1e1-546">The Mid function returns a specified number of characters from a specified position in a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-546">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="aa1e1-547">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-547">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="aa1e1-548">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="aa1e1-548">string: the string to return characters from</span></span>
* <span data-ttu-id="aa1e1-549">start: a number identifying the starting position in string to return characters from</span><span class="sxs-lookup"><span data-stu-id="aa1e1-549">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="aa1e1-550">NumChars: a number identifying the number of characters to return from position in string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-550">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="aa1e1-551">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-551">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-552">Return numChars characters starting from position start in string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-552">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="aa1e1-553">A string containing numChars characters from position start in string:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-553">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="aa1e1-554">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-554">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="aa1e1-555">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-555">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="aa1e1-556">If start > the length of string, return input string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-556">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="aa1e1-557">If start <= 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-557">If start <= 0, return input string.</span></span>
* <span data-ttu-id="aa1e1-558">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-558">If string is null, return empty string.</span></span>

<span data-ttu-id="aa1e1-559">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-559">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="aa1e1-560">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-560">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="aa1e1-561">Returns "hn Do".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-561">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="aa1e1-562">Returns "Doe"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-562">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="aa1e1-563">Now</span><span class="sxs-lookup"><span data-stu-id="aa1e1-563">Now</span></span>
<span data-ttu-id="aa1e1-564">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-564">**Description:**</span></span>  
<span data-ttu-id="aa1e1-565">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-565">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="aa1e1-566">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-566">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="aa1e1-567">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-567">NumFromDate</span></span>
<span data-ttu-id="aa1e1-568">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-568">**Description:**</span></span>  
<span data-ttu-id="aa1e1-569">The NumFromDate function returns a date in AD’s date format.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-569">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="aa1e1-570">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-570">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="aa1e1-571">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-571">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="aa1e1-572">Returns 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="aa1e1-572">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="aa1e1-573">PadLeft</span><span class="sxs-lookup"><span data-stu-id="aa1e1-573">PadLeft</span></span>
<span data-ttu-id="aa1e1-574">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-574">**Description:**</span></span>  
<span data-ttu-id="aa1e1-575">The PadLeft function left-pads a string to a specified length using a provided padding character.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-575">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="aa1e1-576">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-576">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="aa1e1-577">string: the string to pad.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-577">string: the string to pad.</span></span>
* <span data-ttu-id="aa1e1-578">length: An integer representing the desired length of string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-578">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="aa1e1-579">padCharacter: A string consisting of a single character to use as the pad character</span><span class="sxs-lookup"><span data-stu-id="aa1e1-579">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="aa1e1-580">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-580">**Remarks:**</span></span>

* <span data-ttu-id="aa1e1-581">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-581">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="aa1e1-582">PadCharacter can be a space character, but it cannot be a null value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-582">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="aa1e1-583">If the length of string is equal to or greater than length, string is returned unchanged.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-583">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="aa1e1-584">If string has a length greater than or equal to length, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-584">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="aa1e1-585">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-585">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="aa1e1-586">If string is null, the function returns an empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-586">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="aa1e1-587">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-587">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="aa1e1-588">Returns "000000User".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-588">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="aa1e1-589">PadRight</span><span class="sxs-lookup"><span data-stu-id="aa1e1-589">PadRight</span></span>
<span data-ttu-id="aa1e1-590">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-590">**Description:**</span></span>  
<span data-ttu-id="aa1e1-591">The PadRight function right-pads a string to a specified length using a provided padding character.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-591">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="aa1e1-592">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-592">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="aa1e1-593">string: the string to pad.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-593">string: the string to pad.</span></span>
* <span data-ttu-id="aa1e1-594">length: An integer representing the desired length of string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-594">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="aa1e1-595">padCharacter: A string consisting of a single character to use as the pad character</span><span class="sxs-lookup"><span data-stu-id="aa1e1-595">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="aa1e1-596">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-596">**Remarks:**</span></span>

* <span data-ttu-id="aa1e1-597">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-597">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="aa1e1-598">padCharacter can be a space character, but it cannot be a null value.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-598">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="aa1e1-599">If the length of string is equal to or greater than length, string is returned unchanged.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-599">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="aa1e1-600">If string has a length greater than or equal to length, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-600">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="aa1e1-601">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-601">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="aa1e1-602">If string is null, the function returns an empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-602">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="aa1e1-603">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-603">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="aa1e1-604">Returns "User000000".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-604">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="aa1e1-605">PCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-605">PCase</span></span>
<span data-ttu-id="aa1e1-606">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-606">**Description:**</span></span>  
<span data-ttu-id="aa1e1-607">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-607">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="aa1e1-608">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-608">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="aa1e1-609">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-609">**Remarks:**</span></span>

* <span data-ttu-id="aa1e1-610">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-610">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="aa1e1-611">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-611">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="aa1e1-612">Returns "Test".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-612">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="aa1e1-613">Returns "Test"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-613">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="aa1e1-614">RandomNum</span><span class="sxs-lookup"><span data-stu-id="aa1e1-614">RandomNum</span></span>
<span data-ttu-id="aa1e1-615">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-615">**Description:**</span></span>  
<span data-ttu-id="aa1e1-616">The RandomNum function returns a random number between a specified interval.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-616">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="aa1e1-617">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-617">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="aa1e1-618">start: a number identifying the lower limit of the random value to generate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-618">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="aa1e1-619">end: a number identifying the upper limit of the random value to generate</span><span class="sxs-lookup"><span data-stu-id="aa1e1-619">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="aa1e1-620">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-620">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="aa1e1-621">Can return 734.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-621">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="aa1e1-622">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="aa1e1-622">RemoveDuplicates</span></span>
<span data-ttu-id="aa1e1-623">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-623">**Description:**</span></span>  
<span data-ttu-id="aa1e1-624">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-624">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="aa1e1-625">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-625">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="aa1e1-626">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-626">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="aa1e1-627">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-627">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="aa1e1-628">Replace</span><span class="sxs-lookup"><span data-stu-id="aa1e1-628">Replace</span></span>
<span data-ttu-id="aa1e1-629">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-629">**Description:**</span></span>  
<span data-ttu-id="aa1e1-630">The Replace function replaces all occurrences of a string to another string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-630">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="aa1e1-631">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-631">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="aa1e1-632">string: A string to replace values in.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-632">string: A string to replace values in.</span></span>
* <span data-ttu-id="aa1e1-633">OldValue: The string to search for and to replace.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-633">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="aa1e1-634">NewValue: The string to replace to.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-634">NewValue: The string to replace to.</span></span>

<span data-ttu-id="aa1e1-635">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-635">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-636">The function recognizes the following special monikers:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-636">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="aa1e1-637">\n – New Line</span><span class="sxs-lookup"><span data-stu-id="aa1e1-637">\n – New Line</span></span>
* <span data-ttu-id="aa1e1-638">\r – Carriage Return</span><span class="sxs-lookup"><span data-stu-id="aa1e1-638">\r – Carriage Return</span></span>
* <span data-ttu-id="aa1e1-639">\t – Tab</span><span class="sxs-lookup"><span data-stu-id="aa1e1-639">\t – Tab</span></span>

<span data-ttu-id="aa1e1-640">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-640">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="aa1e1-641">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-641">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="aa1e1-642">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="aa1e1-642">ReplaceChars</span></span>
<span data-ttu-id="aa1e1-643">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-643">**Description:**</span></span>  
<span data-ttu-id="aa1e1-644">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-644">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="aa1e1-645">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-645">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="aa1e1-646">string: A string to replace characters in.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-646">string: A string to replace characters in.</span></span>
* <span data-ttu-id="aa1e1-647">ReplacePattern: a string containing a dictionary with characters to replace.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-647">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="aa1e1-648">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-648">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="aa1e1-649">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-649">**Remarks:**</span></span>

* <span data-ttu-id="aa1e1-650">The function takes each occurrence of defined sources and replaces them with the targets.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-650">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="aa1e1-651">The source must be exactly one (unicode) character.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-651">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="aa1e1-652">The source cannot be empty or longer than one character (parsing error).</span><span class="sxs-lookup"><span data-stu-id="aa1e1-652">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="aa1e1-653">The target can have multiple characters, for example ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-653">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="aa1e1-654">The target can be empty indicating that the character should be removed.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-654">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="aa1e1-655">The source is case-sensitive and must be an exact match.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-655">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="aa1e1-656">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-656">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="aa1e1-657">Spaces and other white characters in the ReplacePattern string are ignored.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-657">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="aa1e1-658">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-658">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="aa1e1-659">Returns Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="aa1e1-659">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="aa1e1-660">Returns "ONeil", the single tick is defined to be removed.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-660">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="aa1e1-661">Right</span><span class="sxs-lookup"><span data-stu-id="aa1e1-661">Right</span></span>
<span data-ttu-id="aa1e1-662">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-662">**Description:**</span></span>  
<span data-ttu-id="aa1e1-663">The Right function returns a specified number of characters from the right (end) of a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-663">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="aa1e1-664">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-664">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="aa1e1-665">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="aa1e1-665">string: the string to return characters from</span></span>
* <span data-ttu-id="aa1e1-666">NumChars: a number identifying the number of characters to return from the end (right) of string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-666">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="aa1e1-667">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-667">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-668">NumChars characters are returned from the last position of string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-668">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="aa1e1-669">A string containing the last numChars characters in string:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-669">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="aa1e1-670">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-670">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="aa1e1-671">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-671">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="aa1e1-672">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-672">If string is null, return empty string.</span></span>

<span data-ttu-id="aa1e1-673">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-673">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="aa1e1-674">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-674">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="aa1e1-675">Returns "Doe".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-675">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="aa1e1-676">RTrim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-676">RTrim</span></span>
<span data-ttu-id="aa1e1-677">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-677">**Description:**</span></span>  
<span data-ttu-id="aa1e1-678">The RTrim function removes trailing white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-678">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="aa1e1-679">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-679">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="aa1e1-680">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-680">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="aa1e1-681">Returns " Test".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-681">Returns " Test".</span></span>

- - -
### <a name="split"></a><span data-ttu-id="aa1e1-682">Split</span><span class="sxs-lookup"><span data-stu-id="aa1e1-682">Split</span></span>
<span data-ttu-id="aa1e1-683">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-683">**Description:**</span></span>  
<span data-ttu-id="aa1e1-684">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-684">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="aa1e1-685">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-685">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="aa1e1-686">value: the string with a delimiter character to separate.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-686">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="aa1e1-687">delimiter: single character to be used as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-687">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="aa1e1-688">limit: maximum number of values that can return.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-688">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="aa1e1-689">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-689">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="aa1e1-690">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-690">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="aa1e1-691">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-691">StringFromGuid</span></span>
<span data-ttu-id="aa1e1-692">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-692">**Description:**</span></span>  
<span data-ttu-id="aa1e1-693">The StringFromGuid function takes a binary GUID and converts it to a string</span><span class="sxs-lookup"><span data-stu-id="aa1e1-693">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="aa1e1-694">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-694">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="aa1e1-695">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="aa1e1-695">StringFromSid</span></span>
<span data-ttu-id="aa1e1-696">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-696">**Description:**</span></span>  
<span data-ttu-id="aa1e1-697">The StringFromSid function converts a byte array containing a security identifier to a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-697">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="aa1e1-698">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-698">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="aa1e1-699">Switch</span><span class="sxs-lookup"><span data-stu-id="aa1e1-699">Switch</span></span>
<span data-ttu-id="aa1e1-700">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-700">**Description:**</span></span>  
<span data-ttu-id="aa1e1-701">The Switch function is used to return a single value based on evaluated conditions.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-701">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="aa1e1-702">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-702">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="aa1e1-703">expr: Variant expression you want to evaluate.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-703">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="aa1e1-704">value: Value to be returned if the corresponding expression is True.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-704">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="aa1e1-705">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-705">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-706">The Switch function argument list consists of pairs of expressions and values.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-706">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="aa1e1-707">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-707">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="aa1e1-708">If the parts aren't properly paired, a run-time error occurs.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-708">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="aa1e1-709">For example, if expr1 is True, Switch returns value1.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-709">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="aa1e1-710">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-710">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="aa1e1-711">Switch returns a Nothing if:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-711">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="aa1e1-712">None of the expressions are True.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-712">None of the expressions are True.</span></span>
* <span data-ttu-id="aa1e1-713">The first True expression has a corresponding value that is Null.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-713">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="aa1e1-714">Switch evaluates all expressions, even though it returns only one of them.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-714">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="aa1e1-715">For this reason, you should watch for undesirable side effects.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-715">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="aa1e1-716">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-716">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="aa1e1-717">Value can also be the Error function, which would return a custom string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-717">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="aa1e1-718">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-718">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="aa1e1-719">Returns the language spoken in some major cities, otherwise returns an Error.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-719">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="aa1e1-720">Trim</span><span class="sxs-lookup"><span data-stu-id="aa1e1-720">Trim</span></span>
<span data-ttu-id="aa1e1-721">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-721">**Description:**</span></span>  
<span data-ttu-id="aa1e1-722">The Trim function removes leading and trailing white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-722">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="aa1e1-723">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-723">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="aa1e1-724">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-724">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="aa1e1-725">Returns "Test".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-725">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="aa1e1-726">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-726">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="aa1e1-727">UCase</span><span class="sxs-lookup"><span data-stu-id="aa1e1-727">UCase</span></span>
<span data-ttu-id="aa1e1-728">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-728">**Description:**</span></span>  
<span data-ttu-id="aa1e1-729">The UCase function converts all characters in a string to upper case.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-729">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="aa1e1-730">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-730">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="aa1e1-731">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-731">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="aa1e1-732">Returns "TEST".</span><span class="sxs-lookup"><span data-stu-id="aa1e1-732">Returns "TEST".</span></span>

- - -
### <a name="word"></a><span data-ttu-id="aa1e1-733">Word</span><span class="sxs-lookup"><span data-stu-id="aa1e1-733">Word</span></span>
<span data-ttu-id="aa1e1-734">**Description:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-734">**Description:**</span></span>  
<span data-ttu-id="aa1e1-735">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-735">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="aa1e1-736">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-736">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="aa1e1-737">string: the string to return a word from.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-737">string: the string to return a word from.</span></span>
* <span data-ttu-id="aa1e1-738">WordNumber: a number identifying which word number should return.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-738">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="aa1e1-739">delimiters: a string representing the delimiter(s) that should be used to identify words</span><span class="sxs-lookup"><span data-stu-id="aa1e1-739">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="aa1e1-740">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-740">**Remarks:**</span></span>  
<span data-ttu-id="aa1e1-741">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span><span class="sxs-lookup"><span data-stu-id="aa1e1-741">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="aa1e1-742">If number < 1, returns empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-742">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="aa1e1-743">If string is null, returns empty string.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-743">If string is null, returns empty string.</span></span>

<span data-ttu-id="aa1e1-744">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span><span class="sxs-lookup"><span data-stu-id="aa1e1-744">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="aa1e1-745">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa1e1-745">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="aa1e1-746">Returns "brown"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-746">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="aa1e1-747">Would return "has"</span><span class="sxs-lookup"><span data-stu-id="aa1e1-747">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa1e1-748">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="aa1e1-748">Additional Resources</span></span>
* [<span data-ttu-id="aa1e1-749">Understanding Declarative Provisioning Expressions</span><span class="sxs-lookup"><span data-stu-id="aa1e1-749">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="aa1e1-750">Azure AD Connect Sync: Customizing Synchronization options</span><span class="sxs-lookup"><span data-stu-id="aa1e1-750">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="aa1e1-751">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa1e1-751">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
