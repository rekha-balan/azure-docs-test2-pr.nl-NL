---
title: ClaimsSchema  - Azure Active Directory B2C | Microsoft Docs
description: Specify the ClaimsSchema element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 3ac80b045443614e66bc1d8446047087629b1d96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868647"
---
# <a name="claimsschema"></a><span data-ttu-id="b4ffa-103">ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="b4ffa-103">ClaimsSchema</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b4ffa-104">The **ClaimsSchema** element defines the claim types that can be referenced as part of the policy.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-104">The **ClaimsSchema** element defines the claim types that can be referenced as part of the policy.</span></span> <span data-ttu-id="b4ffa-105">Claims schema is the place where you declare your claims.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-105">Claims schema is the place where you declare your claims.</span></span> <span data-ttu-id="b4ffa-106">A claim can be first name, last name, display name, phone number and more.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-106">A claim can be first name, last name, display name, phone number and more.</span></span> <span data-ttu-id="b4ffa-107">ClaimsSchema element contains list of **ClaimType** elements.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-107">ClaimsSchema element contains list of **ClaimType** elements.</span></span> <span data-ttu-id="b4ffa-108">The **ClaimType** element contains the **Id** attribute, which is the claim name.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-108">The **ClaimType** element contains the **Id** attribute, which is the claim name.</span></span> 

```XML
<BuildingBlocks>
  <ClaimsSchema>
    <ClaimType Id="Id">
      <DisplayName>Surname</DisplayName>
      <DataType>string</DataType>
      <DefaultPartnerClaimTypes>
        <Protocol Name="OAuth2" PartnerClaimType="family_name" />
        <Protocol Name="OpenIdConnect" PartnerClaimType="family_name" />
        <Protocol Name="SAML2" PartnerClaimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname" />
      </DefaultPartnerClaimTypes>
      <UserHelpText>Your surname (also known as family name or last name).</UserHelpText>
      <UserInputType>TextBox</UserInputType>
```

## <a name="claimtype"></a><span data-ttu-id="b4ffa-109">ClaimType</span><span class="sxs-lookup"><span data-stu-id="b4ffa-109">ClaimType</span></span>

<span data-ttu-id="b4ffa-110">The **ClaimType** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-110">The **ClaimType** element contains the following attribute:</span></span>

| <span data-ttu-id="b4ffa-111">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-111">Attribute</span></span> | <span data-ttu-id="b4ffa-112">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-112">Required</span></span> | <span data-ttu-id="b4ffa-113">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-113">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-114">Id</span><span class="sxs-lookup"><span data-stu-id="b4ffa-114">Id</span></span> | <span data-ttu-id="b4ffa-115">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-115">Yes</span></span> | <span data-ttu-id="b4ffa-116">An identifier that's used for the claim type.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-116">An identifier that's used for the claim type.</span></span> <span data-ttu-id="b4ffa-117">Other elements can use this identifier in the policy.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-117">Other elements can use this identifier in the policy.</span></span> |

<span data-ttu-id="b4ffa-118">The **ClaimType** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-118">The **ClaimType** element contains the following elements:</span></span>

| <span data-ttu-id="b4ffa-119">Element</span><span class="sxs-lookup"><span data-stu-id="b4ffa-119">Element</span></span> | <span data-ttu-id="b4ffa-120">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4ffa-120">Occurrences</span></span> | <span data-ttu-id="b4ffa-121">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-121">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4ffa-122">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b4ffa-122">DisplayName</span></span> | <span data-ttu-id="b4ffa-123">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-123">0:1</span></span> | <span data-ttu-id="b4ffa-124">The title that's displayed to users on various screens.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-124">The title that's displayed to users on various screens.</span></span> <span data-ttu-id="b4ffa-125">The value can be [localized](localization.md).</span><span class="sxs-lookup"><span data-stu-id="b4ffa-125">The value can be [localized](localization.md).</span></span> |
| <span data-ttu-id="b4ffa-126">DataType</span><span class="sxs-lookup"><span data-stu-id="b4ffa-126">DataType</span></span> | <span data-ttu-id="b4ffa-127">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-127">0:1</span></span> | <span data-ttu-id="b4ffa-128">The type of the claim.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-128">The type of the claim.</span></span> <span data-ttu-id="b4ffa-129">The data types of boolean, date, dateTime, int, long, string, stringCollection, alternativeSecurityIdCollection can be used.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-129">The data types of boolean, date, dateTime, int, long, string, stringCollection, alternativeSecurityIdCollection can be used.</span></span> |
| <span data-ttu-id="b4ffa-130">DefaultPartnerClaimTypes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-130">DefaultPartnerClaimTypes</span></span> | <span data-ttu-id="b4ffa-131">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-131">0:1</span></span> | <span data-ttu-id="b4ffa-132">The partner default claim types to use for a specified protocol.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-132">The partner default claim types to use for a specified protocol.</span></span> <span data-ttu-id="b4ffa-133">The value can be overwritten in the **PartnerClaimType** specified in the **InputClaim** or **OutputClaim** elements.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-133">The value can be overwritten in the **PartnerClaimType** specified in the **InputClaim** or **OutputClaim** elements.</span></span> <span data-ttu-id="b4ffa-134">Use this element to specify the default name for a protocol.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-134">Use this element to specify the default name for a protocol.</span></span>  |
| <span data-ttu-id="b4ffa-135">Mask</span><span class="sxs-lookup"><span data-stu-id="b4ffa-135">Mask</span></span> | <span data-ttu-id="b4ffa-136">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-136">0:1</span></span> | <span data-ttu-id="b4ffa-137">An optional string of masking characters that can be applied when displaying the claim.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-137">An optional string of masking characters that can be applied when displaying the claim.</span></span> <span data-ttu-id="b4ffa-138">For example, the phone number 324-232-4343 can be masked as XXX-XXX-4343.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-138">For example, the phone number 324-232-4343 can be masked as XXX-XXX-4343.</span></span> |
| <span data-ttu-id="b4ffa-139">UserHelpText</span><span class="sxs-lookup"><span data-stu-id="b4ffa-139">UserHelpText</span></span> | <span data-ttu-id="b4ffa-140">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-140">0:1</span></span> | <span data-ttu-id="b4ffa-141">A description of the claim type that can be helpful for users to understand its purpose.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-141">A description of the claim type that can be helpful for users to understand its purpose.</span></span> <span data-ttu-id="b4ffa-142">The value can be [localized](localization.md).</span><span class="sxs-lookup"><span data-stu-id="b4ffa-142">The value can be [localized](localization.md).</span></span> |
| <span data-ttu-id="b4ffa-143">UserInputType</span><span class="sxs-lookup"><span data-stu-id="b4ffa-143">UserInputType</span></span> | <span data-ttu-id="b4ffa-144">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-144">0:1</span></span> | <span data-ttu-id="b4ffa-145">The type of input control that should be available to the user when manually entering the claim data for the claim type.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-145">The type of input control that should be available to the user when manually entering the claim data for the claim type.</span></span> <span data-ttu-id="b4ffa-146">See the user input types defined later in this page.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-146">See the user input types defined later in this page.</span></span> |
| <span data-ttu-id="b4ffa-147">Restriction</span><span class="sxs-lookup"><span data-stu-id="b4ffa-147">Restriction</span></span> | <span data-ttu-id="b4ffa-148">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-148">0:1</span></span> | <span data-ttu-id="b4ffa-149">The value restrictions for this claim, such as a regular expression (Regex) or a list of acceptable values.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-149">The value restrictions for this claim, such as a regular expression (Regex) or a list of acceptable values.</span></span> <span data-ttu-id="b4ffa-150">The value can be [localized](localization.md).</span><span class="sxs-lookup"><span data-stu-id="b4ffa-150">The value can be [localized](localization.md).</span></span> |
<span data-ttu-id="b4ffa-151">PredicateValidationReference</span><span class="sxs-lookup"><span data-stu-id="b4ffa-151">PredicateValidationReference</span></span>| <span data-ttu-id="b4ffa-152">0:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-152">0:1</span></span> | <span data-ttu-id="b4ffa-153">A reference to a **PredicateValidationsInput** element.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-153">A reference to a **PredicateValidationsInput** element.</span></span> <span data-ttu-id="b4ffa-154">The **PredicateValidationReference** elements enable you to perform a validation process to ensure that only properly formed data is entered.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-154">The **PredicateValidationReference** elements enable you to perform a validation process to ensure that only properly formed data is entered.</span></span> <span data-ttu-id="b4ffa-155">For more information, see [Predicates](predicates.md).</span><span class="sxs-lookup"><span data-stu-id="b4ffa-155">For more information, see [Predicates](predicates.md).</span></span> |

### <a name="defaultpartnerclaimtypes"></a><span data-ttu-id="b4ffa-156">DefaultPartnerClaimTypes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-156">DefaultPartnerClaimTypes</span></span>

<span data-ttu-id="b4ffa-157">The **DefaultPartnerClaimTypes** may contain the following element:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-157">The **DefaultPartnerClaimTypes** may contain the following element:</span></span>

| <span data-ttu-id="b4ffa-158">Element</span><span class="sxs-lookup"><span data-stu-id="b4ffa-158">Element</span></span> | <span data-ttu-id="b4ffa-159">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4ffa-159">Occurrences</span></span> | <span data-ttu-id="b4ffa-160">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-160">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4ffa-161">Protocol</span><span class="sxs-lookup"><span data-stu-id="b4ffa-161">Protocol</span></span> | <span data-ttu-id="b4ffa-162">0:n</span><span class="sxs-lookup"><span data-stu-id="b4ffa-162">0:n</span></span> | <span data-ttu-id="b4ffa-163">List of protocols with their default partner claim type name.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-163">List of protocols with their default partner claim type name.</span></span> |

<span data-ttu-id="b4ffa-164">The **Protocol** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-164">The **Protocol** element contains the following attributes:</span></span>

| <span data-ttu-id="b4ffa-165">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-165">Attribute</span></span> | <span data-ttu-id="b4ffa-166">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-166">Required</span></span> | <span data-ttu-id="b4ffa-167">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-167">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-168">Name</span><span class="sxs-lookup"><span data-stu-id="b4ffa-168">Name</span></span> | <span data-ttu-id="b4ffa-169">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-169">Yes</span></span> | <span data-ttu-id="b4ffa-170">The name of a valid protocol supported by Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-170">The name of a valid protocol supported by Azure AD B2C.</span></span> <span data-ttu-id="b4ffa-171">Possible values are:  OAuth1, OAuth2, SAML2, OpenIdConnect, WsFed, or WsTrust.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-171">Possible values are:  OAuth1, OAuth2, SAML2, OpenIdConnect, WsFed, or WsTrust.</span></span> |
| <span data-ttu-id="b4ffa-172">PartnerClaimType</span><span class="sxs-lookup"><span data-stu-id="b4ffa-172">PartnerClaimType</span></span> | <span data-ttu-id="b4ffa-173">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-173">Yes</span></span> | <span data-ttu-id="b4ffa-174">The claim type name to be used.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-174">The claim type name to be used.</span></span> |

<span data-ttu-id="b4ffa-175">In the following example, when the Identity Experience Framework interacts with a SAML2 identity provider or relying party application, the **surname** claim is mapped to `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`, with OpenIdConnect and OAuth2, the claim is mapped to `family_name`.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-175">In the following example, when the Identity Experience Framework interacts with a SAML2 identity provider or relying party application, the **surname** claim is mapped to `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`, with OpenIdConnect and OAuth2, the claim is mapped to `family_name`.</span></span>

```XML
<ClaimType Id="surname">
  <DisplayName>Surname</DisplayName>
  <DataType>string</DataType>
  <DefaultPartnerClaimTypes>
    <Protocol Name="OAuth2" PartnerClaimType="family_name" />
    <Protocol Name="OpenIdConnect" PartnerClaimType="family_name" />
    <Protocol Name="SAML2" PartnerClaimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname" />
  </DefaultPartnerClaimTypes>
</ClaimType>
```

<span data-ttu-id="b4ffa-176">As a result, the JWT token issued by Azure AD B2C, omits the `family_name` instead of ClaimType name **surname**.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-176">As a result, the JWT token issued by Azure AD B2C, omits the `family_name` instead of ClaimType name **surname**.</span></span>
 
```JSON
{
  "sub": "6fbbd70d-262b-4b50-804c-257ae1706ef2",
  "auth_time": 1535013501,
  "given_name": "David",
  "family_name": "Williams",
  "name": "David Williams",
}
```

### <a name="mask"></a><span data-ttu-id="b4ffa-177">Mask</span><span class="sxs-lookup"><span data-stu-id="b4ffa-177">Mask</span></span>

<span data-ttu-id="b4ffa-178">The **Mask** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-178">The **Mask** element contains the following attributes:</span></span>

| <span data-ttu-id="b4ffa-179">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-179">Attribute</span></span> | <span data-ttu-id="b4ffa-180">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-180">Required</span></span> | <span data-ttu-id="b4ffa-181">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-181">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-182">Type</span><span class="sxs-lookup"><span data-stu-id="b4ffa-182">Type</span></span> | <span data-ttu-id="b4ffa-183">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-183">Yes</span></span> | <span data-ttu-id="b4ffa-184">The type of the claim mask.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-184">The type of the claim mask.</span></span> <span data-ttu-id="b4ffa-185">Possible values: `Simple` or `Regex`.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-185">Possible values: `Simple` or `Regex`.</span></span> <span data-ttu-id="b4ffa-186">The `Simple` value indicates that a simple text mask is applied to the leading portion of a string claim.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-186">The `Simple` value indicates that a simple text mask is applied to the leading portion of a string claim.</span></span> <span data-ttu-id="b4ffa-187">The `Regex` value indicates that a regular expression is applied to the string claim as whole.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-187">The `Regex` value indicates that a regular expression is applied to the string claim as whole.</span></span>  <span data-ttu-id="b4ffa-188">If the `Regex` value is specified, an optional attribute must also be defined with the regular expression to use.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-188">If the `Regex` value is specified, an optional attribute must also be defined with the regular expression to use.</span></span> |
| <span data-ttu-id="b4ffa-189">Regex</span><span class="sxs-lookup"><span data-stu-id="b4ffa-189">Regex</span></span> | <span data-ttu-id="b4ffa-190">No</span><span class="sxs-lookup"><span data-stu-id="b4ffa-190">No</span></span> | <span data-ttu-id="b4ffa-191">If **Type** is set to `Regex`, specify the regular expression to use.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-191">If **Type** is set to `Regex`, specify the regular expression to use.</span></span>

<span data-ttu-id="b4ffa-192">The follwing example configures a **PhoneNumber** claim with the `Simple` mask:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-192">The follwing example configures a **PhoneNumber** claim with the `Simple` mask:</span></span>

```XML
<ClaimType Id="PhoneNumber">
  <DisplayName>Phone</DisplayName>
  <DataType>string</DataType>
  <Mask Type="Simple">XXX-XXX-</Mask>
  <AdminHelpText/>
  <UserHelpText>Your telephone number.</UserHelpText>
</ClaimType>
```

<span data-ttu-id="b4ffa-193">The Identity Experience Framework renders the phone number while hiding the first six digits:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-193">The Identity Experience Framework renders the phone number while hiding the first six digits:</span></span>

![Using claim type with mask](./media/claimsschema/mask.png)

<span data-ttu-id="b4ffa-195">The follwing example configures a **AlternateEmail** claim with the `Regex` mask:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-195">The follwing example configures a **AlternateEmail** claim with the `Regex` mask:</span></span>

```XML
<ClaimType Id="AlternateEmail">
  <DisplayName>Please verify the secondary email linked to your account</DisplayName>
  <DataType>string</DataType>
  <Mask Type="Regex" Regex="(?&lt;=.).(?=.*@)">*</Mask>
  <UserInputType>Readonly</UserInputType>
</ClaimType>
```

<span data-ttu-id="b4ffa-196">The Identity Experience Framework renders only the first letter of the email address and the email domain name:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-196">The Identity Experience Framework renders only the first letter of the email address and the email domain name:</span></span>

![Using claim type with mask](./media/claimsschema/mask-regex.png)


### <a name="restriction"></a><span data-ttu-id="b4ffa-198">Restriction</span><span class="sxs-lookup"><span data-stu-id="b4ffa-198">Restriction</span></span>

<span data-ttu-id="b4ffa-199">The **Restriction** element may contain the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-199">The **Restriction** element may contain the following attribute:</span></span>

| <span data-ttu-id="b4ffa-200">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-200">Attribute</span></span> | <span data-ttu-id="b4ffa-201">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-201">Required</span></span> | <span data-ttu-id="b4ffa-202">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-202">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-203">MergeBehavior</span><span class="sxs-lookup"><span data-stu-id="b4ffa-203">MergeBehavior</span></span> | <span data-ttu-id="b4ffa-204">No</span><span class="sxs-lookup"><span data-stu-id="b4ffa-204">No</span></span> | <span data-ttu-id="b4ffa-205">The method used to merge enumeration values with a ClaimType in a parent policy with the same identifier.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-205">The method used to merge enumeration values with a ClaimType in a parent policy with the same identifier.</span></span> <span data-ttu-id="b4ffa-206">Use this attribute when you overwrite a claim specified in the base policy.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-206">Use this attribute when you overwrite a claim specified in the base policy.</span></span> <span data-ttu-id="b4ffa-207">Possible values: `Append`, `Prepend`, or `ReplaceAll`.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-207">Possible values: `Append`, `Prepend`, or `ReplaceAll`.</span></span> <span data-ttu-id="b4ffa-208">The `Append` value is a collection of data that should be appended to the end of the collection specified in the parent policy.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-208">The `Append` value is a collection of data that should be appended to the end of the collection specified in the parent policy.</span></span> <span data-ttu-id="b4ffa-209">The `Prepend` value is a collection of data that should be added before the collection specified in the parent policy.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-209">The `Prepend` value is a collection of data that should be added before the collection specified in the parent policy.</span></span> <span data-ttu-id="b4ffa-210">The `ReplaceAll` value is a collection of data specified in the parent policy that should be ignored.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-210">The `ReplaceAll` value is a collection of data specified in the parent policy that should be ignored.</span></span> |

<span data-ttu-id="b4ffa-211">The **Restriction** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-211">The **Restriction** element contains the following elements:</span></span>

| <span data-ttu-id="b4ffa-212">Element</span><span class="sxs-lookup"><span data-stu-id="b4ffa-212">Element</span></span> | <span data-ttu-id="b4ffa-213">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4ffa-213">Occurrences</span></span> | <span data-ttu-id="b4ffa-214">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-214">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4ffa-215">Enumeration</span><span class="sxs-lookup"><span data-stu-id="b4ffa-215">Enumeration</span></span> | <span data-ttu-id="b4ffa-216">1:n</span><span class="sxs-lookup"><span data-stu-id="b4ffa-216">1:n</span></span> | <span data-ttu-id="b4ffa-217">The available options in the user interface for the user to select for a claim, such as a value in a dropdown.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-217">The available options in the user interface for the user to select for a claim, such as a value in a dropdown.</span></span> |
| <span data-ttu-id="b4ffa-218">Pattern</span><span class="sxs-lookup"><span data-stu-id="b4ffa-218">Pattern</span></span> | <span data-ttu-id="b4ffa-219">1:1</span><span class="sxs-lookup"><span data-stu-id="b4ffa-219">1:1</span></span> | <span data-ttu-id="b4ffa-220">The regular expression to use.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-220">The regular expression to use.</span></span> |

### <a name="enumeration"></a><span data-ttu-id="b4ffa-221">Enumeration</span><span class="sxs-lookup"><span data-stu-id="b4ffa-221">Enumeration</span></span>

<span data-ttu-id="b4ffa-222">The **Enumeration** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-222">The **Enumeration** element contains the following attributes:</span></span>

| <span data-ttu-id="b4ffa-223">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-223">Attribute</span></span> | <span data-ttu-id="b4ffa-224">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-224">Required</span></span> | <span data-ttu-id="b4ffa-225">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-225">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-226">Text</span><span class="sxs-lookup"><span data-stu-id="b4ffa-226">Text</span></span> | <span data-ttu-id="b4ffa-227">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-227">Yes</span></span> | <span data-ttu-id="b4ffa-228">The display string that is shown to the user in the user interface for this option.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-228">The display string that is shown to the user in the user interface for this option.</span></span> |
|<span data-ttu-id="b4ffa-229">Value</span><span class="sxs-lookup"><span data-stu-id="b4ffa-229">Value</span></span> | <span data-ttu-id="b4ffa-230">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-230">Yes</span></span> | <span data-ttu-id="b4ffa-231">The claim value that is associated with selecting this option.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-231">The claim value that is associated with selecting this option.</span></span> |
| <span data-ttu-id="b4ffa-232">SelectByDefault</span><span class="sxs-lookup"><span data-stu-id="b4ffa-232">SelectByDefault</span></span> | <span data-ttu-id="b4ffa-233">No</span><span class="sxs-lookup"><span data-stu-id="b4ffa-233">No</span></span> | <span data-ttu-id="b4ffa-234">Indicates whether or not this option should be selected by default in the UI.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-234">Indicates whether or not this option should be selected by default in the UI.</span></span> <span data-ttu-id="b4ffa-235">Possible values: True or False.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-235">Possible values: True or False.</span></span> |

<span data-ttu-id="b4ffa-236">The following example configures a **city** dropdown list claim with a default value set to `New York`:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-236">The following example configures a **city** dropdown list claim with a default value set to `New York`:</span></span>

```XML
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="New York" Value="new-york" SelectByDefault="true" />
  </Restriction>
</ClaimType>
```
<span data-ttu-id="b4ffa-237">Dropdown city list with a default value set to New York:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-237">Dropdown city list with a default value set to New York:</span></span>

![Dropdown city list](./media/claimsschema/dropdownsingleselect.png)


### <a name="pattern"></a><span data-ttu-id="b4ffa-239">Pattern</span><span class="sxs-lookup"><span data-stu-id="b4ffa-239">Pattern</span></span>

<span data-ttu-id="b4ffa-240">The **Pattern** element can contain the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-240">The **Pattern** element can contain the following attributes:</span></span>

| <span data-ttu-id="b4ffa-241">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4ffa-241">Attribute</span></span> | <span data-ttu-id="b4ffa-242">Required</span><span class="sxs-lookup"><span data-stu-id="b4ffa-242">Required</span></span> | <span data-ttu-id="b4ffa-243">Description</span><span class="sxs-lookup"><span data-stu-id="b4ffa-243">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4ffa-244">RegularExpression</span><span class="sxs-lookup"><span data-stu-id="b4ffa-244">RegularExpression</span></span> | <span data-ttu-id="b4ffa-245">Yes</span><span class="sxs-lookup"><span data-stu-id="b4ffa-245">Yes</span></span> | <span data-ttu-id="b4ffa-246">The regular expression that claims of this type must match in order to be valid.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-246">The regular expression that claims of this type must match in order to be valid.</span></span> |
| <span data-ttu-id="b4ffa-247">HelpText</span><span class="sxs-lookup"><span data-stu-id="b4ffa-247">HelpText</span></span> | <span data-ttu-id="b4ffa-248">No</span><span class="sxs-lookup"><span data-stu-id="b4ffa-248">No</span></span> | <span data-ttu-id="b4ffa-249">The pattern or regular expression for this claim.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-249">The pattern or regular expression for this claim.</span></span> |

<span data-ttu-id="b4ffa-250">The following example configures an **email** claim with regular expression input validation and help text:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-250">The following example configures an **email** claim with regular expression input validation and help text:</span></span>

```XML
<ClaimType Id="email">
  <DisplayName>Email Address</DisplayName>
  <DataType>string</DataType>
  <DefaultPartnerClaimTypes>
    <Protocol Name="OpenIdConnect" PartnerClaimType="email" />
  </DefaultPartnerClaimTypes>
  <UserHelpText>Email address that can be used to contact you.</UserHelpText>
  <UserInputType>TextBox</UserInputType>
  <Restriction>
    <Pattern RegularExpression="^[a-zA-Z0-9.!#$%&amp;'^_`{}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" HelpText="Please enter a valid email address." />
    </Restriction>
 </ClaimType>
```

<span data-ttu-id="b4ffa-251">The Identity Experience Framework renders the email address claim with email format input validation:</span><span class="sxs-lookup"><span data-stu-id="b4ffa-251">The Identity Experience Framework renders the email address claim with email format input validation:</span></span>

![Using claim type with pattern](./media/claimsschema/pattern.png)

## <a name="userinputtype"></a><span data-ttu-id="b4ffa-253">UserInputType</span><span class="sxs-lookup"><span data-stu-id="b4ffa-253">UserInputType</span></span>

<span data-ttu-id="b4ffa-254">Azure AD B2C supports a variety of user input types, such as a textbox, password, and dropdown list that can be used when manually entering claim data for the claim type.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-254">Azure AD B2C supports a variety of user input types, such as a textbox, password, and dropdown list that can be used when manually entering claim data for the claim type.</span></span> <span data-ttu-id="b4ffa-255">You must specify the **UserInputType** when you collect information from the user by using a [self-asserted technical profile](self-asserted-technical-profile.md).</span><span class="sxs-lookup"><span data-stu-id="b4ffa-255">You must specify the **UserInputType** when you collect information from the user by using a [self-asserted technical profile](self-asserted-technical-profile.md).</span></span>

### <a name="textbox"></a><span data-ttu-id="b4ffa-256">TextBox</span><span class="sxs-lookup"><span data-stu-id="b4ffa-256">TextBox</span></span>

<span data-ttu-id="b4ffa-257">The **TextBox** user input type is used to provide a single-line text box.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-257">The **TextBox** user input type is used to provide a single-line text box.</span></span>

![Using claim type with textbox](./media/claimsschema/textbox.png)

```XML
<ClaimType Id="displayName">
  <DisplayName>Display Name</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your display name.</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

### <a name="emailbox"></a><span data-ttu-id="b4ffa-259">EmailBox</span><span class="sxs-lookup"><span data-stu-id="b4ffa-259">EmailBox</span></span>

<span data-ttu-id="b4ffa-260">The **EmailBox** user input type is used to provide a basic email input field.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-260">The **EmailBox** user input type is used to provide a basic email input field.</span></span>

![Using claim type with emailbox](./media/claimsschema/emailbox.png)

```XML
<ClaimType Id="email">
  <DisplayName>Email Address</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Email address that can be used to contact you.</UserHelpText>
  <UserInputType>EmailBox</UserInputType>
  <Restriction>
    <Pattern RegularExpression="^[a-zA-Z0-9!#$%&amp;'+^_`{}~-]+(?:\.[a-zA-Z0-9!#$%&amp;'+^_`{}~-]+)*@(?:[a-zA-Z0-9](?:[a-zA-Z0-9-]*[a-zA-Z0-9])?\.)+[a-zA-Z0-9](?:[a-zA-Z0-9-]*[a-zA-Z0-9])?$" HelpText="Please enter a valid email address." />
  </Restriction>
</ClaimType>
```

### <a name="password"></a><span data-ttu-id="b4ffa-262">Password</span><span class="sxs-lookup"><span data-stu-id="b4ffa-262">Password</span></span>

<span data-ttu-id="b4ffa-263">The **Password** user input type is used to record a password entered by the user.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-263">The **Password** user input type is used to record a password entered by the user.</span></span>

![Using claim type with password](./media/claimsschema/password.png)

```XML
<ClaimType Id="password">
  <DisplayName>Password</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Enter password</UserHelpText>
  <UserInputType>Password</UserInputType>
</ClaimType>
```

### <a name="datetimedropdown"></a><span data-ttu-id="b4ffa-265">DateTimeDropdown</span><span class="sxs-lookup"><span data-stu-id="b4ffa-265">DateTimeDropdown</span></span>

<span data-ttu-id="b4ffa-266">The **DateTimeDropdown** user input type is used to provide a set of drop-downs to select a day, month, and year.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-266">The **DateTimeDropdown** user input type is used to provide a set of drop-downs to select a day, month, and year.</span></span>

![Using claim type with datetimedropdown](./media/claimsschema/datetimedropdown.png)

```XML
<ClaimType Id="dateOfBirth">
  <DisplayName>Date Of Birth</DisplayName>
  <DataType>date</DataType>
  <AdminHelpText/>
  <UserHelpText>The date on which you were born.</UserHelpText>
  <UserInputType>DateTimeDropdown</UserInputType>
</ClaimType>
```

### <a name="radiosingleselect"></a><span data-ttu-id="b4ffa-268">RadioSingleSelect</span><span class="sxs-lookup"><span data-stu-id="b4ffa-268">RadioSingleSelect</span></span>

<span data-ttu-id="b4ffa-269">The **RadioSingleSelect** user input type is used to provide a collection of radio buttons that allows the user to select one option.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-269">The **RadioSingleSelect** user input type is used to provide a collection of radio buttons that allows the user to select one option.</span></span>

![Using claim type with radiodsingleselect](./media/claimsschema/radiosingleselect.png)

```XML
<ClaimType Id="color">
  <DisplayName>Preferred color</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Blue" Value="Blue" SelectByDefault="false" />
    <Enumeration Text="Green " Value="Green" SelectByDefault="false" />
    <Enumeration Text="Orange" Value="Orange" SelectByDefault="true" />
  </Restriction>
</ClaimType>    
```

### <a name="dropdownsingleselect"></a><span data-ttu-id="b4ffa-271">DropdownSingleSelect</span><span class="sxs-lookup"><span data-stu-id="b4ffa-271">DropdownSingleSelect</span></span>

<span data-ttu-id="b4ffa-272">The **DropdownSingleSelect** user input type is used to provide a drop-down box that allows the user to select one option.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-272">The **DropdownSingleSelect** user input type is used to provide a drop-down box that allows the user to select one option.</span></span>

![Using claim type with dropdownsingleselect](./media/claimsschema/dropdownsingleselect.png)

```XML
<ClaimType Id="city">
  <DisplayName>City where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="New York" Value="new-york" SelectByDefault="true" />
  </Restriction>
</ClaimType>
```

### <a name="checkboxmultiselect"></a><span data-ttu-id="b4ffa-274">CheckboxMultiSelect</span><span class="sxs-lookup"><span data-stu-id="b4ffa-274">CheckboxMultiSelect</span></span>

<span data-ttu-id="b4ffa-275">The **CheckboxMultiSelect** user input type is used to provide a collection of checkboxes that allows the user to select multiple options.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-275">The **CheckboxMultiSelect** user input type is used to provide a collection of checkboxes that allows the user to select multiple options.</span></span>

![Using claim type with checkboxmultiselect](./media/claimsschema/checkboxmultiselect.png)

```XML
<ClaimType Id="languages">
  <DisplayName>Languages you speak</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="English" Value="English" SelectByDefault="true" />
    <Enumeration Text="France " Value="France" SelectByDefault="false" />
    <Enumeration Text="Spanish" Value="Spanish" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

### <a name="readonly"></a><span data-ttu-id="b4ffa-277">Readonly</span><span class="sxs-lookup"><span data-stu-id="b4ffa-277">Readonly</span></span>

<span data-ttu-id="b4ffa-278">The **Readonly** user input type is used to provide a readonly field to display the claim and value.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-278">The **Readonly** user input type is used to provide a readonly field to display the claim and value.</span></span>

![Using claim type with readonly](./media/claimsschema/readonly.png)

```XML
<ClaimType Id="membershipNumber">
  <DisplayName>Membership number</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your membership number (read only)</UserHelpText>
  <UserInputType>Readonly</UserInputType>
</ClaimType>
```


### <a name="paragraph"></a><span data-ttu-id="b4ffa-280">Paragraph</span><span class="sxs-lookup"><span data-stu-id="b4ffa-280">Paragraph</span></span>

<span data-ttu-id="b4ffa-281">The **Paragraph** user input type is used to provide a field that shows text only in a paragraph tag.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-281">The **Paragraph** user input type is used to provide a field that shows text only in a paragraph tag.</span></span> <span data-ttu-id="b4ffa-282">For example, &lt;p&gt;text&lt;/p&gt;.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-282">For example, &lt;p&gt;text&lt;/p&gt;.</span></span>

![Using claim type with paragraph](./media/claimsschema/paragraph.png)

```XML
<ClaimType Id="responseMsg">
  <DisplayName>Error message: </DisplayName>
  <DataType>string</DataType>
  <AdminHelpText>A claim responsible for holding response messages to send to the relying party</AdminHelpText>
  <UserHelpText>A claim responsible for holding response messages to send to the relying party</UserHelpText>
  <UserInputType>Paragraph</UserInputType>
  <Restriction>
    <Enumeration Text="B2C_V1_90001" Value="You cant sign in because you are a minor" />
    <Enumeration Text="B2C_V1_90002" Value="This action can only be performed by gold members" />
    <Enumeration Text="B2C_V1_90003" Value="You have not been enabled for this operation" />
  </Restriction>
</ClaimType>
```

<span data-ttu-id="b4ffa-284">To display one of the **Enumeration** values in a **responseMsg** claim, use `GetMappedValueFromLocalizedCollection` or `CreateStringClaim` claims transformation.</span><span class="sxs-lookup"><span data-stu-id="b4ffa-284">To display one of the **Enumeration** values in a **responseMsg** claim, use `GetMappedValueFromLocalizedCollection` or `CreateStringClaim` claims transformation.</span></span> <span data-ttu-id="b4ffa-285">For more information, see [String Claims Transformations](string-transformations.md)</span><span class="sxs-lookup"><span data-stu-id="b4ffa-285">For more information, see [String Claims Transformations](string-transformations.md)</span></span> 
