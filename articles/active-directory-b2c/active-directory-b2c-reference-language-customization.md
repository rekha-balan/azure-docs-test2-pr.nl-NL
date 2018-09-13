---
title: Language customization in Azure Active Directory B2C | Microsoft Docs
description: Learn about customizing the language experience.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 02/26/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: affd52352dcc745557dd66c61ccfa1e7a99dcdb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871466"
---
# <a name="language-customization-in-azure-active-directory-b2c"></a><span data-ttu-id="f156d-103">Language customization in Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f156d-103">Language customization in Azure Active Directory B2C</span></span>

<span data-ttu-id="f156d-104">Language customization in Azure Active Directory B2C (Azure AD B2C) allows your policy to accommodate different languages to suit your customer needs.</span><span class="sxs-lookup"><span data-stu-id="f156d-104">Language customization in Azure Active Directory B2C (Azure AD B2C) allows your policy to accommodate different languages to suit your customer needs.</span></span>  <span data-ttu-id="f156d-105">Microsoft provides the translations for [36 languages](#supported-languages), but you can also provide your own translations for any language.</span><span class="sxs-lookup"><span data-stu-id="f156d-105">Microsoft provides the translations for [36 languages](#supported-languages), but you can also provide your own translations for any language.</span></span> <span data-ttu-id="f156d-106">Even if your experience is provided for only a single language, you can customize any text on the pages.</span><span class="sxs-lookup"><span data-stu-id="f156d-106">Even if your experience is provided for only a single language, you can customize any text on the pages.</span></span>  

## <a name="how-language-customization-works"></a><span data-ttu-id="f156d-107">How language customization works</span><span class="sxs-lookup"><span data-stu-id="f156d-107">How language customization works</span></span>
<span data-ttu-id="f156d-108">You use language customization to select which languages your user journey is available in.</span><span class="sxs-lookup"><span data-stu-id="f156d-108">You use language customization to select which languages your user journey is available in.</span></span> <span data-ttu-id="f156d-109">After the feature is enabled, you can provide the query string parameter, `ui_locales`, from your application.</span><span class="sxs-lookup"><span data-stu-id="f156d-109">After the feature is enabled, you can provide the query string parameter, `ui_locales`, from your application.</span></span> <span data-ttu-id="f156d-110">When you call into Azure AD B2C, your page is translated to the locale that you have indicated.</span><span class="sxs-lookup"><span data-stu-id="f156d-110">When you call into Azure AD B2C, your page is translated to the locale that you have indicated.</span></span> <span data-ttu-id="f156d-111">This type of configuration gives you complete control over the languages in your user journey and ignores the language settings of the customer's browser.</span><span class="sxs-lookup"><span data-stu-id="f156d-111">This type of configuration gives you complete control over the languages in your user journey and ignores the language settings of the customer's browser.</span></span> 

<span data-ttu-id="f156d-112">You might not need that level of control over what languages your customer sees.</span><span class="sxs-lookup"><span data-stu-id="f156d-112">You might not need that level of control over what languages your customer sees.</span></span> <span data-ttu-id="f156d-113">If you don't provide a `ui_locales` parameter, the customer's experience is dictated by their browser's settings.</span><span class="sxs-lookup"><span data-stu-id="f156d-113">If you don't provide a `ui_locales` parameter, the customer's experience is dictated by their browser's settings.</span></span>  <span data-ttu-id="f156d-114">You can still control which languages your user journey is translated to by adding it as a supported language.</span><span class="sxs-lookup"><span data-stu-id="f156d-114">You can still control which languages your user journey is translated to by adding it as a supported language.</span></span> <span data-ttu-id="f156d-115">If a customer's browser is set to show a language that you don't want to support, then the language that you selected as a default in supported cultures is shown instead.</span><span class="sxs-lookup"><span data-stu-id="f156d-115">If a customer's browser is set to show a language that you don't want to support, then the language that you selected as a default in supported cultures is shown instead.</span></span>

- <span data-ttu-id="f156d-116">**ui-locales specified language**: After you enable language customization, your user journey is translated to the language that's specified here.</span><span class="sxs-lookup"><span data-stu-id="f156d-116">**ui-locales specified language**: After you enable language customization, your user journey is translated to the language that's specified here.</span></span>
- <span data-ttu-id="f156d-117">**Browser-requested language**: If no `ui_locales` parameter was specified, your user journey is translated to the browser-requested language, *if the language is supported*.</span><span class="sxs-lookup"><span data-stu-id="f156d-117">**Browser-requested language**: If no `ui_locales` parameter was specified, your user journey is translated to the browser-requested language, *if the language is supported*.</span></span>
- <span data-ttu-id="f156d-118">**Policy default language**: If the browser doesn't specify a language, or it specifies one that is not supported, the user journey is translated to the policy default language.</span><span class="sxs-lookup"><span data-stu-id="f156d-118">**Policy default language**: If the browser doesn't specify a language, or it specifies one that is not supported, the user journey is translated to the policy default language.</span></span>

>[!NOTE]
><span data-ttu-id="f156d-119">If you're using custom user attributes, you need to provide your own translations.</span><span class="sxs-lookup"><span data-stu-id="f156d-119">If you're using custom user attributes, you need to provide your own translations.</span></span> <span data-ttu-id="f156d-120">For more information, see [Customize your strings](#customize-your-strings).</span><span class="sxs-lookup"><span data-stu-id="f156d-120">For more information, see [Customize your strings](#customize-your-strings).</span></span>
>

## <a name="support-requested-languages-for-uilocales"></a><span data-ttu-id="f156d-121">Support requested languages for ui_locales</span><span class="sxs-lookup"><span data-stu-id="f156d-121">Support requested languages for ui_locales</span></span> 
<span data-ttu-id="f156d-122">Policies that were created before the general availability of language customization need to enable this feature first.</span><span class="sxs-lookup"><span data-stu-id="f156d-122">Policies that were created before the general availability of language customization need to enable this feature first.</span></span> <span data-ttu-id="f156d-123">Policies that were created after have language customization enabled by default.</span><span class="sxs-lookup"><span data-stu-id="f156d-123">Policies that were created after have language customization enabled by default.</span></span> 

<span data-ttu-id="f156d-124">When you enable language customization on a policy, you can control the language of the user journey by adding the `ui_locales` parameter.</span><span class="sxs-lookup"><span data-stu-id="f156d-124">When you enable language customization on a policy, you can control the language of the user journey by adding the `ui_locales` parameter.</span></span>
1. <span data-ttu-id="f156d-125">[Go to the B2C features page on the Azure portal](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="f156d-125">[Go to the B2C features page on the Azure portal](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="f156d-126">Browse to a policy that you want to enable for translations.</span><span class="sxs-lookup"><span data-stu-id="f156d-126">Browse to a policy that you want to enable for translations.</span></span>
3. <span data-ttu-id="f156d-127">Select **Language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-127">Select **Language customization**.</span></span>  
4. <span data-ttu-id="f156d-128">Select **Enable language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-128">Select **Enable language customization**.</span></span>
5. <span data-ttu-id="f156d-129">Read the information in the dialog box, and select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f156d-129">Read the information in the dialog box, and select **Yes**.</span></span>

## <a name="select-which-languages-in-your-user-journey-are-enabled"></a><span data-ttu-id="f156d-130">Select which languages in your user journey are enabled</span><span class="sxs-lookup"><span data-stu-id="f156d-130">Select which languages in your user journey are enabled</span></span> 
<span data-ttu-id="f156d-131">Enable a set of languages for your user journey to be translated to when requested by the browser without the `ui_locales` parameter.</span><span class="sxs-lookup"><span data-stu-id="f156d-131">Enable a set of languages for your user journey to be translated to when requested by the browser without the `ui_locales` parameter.</span></span>
1. <span data-ttu-id="f156d-132">Ensure that your policy has language customization enabled from previous instructions.</span><span class="sxs-lookup"><span data-stu-id="f156d-132">Ensure that your policy has language customization enabled from previous instructions.</span></span>
2. <span data-ttu-id="f156d-133">From the **Edit policy** page, select **Language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-133">From the **Edit policy** page, select **Language customization**.</span></span>
3. <span data-ttu-id="f156d-134">Select a language that you want to support.</span><span class="sxs-lookup"><span data-stu-id="f156d-134">Select a language that you want to support.</span></span>
4. <span data-ttu-id="f156d-135">In the properties pane, change **Enabled** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f156d-135">In the properties pane, change **Enabled** to **Yes**.</span></span>  
5. <span data-ttu-id="f156d-136">Select **Save** at the top of the properties pane.</span><span class="sxs-lookup"><span data-stu-id="f156d-136">Select **Save** at the top of the properties pane.</span></span>

>[!NOTE]
><span data-ttu-id="f156d-137">If a `ui_locales` parameter is not provided, the page is translated to the customer's browser language only if it is enabled.</span><span class="sxs-lookup"><span data-stu-id="f156d-137">If a `ui_locales` parameter is not provided, the page is translated to the customer's browser language only if it is enabled.</span></span>
>

## <a name="customize-your-strings"></a><span data-ttu-id="f156d-138">Customize your strings</span><span class="sxs-lookup"><span data-stu-id="f156d-138">Customize your strings</span></span>
<span data-ttu-id="f156d-139">Language customization enables you to customize any string in your user journey.</span><span class="sxs-lookup"><span data-stu-id="f156d-139">Language customization enables you to customize any string in your user journey.</span></span>
1. <span data-ttu-id="f156d-140">Ensure that your policy has language customization enabled from the previous instructions.</span><span class="sxs-lookup"><span data-stu-id="f156d-140">Ensure that your policy has language customization enabled from the previous instructions.</span></span>
2. <span data-ttu-id="f156d-141">From the **Edit policy** page, select **Language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-141">From the **Edit policy** page, select **Language customization**.</span></span>
3. <span data-ttu-id="f156d-142">Select the language that you want to customize.</span><span class="sxs-lookup"><span data-stu-id="f156d-142">Select the language that you want to customize.</span></span>
4. <span data-ttu-id="f156d-143">Select the page that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="f156d-143">Select the page that you want to edit.</span></span>
5. <span data-ttu-id="f156d-144">Select **Download defaults** (or **Download overrides** if you have previously edited this language).</span><span class="sxs-lookup"><span data-stu-id="f156d-144">Select **Download defaults** (or **Download overrides** if you have previously edited this language).</span></span> 

<span data-ttu-id="f156d-145">These steps give you a JSON file that you can use to start editing your strings.</span><span class="sxs-lookup"><span data-stu-id="f156d-145">These steps give you a JSON file that you can use to start editing your strings.</span></span>

### <a name="change-any-string-on-the-page"></a><span data-ttu-id="f156d-146">Change any string on the page</span><span class="sxs-lookup"><span data-stu-id="f156d-146">Change any string on the page</span></span>
1. <span data-ttu-id="f156d-147">Open the JSON file downloaded from previous instructions in a JSON editor.</span><span class="sxs-lookup"><span data-stu-id="f156d-147">Open the JSON file downloaded from previous instructions in a JSON editor.</span></span>
2. <span data-ttu-id="f156d-148">Find the element that you want to change.</span><span class="sxs-lookup"><span data-stu-id="f156d-148">Find the element that you want to change.</span></span>  <span data-ttu-id="f156d-149">You can find `StringId` for the string you're looking for, or look for the `Value` attribute that you want to change.</span><span class="sxs-lookup"><span data-stu-id="f156d-149">You can find `StringId` for the string you're looking for, or look for the `Value` attribute that you want to change.</span></span>
3. <span data-ttu-id="f156d-150">Update the `Value` attribute with what you want displayed.</span><span class="sxs-lookup"><span data-stu-id="f156d-150">Update the `Value` attribute with what you want displayed.</span></span>
4. <span data-ttu-id="f156d-151">For every string that you want to change, change `Override` to `true`.</span><span class="sxs-lookup"><span data-stu-id="f156d-151">For every string that you want to change, change `Override` to `true`.</span></span>
5. <span data-ttu-id="f156d-152">Save the file and upload your changes.</span><span class="sxs-lookup"><span data-stu-id="f156d-152">Save the file and upload your changes.</span></span> <span data-ttu-id="f156d-153">(You can find the upload control in the same place as where you downloaded the JSON file.)</span><span class="sxs-lookup"><span data-stu-id="f156d-153">(You can find the upload control in the same place as where you downloaded the JSON file.)</span></span> 

>[!IMPORTANT]
><span data-ttu-id="f156d-154">If you need to override a string, make sure to set the `Override` value to `true`.</span><span class="sxs-lookup"><span data-stu-id="f156d-154">If you need to override a string, make sure to set the `Override` value to `true`.</span></span>  <span data-ttu-id="f156d-155">If the value isn't changed, the entry is ignored.</span><span class="sxs-lookup"><span data-stu-id="f156d-155">If the value isn't changed, the entry is ignored.</span></span> 
>

### <a name="change-extension-attributes"></a><span data-ttu-id="f156d-156">Change extension attributes</span><span class="sxs-lookup"><span data-stu-id="f156d-156">Change extension attributes</span></span>
<span data-ttu-id="f156d-157">If you want to change the string for a custom user attribute, or you want to add one to the JSON, it's in the following format:</span><span class="sxs-lookup"><span data-stu-id="f156d-157">If you want to change the string for a custom user attribute, or you want to add one to the JSON, it's in the following format:</span></span>
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": true,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```

<span data-ttu-id="f156d-158">Replace `<ExtensionAttribute>` with the name of your custom user attribute.</span><span class="sxs-lookup"><span data-stu-id="f156d-158">Replace `<ExtensionAttribute>` with the name of your custom user attribute.</span></span>  

<span data-ttu-id="f156d-159">Replace `<ExtensionAttributeValue>` with the new string to be displayed.</span><span class="sxs-lookup"><span data-stu-id="f156d-159">Replace `<ExtensionAttributeValue>` with the new string to be displayed.</span></span>

### <a name="provide-a-list-of-values-by-using-localizedcollections"></a><span data-ttu-id="f156d-160">Provide a list of values by using LocalizedCollections</span><span class="sxs-lookup"><span data-stu-id="f156d-160">Provide a list of values by using LocalizedCollections</span></span>
<span data-ttu-id="f156d-161">If you want to provide a set list of values for responses, you need to create a `LocalizedCollections` attribute.</span><span class="sxs-lookup"><span data-stu-id="f156d-161">If you want to provide a set list of values for responses, you need to create a `LocalizedCollections` attribute.</span></span>  <span data-ttu-id="f156d-162">`LocalizedCollections` is an array of `Name` and `Value` pairs.</span><span class="sxs-lookup"><span data-stu-id="f156d-162">`LocalizedCollections` is an array of `Name` and `Value` pairs.</span></span> <span data-ttu-id="f156d-163">The order for the items will be the order they are displayed.</span><span class="sxs-lookup"><span data-stu-id="f156d-163">The order for the items will be the order they are displayed.</span></span>  <span data-ttu-id="f156d-164">To add `LocalizedCollections`, use the following format:</span><span class="sxs-lookup"><span data-stu-id="f156d-164">To add `LocalizedCollections`, use the following format:</span></span>

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": true,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```

* <span data-ttu-id="f156d-165">`ElementId` is the user attribute that this `LocalizedCollections` attribute is a response to.</span><span class="sxs-lookup"><span data-stu-id="f156d-165">`ElementId` is the user attribute that this `LocalizedCollections` attribute is a response to.</span></span>
* <span data-ttu-id="f156d-166">`Name` is the value that's shown to the user.</span><span class="sxs-lookup"><span data-stu-id="f156d-166">`Name` is the value that's shown to the user.</span></span>
* <span data-ttu-id="f156d-167">`Value` is what is returned in the claim when this option is selected.</span><span class="sxs-lookup"><span data-stu-id="f156d-167">`Value` is what is returned in the claim when this option is selected.</span></span>

### <a name="upload-your-changes"></a><span data-ttu-id="f156d-168">Upload your changes</span><span class="sxs-lookup"><span data-stu-id="f156d-168">Upload your changes</span></span>
1. <span data-ttu-id="f156d-169">After you complete the changes to your JSON file, go back to your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="f156d-169">After you complete the changes to your JSON file, go back to your B2C tenant.</span></span>
2. <span data-ttu-id="f156d-170">From the **Edit policy** page, select **Language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-170">From the **Edit policy** page, select **Language customization**.</span></span>
3. <span data-ttu-id="f156d-171">Select the language that you want to translate to.</span><span class="sxs-lookup"><span data-stu-id="f156d-171">Select the language that you want to translate to.</span></span>
4. <span data-ttu-id="f156d-172">Select the page where you want to provide translations.</span><span class="sxs-lookup"><span data-stu-id="f156d-172">Select the page where you want to provide translations.</span></span>
5. <span data-ttu-id="f156d-173">Select the folder icon, and select the JSON file to upload.</span><span class="sxs-lookup"><span data-stu-id="f156d-173">Select the folder icon, and select the JSON file to upload.</span></span>
 
<span data-ttu-id="f156d-174">The changes are saved to your policy automatically.</span><span class="sxs-lookup"><span data-stu-id="f156d-174">The changes are saved to your policy automatically.</span></span>

## <a name="customize-the-page-ui-by-using-language-customization"></a><span data-ttu-id="f156d-175">Customize the page UI by using language customization</span><span class="sxs-lookup"><span data-stu-id="f156d-175">Customize the page UI by using language customization</span></span>

<span data-ttu-id="f156d-176">There are two ways to localize your HTML content.</span><span class="sxs-lookup"><span data-stu-id="f156d-176">There are two ways to localize your HTML content.</span></span> <span data-ttu-id="f156d-177">One way is to turn on [language customization](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="f156d-177">One way is to turn on [language customization](active-directory-b2c-reference-language-customization.md).</span></span> <span data-ttu-id="f156d-178">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="f156d-178">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span></span>  <span data-ttu-id="f156d-179">Your content server can use this parameter to provide customized HTML pages that are language specific.</span><span class="sxs-lookup"><span data-stu-id="f156d-179">Your content server can use this parameter to provide customized HTML pages that are language specific.</span></span>

<span data-ttu-id="f156d-180">Alternatively, you can pull content from different places based on the locale that's used.</span><span class="sxs-lookup"><span data-stu-id="f156d-180">Alternatively, you can pull content from different places based on the locale that's used.</span></span> <span data-ttu-id="f156d-181">In your CORS-enabled endpoint, you can set up a folder structure to host content for specific languages.</span><span class="sxs-lookup"><span data-stu-id="f156d-181">In your CORS-enabled endpoint, you can set up a folder structure to host content for specific languages.</span></span> <span data-ttu-id="f156d-182">You'll call the right one if you use the wildcard value `{Culture:RFC5646}`.</span><span class="sxs-lookup"><span data-stu-id="f156d-182">You'll call the right one if you use the wildcard value `{Culture:RFC5646}`.</span></span>  <span data-ttu-id="f156d-183">For example, assume that this is your custom page URI:</span><span class="sxs-lookup"><span data-stu-id="f156d-183">For example, assume that this is your custom page URI:</span></span>

```
https://wingtiptoysb2c.blob.core.windows.net/{Culture:RFC5646}/wingtip/unified.html
```
<span data-ttu-id="f156d-184">You can load the page in `fr`.</span><span class="sxs-lookup"><span data-stu-id="f156d-184">You can load the page in `fr`.</span></span> <span data-ttu-id="f156d-185">When the page pulls HTML and CSS content, it's pulling from:</span><span class="sxs-lookup"><span data-stu-id="f156d-185">When the page pulls HTML and CSS content, it's pulling from:</span></span>
```
https://wingtiptoysb2c.blob.core.windows.net/fr/wingtip/unified.html
```

## <a name="add-custom-languages"></a><span data-ttu-id="f156d-186">Add custom languages</span><span class="sxs-lookup"><span data-stu-id="f156d-186">Add custom languages</span></span>

<span data-ttu-id="f156d-187">You can also add languages that Microsoft currently does not provide translations for.</span><span class="sxs-lookup"><span data-stu-id="f156d-187">You can also add languages that Microsoft currently does not provide translations for.</span></span> <span data-ttu-id="f156d-188">You'll need to provide the translations for all the strings in the policy.</span><span class="sxs-lookup"><span data-stu-id="f156d-188">You'll need to provide the translations for all the strings in the policy.</span></span>  <span data-ttu-id="f156d-189">Language and locale codes are limited to those in the ISO 639-1 standard.</span><span class="sxs-lookup"><span data-stu-id="f156d-189">Language and locale codes are limited to those in the ISO 639-1 standard.</span></span> 

1. <span data-ttu-id="f156d-190">From the **Edit policy** page, select **Language customization**.</span><span class="sxs-lookup"><span data-stu-id="f156d-190">From the **Edit policy** page, select **Language customization**.</span></span>
2. <span data-ttu-id="f156d-191">Select **Add custom language** from the top of the page.</span><span class="sxs-lookup"><span data-stu-id="f156d-191">Select **Add custom language** from the top of the page.</span></span>
3. <span data-ttu-id="f156d-192">In the context pane that opens, identify which language you're providing translations for by entering a valid locale code.</span><span class="sxs-lookup"><span data-stu-id="f156d-192">In the context pane that opens, identify which language you're providing translations for by entering a valid locale code.</span></span>
4. <span data-ttu-id="f156d-193">For each page, you can download a set of overrides for English and work on the translations.</span><span class="sxs-lookup"><span data-stu-id="f156d-193">For each page, you can download a set of overrides for English and work on the translations.</span></span>
5. <span data-ttu-id="f156d-194">After you're done with the JSON files, you can upload them for each page.</span><span class="sxs-lookup"><span data-stu-id="f156d-194">After you're done with the JSON files, you can upload them for each page.</span></span>
6. <span data-ttu-id="f156d-195">Select **Enable**, and your policy can now show this language for your users.</span><span class="sxs-lookup"><span data-stu-id="f156d-195">Select **Enable**, and your policy can now show this language for your users.</span></span>
7. <span data-ttu-id="f156d-196">Save the language.</span><span class="sxs-lookup"><span data-stu-id="f156d-196">Save the language.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f156d-197">You need to either enable the custom languages or upload overrides for it before you can save.</span><span class="sxs-lookup"><span data-stu-id="f156d-197">You need to either enable the custom languages or upload overrides for it before you can save.</span></span>
>

## <a name="additional-information"></a><span data-ttu-id="f156d-198">Additional information</span><span class="sxs-lookup"><span data-stu-id="f156d-198">Additional information</span></span>

### <a name="page-ui-customization-labels-as-overrides"></a><span data-ttu-id="f156d-199">Page UI customization labels as overrides</span><span class="sxs-lookup"><span data-stu-id="f156d-199">Page UI customization labels as overrides</span></span>
<span data-ttu-id="f156d-200">When you enable language customization, your previous edits for labels using page UI customization are persisted in a JSON file for English (en).</span><span class="sxs-lookup"><span data-stu-id="f156d-200">When you enable language customization, your previous edits for labels using page UI customization are persisted in a JSON file for English (en).</span></span> <span data-ttu-id="f156d-201">You can continue to change your labels and other strings by uploading language resources in language customization.</span><span class="sxs-lookup"><span data-stu-id="f156d-201">You can continue to change your labels and other strings by uploading language resources in language customization.</span></span>
### <a name="up-to-date-translations"></a><span data-ttu-id="f156d-202">Up-to-date translations</span><span class="sxs-lookup"><span data-stu-id="f156d-202">Up-to-date translations</span></span>
<span data-ttu-id="f156d-203">Microsoft is committed to providing the most up-to-date translations for your use.</span><span class="sxs-lookup"><span data-stu-id="f156d-203">Microsoft is committed to providing the most up-to-date translations for your use.</span></span> <span data-ttu-id="f156d-204">Microsoft continuously improves translations and keeps them in compliance for you.</span><span class="sxs-lookup"><span data-stu-id="f156d-204">Microsoft continuously improves translations and keeps them in compliance for you.</span></span> <span data-ttu-id="f156d-205">Microsoft will identify bugs and changes in global terminology and make updates that will work seamlessly in your user journey.</span><span class="sxs-lookup"><span data-stu-id="f156d-205">Microsoft will identify bugs and changes in global terminology and make updates that will work seamlessly in your user journey.</span></span>
### <a name="support-for-right-to-left-languages"></a><span data-ttu-id="f156d-206">Support for right-to-left languages</span><span class="sxs-lookup"><span data-stu-id="f156d-206">Support for right-to-left languages</span></span>
<span data-ttu-id="f156d-207">Microsoft currently doesn't provide support for right-to-left languages.</span><span class="sxs-lookup"><span data-stu-id="f156d-207">Microsoft currently doesn't provide support for right-to-left languages.</span></span> <span data-ttu-id="f156d-208">You can accomplish this by using custom locales and using CSS to change the way the strings are displayed.</span><span class="sxs-lookup"><span data-stu-id="f156d-208">You can accomplish this by using custom locales and using CSS to change the way the strings are displayed.</span></span>  <span data-ttu-id="f156d-209">If you need this feature, please vote for it on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span><span class="sxs-lookup"><span data-stu-id="f156d-209">If you need this feature, please vote for it on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span></span>
### <a name="social-identity-provider-translations"></a><span data-ttu-id="f156d-210">Social identity provider translations</span><span class="sxs-lookup"><span data-stu-id="f156d-210">Social identity provider translations</span></span>
<span data-ttu-id="f156d-211">Microsoft provides the `ui_locales` OIDC parameter to social logins.</span><span class="sxs-lookup"><span data-stu-id="f156d-211">Microsoft provides the `ui_locales` OIDC parameter to social logins.</span></span> <span data-ttu-id="f156d-212">But some social identity providers, including Facebook and Google, don't honor them.</span><span class="sxs-lookup"><span data-stu-id="f156d-212">But some social identity providers, including Facebook and Google, don't honor them.</span></span> 
### <a name="browser-behavior"></a><span data-ttu-id="f156d-213">Browser behavior</span><span class="sxs-lookup"><span data-stu-id="f156d-213">Browser behavior</span></span>
<span data-ttu-id="f156d-214">Chrome and Firefox both request for their set language.</span><span class="sxs-lookup"><span data-stu-id="f156d-214">Chrome and Firefox both request for their set language.</span></span> <span data-ttu-id="f156d-215">If it's a supported language, it's displayed before the default.</span><span class="sxs-lookup"><span data-stu-id="f156d-215">If it's a supported language, it's displayed before the default.</span></span> <span data-ttu-id="f156d-216">Edge currently does not request a language and goes straight to the default language.</span><span class="sxs-lookup"><span data-stu-id="f156d-216">Edge currently does not request a language and goes straight to the default language.</span></span>

### <a name="supported-languages"></a><span data-ttu-id="f156d-217">Supported languages</span><span class="sxs-lookup"><span data-stu-id="f156d-217">Supported languages</span></span>

| <span data-ttu-id="f156d-218">Language</span><span class="sxs-lookup"><span data-stu-id="f156d-218">Language</span></span>              | <span data-ttu-id="f156d-219">Language code</span><span class="sxs-lookup"><span data-stu-id="f156d-219">Language code</span></span> |
|-----------------------|---------------|
| <span data-ttu-id="f156d-220">Bangla</span><span class="sxs-lookup"><span data-stu-id="f156d-220">Bangla</span></span>                | <span data-ttu-id="f156d-221">bn</span><span class="sxs-lookup"><span data-stu-id="f156d-221">bn</span></span>            |
| <span data-ttu-id="f156d-222">Czech</span><span class="sxs-lookup"><span data-stu-id="f156d-222">Czech</span></span>                 | <span data-ttu-id="f156d-223">cs</span><span class="sxs-lookup"><span data-stu-id="f156d-223">cs</span></span>            |
| <span data-ttu-id="f156d-224">Danish</span><span class="sxs-lookup"><span data-stu-id="f156d-224">Danish</span></span>                | <span data-ttu-id="f156d-225">da</span><span class="sxs-lookup"><span data-stu-id="f156d-225">da</span></span>            |
| <span data-ttu-id="f156d-226">German</span><span class="sxs-lookup"><span data-stu-id="f156d-226">German</span></span>                | <span data-ttu-id="f156d-227">de</span><span class="sxs-lookup"><span data-stu-id="f156d-227">de</span></span>            |
| <span data-ttu-id="f156d-228">Greek</span><span class="sxs-lookup"><span data-stu-id="f156d-228">Greek</span></span>                 | <span data-ttu-id="f156d-229">el</span><span class="sxs-lookup"><span data-stu-id="f156d-229">el</span></span>            |
| <span data-ttu-id="f156d-230">English</span><span class="sxs-lookup"><span data-stu-id="f156d-230">English</span></span>               | <span data-ttu-id="f156d-231">en</span><span class="sxs-lookup"><span data-stu-id="f156d-231">en</span></span>            |
| <span data-ttu-id="f156d-232">Spanish</span><span class="sxs-lookup"><span data-stu-id="f156d-232">Spanish</span></span>               | <span data-ttu-id="f156d-233">es</span><span class="sxs-lookup"><span data-stu-id="f156d-233">es</span></span>            |
| <span data-ttu-id="f156d-234">Finnish</span><span class="sxs-lookup"><span data-stu-id="f156d-234">Finnish</span></span>               | <span data-ttu-id="f156d-235">fi</span><span class="sxs-lookup"><span data-stu-id="f156d-235">fi</span></span>            |
| <span data-ttu-id="f156d-236">French</span><span class="sxs-lookup"><span data-stu-id="f156d-236">French</span></span>                | <span data-ttu-id="f156d-237">fr</span><span class="sxs-lookup"><span data-stu-id="f156d-237">fr</span></span>            |
| <span data-ttu-id="f156d-238">Gujarati</span><span class="sxs-lookup"><span data-stu-id="f156d-238">Gujarati</span></span>              | <span data-ttu-id="f156d-239">gu</span><span class="sxs-lookup"><span data-stu-id="f156d-239">gu</span></span>            |
| <span data-ttu-id="f156d-240">Hindi</span><span class="sxs-lookup"><span data-stu-id="f156d-240">Hindi</span></span>                 | <span data-ttu-id="f156d-241">hi</span><span class="sxs-lookup"><span data-stu-id="f156d-241">hi</span></span>            |
| <span data-ttu-id="f156d-242">Croatian</span><span class="sxs-lookup"><span data-stu-id="f156d-242">Croatian</span></span>              | <span data-ttu-id="f156d-243">hr</span><span class="sxs-lookup"><span data-stu-id="f156d-243">hr</span></span>            |
| <span data-ttu-id="f156d-244">Hungarian</span><span class="sxs-lookup"><span data-stu-id="f156d-244">Hungarian</span></span>             | <span data-ttu-id="f156d-245">hu</span><span class="sxs-lookup"><span data-stu-id="f156d-245">hu</span></span>            |
| <span data-ttu-id="f156d-246">Italian</span><span class="sxs-lookup"><span data-stu-id="f156d-246">Italian</span></span>               | <span data-ttu-id="f156d-247">it</span><span class="sxs-lookup"><span data-stu-id="f156d-247">it</span></span>            |
| <span data-ttu-id="f156d-248">Japanese</span><span class="sxs-lookup"><span data-stu-id="f156d-248">Japanese</span></span>              | <span data-ttu-id="f156d-249">ja</span><span class="sxs-lookup"><span data-stu-id="f156d-249">ja</span></span>            |
| <span data-ttu-id="f156d-250">Kannada</span><span class="sxs-lookup"><span data-stu-id="f156d-250">Kannada</span></span>               | <span data-ttu-id="f156d-251">kn</span><span class="sxs-lookup"><span data-stu-id="f156d-251">kn</span></span>            |
| <span data-ttu-id="f156d-252">Korean</span><span class="sxs-lookup"><span data-stu-id="f156d-252">Korean</span></span>                | <span data-ttu-id="f156d-253">ko</span><span class="sxs-lookup"><span data-stu-id="f156d-253">ko</span></span>            |
| <span data-ttu-id="f156d-254">Malayalam</span><span class="sxs-lookup"><span data-stu-id="f156d-254">Malayalam</span></span>             | <span data-ttu-id="f156d-255">ml</span><span class="sxs-lookup"><span data-stu-id="f156d-255">ml</span></span>            |
| <span data-ttu-id="f156d-256">Marathi</span><span class="sxs-lookup"><span data-stu-id="f156d-256">Marathi</span></span>               | <span data-ttu-id="f156d-257">mr</span><span class="sxs-lookup"><span data-stu-id="f156d-257">mr</span></span>            |
| <span data-ttu-id="f156d-258">Malay</span><span class="sxs-lookup"><span data-stu-id="f156d-258">Malay</span></span>                 | <span data-ttu-id="f156d-259">ms</span><span class="sxs-lookup"><span data-stu-id="f156d-259">ms</span></span>            |
| <span data-ttu-id="f156d-260">Norwegian Bokmal</span><span class="sxs-lookup"><span data-stu-id="f156d-260">Norwegian Bokmal</span></span>      | <span data-ttu-id="f156d-261">nb</span><span class="sxs-lookup"><span data-stu-id="f156d-261">nb</span></span>            |
| <span data-ttu-id="f156d-262">Dutch</span><span class="sxs-lookup"><span data-stu-id="f156d-262">Dutch</span></span>                 | <span data-ttu-id="f156d-263">nl</span><span class="sxs-lookup"><span data-stu-id="f156d-263">nl</span></span>            |
| <span data-ttu-id="f156d-264">Punjabi</span><span class="sxs-lookup"><span data-stu-id="f156d-264">Punjabi</span></span>               | <span data-ttu-id="f156d-265">pa</span><span class="sxs-lookup"><span data-stu-id="f156d-265">pa</span></span>            |
| <span data-ttu-id="f156d-266">Polish</span><span class="sxs-lookup"><span data-stu-id="f156d-266">Polish</span></span>                | <span data-ttu-id="f156d-267">pl</span><span class="sxs-lookup"><span data-stu-id="f156d-267">pl</span></span>            |
| <span data-ttu-id="f156d-268">Portuguese - Brazil</span><span class="sxs-lookup"><span data-stu-id="f156d-268">Portuguese - Brazil</span></span>   | <span data-ttu-id="f156d-269">pt-br</span><span class="sxs-lookup"><span data-stu-id="f156d-269">pt-br</span></span>         |
| <span data-ttu-id="f156d-270">Portuguese - Portugal</span><span class="sxs-lookup"><span data-stu-id="f156d-270">Portuguese - Portugal</span></span> | <span data-ttu-id="f156d-271">pt-pt</span><span class="sxs-lookup"><span data-stu-id="f156d-271">pt-pt</span></span>         |
| <span data-ttu-id="f156d-272">Romanian</span><span class="sxs-lookup"><span data-stu-id="f156d-272">Romanian</span></span>              | <span data-ttu-id="f156d-273">ro</span><span class="sxs-lookup"><span data-stu-id="f156d-273">ro</span></span>            |
| <span data-ttu-id="f156d-274">Russian</span><span class="sxs-lookup"><span data-stu-id="f156d-274">Russian</span></span>               | <span data-ttu-id="f156d-275">ru</span><span class="sxs-lookup"><span data-stu-id="f156d-275">ru</span></span>            |
| <span data-ttu-id="f156d-276">Slovak</span><span class="sxs-lookup"><span data-stu-id="f156d-276">Slovak</span></span>                | <span data-ttu-id="f156d-277">sk</span><span class="sxs-lookup"><span data-stu-id="f156d-277">sk</span></span>            |
| <span data-ttu-id="f156d-278">Swedish</span><span class="sxs-lookup"><span data-stu-id="f156d-278">Swedish</span></span>               | <span data-ttu-id="f156d-279">sv</span><span class="sxs-lookup"><span data-stu-id="f156d-279">sv</span></span>            |
| <span data-ttu-id="f156d-280">Tamil</span><span class="sxs-lookup"><span data-stu-id="f156d-280">Tamil</span></span>                 | <span data-ttu-id="f156d-281">ta</span><span class="sxs-lookup"><span data-stu-id="f156d-281">ta</span></span>            |
| <span data-ttu-id="f156d-282">Telugu</span><span class="sxs-lookup"><span data-stu-id="f156d-282">Telugu</span></span>                | <span data-ttu-id="f156d-283">te</span><span class="sxs-lookup"><span data-stu-id="f156d-283">te</span></span>            |
| <span data-ttu-id="f156d-284">Thai</span><span class="sxs-lookup"><span data-stu-id="f156d-284">Thai</span></span>                  | <span data-ttu-id="f156d-285">th</span><span class="sxs-lookup"><span data-stu-id="f156d-285">th</span></span>            |
| <span data-ttu-id="f156d-286">Turkish</span><span class="sxs-lookup"><span data-stu-id="f156d-286">Turkish</span></span>               | <span data-ttu-id="f156d-287">tr</span><span class="sxs-lookup"><span data-stu-id="f156d-287">tr</span></span>            |
| <span data-ttu-id="f156d-288">Chinese - Simplified</span><span class="sxs-lookup"><span data-stu-id="f156d-288">Chinese - Simplified</span></span>  | <span data-ttu-id="f156d-289">zh-hans</span><span class="sxs-lookup"><span data-stu-id="f156d-289">zh-hans</span></span>       |
| <span data-ttu-id="f156d-290">Chinese - Traditional</span><span class="sxs-lookup"><span data-stu-id="f156d-290">Chinese - Traditional</span></span> | <span data-ttu-id="f156d-291">zh-hant</span><span class="sxs-lookup"><span data-stu-id="f156d-291">zh-hant</span></span>       |
