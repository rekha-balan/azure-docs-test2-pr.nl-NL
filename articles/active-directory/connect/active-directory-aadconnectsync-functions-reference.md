---
title: 'Azure AD Connect sync: Functions Reference | Microsoft Docs'
description: Reference of declarative provisioning expressions in Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 4814d53a86b0d90cf16f76e75c7044448cf791eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809483"
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="ec844-103">Azure AD Connect sync: Functions Reference</span><span class="sxs-lookup"><span data-stu-id="ec844-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="ec844-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span><span class="sxs-lookup"><span data-stu-id="ec844-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="ec844-105">The Syntax of the functions is expressed using the following format:</span><span class="sxs-lookup"><span data-stu-id="ec844-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="ec844-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span><span class="sxs-lookup"><span data-stu-id="ec844-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="ec844-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span><span class="sxs-lookup"><span data-stu-id="ec844-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="ec844-108">If the type does not match, an error is thrown.</span><span class="sxs-lookup"><span data-stu-id="ec844-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="ec844-109">The types are expressed with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="ec844-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="ec844-110">**bin** – Binary</span><span class="sxs-lookup"><span data-stu-id="ec844-110">**bin** – Binary</span></span>
* <span data-ttu-id="ec844-111">**bool** – Boolean</span><span class="sxs-lookup"><span data-stu-id="ec844-111">**bool** – Boolean</span></span>
* <span data-ttu-id="ec844-112">**dt** – UTC Date/Time</span><span class="sxs-lookup"><span data-stu-id="ec844-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="ec844-113">**enum** – Enumeration of known constants</span><span class="sxs-lookup"><span data-stu-id="ec844-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="ec844-114">**exp** – Expression, which is expected to evaluate to a Boolean</span><span class="sxs-lookup"><span data-stu-id="ec844-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="ec844-115">**mvbin** – Multi-Valued Binary</span><span class="sxs-lookup"><span data-stu-id="ec844-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="ec844-116">**mvstr** – Multi-Valued String</span><span class="sxs-lookup"><span data-stu-id="ec844-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="ec844-117">**mvref** – Multi-Valued Reference</span><span class="sxs-lookup"><span data-stu-id="ec844-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="ec844-118">**num** – Numeric</span><span class="sxs-lookup"><span data-stu-id="ec844-118">**num** – Numeric</span></span>
* <span data-ttu-id="ec844-119">**ref** – Reference</span><span class="sxs-lookup"><span data-stu-id="ec844-119">**ref** – Reference</span></span>
* <span data-ttu-id="ec844-120">**str** – String</span><span class="sxs-lookup"><span data-stu-id="ec844-120">**str** – String</span></span>
* <span data-ttu-id="ec844-121">**var** – A variant of (almost) any other type</span><span class="sxs-lookup"><span data-stu-id="ec844-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="ec844-122">**void** – doesn’t return a value</span><span class="sxs-lookup"><span data-stu-id="ec844-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="ec844-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="ec844-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="ec844-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="ec844-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="ec844-125">Functions Reference</span><span class="sxs-lookup"><span data-stu-id="ec844-125">Functions Reference</span></span>
| <span data-ttu-id="ec844-126">List of functions</span><span class="sxs-lookup"><span data-stu-id="ec844-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="ec844-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="ec844-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="ec844-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="ec844-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="ec844-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="ec844-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="ec844-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="ec844-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="ec844-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="ec844-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="ec844-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="ec844-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="ec844-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="ec844-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="ec844-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="ec844-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="ec844-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="ec844-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="ec844-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="ec844-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="ec844-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="ec844-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="ec844-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="ec844-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="ec844-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="ec844-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="ec844-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="ec844-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="ec844-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="ec844-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="ec844-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="ec844-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="ec844-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="ec844-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="ec844-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="ec844-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="ec844-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="ec844-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="ec844-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="ec844-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="ec844-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="ec844-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="ec844-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="ec844-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="ec844-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="ec844-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="ec844-150">**Conversion**</span><span class="sxs-lookup"><span data-stu-id="ec844-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="ec844-151">CBool</span><span class="sxs-lookup"><span data-stu-id="ec844-151">CBool</span></span>](#cbool) |[<span data-ttu-id="ec844-152">CDate</span><span class="sxs-lookup"><span data-stu-id="ec844-152">CDate</span></span>](#cdate) |[<span data-ttu-id="ec844-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="ec844-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="ec844-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="ec844-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="ec844-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="ec844-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="ec844-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="ec844-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="ec844-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="ec844-158">CNum</span><span class="sxs-lookup"><span data-stu-id="ec844-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="ec844-159">CRef</span><span class="sxs-lookup"><span data-stu-id="ec844-159">CRef</span></span>](#cref) |[<span data-ttu-id="ec844-160">CStr</span><span class="sxs-lookup"><span data-stu-id="ec844-160">CStr</span></span>](#cstr) |[<span data-ttu-id="ec844-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="ec844-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="ec844-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="ec844-163">**Date / Time**</span><span class="sxs-lookup"><span data-stu-id="ec844-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="ec844-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="ec844-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="ec844-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="ec844-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="ec844-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="ec844-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="ec844-167">Now</span><span class="sxs-lookup"><span data-stu-id="ec844-167">Now</span></span>](#now) | |
| [<span data-ttu-id="ec844-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="ec844-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="ec844-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="ec844-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="ec844-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="ec844-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="ec844-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="ec844-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="ec844-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="ec844-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="ec844-173">**Evaluation**</span><span class="sxs-lookup"><span data-stu-id="ec844-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="ec844-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="ec844-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="ec844-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="ec844-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="ec844-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="ec844-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="ec844-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="ec844-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="ec844-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="ec844-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="ec844-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="ec844-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="ec844-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="ec844-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="ec844-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="ec844-182">IsString</span><span class="sxs-lookup"><span data-stu-id="ec844-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="ec844-183">**Math**</span><span class="sxs-lookup"><span data-stu-id="ec844-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="ec844-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="ec844-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="ec844-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="ec844-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="ec844-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="ec844-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="ec844-187">**Multi-valued**</span><span class="sxs-lookup"><span data-stu-id="ec844-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="ec844-188">Contains</span><span class="sxs-lookup"><span data-stu-id="ec844-188">Contains</span></span>](#contains) |[<span data-ttu-id="ec844-189">Count</span><span class="sxs-lookup"><span data-stu-id="ec844-189">Count</span></span>](#count) |[<span data-ttu-id="ec844-190">Item</span><span class="sxs-lookup"><span data-stu-id="ec844-190">Item</span></span>](#item) |[<span data-ttu-id="ec844-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="ec844-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="ec844-192">Join</span><span class="sxs-lookup"><span data-stu-id="ec844-192">Join</span></span>](#join) |[<span data-ttu-id="ec844-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="ec844-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="ec844-194">Split</span><span class="sxs-lookup"><span data-stu-id="ec844-194">Split</span></span>](#split) | | |
| <span data-ttu-id="ec844-195">**Program Flow**</span><span class="sxs-lookup"><span data-stu-id="ec844-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="ec844-196">Error</span><span class="sxs-lookup"><span data-stu-id="ec844-196">Error</span></span>](#error) |[<span data-ttu-id="ec844-197">IIF</span><span class="sxs-lookup"><span data-stu-id="ec844-197">IIF</span></span>](#iif) |[<span data-ttu-id="ec844-198">Select</span><span class="sxs-lookup"><span data-stu-id="ec844-198">Select</span></span>](#select) |[<span data-ttu-id="ec844-199">Switch</span><span class="sxs-lookup"><span data-stu-id="ec844-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="ec844-200">Where</span><span class="sxs-lookup"><span data-stu-id="ec844-200">Where</span></span>](#where) |[<span data-ttu-id="ec844-201">With</span><span class="sxs-lookup"><span data-stu-id="ec844-201">With</span></span>](#with) | | | |
| <span data-ttu-id="ec844-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="ec844-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="ec844-203">GUID</span><span class="sxs-lookup"><span data-stu-id="ec844-203">GUID</span></span>](#guid) |[<span data-ttu-id="ec844-204">InStr</span><span class="sxs-lookup"><span data-stu-id="ec844-204">InStr</span></span>](#instr) |[<span data-ttu-id="ec844-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="ec844-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="ec844-206">LCase</span><span class="sxs-lookup"><span data-stu-id="ec844-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="ec844-207">Left</span><span class="sxs-lookup"><span data-stu-id="ec844-207">Left</span></span>](#left) |[<span data-ttu-id="ec844-208">Len</span><span class="sxs-lookup"><span data-stu-id="ec844-208">Len</span></span>](#len) |[<span data-ttu-id="ec844-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="ec844-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="ec844-210">Mid</span><span class="sxs-lookup"><span data-stu-id="ec844-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="ec844-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="ec844-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="ec844-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="ec844-212">PadRight</span></span>](#padright) |[<span data-ttu-id="ec844-213">PCase</span><span class="sxs-lookup"><span data-stu-id="ec844-213">PCase</span></span>](#pcase) |[<span data-ttu-id="ec844-214">Replace</span><span class="sxs-lookup"><span data-stu-id="ec844-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="ec844-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="ec844-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="ec844-216">Right</span><span class="sxs-lookup"><span data-stu-id="ec844-216">Right</span></span>](#right) |[<span data-ttu-id="ec844-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="ec844-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="ec844-218">Trim</span><span class="sxs-lookup"><span data-stu-id="ec844-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="ec844-219">UCase</span><span class="sxs-lookup"><span data-stu-id="ec844-219">UCase</span></span>](#ucase) |[<span data-ttu-id="ec844-220">Word</span><span class="sxs-lookup"><span data-stu-id="ec844-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="ec844-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="ec844-221">BitAnd</span></span>
<span data-ttu-id="ec844-222">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-222">**Description:**</span></span>  
<span data-ttu-id="ec844-223">The BitAnd function sets specified bits on a value.</span><span class="sxs-lookup"><span data-stu-id="ec844-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="ec844-224">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="ec844-225">value1, value2: numeric values that should be AND’ed together</span><span class="sxs-lookup"><span data-stu-id="ec844-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="ec844-226">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-226">**Remarks:**</span></span>  
<span data-ttu-id="ec844-227">This function converts both parameters to the binary representation and sets a bit to:</span><span class="sxs-lookup"><span data-stu-id="ec844-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="ec844-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span><span class="sxs-lookup"><span data-stu-id="ec844-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="ec844-229">1 - if both of the corresponding bits are 1.</span><span class="sxs-lookup"><span data-stu-id="ec844-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="ec844-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span><span class="sxs-lookup"><span data-stu-id="ec844-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="ec844-231">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="ec844-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span><span class="sxs-lookup"><span data-stu-id="ec844-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="ec844-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="ec844-233">BitOr</span></span>
<span data-ttu-id="ec844-234">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-234">**Description:**</span></span>  
<span data-ttu-id="ec844-235">The BitOr function sets specified bits on a value.</span><span class="sxs-lookup"><span data-stu-id="ec844-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="ec844-236">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="ec844-237">value1, value2: numeric values that should be OR’ed together</span><span class="sxs-lookup"><span data-stu-id="ec844-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="ec844-238">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-238">**Remarks:**</span></span>  
<span data-ttu-id="ec844-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span><span class="sxs-lookup"><span data-stu-id="ec844-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="ec844-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span><span class="sxs-lookup"><span data-stu-id="ec844-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="ec844-241">CBool</span><span class="sxs-lookup"><span data-stu-id="ec844-241">CBool</span></span>
<span data-ttu-id="ec844-242">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-242">**Description:**</span></span>  
<span data-ttu-id="ec844-243">The CBool function returns a Boolean based on the evaluated expression</span><span class="sxs-lookup"><span data-stu-id="ec844-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="ec844-244">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="ec844-245">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-245">**Remarks:**</span></span>  
<span data-ttu-id="ec844-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span><span class="sxs-lookup"><span data-stu-id="ec844-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="ec844-247">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="ec844-248">Returns True if both attributes have the same value.</span><span class="sxs-lookup"><span data-stu-id="ec844-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="ec844-249">CDate</span><span class="sxs-lookup"><span data-stu-id="ec844-249">CDate</span></span>
<span data-ttu-id="ec844-250">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-250">**Description:**</span></span>  
<span data-ttu-id="ec844-251">The CDate function returns a UTC DateTime from a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="ec844-252">DateTime is not a native attribute type in Sync but is used by some functions.</span><span class="sxs-lookup"><span data-stu-id="ec844-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="ec844-253">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="ec844-254">Value: A string with a date, time, and optionally time zone</span><span class="sxs-lookup"><span data-stu-id="ec844-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="ec844-255">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-255">**Remarks:**</span></span>  
<span data-ttu-id="ec844-256">The returned string is always in UTC.</span><span class="sxs-lookup"><span data-stu-id="ec844-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="ec844-257">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="ec844-258">Returns a DateTime based on the employee’s start time</span><span class="sxs-lookup"><span data-stu-id="ec844-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="ec844-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span><span class="sxs-lookup"><span data-stu-id="ec844-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>


- - -
### <a name="certextensionoids"></a><span data-ttu-id="ec844-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="ec844-260">CertExtensionOids</span></span>
<span data-ttu-id="ec844-261">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-261">**Description:**</span></span>  
<span data-ttu-id="ec844-262">Returns the Oid values of all the critical extensions of a certificate object.</span><span class="sxs-lookup"><span data-stu-id="ec844-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="ec844-263">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="ec844-264">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="ec844-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="ec844-266">CertFormat</span></span>
<span data-ttu-id="ec844-267">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-267">**Description:**</span></span>  
<span data-ttu-id="ec844-268">Returns the name of the format of this X.509v3 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="ec844-269">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="ec844-270">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="ec844-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="ec844-272">CertFriendlyName</span></span>
<span data-ttu-id="ec844-273">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-273">**Description:**</span></span>  
<span data-ttu-id="ec844-274">Returns the associated alias for a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="ec844-275">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="ec844-276">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="ec844-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="ec844-278">CertHashString</span></span>
<span data-ttu-id="ec844-279">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-279">**Description:**</span></span>  
<span data-ttu-id="ec844-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span><span class="sxs-lookup"><span data-stu-id="ec844-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="ec844-281">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="ec844-282">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="ec844-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="ec844-284">CertIssuer</span></span>
<span data-ttu-id="ec844-285">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-285">**Description:**</span></span>  
<span data-ttu-id="ec844-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="ec844-287">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="ec844-288">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="ec844-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="ec844-290">CertIssuerDN</span></span>
<span data-ttu-id="ec844-291">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-291">**Description:**</span></span>  
<span data-ttu-id="ec844-292">Returns the distinguished name of the certificate issuer.</span><span class="sxs-lookup"><span data-stu-id="ec844-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="ec844-293">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="ec844-294">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="ec844-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="ec844-296">CertIssuerOid</span></span>
<span data-ttu-id="ec844-297">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-297">**Description:**</span></span>  
<span data-ttu-id="ec844-298">Returns the Oid of the certificate issuer.</span><span class="sxs-lookup"><span data-stu-id="ec844-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="ec844-299">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="ec844-300">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="ec844-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="ec844-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="ec844-303">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-303">**Description:**</span></span>  
<span data-ttu-id="ec844-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="ec844-305">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="ec844-306">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="ec844-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="ec844-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="ec844-309">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-309">**Description:**</span></span>  
<span data-ttu-id="ec844-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span><span class="sxs-lookup"><span data-stu-id="ec844-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="ec844-311">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="ec844-312">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="ec844-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="ec844-314">CertNameInfo</span></span>
<span data-ttu-id="ec844-315">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-315">**Description:**</span></span>  
<span data-ttu-id="ec844-316">Returns the subject and issuer names from a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="ec844-317">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="ec844-318">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="ec844-320">X509NameType: The X509NameType value for the subject.</span><span class="sxs-lookup"><span data-stu-id="ec844-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="ec844-321">includesIssuerName: true to include the issuer name; otherwise, false.</span><span class="sxs-lookup"><span data-stu-id="ec844-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="ec844-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="ec844-322">CertNotAfter</span></span>
<span data-ttu-id="ec844-323">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-323">**Description:**</span></span>  
<span data-ttu-id="ec844-324">Returns the date in local time after which a certificate is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="ec844-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="ec844-325">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="ec844-326">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="ec844-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="ec844-328">CertNotBefore</span></span>
<span data-ttu-id="ec844-329">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-329">**Description:**</span></span>  
<span data-ttu-id="ec844-330">Returns the date in local time on which a certificate becomes valid.</span><span class="sxs-lookup"><span data-stu-id="ec844-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="ec844-331">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="ec844-332">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="ec844-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="ec844-334">CertPublicKeyOid</span></span>
<span data-ttu-id="ec844-335">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-335">**Description:**</span></span>  
<span data-ttu-id="ec844-336">Returns the Oid of the public key for the X.509v3 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="ec844-337">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="ec844-338">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="ec844-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="ec844-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="ec844-341">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-341">**Description:**</span></span>  
<span data-ttu-id="ec844-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="ec844-343">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="ec844-344">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="ec844-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="ec844-346">CertSerialNumber</span></span>
<span data-ttu-id="ec844-347">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-347">**Description:**</span></span>  
<span data-ttu-id="ec844-348">Returns the serial number of the X.509v3 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="ec844-349">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="ec844-350">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="ec844-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="ec844-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="ec844-353">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-353">**Description:**</span></span>  
<span data-ttu-id="ec844-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="ec844-355">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="ec844-356">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="ec844-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="ec844-358">CertSubject</span></span>
<span data-ttu-id="ec844-359">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-359">**Description:**</span></span>  
<span data-ttu-id="ec844-360">Gets the subject distinguished name from a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="ec844-361">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="ec844-362">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="ec844-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="ec844-364">CertSubjectNameDN</span></span>
<span data-ttu-id="ec844-365">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-365">**Description:**</span></span>  
<span data-ttu-id="ec844-366">Returns the subject distinguished name from a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="ec844-367">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="ec844-368">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="ec844-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="ec844-370">CertSubjectNameOid</span></span>
<span data-ttu-id="ec844-371">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-371">**Description:**</span></span>  
<span data-ttu-id="ec844-372">Returns the Oid of the subject name from a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="ec844-373">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="ec844-374">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="ec844-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="ec844-376">CertThumbprint</span></span>
<span data-ttu-id="ec844-377">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-377">**Description:**</span></span>  
<span data-ttu-id="ec844-378">Returns the thumbprint of a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="ec844-379">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="ec844-380">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="ec844-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="ec844-382">CertVersion</span></span>
<span data-ttu-id="ec844-383">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-383">**Description:**</span></span>  
<span data-ttu-id="ec844-384">Returns the X.509 format version of a certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="ec844-385">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="ec844-386">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="ec844-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-388">CGuid</span></span>
<span data-ttu-id="ec844-389">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-389">**Description:**</span></span>  
<span data-ttu-id="ec844-390">The CGuid function converts the string representation of a GUID to its binary representation.</span><span class="sxs-lookup"><span data-stu-id="ec844-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="ec844-391">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="ec844-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="ec844-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="ec844-393">Contains</span><span class="sxs-lookup"><span data-stu-id="ec844-393">Contains</span></span>
<span data-ttu-id="ec844-394">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-394">**Description:**</span></span>  
<span data-ttu-id="ec844-395">The Contains function finds a string inside a multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="ec844-396">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-396">**Syntax:**</span></span>  
<span data-ttu-id="ec844-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span><span class="sxs-lookup"><span data-stu-id="ec844-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="ec844-398">`num Contains (mvref attribute, str search)` - case-sensitive</span><span class="sxs-lookup"><span data-stu-id="ec844-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="ec844-399">attribute: the multi-valued attribute to search.</span><span class="sxs-lookup"><span data-stu-id="ec844-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="ec844-400">search: string to find in the attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="ec844-401">Casetype: CaseInsensitive or CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="ec844-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="ec844-402">Returns index in the multi-valued attribute where the string was found.</span><span class="sxs-lookup"><span data-stu-id="ec844-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="ec844-403">0 is returned if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="ec844-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="ec844-404">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-404">**Remarks:**</span></span>  
<span data-ttu-id="ec844-405">For multi-valued string attributes, the search finds substrings in the values.</span><span class="sxs-lookup"><span data-stu-id="ec844-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="ec844-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span><span class="sxs-lookup"><span data-stu-id="ec844-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="ec844-407">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="ec844-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span><span class="sxs-lookup"><span data-stu-id="ec844-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="ec844-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="ec844-409">ConvertFromBase64</span></span>
<span data-ttu-id="ec844-410">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-410">**Description:**</span></span>  
<span data-ttu-id="ec844-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span><span class="sxs-lookup"><span data-stu-id="ec844-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="ec844-412">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-412">**Syntax:**</span></span>  
<span data-ttu-id="ec844-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span><span class="sxs-lookup"><span data-stu-id="ec844-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="ec844-414">source: Base64 encoded string</span><span class="sxs-lookup"><span data-stu-id="ec844-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="ec844-415">Encoding: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="ec844-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="ec844-416">**Example**</span><span class="sxs-lookup"><span data-stu-id="ec844-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="ec844-417">Both examples return "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="ec844-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="ec844-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="ec844-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="ec844-419">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-419">**Description:**</span></span>  
<span data-ttu-id="ec844-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="ec844-421">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="ec844-422">source: UTF8 2-byte encoded sting</span><span class="sxs-lookup"><span data-stu-id="ec844-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="ec844-423">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-423">**Remarks:**</span></span>  
<span data-ttu-id="ec844-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="ec844-425">This format is used by Azure Active Directory as DN.</span><span class="sxs-lookup"><span data-stu-id="ec844-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="ec844-426">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="ec844-427">Returns "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="ec844-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="ec844-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="ec844-428">ConvertToBase64</span></span>
<span data-ttu-id="ec844-429">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-429">**Description:**</span></span>  
<span data-ttu-id="ec844-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span><span class="sxs-lookup"><span data-stu-id="ec844-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="ec844-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span><span class="sxs-lookup"><span data-stu-id="ec844-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="ec844-432">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="ec844-433">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="ec844-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="ec844-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="ec844-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="ec844-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="ec844-436">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-436">**Description:**</span></span>  
<span data-ttu-id="ec844-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span><span class="sxs-lookup"><span data-stu-id="ec844-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="ec844-438">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="ec844-439">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-439">**Remarks:**</span></span>  
<span data-ttu-id="ec844-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span><span class="sxs-lookup"><span data-stu-id="ec844-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="ec844-441">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="ec844-442">Returns 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="ec844-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="ec844-443">Count</span><span class="sxs-lookup"><span data-stu-id="ec844-443">Count</span></span>
<span data-ttu-id="ec844-444">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-444">**Description:**</span></span>  
<span data-ttu-id="ec844-445">The Count function returns the number of elements in a multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="ec844-446">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="ec844-447">CNum</span><span class="sxs-lookup"><span data-stu-id="ec844-447">CNum</span></span>
<span data-ttu-id="ec844-448">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-448">**Description:**</span></span>  
<span data-ttu-id="ec844-449">The CNum function takes a string and returns a numeric data type.</span><span class="sxs-lookup"><span data-stu-id="ec844-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="ec844-450">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="ec844-451">CRef</span><span class="sxs-lookup"><span data-stu-id="ec844-451">CRef</span></span>
<span data-ttu-id="ec844-452">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-452">**Description:**</span></span>  
<span data-ttu-id="ec844-453">Converts a string to a reference attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="ec844-454">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="ec844-455">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="ec844-456">CStr</span><span class="sxs-lookup"><span data-stu-id="ec844-456">CStr</span></span>
<span data-ttu-id="ec844-457">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-457">**Description:**</span></span>  
<span data-ttu-id="ec844-458">The CStr function converts to a string data type.</span><span class="sxs-lookup"><span data-stu-id="ec844-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="ec844-459">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="ec844-460">value: Can be a numeric value, reference attribute, or Boolean.</span><span class="sxs-lookup"><span data-stu-id="ec844-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="ec844-461">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="ec844-462">Could return "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="ec844-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="ec844-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="ec844-463">DateAdd</span></span>
<span data-ttu-id="ec844-464">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-464">**Description:**</span></span>  
<span data-ttu-id="ec844-465">Returns a Date containing a date to which a specified time interval has been added.</span><span class="sxs-lookup"><span data-stu-id="ec844-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="ec844-466">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="ec844-467">interval: String expression that is the interval of time you want to add.</span><span class="sxs-lookup"><span data-stu-id="ec844-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="ec844-468">The string must have one of the following values:</span><span class="sxs-lookup"><span data-stu-id="ec844-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="ec844-469">yyyy Year</span><span class="sxs-lookup"><span data-stu-id="ec844-469">yyyy Year</span></span>
  * <span data-ttu-id="ec844-470">q Quarter</span><span class="sxs-lookup"><span data-stu-id="ec844-470">q Quarter</span></span>
  * <span data-ttu-id="ec844-471">m Month</span><span class="sxs-lookup"><span data-stu-id="ec844-471">m Month</span></span>
  * <span data-ttu-id="ec844-472">y Day of year</span><span class="sxs-lookup"><span data-stu-id="ec844-472">y Day of year</span></span>
  * <span data-ttu-id="ec844-473">d Day</span><span class="sxs-lookup"><span data-stu-id="ec844-473">d Day</span></span>
  * <span data-ttu-id="ec844-474">w Weekday</span><span class="sxs-lookup"><span data-stu-id="ec844-474">w Weekday</span></span>
  * <span data-ttu-id="ec844-475">ww Week</span><span class="sxs-lookup"><span data-stu-id="ec844-475">ww Week</span></span>
  * <span data-ttu-id="ec844-476">h Hour</span><span class="sxs-lookup"><span data-stu-id="ec844-476">h Hour</span></span>
  * <span data-ttu-id="ec844-477">n Minute</span><span class="sxs-lookup"><span data-stu-id="ec844-477">n Minute</span></span>
  * <span data-ttu-id="ec844-478">s Second</span><span class="sxs-lookup"><span data-stu-id="ec844-478">s Second</span></span>
* <span data-ttu-id="ec844-479">value: The number of units you want to add.</span><span class="sxs-lookup"><span data-stu-id="ec844-479">value: The number of units you want to add.</span></span> <span data-ttu-id="ec844-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span><span class="sxs-lookup"><span data-stu-id="ec844-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="ec844-481">date: DateTime representing date to which the interval is added.</span><span class="sxs-lookup"><span data-stu-id="ec844-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="ec844-482">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="ec844-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="ec844-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="ec844-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="ec844-484">DateFromNum</span></span>
<span data-ttu-id="ec844-485">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-485">**Description:**</span></span>  
<span data-ttu-id="ec844-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span><span class="sxs-lookup"><span data-stu-id="ec844-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="ec844-487">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="ec844-488">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="ec844-489">Returns a DateTime representing 2012-01-01 23:00:00</span><span class="sxs-lookup"><span data-stu-id="ec844-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="ec844-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="ec844-490">DNComponent</span></span>
<span data-ttu-id="ec844-491">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-491">**Description:**</span></span>  
<span data-ttu-id="ec844-492">The DNComponent function returns the value of a specified DN component going from left.</span><span class="sxs-lookup"><span data-stu-id="ec844-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="ec844-493">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="ec844-494">dn: the reference attribute to interpret</span><span class="sxs-lookup"><span data-stu-id="ec844-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="ec844-495">ComponentNumber: The component in the DN to return</span><span class="sxs-lookup"><span data-stu-id="ec844-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="ec844-496">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-496">**Example:**</span></span>  
`DNComponent(CRef([dn]),1)`  
<span data-ttu-id="ec844-497">If dn is "cn=Joe,ou=…," it returns Joe</span><span class="sxs-lookup"><span data-stu-id="ec844-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="ec844-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="ec844-498">DNComponentRev</span></span>
<span data-ttu-id="ec844-499">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-499">**Description:**</span></span>  
<span data-ttu-id="ec844-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span><span class="sxs-lookup"><span data-stu-id="ec844-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="ec844-501">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="ec844-502">dn: the reference attribute to interpret</span><span class="sxs-lookup"><span data-stu-id="ec844-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="ec844-503">ComponentNumber - The component in the DN to return</span><span class="sxs-lookup"><span data-stu-id="ec844-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="ec844-504">Options: DC – Ignore all components with "dc="</span><span class="sxs-lookup"><span data-stu-id="ec844-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="ec844-505">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-505">**Example:**</span></span>  
<span data-ttu-id="ec844-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span><span class="sxs-lookup"><span data-stu-id="ec844-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev(CRef([dn]),3)`  
`DNComponentRev(CRef([dn]),1,"DC")`  
<span data-ttu-id="ec844-507">Both return US.</span><span class="sxs-lookup"><span data-stu-id="ec844-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="ec844-508">Error</span><span class="sxs-lookup"><span data-stu-id="ec844-508">Error</span></span>
<span data-ttu-id="ec844-509">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-509">**Description:**</span></span>  
<span data-ttu-id="ec844-510">The Error function is used to return a custom error.</span><span class="sxs-lookup"><span data-stu-id="ec844-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="ec844-511">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="ec844-512">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="ec844-513">If the attribute accountName is not present, throw an error on the object.</span><span class="sxs-lookup"><span data-stu-id="ec844-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="ec844-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="ec844-514">EscapeDNComponent</span></span>
<span data-ttu-id="ec844-515">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-515">**Description:**</span></span>  
<span data-ttu-id="ec844-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span><span class="sxs-lookup"><span data-stu-id="ec844-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="ec844-517">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="ec844-518">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="ec844-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span><span class="sxs-lookup"><span data-stu-id="ec844-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="ec844-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="ec844-520">FormatDateTime</span></span>
<span data-ttu-id="ec844-521">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-521">**Description:**</span></span>  
<span data-ttu-id="ec844-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span><span class="sxs-lookup"><span data-stu-id="ec844-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="ec844-523">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="ec844-524">value: a value in the DateTime format</span><span class="sxs-lookup"><span data-stu-id="ec844-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="ec844-525">format: a string representing the format to convert to.</span><span class="sxs-lookup"><span data-stu-id="ec844-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="ec844-526">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-526">**Remarks:**</span></span>  
<span data-ttu-id="ec844-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="ec844-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="ec844-528">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="ec844-529">Results in "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="ec844-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="ec844-530">Can result in "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="ec844-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="ec844-531">Guid</span><span class="sxs-lookup"><span data-stu-id="ec844-531">Guid</span></span>
<span data-ttu-id="ec844-532">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-532">**Description:**</span></span>  
<span data-ttu-id="ec844-533">The function Guid generates a new random GUID</span><span class="sxs-lookup"><span data-stu-id="ec844-533">The function Guid generates a new random GUID</span></span>

<span data-ttu-id="ec844-534">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-534">**Syntax:**</span></span>  
`str Guid()`

- - -
### <a name="iif"></a><span data-ttu-id="ec844-535">IIF</span><span class="sxs-lookup"><span data-stu-id="ec844-535">IIF</span></span>
<span data-ttu-id="ec844-536">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-536">**Description:**</span></span>  
<span data-ttu-id="ec844-537">The IIF function returns one of a set of possible values based on a specified condition.</span><span class="sxs-lookup"><span data-stu-id="ec844-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="ec844-538">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="ec844-539">condition: any value or expression that can be evaluated to true or false.</span><span class="sxs-lookup"><span data-stu-id="ec844-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="ec844-540">valueIfTrue: If the condition evaluates to true, the returned value.</span><span class="sxs-lookup"><span data-stu-id="ec844-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="ec844-541">valueIfFalse: If the condition evaluates to false, the returned value.</span><span class="sxs-lookup"><span data-stu-id="ec844-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="ec844-542">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="ec844-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span><span class="sxs-lookup"><span data-stu-id="ec844-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="ec844-544">InStr</span><span class="sxs-lookup"><span data-stu-id="ec844-544">InStr</span></span>
<span data-ttu-id="ec844-545">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-545">**Description:**</span></span>  
<span data-ttu-id="ec844-546">The InStr function finds the first occurrence of a substring in a string</span><span class="sxs-lookup"><span data-stu-id="ec844-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="ec844-547">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="ec844-548">stringcheck: string to be searched</span><span class="sxs-lookup"><span data-stu-id="ec844-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="ec844-549">stringmatch: string to be found</span><span class="sxs-lookup"><span data-stu-id="ec844-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="ec844-550">start: starting position to find the substring</span><span class="sxs-lookup"><span data-stu-id="ec844-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="ec844-551">compare: vbTextCompare or vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="ec844-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="ec844-552">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-552">**Remarks:**</span></span>  
<span data-ttu-id="ec844-553">Returns the position where the substring was found or 0 if not found.</span><span class="sxs-lookup"><span data-stu-id="ec844-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="ec844-554">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="ec844-555">Evalues to 5</span><span class="sxs-lookup"><span data-stu-id="ec844-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="ec844-556">Evaluates to 7</span><span class="sxs-lookup"><span data-stu-id="ec844-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="ec844-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="ec844-557">InStrRev</span></span>
<span data-ttu-id="ec844-558">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-558">**Description:**</span></span>  
<span data-ttu-id="ec844-559">The InStrRev function finds the last occurrence of a substring in a string</span><span class="sxs-lookup"><span data-stu-id="ec844-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="ec844-560">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="ec844-561">stringcheck: string to be searched</span><span class="sxs-lookup"><span data-stu-id="ec844-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="ec844-562">stringmatch: string to be found</span><span class="sxs-lookup"><span data-stu-id="ec844-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="ec844-563">start: starting position to find the substring</span><span class="sxs-lookup"><span data-stu-id="ec844-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="ec844-564">compare: vbTextCompare or vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="ec844-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="ec844-565">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-565">**Remarks:**</span></span>  
<span data-ttu-id="ec844-566">Returns the position where the substring was found or 0 if not found.</span><span class="sxs-lookup"><span data-stu-id="ec844-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="ec844-567">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="ec844-568">Returns 7</span><span class="sxs-lookup"><span data-stu-id="ec844-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="ec844-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="ec844-569">IsBitSet</span></span>
<span data-ttu-id="ec844-570">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-570">**Description:**</span></span>  
<span data-ttu-id="ec844-571">The function IsBitSet Tests if a bit is set or not</span><span class="sxs-lookup"><span data-stu-id="ec844-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="ec844-572">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="ec844-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span><span class="sxs-lookup"><span data-stu-id="ec844-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="ec844-574">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="ec844-575">Returns True because bit "4" is set in the hexadecimal value "F"</span><span class="sxs-lookup"><span data-stu-id="ec844-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="ec844-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="ec844-576">IsDate</span></span>
<span data-ttu-id="ec844-577">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-577">**Description:**</span></span>  
<span data-ttu-id="ec844-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="ec844-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="ec844-579">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="ec844-580">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-580">**Remarks:**</span></span>  
<span data-ttu-id="ec844-581">Used to determine if CDate() can be successful.</span><span class="sxs-lookup"><span data-stu-id="ec844-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="ec844-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="ec844-582">IsCert</span></span>
<span data-ttu-id="ec844-583">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-583">**Description:**</span></span>  
<span data-ttu-id="ec844-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span><span class="sxs-lookup"><span data-stu-id="ec844-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="ec844-585">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="ec844-586">certificateRawData: Byte array representation of an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="ec844-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="ec844-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span><span class="sxs-lookup"><span data-stu-id="ec844-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="ec844-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="ec844-588">IsEmpty</span></span>
<span data-ttu-id="ec844-589">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-589">**Description:**</span></span>  
<span data-ttu-id="ec844-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="ec844-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="ec844-591">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="ec844-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-592">IsGuid</span></span>
<span data-ttu-id="ec844-593">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-593">**Description:**</span></span>  
<span data-ttu-id="ec844-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span><span class="sxs-lookup"><span data-stu-id="ec844-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="ec844-595">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="ec844-596">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-596">**Remarks:**</span></span>  
<span data-ttu-id="ec844-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="ec844-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="ec844-598">Used to determine if CGuid() can be successful.</span><span class="sxs-lookup"><span data-stu-id="ec844-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="ec844-599">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="ec844-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span><span class="sxs-lookup"><span data-stu-id="ec844-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="ec844-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="ec844-601">IsNull</span></span>
<span data-ttu-id="ec844-602">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-602">**Description:**</span></span>  
<span data-ttu-id="ec844-603">If the expression evaluates to Null, then the IsNull function returns true.</span><span class="sxs-lookup"><span data-stu-id="ec844-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="ec844-604">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="ec844-605">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-605">**Remarks:**</span></span>  
<span data-ttu-id="ec844-606">For an attribute, a Null is expressed by the absence of the attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="ec844-607">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="ec844-608">Returns True if the attribute is not present in the CS or MV.</span><span class="sxs-lookup"><span data-stu-id="ec844-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="ec844-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="ec844-609">IsNullOrEmpty</span></span>
<span data-ttu-id="ec844-610">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-610">**Description:**</span></span>  
<span data-ttu-id="ec844-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span><span class="sxs-lookup"><span data-stu-id="ec844-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="ec844-612">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="ec844-613">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-613">**Remarks:**</span></span>  
<span data-ttu-id="ec844-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="ec844-615">The inverse of this function is named IsPresent.</span><span class="sxs-lookup"><span data-stu-id="ec844-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="ec844-616">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="ec844-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span><span class="sxs-lookup"><span data-stu-id="ec844-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="ec844-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="ec844-618">IsNumeric</span></span>
<span data-ttu-id="ec844-619">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-619">**Description:**</span></span>  
<span data-ttu-id="ec844-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span><span class="sxs-lookup"><span data-stu-id="ec844-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="ec844-621">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="ec844-622">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-622">**Remarks:**</span></span>  
<span data-ttu-id="ec844-623">Used to determine if CNum() can be successful to parse the expression.</span><span class="sxs-lookup"><span data-stu-id="ec844-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="ec844-624">IsString</span><span class="sxs-lookup"><span data-stu-id="ec844-624">IsString</span></span>
<span data-ttu-id="ec844-625">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-625">**Description:**</span></span>  
<span data-ttu-id="ec844-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span><span class="sxs-lookup"><span data-stu-id="ec844-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="ec844-627">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="ec844-628">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-628">**Remarks:**</span></span>  
<span data-ttu-id="ec844-629">Used to determine if CStr() can be successful to parse the expression.</span><span class="sxs-lookup"><span data-stu-id="ec844-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="ec844-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="ec844-630">IsPresent</span></span>
<span data-ttu-id="ec844-631">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-631">**Description:**</span></span>  
<span data-ttu-id="ec844-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span><span class="sxs-lookup"><span data-stu-id="ec844-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="ec844-633">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="ec844-634">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-634">**Remarks:**</span></span>  
<span data-ttu-id="ec844-635">The inverse of this function is named IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="ec844-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="ec844-636">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="ec844-637">Item</span><span class="sxs-lookup"><span data-stu-id="ec844-637">Item</span></span>
<span data-ttu-id="ec844-638">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-638">**Description:**</span></span>  
<span data-ttu-id="ec844-639">The Item function returns one item from a multi-valued string/attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="ec844-640">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="ec844-641">attribute: multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="ec844-642">index: index to an item in the multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="ec844-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="ec844-643">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-643">**Remarks:**</span></span>  
<span data-ttu-id="ec844-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="ec844-645">Throws an error if index is out of bounds.</span><span class="sxs-lookup"><span data-stu-id="ec844-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="ec844-646">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-646">**Example:**</span></span>  
`Mid(Item([proxyAddresses],Contains([proxyAddresses], "SMTP:")),6)`  
<span data-ttu-id="ec844-647">Returns the primary email address.</span><span class="sxs-lookup"><span data-stu-id="ec844-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="ec844-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="ec844-648">ItemOrNull</span></span>
<span data-ttu-id="ec844-649">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-649">**Description:**</span></span>  
<span data-ttu-id="ec844-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="ec844-651">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="ec844-652">attribute: multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="ec844-653">index: index to an item in the multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="ec844-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="ec844-654">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-654">**Remarks:**</span></span>  
<span data-ttu-id="ec844-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="ec844-656">If index is out of bounds, then returns a Null value.</span><span class="sxs-lookup"><span data-stu-id="ec844-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="ec844-657">Join</span><span class="sxs-lookup"><span data-stu-id="ec844-657">Join</span></span>
<span data-ttu-id="ec844-658">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-658">**Description:**</span></span>  
<span data-ttu-id="ec844-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span><span class="sxs-lookup"><span data-stu-id="ec844-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="ec844-660">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="ec844-661">attribute: Multi-valued attribute containing strings to be joined.</span><span class="sxs-lookup"><span data-stu-id="ec844-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="ec844-662">delimiter: Any string, used to separate the substrings in the returned string.</span><span class="sxs-lookup"><span data-stu-id="ec844-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="ec844-663">If omitted, the space character (" ") is used.</span><span class="sxs-lookup"><span data-stu-id="ec844-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="ec844-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span><span class="sxs-lookup"><span data-stu-id="ec844-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="ec844-665">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="ec844-665">**Remarks**</span></span>  
<span data-ttu-id="ec844-666">There is parity between the Join and Split functions.</span><span class="sxs-lookup"><span data-stu-id="ec844-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="ec844-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span><span class="sxs-lookup"><span data-stu-id="ec844-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="ec844-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span><span class="sxs-lookup"><span data-stu-id="ec844-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="ec844-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span><span class="sxs-lookup"><span data-stu-id="ec844-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="ec844-670">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="ec844-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="ec844-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="ec844-672">LCase</span><span class="sxs-lookup"><span data-stu-id="ec844-672">LCase</span></span>
<span data-ttu-id="ec844-673">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-673">**Description:**</span></span>  
<span data-ttu-id="ec844-674">The LCase function converts all characters in a string to lower case.</span><span class="sxs-lookup"><span data-stu-id="ec844-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="ec844-675">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="ec844-676">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="ec844-677">Returns "test".</span><span class="sxs-lookup"><span data-stu-id="ec844-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="ec844-678">Left</span><span class="sxs-lookup"><span data-stu-id="ec844-678">Left</span></span>
<span data-ttu-id="ec844-679">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-679">**Description:**</span></span>  
<span data-ttu-id="ec844-680">The Left function returns a specified number of characters from the left of a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="ec844-681">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="ec844-682">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="ec844-682">string: the string to return characters from</span></span>
* <span data-ttu-id="ec844-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span><span class="sxs-lookup"><span data-stu-id="ec844-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="ec844-684">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-684">**Remarks:**</span></span>  
<span data-ttu-id="ec844-685">A string containing the first numChars characters in string:</span><span class="sxs-lookup"><span data-stu-id="ec844-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="ec844-686">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="ec844-687">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="ec844-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="ec844-688">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-688">If string is null, return empty string.</span></span>

<span data-ttu-id="ec844-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="ec844-690">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="ec844-691">Returns "Joh".</span><span class="sxs-lookup"><span data-stu-id="ec844-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="ec844-692">Len</span><span class="sxs-lookup"><span data-stu-id="ec844-692">Len</span></span>
<span data-ttu-id="ec844-693">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-693">**Description:**</span></span>  
<span data-ttu-id="ec844-694">The Len function returns number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="ec844-695">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="ec844-696">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="ec844-697">Returns 8</span><span class="sxs-lookup"><span data-stu-id="ec844-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="ec844-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="ec844-698">LTrim</span></span>
<span data-ttu-id="ec844-699">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-699">**Description:**</span></span>  
<span data-ttu-id="ec844-700">The LTrim function removes leading white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="ec844-701">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="ec844-702">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="ec844-703">Returns "Test "</span><span class="sxs-lookup"><span data-stu-id="ec844-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="ec844-704">Mid</span><span class="sxs-lookup"><span data-stu-id="ec844-704">Mid</span></span>
<span data-ttu-id="ec844-705">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-705">**Description:**</span></span>  
<span data-ttu-id="ec844-706">The Mid function returns a specified number of characters from a specified position in a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="ec844-707">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="ec844-708">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="ec844-708">string: the string to return characters from</span></span>
* <span data-ttu-id="ec844-709">start: a number identifying the starting position in string to return characters from</span><span class="sxs-lookup"><span data-stu-id="ec844-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="ec844-710">NumChars: a number identifying the number of characters to return from position in string</span><span class="sxs-lookup"><span data-stu-id="ec844-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="ec844-711">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-711">**Remarks:**</span></span>  
<span data-ttu-id="ec844-712">Return numChars characters starting from position start in string.</span><span class="sxs-lookup"><span data-stu-id="ec844-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="ec844-713">A string containing numChars characters from position start in string:</span><span class="sxs-lookup"><span data-stu-id="ec844-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="ec844-714">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="ec844-715">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="ec844-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="ec844-716">If start > the length of string, return input string.</span><span class="sxs-lookup"><span data-stu-id="ec844-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="ec844-717">If start <= 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="ec844-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="ec844-718">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-718">If string is null, return empty string.</span></span>

<span data-ttu-id="ec844-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="ec844-720">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="ec844-721">Returns "hn Do".</span><span class="sxs-lookup"><span data-stu-id="ec844-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="ec844-722">Returns "Doe"</span><span class="sxs-lookup"><span data-stu-id="ec844-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="ec844-723">Now</span><span class="sxs-lookup"><span data-stu-id="ec844-723">Now</span></span>
<span data-ttu-id="ec844-724">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-724">**Description:**</span></span>  
<span data-ttu-id="ec844-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span><span class="sxs-lookup"><span data-stu-id="ec844-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="ec844-726">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="ec844-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="ec844-727">NumFromDate</span></span>
<span data-ttu-id="ec844-728">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-728">**Description:**</span></span>  
<span data-ttu-id="ec844-729">The NumFromDate function returns a date in AD’s date format.</span><span class="sxs-lookup"><span data-stu-id="ec844-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="ec844-730">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="ec844-731">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="ec844-732">Returns 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="ec844-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="ec844-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="ec844-733">PadLeft</span></span>
<span data-ttu-id="ec844-734">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-734">**Description:**</span></span>  
<span data-ttu-id="ec844-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span><span class="sxs-lookup"><span data-stu-id="ec844-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="ec844-736">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="ec844-737">string: the string to pad.</span><span class="sxs-lookup"><span data-stu-id="ec844-737">string: the string to pad.</span></span>
* <span data-ttu-id="ec844-738">length: An integer representing the desired length of string.</span><span class="sxs-lookup"><span data-stu-id="ec844-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="ec844-739">padCharacter: A string consisting of a single character to use as the pad character</span><span class="sxs-lookup"><span data-stu-id="ec844-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="ec844-740">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-740">**Remarks:**</span></span>

* <span data-ttu-id="ec844-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span><span class="sxs-lookup"><span data-stu-id="ec844-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="ec844-742">PadCharacter can be a space character, but it cannot be a null value.</span><span class="sxs-lookup"><span data-stu-id="ec844-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="ec844-743">If the length of string is equal to or greater than length, string is returned unchanged.</span><span class="sxs-lookup"><span data-stu-id="ec844-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="ec844-744">If string has a length greater than or equal to length, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="ec844-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span><span class="sxs-lookup"><span data-stu-id="ec844-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="ec844-746">If string is null, the function returns an empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="ec844-747">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="ec844-748">Returns "000000User".</span><span class="sxs-lookup"><span data-stu-id="ec844-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="ec844-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="ec844-749">PadRight</span></span>
<span data-ttu-id="ec844-750">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-750">**Description:**</span></span>  
<span data-ttu-id="ec844-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span><span class="sxs-lookup"><span data-stu-id="ec844-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="ec844-752">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="ec844-753">string: the string to pad.</span><span class="sxs-lookup"><span data-stu-id="ec844-753">string: the string to pad.</span></span>
* <span data-ttu-id="ec844-754">length: An integer representing the desired length of string.</span><span class="sxs-lookup"><span data-stu-id="ec844-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="ec844-755">padCharacter: A string consisting of a single character to use as the pad character</span><span class="sxs-lookup"><span data-stu-id="ec844-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="ec844-756">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-756">**Remarks:**</span></span>

* <span data-ttu-id="ec844-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span><span class="sxs-lookup"><span data-stu-id="ec844-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="ec844-758">padCharacter can be a space character, but it cannot be a null value.</span><span class="sxs-lookup"><span data-stu-id="ec844-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="ec844-759">If the length of string is equal to or greater than length, string is returned unchanged.</span><span class="sxs-lookup"><span data-stu-id="ec844-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="ec844-760">If string has a length greater than or equal to length, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="ec844-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span><span class="sxs-lookup"><span data-stu-id="ec844-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="ec844-762">If string is null, the function returns an empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="ec844-763">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="ec844-764">Returns "User000000".</span><span class="sxs-lookup"><span data-stu-id="ec844-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="ec844-765">PCase</span><span class="sxs-lookup"><span data-stu-id="ec844-765">PCase</span></span>
<span data-ttu-id="ec844-766">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-766">**Description:**</span></span>  
<span data-ttu-id="ec844-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span><span class="sxs-lookup"><span data-stu-id="ec844-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="ec844-768">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="ec844-769">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-769">**Remarks:**</span></span>

* <span data-ttu-id="ec844-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span><span class="sxs-lookup"><span data-stu-id="ec844-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="ec844-771">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="ec844-772">Returns "Test".</span><span class="sxs-lookup"><span data-stu-id="ec844-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="ec844-773">Returns "Test"</span><span class="sxs-lookup"><span data-stu-id="ec844-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="ec844-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="ec844-774">RandomNum</span></span>
<span data-ttu-id="ec844-775">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-775">**Description:**</span></span>  
<span data-ttu-id="ec844-776">The RandomNum function returns a random number between a specified interval.</span><span class="sxs-lookup"><span data-stu-id="ec844-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="ec844-777">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="ec844-778">start: a number identifying the lower limit of the random value to generate</span><span class="sxs-lookup"><span data-stu-id="ec844-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="ec844-779">end: a number identifying the upper limit of the random value to generate</span><span class="sxs-lookup"><span data-stu-id="ec844-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="ec844-780">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="ec844-781">Can return 734.</span><span class="sxs-lookup"><span data-stu-id="ec844-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="ec844-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="ec844-782">RemoveDuplicates</span></span>
<span data-ttu-id="ec844-783">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-783">**Description:**</span></span>  
<span data-ttu-id="ec844-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span><span class="sxs-lookup"><span data-stu-id="ec844-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="ec844-785">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="ec844-786">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="ec844-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span><span class="sxs-lookup"><span data-stu-id="ec844-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="ec844-788">Replace</span><span class="sxs-lookup"><span data-stu-id="ec844-788">Replace</span></span>
<span data-ttu-id="ec844-789">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-789">**Description:**</span></span>  
<span data-ttu-id="ec844-790">The Replace function replaces all occurrences of a string to another string.</span><span class="sxs-lookup"><span data-stu-id="ec844-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="ec844-791">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="ec844-792">string: A string to replace values in.</span><span class="sxs-lookup"><span data-stu-id="ec844-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="ec844-793">OldValue: The string to search for and to replace.</span><span class="sxs-lookup"><span data-stu-id="ec844-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="ec844-794">NewValue: The string to replace to.</span><span class="sxs-lookup"><span data-stu-id="ec844-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="ec844-795">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-795">**Remarks:**</span></span>  
<span data-ttu-id="ec844-796">The function recognizes the following special monikers:</span><span class="sxs-lookup"><span data-stu-id="ec844-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="ec844-797">\n – New Line</span><span class="sxs-lookup"><span data-stu-id="ec844-797">\n – New Line</span></span>
* <span data-ttu-id="ec844-798">\r – Carriage Return</span><span class="sxs-lookup"><span data-stu-id="ec844-798">\r – Carriage Return</span></span>
* <span data-ttu-id="ec844-799">\t – Tab</span><span class="sxs-lookup"><span data-stu-id="ec844-799">\t – Tab</span></span>

<span data-ttu-id="ec844-800">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="ec844-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="ec844-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="ec844-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="ec844-802">ReplaceChars</span></span>
<span data-ttu-id="ec844-803">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-803">**Description:**</span></span>  
<span data-ttu-id="ec844-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span><span class="sxs-lookup"><span data-stu-id="ec844-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="ec844-805">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="ec844-806">string: A string to replace characters in.</span><span class="sxs-lookup"><span data-stu-id="ec844-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="ec844-807">ReplacePattern: a string containing a dictionary with characters to replace.</span><span class="sxs-lookup"><span data-stu-id="ec844-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="ec844-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span><span class="sxs-lookup"><span data-stu-id="ec844-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="ec844-809">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-809">**Remarks:**</span></span>

* <span data-ttu-id="ec844-810">The function takes each occurrence of defined sources and replaces them with the targets.</span><span class="sxs-lookup"><span data-stu-id="ec844-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="ec844-811">The source must be exactly one (unicode) character.</span><span class="sxs-lookup"><span data-stu-id="ec844-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="ec844-812">The source cannot be empty or longer than one character (parsing error).</span><span class="sxs-lookup"><span data-stu-id="ec844-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="ec844-813">The target can have multiple characters, for example ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="ec844-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="ec844-814">The target can be empty indicating that the character should be removed.</span><span class="sxs-lookup"><span data-stu-id="ec844-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="ec844-815">The source is case-sensitive and must be an exact match.</span><span class="sxs-lookup"><span data-stu-id="ec844-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="ec844-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span><span class="sxs-lookup"><span data-stu-id="ec844-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="ec844-817">Spaces and other white characters in the ReplacePattern string are ignored.</span><span class="sxs-lookup"><span data-stu-id="ec844-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="ec844-818">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="ec844-819">Returns Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="ec844-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="ec844-820">Returns "ONeil", the single tick is defined to be removed.</span><span class="sxs-lookup"><span data-stu-id="ec844-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="ec844-821">Right</span><span class="sxs-lookup"><span data-stu-id="ec844-821">Right</span></span>
<span data-ttu-id="ec844-822">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-822">**Description:**</span></span>  
<span data-ttu-id="ec844-823">The Right function returns a specified number of characters from the right (end) of a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="ec844-824">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="ec844-825">string: the string to return characters from</span><span class="sxs-lookup"><span data-stu-id="ec844-825">string: the string to return characters from</span></span>
* <span data-ttu-id="ec844-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span><span class="sxs-lookup"><span data-stu-id="ec844-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="ec844-827">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-827">**Remarks:**</span></span>  
<span data-ttu-id="ec844-828">NumChars characters are returned from the last position of string.</span><span class="sxs-lookup"><span data-stu-id="ec844-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="ec844-829">A string containing the last numChars characters in string:</span><span class="sxs-lookup"><span data-stu-id="ec844-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="ec844-830">If numChars = 0, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="ec844-831">If numChars < 0, return input string.</span><span class="sxs-lookup"><span data-stu-id="ec844-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="ec844-832">If string is null, return empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-832">If string is null, return empty string.</span></span>

<span data-ttu-id="ec844-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="ec844-834">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="ec844-835">Returns "Doe".</span><span class="sxs-lookup"><span data-stu-id="ec844-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="ec844-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="ec844-836">RTrim</span></span>
<span data-ttu-id="ec844-837">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-837">**Description:**</span></span>  
<span data-ttu-id="ec844-838">The RTrim function removes trailing white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="ec844-839">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="ec844-840">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="ec844-841">Returns " Test".</span><span class="sxs-lookup"><span data-stu-id="ec844-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="ec844-842">Select</span><span class="sxs-lookup"><span data-stu-id="ec844-842">Select</span></span>
<span data-ttu-id="ec844-843">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-843">**Description:**</span></span>  
<span data-ttu-id="ec844-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span><span class="sxs-lookup"><span data-stu-id="ec844-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="ec844-845">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="ec844-846">item: Represents an element in the multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="ec844-847">attribute: the multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="ec844-848">expression: an expression that returns a collection of values</span><span class="sxs-lookup"><span data-stu-id="ec844-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="ec844-849">condition: any function that can process an item in the attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="ec844-850">**Examples:**</span><span class="sxs-lookup"><span data-stu-id="ec844-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,"-",""))`  
<span data-ttu-id="ec844-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span><span class="sxs-lookup"><span data-stu-id="ec844-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="ec844-852">Split</span><span class="sxs-lookup"><span data-stu-id="ec844-852">Split</span></span>
<span data-ttu-id="ec844-853">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-853">**Description:**</span></span>  
<span data-ttu-id="ec844-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span><span class="sxs-lookup"><span data-stu-id="ec844-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="ec844-855">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="ec844-856">value: the string with a delimiter character to separate.</span><span class="sxs-lookup"><span data-stu-id="ec844-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="ec844-857">delimiter: single character to be used as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="ec844-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="ec844-858">limit: maximum number of values that can return.</span><span class="sxs-lookup"><span data-stu-id="ec844-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="ec844-859">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="ec844-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="ec844-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="ec844-861">StringFromGuid</span></span>
<span data-ttu-id="ec844-862">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-862">**Description:**</span></span>  
<span data-ttu-id="ec844-863">The StringFromGuid function takes a binary GUID and converts it to a string</span><span class="sxs-lookup"><span data-stu-id="ec844-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="ec844-864">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="ec844-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="ec844-865">StringFromSid</span></span>
<span data-ttu-id="ec844-866">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-866">**Description:**</span></span>  
<span data-ttu-id="ec844-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="ec844-868">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="ec844-869">Switch</span><span class="sxs-lookup"><span data-stu-id="ec844-869">Switch</span></span>
<span data-ttu-id="ec844-870">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-870">**Description:**</span></span>  
<span data-ttu-id="ec844-871">The Switch function is used to return a single value based on evaluated conditions.</span><span class="sxs-lookup"><span data-stu-id="ec844-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="ec844-872">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="ec844-873">expr: Variant expression you want to evaluate.</span><span class="sxs-lookup"><span data-stu-id="ec844-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="ec844-874">value: Value to be returned if the corresponding expression is True.</span><span class="sxs-lookup"><span data-stu-id="ec844-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="ec844-875">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-875">**Remarks:**</span></span>  
<span data-ttu-id="ec844-876">The Switch function argument list consists of pairs of expressions and values.</span><span class="sxs-lookup"><span data-stu-id="ec844-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="ec844-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="ec844-878">If the parts aren't properly paired, a run-time error occurs.</span><span class="sxs-lookup"><span data-stu-id="ec844-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="ec844-879">For example, if expr1 is True, Switch returns value1.</span><span class="sxs-lookup"><span data-stu-id="ec844-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="ec844-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span><span class="sxs-lookup"><span data-stu-id="ec844-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="ec844-881">Switch returns a Nothing if:</span><span class="sxs-lookup"><span data-stu-id="ec844-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="ec844-882">None of the expressions are True.</span><span class="sxs-lookup"><span data-stu-id="ec844-882">None of the expressions are True.</span></span>
* <span data-ttu-id="ec844-883">The first True expression has a corresponding value that is Null.</span><span class="sxs-lookup"><span data-stu-id="ec844-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="ec844-884">Switch evaluates all expressions, even though it returns only one of them.</span><span class="sxs-lookup"><span data-stu-id="ec844-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="ec844-885">For this reason, you should watch for undesirable side effects.</span><span class="sxs-lookup"><span data-stu-id="ec844-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="ec844-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span><span class="sxs-lookup"><span data-stu-id="ec844-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="ec844-887">Value can also be the Error function, which would return a custom string.</span><span class="sxs-lookup"><span data-stu-id="ec844-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="ec844-888">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="ec844-889">Returns the language spoken in some major cities, otherwise returns an Error.</span><span class="sxs-lookup"><span data-stu-id="ec844-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="ec844-890">Trim</span><span class="sxs-lookup"><span data-stu-id="ec844-890">Trim</span></span>
<span data-ttu-id="ec844-891">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-891">**Description:**</span></span>  
<span data-ttu-id="ec844-892">The Trim function removes leading and trailing white spaces from a string.</span><span class="sxs-lookup"><span data-stu-id="ec844-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="ec844-893">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="ec844-894">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="ec844-895">Returns "Test".</span><span class="sxs-lookup"><span data-stu-id="ec844-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="ec844-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="ec844-897">UCase</span><span class="sxs-lookup"><span data-stu-id="ec844-897">UCase</span></span>
<span data-ttu-id="ec844-898">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-898">**Description:**</span></span>  
<span data-ttu-id="ec844-899">The UCase function converts all characters in a string to upper case.</span><span class="sxs-lookup"><span data-stu-id="ec844-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="ec844-900">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="ec844-901">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="ec844-902">Returns "TEST".</span><span class="sxs-lookup"><span data-stu-id="ec844-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="ec844-903">Where</span><span class="sxs-lookup"><span data-stu-id="ec844-903">Where</span></span>

<span data-ttu-id="ec844-904">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-904">**Description:**</span></span>  
<span data-ttu-id="ec844-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span><span class="sxs-lookup"><span data-stu-id="ec844-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="ec844-906">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="ec844-907">item: Represents an element in the multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="ec844-908">attribute: the multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="ec844-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="ec844-909">condition: any expression that can be evaluated to true or false</span><span class="sxs-lookup"><span data-stu-id="ec844-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="ec844-910">expression: an expression that returns a collection of values</span><span class="sxs-lookup"><span data-stu-id="ec844-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="ec844-911">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="ec844-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span><span class="sxs-lookup"><span data-stu-id="ec844-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="ec844-913">With</span><span class="sxs-lookup"><span data-stu-id="ec844-913">With</span></span>
<span data-ttu-id="ec844-914">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-914">**Description:**</span></span>  
<span data-ttu-id="ec844-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span><span class="sxs-lookup"><span data-stu-id="ec844-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="ec844-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="ec844-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="ec844-917">variable: Represents the subexpression.</span><span class="sxs-lookup"><span data-stu-id="ec844-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="ec844-918">subExpression: subexpression represented by variable.</span><span class="sxs-lookup"><span data-stu-id="ec844-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="ec844-919">complexExpression: A complex expression.</span><span class="sxs-lookup"><span data-stu-id="ec844-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="ec844-920">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="ec844-921">Is functionally equivalent to:</span><span class="sxs-lookup"><span data-stu-id="ec844-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="ec844-922">Which returns only unexpired certificate values in the userCertificate attribute.</span><span class="sxs-lookup"><span data-stu-id="ec844-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="ec844-923">Word</span><span class="sxs-lookup"><span data-stu-id="ec844-923">Word</span></span>
<span data-ttu-id="ec844-924">**Description:**</span><span class="sxs-lookup"><span data-stu-id="ec844-924">**Description:**</span></span>  
<span data-ttu-id="ec844-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span><span class="sxs-lookup"><span data-stu-id="ec844-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="ec844-926">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="ec844-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="ec844-927">string: the string to return a word from.</span><span class="sxs-lookup"><span data-stu-id="ec844-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="ec844-928">WordNumber: a number identifying which word number should return.</span><span class="sxs-lookup"><span data-stu-id="ec844-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="ec844-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span><span class="sxs-lookup"><span data-stu-id="ec844-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="ec844-930">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="ec844-930">**Remarks:**</span></span>  
<span data-ttu-id="ec844-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span><span class="sxs-lookup"><span data-stu-id="ec844-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="ec844-932">If number < 1, returns empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="ec844-933">If string is null, returns empty string.</span><span class="sxs-lookup"><span data-stu-id="ec844-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="ec844-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span><span class="sxs-lookup"><span data-stu-id="ec844-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="ec844-935">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ec844-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="ec844-936">Returns "brown"</span><span class="sxs-lookup"><span data-stu-id="ec844-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="ec844-937">Would return "has"</span><span class="sxs-lookup"><span data-stu-id="ec844-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec844-938">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ec844-938">Additional Resources</span></span>
* [<span data-ttu-id="ec844-939">Understanding Declarative Provisioning Expressions</span><span class="sxs-lookup"><span data-stu-id="ec844-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="ec844-940">Azure AD Connect Sync: Customizing Synchronization options</span><span class="sxs-lookup"><span data-stu-id="ec844-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="ec844-941">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec844-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
