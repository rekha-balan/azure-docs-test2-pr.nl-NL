---
title: Localization - Azure Active Directory B2C | Microsoft Docs
description: Specify the Localization element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e9442302b8d15a3a6a4c9fe148b48845b3535204
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870334"
---
# <a name="localization"></a><span data-ttu-id="d968f-103">Localization</span><span class="sxs-lookup"><span data-stu-id="d968f-103">Localization</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="d968f-104">The **Localization** element allows you to support multiple locales or languages in the policy for the user journeys.</span><span class="sxs-lookup"><span data-stu-id="d968f-104">The **Localization** element allows you to support multiple locales or languages in the policy for the user journeys.</span></span> <span data-ttu-id="d968f-105">The localization support in policies allows you to:</span><span class="sxs-lookup"><span data-stu-id="d968f-105">The localization support in policies allows you to:</span></span>

- <span data-ttu-id="d968f-106">Set up the explicit list of the supported languages in a policy and pick a default language.</span><span class="sxs-lookup"><span data-stu-id="d968f-106">Set up the explicit list of the supported languages in a policy and pick a default language.</span></span>
- <span data-ttu-id="d968f-107">Provide language-specific strings and collections.</span><span class="sxs-lookup"><span data-stu-id="d968f-107">Provide language-specific strings and collections.</span></span>

```XML
<Localization Enabled="true">
  <SupportedLanguages DefaultLanguage="en" MergeBehavior="ReplaceAll">
    <SupportedLanguage>en</SupportedLanguage>
    <SupportedLanguage>es</SupportedLanguage>
  </SupportedLanguages>
  <LocalizedResources Id="api.localaccountsignup.en">
  <LocalizedResources Id="api.localaccountsignup.es">
  ...
```

<span data-ttu-id="d968f-108">The **Localization** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-108">The **Localization** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-109">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-109">Attribute</span></span> | <span data-ttu-id="d968f-110">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-110">Required</span></span> | <span data-ttu-id="d968f-111">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-111">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-112">Enabled</span><span class="sxs-lookup"><span data-stu-id="d968f-112">Enabled</span></span> | <span data-ttu-id="d968f-113">No</span><span class="sxs-lookup"><span data-stu-id="d968f-113">No</span></span> | <span data-ttu-id="d968f-114">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="d968f-114">Possible values: `true` or `false`.</span></span> |

<span data-ttu-id="d968f-115">The **Localization** element contains following XML elements</span><span class="sxs-lookup"><span data-stu-id="d968f-115">The **Localization** element contains following XML elements</span></span>

| <span data-ttu-id="d968f-116">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-116">Element</span></span> | <span data-ttu-id="d968f-117">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-117">Occurrences</span></span> | <span data-ttu-id="d968f-118">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-118">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-119">SupportedLanguages</span><span class="sxs-lookup"><span data-stu-id="d968f-119">SupportedLanguages</span></span> | <span data-ttu-id="d968f-120">1:n</span><span class="sxs-lookup"><span data-stu-id="d968f-120">1:n</span></span> | <span data-ttu-id="d968f-121">List of supported languages.</span><span class="sxs-lookup"><span data-stu-id="d968f-121">List of supported languages.</span></span> | 
| <span data-ttu-id="d968f-122">LocalizedResources</span><span class="sxs-lookup"><span data-stu-id="d968f-122">LocalizedResources</span></span> | <span data-ttu-id="d968f-123">0:n</span><span class="sxs-lookup"><span data-stu-id="d968f-123">0:n</span></span> | <span data-ttu-id="d968f-124">List of localized resources.</span><span class="sxs-lookup"><span data-stu-id="d968f-124">List of localized resources.</span></span> |

## <a name="supportedlanguages"></a><span data-ttu-id="d968f-125">SupportedLanguages</span><span class="sxs-lookup"><span data-stu-id="d968f-125">SupportedLanguages</span></span>

<span data-ttu-id="d968f-126">The **SupportedLanguages** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-126">The **SupportedLanguages** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-127">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-127">Attribute</span></span> | <span data-ttu-id="d968f-128">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-128">Required</span></span> | <span data-ttu-id="d968f-129">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-129">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-130">DefaultLanguage</span><span class="sxs-lookup"><span data-stu-id="d968f-130">DefaultLanguage</span></span> | <span data-ttu-id="d968f-131">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-131">Yes</span></span> | <span data-ttu-id="d968f-132">The language to be used as the default for localized resources.</span><span class="sxs-lookup"><span data-stu-id="d968f-132">The language to be used as the default for localized resources.</span></span> |
| <span data-ttu-id="d968f-133">MergeBehavior</span><span class="sxs-lookup"><span data-stu-id="d968f-133">MergeBehavior</span></span> | <span data-ttu-id="d968f-134">No</span><span class="sxs-lookup"><span data-stu-id="d968f-134">No</span></span> | <span data-ttu-id="d968f-135">An enumeration values of values that are merged together with any ClaimType present in a parent policy with the same identifier.</span><span class="sxs-lookup"><span data-stu-id="d968f-135">An enumeration values of values that are merged together with any ClaimType present in a parent policy with the same identifier.</span></span> <span data-ttu-id="d968f-136">Use this attribute when you overwrite a claim specified in base policy.</span><span class="sxs-lookup"><span data-stu-id="d968f-136">Use this attribute when you overwrite a claim specified in base policy.</span></span> <span data-ttu-id="d968f-137">Possible values: `Append`, `Prepend`, or `ReplaceAll`.</span><span class="sxs-lookup"><span data-stu-id="d968f-137">Possible values: `Append`, `Prepend`, or `ReplaceAll`.</span></span> <span data-ttu-id="d968f-138">The `Append` value specifies that the collection of data present should be appended to the end of the collection specified in the parent policy.</span><span class="sxs-lookup"><span data-stu-id="d968f-138">The `Append` value specifies that the collection of data present should be appended to the end of the collection specified in the parent policy.</span></span> <span data-ttu-id="d968f-139">The `Prepend` value specifies that the collection of data present should be added before the collection specified in the parent policy.</span><span class="sxs-lookup"><span data-stu-id="d968f-139">The `Prepend` value specifies that the collection of data present should be added before the collection specified in the parent policy.</span></span> <span data-ttu-id="d968f-140">The `ReplaceAll` value specifies that the collection of data defined in the parent policy should be ignored, using instead the data defined in the current policy.</span><span class="sxs-lookup"><span data-stu-id="d968f-140">The `ReplaceAll` value specifies that the collection of data defined in the parent policy should be ignored, using instead the data defined in the current policy.</span></span> |

### <a name="supportedlanguages"></a><span data-ttu-id="d968f-141">SupportedLanguages</span><span class="sxs-lookup"><span data-stu-id="d968f-141">SupportedLanguages</span></span>

<span data-ttu-id="d968f-142">The **SupportedLanguages** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="d968f-142">The **SupportedLanguages** element contains the following elements:</span></span>

| <span data-ttu-id="d968f-143">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-143">Element</span></span> | <span data-ttu-id="d968f-144">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-144">Occurrences</span></span> | <span data-ttu-id="d968f-145">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-145">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-146">SupportedLanguage</span><span class="sxs-lookup"><span data-stu-id="d968f-146">SupportedLanguage</span></span> | <span data-ttu-id="d968f-147">1:n</span><span class="sxs-lookup"><span data-stu-id="d968f-147">1:n</span></span> | <span data-ttu-id="d968f-148">Displays content that conforms to a language tag per RFC 5646 - Tags for Identifying Languages.</span><span class="sxs-lookup"><span data-stu-id="d968f-148">Displays content that conforms to a language tag per RFC 5646 - Tags for Identifying Languages.</span></span> | 

## <a name="localizedresources"></a><span data-ttu-id="d968f-149">LocalizedResources</span><span class="sxs-lookup"><span data-stu-id="d968f-149">LocalizedResources</span></span>

<span data-ttu-id="d968f-150">The **LocalizedResources** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-150">The **LocalizedResources** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-151">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-151">Attribute</span></span> | <span data-ttu-id="d968f-152">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-152">Required</span></span> | <span data-ttu-id="d968f-153">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-153">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-154">Id</span><span class="sxs-lookup"><span data-stu-id="d968f-154">Id</span></span> | <span data-ttu-id="d968f-155">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-155">Yes</span></span> | <span data-ttu-id="d968f-156">An identifier that is used to uniquely identify localized resources.</span><span class="sxs-lookup"><span data-stu-id="d968f-156">An identifier that is used to uniquely identify localized resources.</span></span> |

<span data-ttu-id="d968f-157">The **LocalizedResources** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="d968f-157">The **LocalizedResources** element contains the following elements:</span></span>

| <span data-ttu-id="d968f-158">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-158">Element</span></span> | <span data-ttu-id="d968f-159">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-159">Occurrences</span></span> | <span data-ttu-id="d968f-160">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-160">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-161">LocalizedCollections</span><span class="sxs-lookup"><span data-stu-id="d968f-161">LocalizedCollections</span></span> | <span data-ttu-id="d968f-162">0:n</span><span class="sxs-lookup"><span data-stu-id="d968f-162">0:n</span></span> | <span data-ttu-id="d968f-163">Defines entire collections in various cultures.</span><span class="sxs-lookup"><span data-stu-id="d968f-163">Defines entire collections in various cultures.</span></span> <span data-ttu-id="d968f-164">A collection can have different number of items and different strings for various cultures.</span><span class="sxs-lookup"><span data-stu-id="d968f-164">A collection can have different number of items and different strings for various cultures.</span></span> <span data-ttu-id="d968f-165">Examples of collections include the enumerations that appear in claim types.</span><span class="sxs-lookup"><span data-stu-id="d968f-165">Examples of collections include the enumerations that appear in claim types.</span></span> <span data-ttu-id="d968f-166">For example, a country/region list is shown to the user in a drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d968f-166">For example, a country/region list is shown to the user in a drop-down list.</span></span> |
| <span data-ttu-id="d968f-167">LocalizedStrings</span><span class="sxs-lookup"><span data-stu-id="d968f-167">LocalizedStrings</span></span> | <span data-ttu-id="d968f-168">0:n</span><span class="sxs-lookup"><span data-stu-id="d968f-168">0:n</span></span> | <span data-ttu-id="d968f-169">Defines all of the strings, except those strings that appear in collections, in various cultures.</span><span class="sxs-lookup"><span data-stu-id="d968f-169">Defines all of the strings, except those strings that appear in collections, in various cultures.</span></span> |

### <a name="localizedcollections"></a><span data-ttu-id="d968f-170">LocalizedCollections</span><span class="sxs-lookup"><span data-stu-id="d968f-170">LocalizedCollections</span></span>

<span data-ttu-id="d968f-171">The **LocalizedCollections** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="d968f-171">The **LocalizedCollections** element contains the following elements:</span></span>

| <span data-ttu-id="d968f-172">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-172">Element</span></span> | <span data-ttu-id="d968f-173">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-173">Occurrences</span></span> | <span data-ttu-id="d968f-174">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-174">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-175">LocalizedCollection</span><span class="sxs-lookup"><span data-stu-id="d968f-175">LocalizedCollection</span></span> | <span data-ttu-id="d968f-176">1:n</span><span class="sxs-lookup"><span data-stu-id="d968f-176">1:n</span></span> | <span data-ttu-id="d968f-177">List of supported languages.</span><span class="sxs-lookup"><span data-stu-id="d968f-177">List of supported languages.</span></span> |

#### <a name="localizedcollection"></a><span data-ttu-id="d968f-178">LocalizedCollection</span><span class="sxs-lookup"><span data-stu-id="d968f-178">LocalizedCollection</span></span>

<span data-ttu-id="d968f-179">The **LocalizedCollection** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-179">The **LocalizedCollection** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-180">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-180">Attribute</span></span> | <span data-ttu-id="d968f-181">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-181">Required</span></span> | <span data-ttu-id="d968f-182">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-182">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-183">ElementType</span><span class="sxs-lookup"><span data-stu-id="d968f-183">ElementType</span></span> | <span data-ttu-id="d968f-184">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-184">Yes</span></span> | <span data-ttu-id="d968f-185">References a ClaimType element or a user interface element in the policy file.</span><span class="sxs-lookup"><span data-stu-id="d968f-185">References a ClaimType element or a user interface element in the policy file.</span></span> |
| <span data-ttu-id="d968f-186">ElementId</span><span class="sxs-lookup"><span data-stu-id="d968f-186">ElementId</span></span> | <span data-ttu-id="d968f-187">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-187">Yes</span></span> | <span data-ttu-id="d968f-188">A string that contains a reference to a claim type already defined in the ClaimsSchema section that is used if **ElementType** is set to a ClaimType.</span><span class="sxs-lookup"><span data-stu-id="d968f-188">A string that contains a reference to a claim type already defined in the ClaimsSchema section that is used if **ElementType** is set to a ClaimType.</span></span> |
| <span data-ttu-id="d968f-189">TargetCollection</span><span class="sxs-lookup"><span data-stu-id="d968f-189">TargetCollection</span></span> | <span data-ttu-id="d968f-190">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-190">Yes</span></span> | <span data-ttu-id="d968f-191">The target collection.</span><span class="sxs-lookup"><span data-stu-id="d968f-191">The target collection.</span></span> |

<span data-ttu-id="d968f-192">The **LocalizedCollection** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="d968f-192">The **LocalizedCollection** element contains the following elements:</span></span>

| <span data-ttu-id="d968f-193">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-193">Element</span></span> | <span data-ttu-id="d968f-194">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-194">Occurrences</span></span> | <span data-ttu-id="d968f-195">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-195">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-196">Item</span><span class="sxs-lookup"><span data-stu-id="d968f-196">Item</span></span> | <span data-ttu-id="d968f-197">0:n</span><span class="sxs-lookup"><span data-stu-id="d968f-197">0:n</span></span> | <span data-ttu-id="d968f-198">Defines an available option for the user to select for a claim in the user interface, such as a value in a dropdown.</span><span class="sxs-lookup"><span data-stu-id="d968f-198">Defines an available option for the user to select for a claim in the user interface, such as a value in a dropdown.</span></span> |

<span data-ttu-id="d968f-199">The **Item** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-199">The **Item** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-200">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-200">Attribute</span></span> | <span data-ttu-id="d968f-201">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-201">Required</span></span> | <span data-ttu-id="d968f-202">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-202">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-203">Text</span><span class="sxs-lookup"><span data-stu-id="d968f-203">Text</span></span> | <span data-ttu-id="d968f-204">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-204">Yes</span></span> | <span data-ttu-id="d968f-205">The user-friendly display string that should be shown to the user in the user interface for this option.</span><span class="sxs-lookup"><span data-stu-id="d968f-205">The user-friendly display string that should be shown to the user in the user interface for this option.</span></span> |
| <span data-ttu-id="d968f-206">Value</span><span class="sxs-lookup"><span data-stu-id="d968f-206">Value</span></span> | <span data-ttu-id="d968f-207">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-207">Yes</span></span> | <span data-ttu-id="d968f-208">The string claim value associated with selecting this option.</span><span class="sxs-lookup"><span data-stu-id="d968f-208">The string claim value associated with selecting this option.</span></span> |

<span data-ttu-id="d968f-209">The following example shows the use of the **LocalizedCollections** element.</span><span class="sxs-lookup"><span data-stu-id="d968f-209">The following example shows the use of the **LocalizedCollections** element.</span></span> <span data-ttu-id="d968f-210">It contains two **LocalizedCollection** elements, one for English and another one for Spanish.</span><span class="sxs-lookup"><span data-stu-id="d968f-210">It contains two **LocalizedCollection** elements, one for English and another one for Spanish.</span></span> <span data-ttu-id="d968f-211">Both set the **Restriction** collection of the claim `Gender` with a list of items for English and Spanish.</span><span class="sxs-lookup"><span data-stu-id="d968f-211">Both set the **Restriction** collection of the claim `Gender` with a list of items for English and Spanish.</span></span>

```XML
<LocalizedResources Id="api.selfasserted.en">
 <LocalizedCollections>
   <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
      <Item Text="Female" Value="F" />
      <Item Text="Male" Value="M" />
    </LocalizedCollection>
</LocalizedCollections>

<LocalizedResources Id="api.selfasserted.es">
 <LocalizedCollections>
   <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
      <Item Text="Femenino" Value="F" />
      <Item Text="Masculino" Value="M" />
    </LocalizedCollection>
</LocalizedCollections>

```

### <a name="localizedstrings"></a><span data-ttu-id="d968f-212">LocalizedStrings</span><span class="sxs-lookup"><span data-stu-id="d968f-212">LocalizedStrings</span></span>

<span data-ttu-id="d968f-213">The **LocalizedStrings** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="d968f-213">The **LocalizedStrings** element contains the following elements:</span></span>

| <span data-ttu-id="d968f-214">Element</span><span class="sxs-lookup"><span data-stu-id="d968f-214">Element</span></span> | <span data-ttu-id="d968f-215">Occurrences</span><span class="sxs-lookup"><span data-stu-id="d968f-215">Occurrences</span></span> | <span data-ttu-id="d968f-216">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-216">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="d968f-217">LocalizedString</span><span class="sxs-lookup"><span data-stu-id="d968f-217">LocalizedString</span></span> | <span data-ttu-id="d968f-218">1:n</span><span class="sxs-lookup"><span data-stu-id="d968f-218">1:n</span></span> | <span data-ttu-id="d968f-219">A localized string.</span><span class="sxs-lookup"><span data-stu-id="d968f-219">A localized string.</span></span> |

<span data-ttu-id="d968f-220">The **LocalizedString** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d968f-220">The **LocalizedString** element contains the following attributes:</span></span>

| <span data-ttu-id="d968f-221">Attribute</span><span class="sxs-lookup"><span data-stu-id="d968f-221">Attribute</span></span> | <span data-ttu-id="d968f-222">Required</span><span class="sxs-lookup"><span data-stu-id="d968f-222">Required</span></span> | <span data-ttu-id="d968f-223">Description</span><span class="sxs-lookup"><span data-stu-id="d968f-223">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="d968f-224">ElementType</span><span class="sxs-lookup"><span data-stu-id="d968f-224">ElementType</span></span> | <span data-ttu-id="d968f-225">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-225">Yes</span></span> | <span data-ttu-id="d968f-226">A reference to a claim type element or a user interface element in the policy.</span><span class="sxs-lookup"><span data-stu-id="d968f-226">A reference to a claim type element or a user interface element in the policy.</span></span> <span data-ttu-id="d968f-227">Possible values: `ClaimType`, `UxElement`, `ErrorMessage`, `Predicate`, or  .</span><span class="sxs-lookup"><span data-stu-id="d968f-227">Possible values: `ClaimType`, `UxElement`, `ErrorMessage`, `Predicate`, or  .</span></span> <span data-ttu-id="d968f-228">The `ClaimType` value is used to localize one of the claim attributes, as specified in the StringId.</span><span class="sxs-lookup"><span data-stu-id="d968f-228">The `ClaimType` value is used to localize one of the claim attributes, as specified in the StringId.</span></span> <span data-ttu-id="d968f-229">The `UxElement` value is used to localize one of the user interface elements as specified in the StringId.</span><span class="sxs-lookup"><span data-stu-id="d968f-229">The `UxElement` value is used to localize one of the user interface elements as specified in the StringId.</span></span> <span data-ttu-id="d968f-230">The `ErrorMessage` value is used to localize one of the system error messages as specified in the StringId.</span><span class="sxs-lookup"><span data-stu-id="d968f-230">The `ErrorMessage` value is used to localize one of the system error messages as specified in the StringId.</span></span> <span data-ttu-id="d968f-231">The `Predicate` value is used to localize one of the [Predicate](predicates.md) error messages, as specified in the StringId.</span><span class="sxs-lookup"><span data-stu-id="d968f-231">The `Predicate` value is used to localize one of the [Predicate](predicates.md) error messages, as specified in the StringId.</span></span> <span data-ttu-id="d968f-232">The `InputValidation` value is used to localize one of the [PredicateValidation](predicates.md) group error messages as specified in the StringId.</span><span class="sxs-lookup"><span data-stu-id="d968f-232">The `InputValidation` value is used to localize one of the [PredicateValidation](predicates.md) group error messages as specified in the StringId.</span></span> |
| <span data-ttu-id="d968f-233">ElementId</span><span class="sxs-lookup"><span data-stu-id="d968f-233">ElementId</span></span> | <span data-ttu-id="d968f-234">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-234">Yes</span></span> | <span data-ttu-id="d968f-235">If **ElementType** is set to `ClaimType`, `Predicate`, or `InputValidation`, this element contains a reference to a claim type already defined in the ClaimsSchema section.</span><span class="sxs-lookup"><span data-stu-id="d968f-235">If **ElementType** is set to `ClaimType`, `Predicate`, or `InputValidation`, this element contains a reference to a claim type already defined in the ClaimsSchema section.</span></span> | 
| <span data-ttu-id="d968f-236">StringId</span><span class="sxs-lookup"><span data-stu-id="d968f-236">StringId</span></span> | <span data-ttu-id="d968f-237">Yes</span><span class="sxs-lookup"><span data-stu-id="d968f-237">Yes</span></span> | <span data-ttu-id="d968f-238">If **ElementType** is set to `ClaimType`, this element contains a reference to an attribute of a claim type.</span><span class="sxs-lookup"><span data-stu-id="d968f-238">If **ElementType** is set to `ClaimType`, this element contains a reference to an attribute of a claim type.</span></span> <span data-ttu-id="d968f-239">Possible values: `DisplayName`, `AdminHelpText`, or `PatternHelpText`.</span><span class="sxs-lookup"><span data-stu-id="d968f-239">Possible values: `DisplayName`, `AdminHelpText`, or `PatternHelpText`.</span></span> <span data-ttu-id="d968f-240">The `DisplayName` value is used to set the claim display name.</span><span class="sxs-lookup"><span data-stu-id="d968f-240">The `DisplayName` value is used to set the claim display name.</span></span> <span data-ttu-id="d968f-241">The `AdminHelpText` value is used to set the help text name of the claim user.</span><span class="sxs-lookup"><span data-stu-id="d968f-241">The `AdminHelpText` value is used to set the help text name of the claim user.</span></span> <span data-ttu-id="d968f-242">The `PatternHelpText` value is used to set the claim pattern help text.</span><span class="sxs-lookup"><span data-stu-id="d968f-242">The `PatternHelpText` value is used to set the claim pattern help text.</span></span> <span data-ttu-id="d968f-243">If **ElementType** is set to `UxElement`, this element contains a reference to an attribute of a user interface element.</span><span class="sxs-lookup"><span data-stu-id="d968f-243">If **ElementType** is set to `UxElement`, this element contains a reference to an attribute of a user interface element.</span></span> <span data-ttu-id="d968f-244">If **ElementType** is set to `ErrorMessage`, this element specifies the identifier of an error message.</span><span class="sxs-lookup"><span data-stu-id="d968f-244">If **ElementType** is set to `ErrorMessage`, this element specifies the identifier of an error message.</span></span> <span data-ttu-id="d968f-245">See [Localization string IDs](localization-string-ids.md) for a complete list of the `UxElement` identifiers.</span><span class="sxs-lookup"><span data-stu-id="d968f-245">See [Localization string IDs](localization-string-ids.md) for a complete list of the `UxElement` identifiers.</span></span>|


<span data-ttu-id="d968f-246">The following example shows a localized sign-up page.</span><span class="sxs-lookup"><span data-stu-id="d968f-246">The following example shows a localized sign-up page.</span></span> <span data-ttu-id="d968f-247">The first three **LocalizedString** values set the claim attribute.</span><span class="sxs-lookup"><span data-stu-id="d968f-247">The first three **LocalizedString** values set the claim attribute.</span></span> <span data-ttu-id="d968f-248">The third changes the value of the continue button.</span><span class="sxs-lookup"><span data-stu-id="d968f-248">The third changes the value of the continue button.</span></span> <span data-ttu-id="d968f-249">The last one changes the error message.</span><span class="sxs-lookup"><span data-stu-id="d968f-249">The last one changes the error message.</span></span>

```XML
<LocalizedResources Id="api.selfasserted.en">
  <LocalizedStrings>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="DisplayName">Email</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="UserHelpText">Please enter your email</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="PatternHelpText">Please enter a valid email address</LocalizedString>
    <LocalizedString ElementType="UxElement" StringId="button_continue">Create new account</LocalizedString>
   <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfClaimsPrincipalAlreadyExists">The account you are trying to create already exists, please sign-in.</LocalizedString>
  </LocalizedStrings>
</LocalizedResources>
```

<span data-ttu-id="d968f-250">The following example shows a localized the **UserHelpText** of **Predicate** with Id `IsLengthBetween8And64`.</span><span class="sxs-lookup"><span data-stu-id="d968f-250">The following example shows a localized the **UserHelpText** of **Predicate** with Id `IsLengthBetween8And64`.</span></span> <span data-ttu-id="d968f-251">And a localized **UserHelpText** of **PredicateGroup** with Id `CharacterClasses` of **PredicateValidation** with Id `StrongPassword`.</span><span class="sxs-lookup"><span data-stu-id="d968f-251">And a localized **UserHelpText** of **PredicateGroup** with Id `CharacterClasses` of **PredicateValidation** with Id `StrongPassword`.</span></span>

```XML
<PredicateValidation Id="StrongPassword">
  <PredicateGroups>
    ...
    <PredicateGroup Id="CharacterClasses">
    ...
    </PredicateGroup>
  </PredicateGroups>
</PredicateValidation>

...

<Predicate Id="IsLengthBetween8And64" Method="IsLengthRange">
  ...
</Predicate>
...


<LocalizedString ElementType="InputValidation" ElementId="StrongPassword" StringId="CharacterClasses">The password must have at least 3 of the following:</LocalizedString>

<LocalizedString ElementType="Predicate" ElementId="IsLengthBetween8And64" StringId="HelpText">The password must be between 8 and 64 characters.</LocalizedString>              
```

## <a name="set-up-localization"></a><span data-ttu-id="d968f-252">Set up localization</span><span class="sxs-lookup"><span data-stu-id="d968f-252">Set up localization</span></span>

<span data-ttu-id="d968f-253">This article shows you how to support multiple locales or languages in the policy for user journeys.</span><span class="sxs-lookup"><span data-stu-id="d968f-253">This article shows you how to support multiple locales or languages in the policy for user journeys.</span></span> <span data-ttu-id="d968f-254">Localization requires three steps: set-up the explicit list of the supported languages, provide language-specific strings and collections, and edit the ContentDefinition for the page.</span><span class="sxs-lookup"><span data-stu-id="d968f-254">Localization requires three steps: set-up the explicit list of the supported languages, provide language-specific strings and collections, and edit the ContentDefinition for the page.</span></span>

### <a name="set-up-the-explicit-list-of-supported-languages"></a><span data-ttu-id="d968f-255">Set up the explicit list of supported languages</span><span class="sxs-lookup"><span data-stu-id="d968f-255">Set up the explicit list of supported languages</span></span>

<span data-ttu-id="d968f-256">Under the **BuildingBlocks** element, add the **Localization** element with the list of supported languages.</span><span class="sxs-lookup"><span data-stu-id="d968f-256">Under the **BuildingBlocks** element, add the **Localization** element with the list of supported languages.</span></span> <span data-ttu-id="d968f-257">The following example shows how to define the localization support for both English (default) and Spanish:</span><span class="sxs-lookup"><span data-stu-id="d968f-257">The following example shows how to define the localization support for both English (default) and Spanish:</span></span>

```XML
<Localization Enabled="true">
  <SupportedLanguages DefaultLanguage="en" MergeBehavior="ReplaceAll">
    <SupportedLanguage>en</SupportedLanguage>
    <SupportedLanguage>es</SupportedLanguage>
  </SupportedLanguages>
</Localization>
```

### <a name="provide-language-specific-strings-and-collections"></a><span data-ttu-id="d968f-258">Provide language-specific strings and collections</span><span class="sxs-lookup"><span data-stu-id="d968f-258">Provide language-specific strings and collections</span></span> 

<span data-ttu-id="d968f-259">Add **LocalizedResources** elements inside the **Localization** element after the close of the **SupportedLanguages** element.</span><span class="sxs-lookup"><span data-stu-id="d968f-259">Add **LocalizedResources** elements inside the **Localization** element after the close of the **SupportedLanguages** element.</span></span> <span data-ttu-id="d968f-260">You add **LocalizedResources** elements for each page (content definition) and any language you want to support.</span><span class="sxs-lookup"><span data-stu-id="d968f-260">You add **LocalizedResources** elements for each page (content definition) and any language you want to support.</span></span> <span data-ttu-id="d968f-261">To customize the unified sign-up or sign-in page, sign-up and multi-factor authentication (MFA) pages for English, Spanish, and France, you add the following **LocalizedResources** elements.</span><span class="sxs-lookup"><span data-stu-id="d968f-261">To customize the unified sign-up or sign-in page, sign-up and multi-factor authentication (MFA) pages for English, Spanish, and France, you add the following **LocalizedResources** elements.</span></span>  
- <span data-ttu-id="d968f-262">Unified sign-up or sign-in page, English `<LocalizedResources Id="api.signuporsignin.en">`</span><span class="sxs-lookup"><span data-stu-id="d968f-262">Unified sign-up or sign-in page, English `<LocalizedResources Id="api.signuporsignin.en">`</span></span>
- <span data-ttu-id="d968f-263">Unified sign-up or sign-in page, Spanish `<LocalizedResources Id="api.signuporsignin.es">`</span><span class="sxs-lookup"><span data-stu-id="d968f-263">Unified sign-up or sign-in page, Spanish `<LocalizedResources Id="api.signuporsignin.es">`</span></span>
- <span data-ttu-id="d968f-264">Unified sign-up or sign-in page, France `<LocalizedResources Id="api.signuporsignin.fr">`</span><span class="sxs-lookup"><span data-stu-id="d968f-264">Unified sign-up or sign-in page, France `<LocalizedResources Id="api.signuporsignin.fr">`</span></span> 
- <span data-ttu-id="d968f-265">Sign-Up, English `<LocalizedResources Id="api.localaccountsignup.en">`</span><span class="sxs-lookup"><span data-stu-id="d968f-265">Sign-Up, English `<LocalizedResources Id="api.localaccountsignup.en">`</span></span>
- <span data-ttu-id="d968f-266">Sign-Up, Spanish `<LocalizedResources Id="api.localaccountsignup.es">`</span><span class="sxs-lookup"><span data-stu-id="d968f-266">Sign-Up, Spanish `<LocalizedResources Id="api.localaccountsignup.es">`</span></span>
- <span data-ttu-id="d968f-267">Sign-Up, France `<LocalizedResources Id="api.localaccountsignup.fr">`</span><span class="sxs-lookup"><span data-stu-id="d968f-267">Sign-Up, France `<LocalizedResources Id="api.localaccountsignup.fr">`</span></span>
- <span data-ttu-id="d968f-268">MFA, English `<LocalizedResources Id="api.phonefactor.en">`</span><span class="sxs-lookup"><span data-stu-id="d968f-268">MFA, English `<LocalizedResources Id="api.phonefactor.en">`</span></span>
- <span data-ttu-id="d968f-269">MFA, Spanish `<LocalizedResources Id="api.phonefactor.es">`</span><span class="sxs-lookup"><span data-stu-id="d968f-269">MFA, Spanish `<LocalizedResources Id="api.phonefactor.es">`</span></span>
- <span data-ttu-id="d968f-270">MFA, France `<LocalizedResources Id="api.phonefactor.fr">`</span><span class="sxs-lookup"><span data-stu-id="d968f-270">MFA, France `<LocalizedResources Id="api.phonefactor.fr">`</span></span>

<span data-ttu-id="d968f-271">Each **LocalizedResources** element contains all of the required  **LocalizedStrings** elements with multiple **LocalizedString** elements and **LocalizedCollections** elements with multiple **LocalizedCollection** elements.</span><span class="sxs-lookup"><span data-stu-id="d968f-271">Each **LocalizedResources** element contains all of the required  **LocalizedStrings** elements with multiple **LocalizedString** elements and **LocalizedCollections** elements with multiple **LocalizedCollection** elements.</span></span>  <span data-ttu-id="d968f-272">The following example adds the sign-up page English localization:</span><span class="sxs-lookup"><span data-stu-id="d968f-272">The following example adds the sign-up page English localization:</span></span> 

<span data-ttu-id="d968f-273">Note: This example makes a reference to `Gender` and `City` claim types.</span><span class="sxs-lookup"><span data-stu-id="d968f-273">Note: This example makes a reference to `Gender` and `City` claim types.</span></span> <span data-ttu-id="d968f-274">To use this example, make sure you define those claims.</span><span class="sxs-lookup"><span data-stu-id="d968f-274">To use this example, make sure you define those claims.</span></span> <span data-ttu-id="d968f-275">For more information, see [ClaimsSchema](claimsschema.md).</span><span class="sxs-lookup"><span data-stu-id="d968f-275">For more information, see [ClaimsSchema](claimsschema.md).</span></span>

```XML
<LocalizedResources Id="api.localaccountsignup.en">

 <LocalizedCollections>
   <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
      <Item Text="Female" Value="F" />
      <Item Text="Male" Value="M" />
    </LocalizedCollection>
   <LocalizedCollection ElementType="ClaimType" ElementId="City" TargetCollection="Restriction">
      <Item Text="New York" Value="NY" />
      <Item Text="Paris" Value="Paris" />
      <Item Text="London" Value="London" />
    </LocalizedCollection>
  </LocalizedCollections>

  <LocalizedStrings>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="DisplayName">Email</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="UserHelpText">Please enter your email</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="PatternHelpText">Please enter a valid email address</LocalizedString>
    <LocalizedString ElementType="UxElement" StringId="button_continue">Create new account</LocalizedString>
   <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfClaimsPrincipalAlreadyExists">The account you are trying to create already exists, please sign-in.</LocalizedString>
  </LocalizedStrings>
</LocalizedResources>
```

<span data-ttu-id="d968f-276">The sign-up page localization for Spanish.</span><span class="sxs-lookup"><span data-stu-id="d968f-276">The sign-up page localization for Spanish.</span></span>

```XML
<LocalizedResources Id="api.localaccountsignup.es">

 <LocalizedCollections>
   <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
      <Item Text="Femenino" Value="F" />
      <Item Text="Masculino" Value="M" />
    </LocalizedCollection>
   <LocalizedCollection ElementType="ClaimType" ElementId="City" TargetCollection="Restriction">
      <Item Text="Nueva York" Value="NY" />
      <Item Text="París" Value="Paris" />
      <Item Text="Londres" Value="London" />
    </LocalizedCollection>
  </LocalizedCollections>

  <LocalizedStrings>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="DisplayName">Dirección de correo electrónico</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="UserHelpText">Dirección de correo electrónico que puede usarse para ponerse en contacto con usted.</LocalizedString>
    <LocalizedString ElementType="ClaimType" ElementId="email" StringId="PatternHelpText">Introduzca una dirección de correo electrónico.</LocalizedString>
    <LocalizedString ElementType="UxElement" StringId="button_continue">Crear</LocalizedString>
   <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfClaimsPrincipalAlreadyExists">Ya existe un usuario con el id. especificado. Elija otro diferente.</LocalizedString>
  </LocalizedStrings>
</LocalizedResources>
```

### <a name="edit-the-contentdefinition-for-the-page"></a><span data-ttu-id="d968f-277">Edit the ContentDefinition for the page</span><span class="sxs-lookup"><span data-stu-id="d968f-277">Edit the ContentDefinition for the page</span></span> 

<span data-ttu-id="d968f-278">For each page that you want to localize, specify the language codes to look for in the **ContentDefinition**.</span><span class="sxs-lookup"><span data-stu-id="d968f-278">For each page that you want to localize, specify the language codes to look for in the **ContentDefinition**.</span></span>

<span data-ttu-id="d968f-279">In the following example, English (en) and Spanish (es) custom strings are added to the sign-up page.</span><span class="sxs-lookup"><span data-stu-id="d968f-279">In the following example, English (en) and Spanish (es) custom strings are added to the sign-up page.</span></span> <span data-ttu-id="d968f-280">The **LocalizedResourcesReferenceId** for each **LocalizedResourcesReference** is the same as their locale, but you could use any string as the identifier.</span><span class="sxs-lookup"><span data-stu-id="d968f-280">The **LocalizedResourcesReferenceId** for each **LocalizedResourcesReference** is the same as their locale, but you could use any string as the identifier.</span></span> <span data-ttu-id="d968f-281">For each language and page combination, you point to the  corresponding **LocalizedResources** you previously created.</span><span class="sxs-lookup"><span data-stu-id="d968f-281">For each language and page combination, you point to the  corresponding **LocalizedResources** you previously created.</span></span>

```XML
<ContentDefinition Id="api.localaccountsignup">
...
  <LocalizedResourcesReferences MergeBehavior="Prepend">
    <LocalizedResourcesReference Language="en" LocalizedResourcesReferenceId="api.localaccountsignup.en" />
    <LocalizedResourcesReference Language="es" LocalizedResourcesReferenceId="api.localaccountsignup.es" />
  </LocalizedResourcesReferences>
</ContentDefinition>
```

<span data-ttu-id="d968f-282">The following example shows the final XML:</span><span class="sxs-lookup"><span data-stu-id="d968f-282">The following example shows the final XML:</span></span>

```XML
<BuildingBlocks>
  <ContentDefinitions>
    <ContentDefinition Id="api.localaccountsignup">
      <!-- Other content definitions elements... -->
      <LocalizedResourcesReferences MergeBehavior="Prepend">
         <LocalizedResourcesReference Language="en" LocalizedResourcesReferenceId="api.localaccountsignup.en" />
         <LocalizedResourcesReference Language="es" LocalizedResourcesReferenceId="api.localaccountsignup.es" />
      </LocalizedResourcesReferences>
    </ContentDefinition>
    <!-- More content definitions... -->
  </ContentDefinitions>

  <Localization Enabled="true">

    <SupportedLanguages DefaultLanguage="en" MergeBehavior="ReplaceAll">
      <SupportedLanguage>en</SupportedLanguage>
      <SupportedLanguage>es</SupportedLanguage>
      <!-- More supported language... -->
    </SupportedLanguages>

    <LocalizedResources Id="api.localaccountsignup.en">
      <LocalizedCollections>
        <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
          <Item Text="Female" Value="F" />
          <Item Text="Male" Value="M" />
          <!-- More items... -->
        </LocalizedCollection>
        <LocalizedCollection ElementType="ClaimType" ElementId="City" TargetCollection="Restriction">
          <Item Text="New York" Value="NY" />
          <Item Text="Paris" Value="Paris" />
          <Item Text="London" Value="London" />
        </LocalizedCollection>
        <!-- More localized collections... -->
      </LocalizedCollections>
      <LocalizedStrings>
        <LocalizedString ElementType="ClaimType" ElementId="email" StringId="DisplayName">Email</LocalizedString>
      <LocalizedString ElementType="ClaimType" ElementId="email" StringId="UserHelpText">Please enter your email</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="email" StringId="PatternHelpText">Please enter a valid email address</LocalizedString>
        <LocalizedString ElementType="UxElement" StringId="button_continue">Create new account</LocalizedString>
       <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfClaimsPrincipalAlreadyExists">The account you are trying to create already exists, please sign-in.</LocalizedString>
        <!-- More localized strings... -->
      </LocalizedStrings>
    </LocalizedResources>

    <LocalizedResources Id="api.localaccountsignup.es">
      <LocalizedCollections>
       <LocalizedCollection ElementType="ClaimType" ElementId="Gender" TargetCollection="Restriction">
          <Item Text="Femenino" Value="F" />
          <Item Text="Masculino" Value="M" />
        </LocalizedCollection>
        <LocalizedCollection ElementType="ClaimType" ElementId="City" TargetCollection="Restriction">
          <Item Text="Nueva York" Value="NY" />
          <Item Text="París" Value="Paris" />
          <Item Text="Londres" Value="London" />
        </LocalizedCollection>
      </LocalizedCollections>
      <LocalizedStrings>
        <LocalizedString ElementType="ClaimType" ElementId="email" StringId="DisplayName">Dirección de correo electrónico</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="email" StringId="UserHelpText">Dirección de correo electrónico que puede usarse para ponerse en contacto con usted.</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="email" StringId="PatternHelpText">Introduzca una dirección de correo electrónico.</LocalizedString>
        <LocalizedString ElementType="UxElement" StringId="button_continue">Crear</LocalizedString>
      <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfClaimsPrincipalAlreadyExists">Ya existe un usuario con el id. especificado. Elija otro diferente.</LocalizedString>
      </LocalizedStrings>
    </LocalizedResources>
    <!-- More localized resources... -->
  </Localization>
</BuildingBlocks>
```




