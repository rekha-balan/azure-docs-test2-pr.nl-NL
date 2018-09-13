---
title: BuildingBlocks - Azure Active Directory B2C | Microsoft Docs
description: Specify the BuildingBlocks element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 2582284f56da1dd1c49c4183ba07a4f60d4f6061
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868961"
---
# <a name="buildingblocks"></a><span data-ttu-id="74203-103">BuildingBlocks</span><span class="sxs-lookup"><span data-stu-id="74203-103">BuildingBlocks</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="74203-104">The **BuildingBlocks** element is added inside the [TrustFrameworkPolicy](trustframeworkpolicy.md) element.</span><span class="sxs-lookup"><span data-stu-id="74203-104">The **BuildingBlocks** element is added inside the [TrustFrameworkPolicy](trustframeworkpolicy.md) element.</span></span>

```XML
<TrustFrameworkPolicy
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
  PolicySchemaVersion="0.3.0.0"
  TenantId="mytenant.onmicrosoft.com"
  PolicyId="B2C_1A_TrustFrameworkBase"
  PublicPolicyUri="http://mytenant.onmicrosoft.com/B2C_1A_TrustFrameworkBase">

  <BuildingBlocks>
    <ClaimsSchema>
      ...
    </ClaimsSchema>
    <ClaimsTransformations>
      ...
    </ClaimsTransformations>
    <Predicates>
    ...
    </Predicates>
    <PredicateValidations>
    ...
    </PredicateValidations>
    <ContentDefinitions>
      ...
    </ContentDefinitions>
    <Localization>
      ...
    </Localization>
 </BuildingBlocks>
```

<span data-ttu-id="74203-105">The **BuildingBlocks** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="74203-105">The **BuildingBlocks** element contains the following elements:</span></span>

- <span data-ttu-id="74203-106">[ClaimsSchema](claimsschema.md) - Defines the claim types that can be referenced as part of the policy.</span><span class="sxs-lookup"><span data-stu-id="74203-106">[ClaimsSchema](claimsschema.md) - Defines the claim types that can be referenced as part of the policy.</span></span> <span data-ttu-id="74203-107">The claims schema is the place where you declare your claim types.</span><span class="sxs-lookup"><span data-stu-id="74203-107">The claims schema is the place where you declare your claim types.</span></span> <span data-ttu-id="74203-108">A claim type is similar to a variable in many programmatic languages.</span><span class="sxs-lookup"><span data-stu-id="74203-108">A claim type is similar to a variable in many programmatic languages.</span></span> <span data-ttu-id="74203-109">You can use the claim type to collect data from the user of your application, receive claims from social identity providers, send and receive data from a custom REST API, or store any internal data used by your custom policy.</span><span class="sxs-lookup"><span data-stu-id="74203-109">You can use the claim type to collect data from the user of your application, receive claims from social identity providers, send and receive data from a custom REST API, or store any internal data used by your custom policy.</span></span> 
 
- <span data-ttu-id="74203-110">[ClaimsTransformations](claimstransformations.md) - Contains a list of claims transformations that can be used in your policy.</span><span class="sxs-lookup"><span data-stu-id="74203-110">[ClaimsTransformations](claimstransformations.md) - Contains a list of claims transformations that can be used in your policy.</span></span>  <span data-ttu-id="74203-111">A claims transformation converts one claim into another.</span><span class="sxs-lookup"><span data-stu-id="74203-111">A claims transformation converts one claim into another.</span></span> <span data-ttu-id="74203-112">In the claims transformation, you specify a transform method, such as:</span><span class="sxs-lookup"><span data-stu-id="74203-112">In the claims transformation, you specify a transform method, such as:</span></span> 
    - <span data-ttu-id="74203-113">Changing the case of a string claim to the one specified.</span><span class="sxs-lookup"><span data-stu-id="74203-113">Changing the case of a string claim to the one specified.</span></span> <span data-ttu-id="74203-114">For example, changing a string from lowercase to uppercase.</span><span class="sxs-lookup"><span data-stu-id="74203-114">For example, changing a string from lowercase to uppercase.</span></span>
    - <span data-ttu-id="74203-115">Comparing two claims and returning a claim with true indicating that the claims match, otherwise false.</span><span class="sxs-lookup"><span data-stu-id="74203-115">Comparing two claims and returning a claim with true indicating that the claims match, otherwise false.</span></span>
    - <span data-ttu-id="74203-116">Creating a string claim from the provided parameter in the policy.</span><span class="sxs-lookup"><span data-stu-id="74203-116">Creating a string claim from the provided parameter in the policy.</span></span>
    - <span data-ttu-id="74203-117">Creating a random string using the random number generator.</span><span class="sxs-lookup"><span data-stu-id="74203-117">Creating a random string using the random number generator.</span></span>
    - <span data-ttu-id="74203-118">Formatting a claim according to the provided format string.</span><span class="sxs-lookup"><span data-stu-id="74203-118">Formatting a claim according to the provided format string.</span></span> <span data-ttu-id="74203-119">This transformation uses the C# `String.Format` method.</span><span class="sxs-lookup"><span data-stu-id="74203-119">This transformation uses the C# `String.Format` method.</span></span>

- <span data-ttu-id="74203-120">[ContentDefinitions](contentdefinitions.md) - Contains URLs for HTML5 templates to use in your user journey.</span><span class="sxs-lookup"><span data-stu-id="74203-120">[ContentDefinitions](contentdefinitions.md) - Contains URLs for HTML5 templates to use in your user journey.</span></span> <span data-ttu-id="74203-121">In a custom policy, a content definition defines the HTML5 page URI that's used for a specified step in the user journey.</span><span class="sxs-lookup"><span data-stu-id="74203-121">In a custom policy, a content definition defines the HTML5 page URI that's used for a specified step in the user journey.</span></span> <span data-ttu-id="74203-122">For example, the sign-in or sign-up, password reset, or error pages.</span><span class="sxs-lookup"><span data-stu-id="74203-122">For example, the sign-in or sign-up, password reset, or error pages.</span></span> <span data-ttu-id="74203-123">You can modify the look and feel by overriding the LoadUri for the HTML5 file.</span><span class="sxs-lookup"><span data-stu-id="74203-123">You can modify the look and feel by overriding the LoadUri for the HTML5 file.</span></span> <span data-ttu-id="74203-124">Or you can create new content definitions according to your needs.</span><span class="sxs-lookup"><span data-stu-id="74203-124">Or you can create new content definitions according to your needs.</span></span> <span data-ttu-id="74203-125">This element may contain a localized resources reference using a localization ID.</span><span class="sxs-lookup"><span data-stu-id="74203-125">This element may contain a localized resources reference using a localization ID.</span></span>

- <span data-ttu-id="74203-126">[Localization](localization.md) - Allows you to support multiple languages.</span><span class="sxs-lookup"><span data-stu-id="74203-126">[Localization](localization.md) - Allows you to support multiple languages.</span></span> <span data-ttu-id="74203-127">The localization support in policies allows you set up the list of supported languages in a policy and pick a default language.</span><span class="sxs-lookup"><span data-stu-id="74203-127">The localization support in policies allows you set up the list of supported languages in a policy and pick a default language.</span></span> <span data-ttu-id="74203-128">Language-specific strings and collections are also supported.</span><span class="sxs-lookup"><span data-stu-id="74203-128">Language-specific strings and collections are also supported.</span></span>

- <span data-ttu-id="74203-129">[Predicates and PredicateValidationsInput](predicates.md) - Enables you to perform a validation process to ensure that only properly formed data is entered into a claim.</span><span class="sxs-lookup"><span data-stu-id="74203-129">[Predicates and PredicateValidationsInput](predicates.md) - Enables you to perform a validation process to ensure that only properly formed data is entered into a claim.</span></span>
