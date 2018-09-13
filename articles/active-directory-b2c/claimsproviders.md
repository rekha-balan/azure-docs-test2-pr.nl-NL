---
title: ClaimsProviders  - Azure Active Directory B2C | Microsoft Docs
description: Specify the ClaimsProvider element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: a9159ade6e16c1d14149197e85cee8720dd98b09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856114"
---
# <a name="claimsproviders"></a><span data-ttu-id="6cef5-103">ClaimsProviders</span><span class="sxs-lookup"><span data-stu-id="6cef5-103">ClaimsProviders</span></span> 

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6cef5-104">A claims provider contains a set of [technical profiles](technicalprofiles.md).</span><span class="sxs-lookup"><span data-stu-id="6cef5-104">A claims provider contains a set of [technical profiles](technicalprofiles.md).</span></span> <span data-ttu-id="6cef5-105">Every claims provider must have one or more technical profiles that determine the endpoints and the protocols needed to communicate with the claims provider.</span><span class="sxs-lookup"><span data-stu-id="6cef5-105">Every claims provider must have one or more technical profiles that determine the endpoints and the protocols needed to communicate with the claims provider.</span></span> <span data-ttu-id="6cef5-106">A claims provider can have multiple technical profiles.</span><span class="sxs-lookup"><span data-stu-id="6cef5-106">A claims provider can have multiple technical profiles.</span></span> <span data-ttu-id="6cef5-107">For example, multiple technical profiles may be defined because the claims provider supports multiple protocols, various endpoints with different capabilities, or releases different claims at different assurance levels.</span><span class="sxs-lookup"><span data-stu-id="6cef5-107">For example, multiple technical profiles may be defined because the claims provider supports multiple protocols, various endpoints with different capabilities, or releases different claims at different assurance levels.</span></span> <span data-ttu-id="6cef5-108">It may be acceptable to release sensitive claims in one user journey, but not in another.</span><span class="sxs-lookup"><span data-stu-id="6cef5-108">It may be acceptable to release sensitive claims in one user journey, but not in another.</span></span>

```XML
<ClaimsProviders>
  <ClaimsProvider>
    <Domain>Domain name</Domain>
    <DisplayName>Display name</DisplayName>
    <TechnicalProfiles>
      </TechnicalProfile>
        ...
      </TechnicalProfile>
        ...
    </TechnicalProfiles>
  </ClaimsProvider>
</ClaimsProvider>
  ...
</ClaimsProviders>
```

<span data-ttu-id="6cef5-109">The **ClaimsProviders** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="6cef5-109">The **ClaimsProviders** element contains the following element:</span></span>

| <span data-ttu-id="6cef5-110">Element</span><span class="sxs-lookup"><span data-stu-id="6cef5-110">Element</span></span> | <span data-ttu-id="6cef5-111">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6cef5-111">Occurrences</span></span> | <span data-ttu-id="6cef5-112">Description</span><span class="sxs-lookup"><span data-stu-id="6cef5-112">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6cef5-113">ClaimsProvider</span><span class="sxs-lookup"><span data-stu-id="6cef5-113">ClaimsProvider</span></span> | <span data-ttu-id="6cef5-114">1:n</span><span class="sxs-lookup"><span data-stu-id="6cef5-114">1:n</span></span> | <span data-ttu-id="6cef5-115">An accredited claims provider that can be leveraged in various user journeys.</span><span class="sxs-lookup"><span data-stu-id="6cef5-115">An accredited claims provider that can be leveraged in various user journeys.</span></span> |

## <a name="claimsprovider"></a><span data-ttu-id="6cef5-116">ClaimsProvider</span><span class="sxs-lookup"><span data-stu-id="6cef5-116">ClaimsProvider</span></span>

<span data-ttu-id="6cef5-117">The **ClaimsProvider** element contains the following child elements:</span><span class="sxs-lookup"><span data-stu-id="6cef5-117">The **ClaimsProvider** element contains the following child elements:</span></span>

| <span data-ttu-id="6cef5-118">Element</span><span class="sxs-lookup"><span data-stu-id="6cef5-118">Element</span></span> | <span data-ttu-id="6cef5-119">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6cef5-119">Occurrences</span></span> | <span data-ttu-id="6cef5-120">Description</span><span class="sxs-lookup"><span data-stu-id="6cef5-120">Description</span></span> |
| ------- | ---------- | ----------- |
| <span data-ttu-id="6cef5-121">Domain</span><span class="sxs-lookup"><span data-stu-id="6cef5-121">Domain</span></span> | <span data-ttu-id="6cef5-122">0:1</span><span class="sxs-lookup"><span data-stu-id="6cef5-122">0:1</span></span> | <span data-ttu-id="6cef5-123">A string that contains the domain name for the claim provider.</span><span class="sxs-lookup"><span data-stu-id="6cef5-123">A string that contains the domain name for the claim provider.</span></span> <span data-ttu-id="6cef5-124">For example, if your claims provider includes the Facebook technical profile, the domain name is Facebook.com.</span><span class="sxs-lookup"><span data-stu-id="6cef5-124">For example, if your claims provider includes the Facebook technical profile, the domain name is Facebook.com.</span></span> <span data-ttu-id="6cef5-125">This domain name is used for all technical profiles defined in the claims provider unless overridden by the technical profile.</span><span class="sxs-lookup"><span data-stu-id="6cef5-125">This domain name is used for all technical profiles defined in the claims provider unless overridden by the technical profile.</span></span> |
| <span data-ttu-id="6cef5-126">DisplayName</span><span class="sxs-lookup"><span data-stu-id="6cef5-126">DisplayName</span></span> | <span data-ttu-id="6cef5-127">0:1</span><span class="sxs-lookup"><span data-stu-id="6cef5-127">0:1</span></span> | <span data-ttu-id="6cef5-128">A string that contains the name of the claims provider that can be displayed to users.</span><span class="sxs-lookup"><span data-stu-id="6cef5-128">A string that contains the name of the claims provider that can be displayed to users.</span></span> |
| [<span data-ttu-id="6cef5-129">TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="6cef5-129">TechnicalProfiles</span></span>](technicalprofiles.md) | <span data-ttu-id="6cef5-130">0:1</span><span class="sxs-lookup"><span data-stu-id="6cef5-130">0:1</span></span> | <span data-ttu-id="6cef5-131">A set of technical profiles supported by the claim provider</span><span class="sxs-lookup"><span data-stu-id="6cef5-131">A set of technical profiles supported by the claim provider</span></span> |

<span data-ttu-id="6cef5-132">**ClaimsProvider** organizes your technical profiles relate to the claims provider.</span><span class="sxs-lookup"><span data-stu-id="6cef5-132">**ClaimsProvider** organizes your technical profiles relate to the claims provider.</span></span> <span data-ttu-id="6cef5-133">The following example shows the Azure Active Directory claims provider with the Azure Active Directory technical profiles:</span><span class="sxs-lookup"><span data-stu-id="6cef5-133">The following example shows the Azure Active Directory claims provider with the Azure Active Directory technical profiles:</span></span> 

```XML
<ClaimsProvider>
  <DisplayName>Azure Active Directory</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="AAD-Common">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId-NoError">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
      ...
    </TechnicalProfile>
      ...
    <TechnicalProfile Id="AAD-UserWritePasswordUsingObjectId">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
      ...    
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserReadUsingObjectId">
      ...
    </TechnicalProfile>
    <TechnicalProfile Id="AAD-UserWritePhoneNumberUsingObjectId">
      ...
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="6cef5-134">The following example shows the Facebook claims provider with the **Facebook-OAUTH** technical profile.</span><span class="sxs-lookup"><span data-stu-id="6cef5-134">The following example shows the Facebook claims provider with the **Facebook-OAUTH** technical profile.</span></span>

```XML
<ClaimsProvider>
  <Domain>facebook.com</Domain>
  <DisplayName>Facebook</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="Facebook-OAUTH">
      <DisplayName>Facebook</DisplayName>
      <Protocol Name="OAuth2" />
        ...
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```
 
