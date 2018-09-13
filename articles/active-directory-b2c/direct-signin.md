---
title: Set up direct sign-in using Azure Active Directory B2C | Microsoft Docs
description: Learn how to prepopulate the sign-in name or redirect straight to a social identity provider.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 06/18/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 62ded87067bf597a2f40ec8e8405142297d4fb78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869891"
---
# <a name="set-up-direct-sign-in-using-azure-active-directory-b2c"></a><span data-ttu-id="04651-103">Set up direct sign-in using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="04651-103">Set up direct sign-in using Azure Active Directory B2C</span></span>

<span data-ttu-id="04651-104">When setting up sign-in for your application using Azure Active Directory (AD) B2C, you can prepopulate the sign-in name or direct sign-in to a specific social identity provider, such as Facebook, LinkedIn, or a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="04651-104">When setting up sign-in for your application using Azure Active Directory (AD) B2C, you can prepopulate the sign-in name or direct sign-in to a specific social identity provider, such as Facebook, LinkedIn, or a Microsoft account.</span></span> 

## <a name="prepopulate-the-sign-in-name"></a><span data-ttu-id="04651-105">Prepopulate the sign-in name</span><span class="sxs-lookup"><span data-stu-id="04651-105">Prepopulate the sign-in name</span></span>

<span data-ttu-id="04651-106">During a sign-in user journey, a relying party application may target a specific user or domain name.</span><span class="sxs-lookup"><span data-stu-id="04651-106">During a sign-in user journey, a relying party application may target a specific user or domain name.</span></span> <span data-ttu-id="04651-107">When targeting a user, an application can specify, in the authorization request, the `login_hint` query parameter with the user sign-in name.</span><span class="sxs-lookup"><span data-stu-id="04651-107">When targeting a user, an application can specify, in the authorization request, the `login_hint` query parameter with the user sign-in name.</span></span> <span data-ttu-id="04651-108">Azure AD B2C automatically populates the sign-in name, while the user only needs to provide the password.</span><span class="sxs-lookup"><span data-stu-id="04651-108">Azure AD B2C automatically populates the sign-in name, while the user only needs to provide the password.</span></span>

![using login hint](./media/direct-signin/login-hint.png) 

<span data-ttu-id="04651-110">The user is able to change the value in the sign-in textbox.</span><span class="sxs-lookup"><span data-stu-id="04651-110">The user is able to change the value in the sign-in textbox.</span></span>

<span data-ttu-id="04651-111">If you are using a custom policy, override the `SelfAsserted-LocalAccountSignin-Email` technical profile.</span><span class="sxs-lookup"><span data-stu-id="04651-111">If you are using a custom policy, override the `SelfAsserted-LocalAccountSignin-Email` technical profile.</span></span> <span data-ttu-id="04651-112">In the `<InputClaims>` section, set the DefaultValue of the signInName claim to `{OIDC:LoginHint}`.</span><span class="sxs-lookup"><span data-stu-id="04651-112">In the `<InputClaims>` section, set the DefaultValue of the signInName claim to `{OIDC:LoginHint}`.</span></span> <span data-ttu-id="04651-113">The `{OIDC:LoginHint}` variable contains the value of the `login_hint` parameter.</span><span class="sxs-lookup"><span data-stu-id="04651-113">The `{OIDC:LoginHint}` variable contains the value of the `login_hint` parameter.</span></span> <span data-ttu-id="04651-114">Azure AD B2C reads the value of the signInName claim and pre-populates the signInName textbox.</span><span class="sxs-lookup"><span data-stu-id="04651-114">Azure AD B2C reads the value of the signInName claim and pre-populates the signInName textbox.</span></span>

```xml
<ClaimsProvider>
  <DisplayName>Local Account</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="SelfAsserted-LocalAccountSignin-Email">
      <InputClaims>
        <!-- Add the login hint value to the sign-in names claim type -->
        <InputClaim ClaimTypeReferenceId="signInName" DefaultValue="{OIDC:LoginHint}" />
      </InputClaims>
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="redirect-sign-in-to-a-social-provider"></a><span data-ttu-id="04651-115">Redirect sign-in to a social provider</span><span class="sxs-lookup"><span data-stu-id="04651-115">Redirect sign-in to a social provider</span></span>

<span data-ttu-id="04651-116">If you configured the sign-in journey for your application to include social accounts, such as Facebook, LinkedIn, or Google, you can specify the `domain_hint` parameter.</span><span class="sxs-lookup"><span data-stu-id="04651-116">If you configured the sign-in journey for your application to include social accounts, such as Facebook, LinkedIn, or Google, you can specify the `domain_hint` parameter.</span></span> <span data-ttu-id="04651-117">This query parameter provides a hint to Azure AD B2C about the social identity provider that should be used for sign-in.</span><span class="sxs-lookup"><span data-stu-id="04651-117">This query parameter provides a hint to Azure AD B2C about the social identity provider that should be used for sign-in.</span></span> <span data-ttu-id="04651-118">For example, if the application specifies `domain_hint=facebook.com`, sign-in goes directly to the Facebook sign-in page.</span><span class="sxs-lookup"><span data-stu-id="04651-118">For example, if the application specifies `domain_hint=facebook.com`, sign-in goes directly to the Facebook sign-in page.</span></span>

![using domain hint](./media/direct-signin/domain-hint.png) 

<span data-ttu-id="04651-120">If you are using a custom policy, you can configure the domain name using the `<Domain>domain name</Domain>` XML element of any `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="04651-120">If you are using a custom policy, you can configure the domain name using the `<Domain>domain name</Domain>` XML element of any `<ClaimsProvider>`.</span></span> 

```xml
<ClaimsProvider>
    <!-- Add the domain hint value to the claims provider -->
    <Domain>facebook.com</Domain>
    <DisplayName>Facebook</DisplayName>
    <TechnicalProfiles>
    ...
```


