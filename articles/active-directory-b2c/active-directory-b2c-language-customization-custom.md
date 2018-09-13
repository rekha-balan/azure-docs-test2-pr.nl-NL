---
title: Language customization in Azure Active Directory B2C custom policies | Microsoft Docs
description: Learn how to use localize content in custom policies for multiple languages.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 11/13/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6269ac65e5db20521346d5312bcbadd0905c36e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867874"
---
# <a name="language-customization-in-custom-policies"></a><span data-ttu-id="60e82-103">Language customization in custom policies</span><span class="sxs-lookup"><span data-stu-id="60e82-103">Language customization in custom policies</span></span>

> [!NOTE]
> <span data-ttu-id="60e82-104">This feature is in public preview.</span><span class="sxs-lookup"><span data-stu-id="60e82-104">This feature is in public preview.</span></span>
> 

<span data-ttu-id="60e82-105">In custom policies, language customization works the same as in built-in policies.</span><span class="sxs-lookup"><span data-stu-id="60e82-105">In custom policies, language customization works the same as in built-in policies.</span></span>  <span data-ttu-id="60e82-106">See the built-in [documentation](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-language-customization) that describes the behavior in how a language is chosen based on the parameters and browser settings.</span><span class="sxs-lookup"><span data-stu-id="60e82-106">See the built-in [documentation](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-language-customization) that describes the behavior in how a language is chosen based on the parameters and browser settings.</span></span>

## <a name="enable-supported-languages"></a><span data-ttu-id="60e82-107">Enable supported languages</span><span class="sxs-lookup"><span data-stu-id="60e82-107">Enable supported languages</span></span>
<span data-ttu-id="60e82-108">If ui-locales was not specified and the user's browser asks for one of these languages, supported languages are shown to the user.</span><span class="sxs-lookup"><span data-stu-id="60e82-108">If ui-locales was not specified and the user's browser asks for one of these languages, supported languages are shown to the user.</span></span>  

<span data-ttu-id="60e82-109">Supported languages are defined in `<BuildingBlocks>` in the following format:</span><span class="sxs-lookup"><span data-stu-id="60e82-109">Supported languages are defined in `<BuildingBlocks>` in the following format:</span></span>

```XML
<BuildingBlocks>
  <Localization>
    <SupportedLanguages DefaultLanguage="en">
      <SupportedLanguage>qps-ploc</SupportedLanguage>
      <SupportedLanguage>en</SupportedLanguage>
    </SupportedLanguages>
  </Localization>
</BuildingBlocks>
```

<span data-ttu-id="60e82-110">Default language and supported languages behave in the same way as they do in built-in policies.</span><span class="sxs-lookup"><span data-stu-id="60e82-110">Default language and supported languages behave in the same way as they do in built-in policies.</span></span>

## <a name="enable-custom-language-strings"></a><span data-ttu-id="60e82-111">Enable custom language strings</span><span class="sxs-lookup"><span data-stu-id="60e82-111">Enable custom language strings</span></span>

<span data-ttu-id="60e82-112">Creating custom language strings requires two steps:</span><span class="sxs-lookup"><span data-stu-id="60e82-112">Creating custom language strings requires two steps:</span></span>
1. <span data-ttu-id="60e82-113">Edit the `<ContentDefinition>` for the page to specify a resource ID for the desired languages</span><span class="sxs-lookup"><span data-stu-id="60e82-113">Edit the `<ContentDefinition>` for the page to specify a resource ID for the desired languages</span></span>
2. <span data-ttu-id="60e82-114">Create the `<LocalizedResources>` with corresponding IDs in your `<BuildingBlocks>`</span><span class="sxs-lookup"><span data-stu-id="60e82-114">Create the `<LocalizedResources>` with corresponding IDs in your `<BuildingBlocks>`</span></span>

<span data-ttu-id="60e82-115">Keep in mind that you can put a `<ContentDefinition>` and `<BuildingBlock>` in both your extension file or the relying policy file depending on whether you want the changes to be in all your inheriting policies or not.</span><span class="sxs-lookup"><span data-stu-id="60e82-115">Keep in mind that you can put a `<ContentDefinition>` and `<BuildingBlock>` in both your extension file or the relying policy file depending on whether you want the changes to be in all your inheriting policies or not.</span></span>

### <a name="edit-the-contentdefinition-for-the-page"></a><span data-ttu-id="60e82-116">Edit the ContentDefinition for the page</span><span class="sxs-lookup"><span data-stu-id="60e82-116">Edit the ContentDefinition for the page</span></span>

<span data-ttu-id="60e82-117">For each page you want to localize, you can specify in the `<ContentDefinition>` what language resources to look for each language code.</span><span class="sxs-lookup"><span data-stu-id="60e82-117">For each page you want to localize, you can specify in the `<ContentDefinition>` what language resources to look for each language code.</span></span>

```XML
<ContentDefinition Id="api.signuporsignin">
      <LocalizedResourcesReferences>
        <LocalizedResourcesReference Language="fr" LocalizedResourcesReferenceId="fr" />
        <LocalizedResourcesReference Language="en" LocalizedResourcesReferenceId="en" />
      </LocalizedResourcesReferences>
</ContentDefinition>
```

<span data-ttu-id="60e82-118">In this sample, French (fr) and English (en) custom strings are added to the Unified sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="60e82-118">In this sample, French (fr) and English (en) custom strings are added to the Unified sign-up or sign-in page.</span></span>  <span data-ttu-id="60e82-119">The `LocalizedResourcesReferenceId` for each `LocalizedResourcesReference` is the same as their locale, but you could use any string as the ID.</span><span class="sxs-lookup"><span data-stu-id="60e82-119">The `LocalizedResourcesReferenceId` for each `LocalizedResourcesReference` is the same as their locale, but you could use any string as the ID.</span></span>  <span data-ttu-id="60e82-120">For each language and page combination, you have to create a corresponding `<LocalizedResources>` shown in the following.</span><span class="sxs-lookup"><span data-stu-id="60e82-120">For each language and page combination, you have to create a corresponding `<LocalizedResources>` shown in the following.</span></span>


### <a name="create-the-localizedresources"></a><span data-ttu-id="60e82-121">Create the LocalizedResources</span><span class="sxs-lookup"><span data-stu-id="60e82-121">Create the LocalizedResources</span></span>

<span data-ttu-id="60e82-122">Your overrides are contained in your `<BuildingBlocks>` and there is a `<LocalizedResources>` for each page and language you have specified in the `<ContentDefinition>` for each page.</span><span class="sxs-lookup"><span data-stu-id="60e82-122">Your overrides are contained in your `<BuildingBlocks>` and there is a `<LocalizedResources>` for each page and language you have specified in the `<ContentDefinition>` for each page.</span></span>  <span data-ttu-id="60e82-123">Each override is specified as a `<LocalizedString>` such as in the following sample:</span><span class="sxs-lookup"><span data-stu-id="60e82-123">Each override is specified as a `<LocalizedString>` such as in the following sample:</span></span>

```XML
<BuildingBlocks>
  <Localization>
    <LocalizedResources Id="en">
      <LocalizedStrings>
        <LocalizedString ElementType="ClaimsProvider" StringId="SignInWithLogonNameExchange">Local Account Sign-in</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="UserId" StringId="DisplayName">Username</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="UserId" StringId="UserHelpText">Username used for signing in.</LocalizedString>
        <LocalizedString ElementType="ClaimType" ElementId="UserId" StringId="PatternHelpText">The username you provided is not valid.</LocalizedString>
        <LocalizedString ElementType="UxElement" StringId="button_signin">Sign In Now</LocalizedString>
        <LocalizedString ElementType="ErrorMessage" StringId="UserMessageIfInvalidPassword">Your password is incorrect.</LocalizedString>
      </LocalizedStrings>
    </LocalizedResources>
  </Localization>
</BuildingBlocks>
```

<span data-ttu-id="60e82-124">There are four types of string elements on the page:</span><span class="sxs-lookup"><span data-stu-id="60e82-124">There are four types of string elements on the page:</span></span>

<span data-ttu-id="60e82-125">**ClaimsProvider** - Labels for your identity providers (Facebook, Google, Azure AD etc.) **ClaimType** - Labels for your attributes and their corresponding help text, or field validation errors **UxElement** - Other string elements on the page that are there by default, such as buttons, links, or text **ErrorMessage** - Form validation error messages</span><span class="sxs-lookup"><span data-stu-id="60e82-125">**ClaimsProvider** - Labels for your identity providers (Facebook, Google, Azure AD etc.) **ClaimType** - Labels for your attributes and their corresponding help text, or field validation errors **UxElement** - Other string elements on the page that are there by default, such as buttons, links, or text **ErrorMessage** - Form validation error messages</span></span>

<span data-ttu-id="60e82-126">Ensure that the `StringId`s match for the page that you are using these overrides otherwise it is blocked by policy validation on upload.</span><span class="sxs-lookup"><span data-stu-id="60e82-126">Ensure that the `StringId`s match for the page that you are using these overrides otherwise it is blocked by policy validation on upload.</span></span>  