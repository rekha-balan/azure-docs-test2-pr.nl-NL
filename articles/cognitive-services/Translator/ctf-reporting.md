---
title: Microsoft Translator Collaborative Translation Framework (CTF) Reporting
description: How to use Collaborative Translation Framework (CTF) reporting.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 2d7f5d64738ff62aa18e6bb5ae642bd01eae80cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871346"
---
# <a name="how-to-use-collaborative-translation-framework-ctf-reporting"></a><span data-ttu-id="f56f1-103">How to use Collaborative Translation Framework (CTF) reporting</span><span class="sxs-lookup"><span data-stu-id="f56f1-103">How to use Collaborative Translation Framework (CTF) reporting</span></span>

> [!NOTE]
> <span data-ttu-id="f56f1-104">This method is deprecated.</span><span class="sxs-lookup"><span data-stu-id="f56f1-104">This method is deprecated.</span></span> <span data-ttu-id="f56f1-105">It is not available in V3.0 of the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="f56f1-105">It is not available in V3.0 of the Translator Text API.</span></span>

> <span data-ttu-id="f56f1-106">The Collaborative Translations Framework (CTF), previously available for V2.0 of the Translator Text API, was deprecated as of February 1, 2018.</span><span class="sxs-lookup"><span data-stu-id="f56f1-106">The Collaborative Translations Framework (CTF), previously available for V2.0 of the Translator Text API, was deprecated as of February 1, 2018.</span></span> <span data-ttu-id="f56f1-107">The AddTranslation and AddTranslationArray functions let users enable corrections through the Collaborative Translation Framework.</span><span class="sxs-lookup"><span data-stu-id="f56f1-107">The AddTranslation and AddTranslationArray functions let users enable corrections through the Collaborative Translation Framework.</span></span> <span data-ttu-id="f56f1-108">After January 31, 2018, these two functions did not accept new sentence submissions, and users receive an error message.</span><span class="sxs-lookup"><span data-stu-id="f56f1-108">After January 31, 2018, these two functions did not accept new sentence submissions, and users receive an error message.</span></span> <span data-ttu-id="f56f1-109">These functions were being retired and will not be replaced.</span><span class="sxs-lookup"><span data-stu-id="f56f1-109">These functions were being retired and will not be replaced.</span></span> 

><span data-ttu-id="f56f1-110">Similar functionality is available in the Translator Hub API, allowing you to build a custom translation system with your terminology and style, and you can invoke it using the Category ID in the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="f56f1-110">Similar functionality is available in the Translator Hub API, allowing you to build a custom translation system with your terminology and style, and you can invoke it using the Category ID in the Translator Text API.</span></span> <span data-ttu-id="f56f1-111">Translator Hub: [https://hub.microsofttranslator.com](https://hub.microsofttranslator.com).</span><span class="sxs-lookup"><span data-stu-id="f56f1-111">Translator Hub: [https://hub.microsofttranslator.com](https://hub.microsofttranslator.com).</span></span> <span data-ttu-id="f56f1-112">Translator Hub API: [https://hub.microsofttranslator.com/swagger](https://hub.microsofttranslator.com/swagger).</span><span class="sxs-lookup"><span data-stu-id="f56f1-112">Translator Hub API: [https://hub.microsofttranslator.com/swagger](https://hub.microsofttranslator.com/swagger).</span></span>

<span data-ttu-id="f56f1-113">The Collaborative Translation Framework (CTF) Reporting API returns statistics and the actual content in the CTF store.</span><span class="sxs-lookup"><span data-stu-id="f56f1-113">The Collaborative Translation Framework (CTF) Reporting API returns statistics and the actual content in the CTF store.</span></span> <span data-ttu-id="f56f1-114">This API is different from the GetTranslations() method because it:</span><span class="sxs-lookup"><span data-stu-id="f56f1-114">This API is different from the GetTranslations() method because it:</span></span>
* <span data-ttu-id="f56f1-115">Returns the translated content and its total count only from your account (appId or Azure Marketplace account).</span><span class="sxs-lookup"><span data-stu-id="f56f1-115">Returns the translated content and its total count only from your account (appId or Azure Marketplace account).</span></span>
* <span data-ttu-id="f56f1-116">Returns the translated content and its total count without requiring a match of the source sentence.</span><span class="sxs-lookup"><span data-stu-id="f56f1-116">Returns the translated content and its total count without requiring a match of the source sentence.</span></span>
* <span data-ttu-id="f56f1-117">Does not return the automatic translation (machine translation).</span><span class="sxs-lookup"><span data-stu-id="f56f1-117">Does not return the automatic translation (machine translation).</span></span>

## <a name="endpoint"></a><span data-ttu-id="f56f1-118">Endpoint</span><span class="sxs-lookup"><span data-stu-id="f56f1-118">Endpoint</span></span>
<span data-ttu-id="f56f1-119">The endpoint of the CTF Reporting API is http://api.microsofttranslator.com/v2/beta/ctfreporting.svc</span><span class="sxs-lookup"><span data-stu-id="f56f1-119">The endpoint of the CTF Reporting API is http://api.microsofttranslator.com/v2/beta/ctfreporting.svc</span></span>
                        

## <a name="methods"></a><span data-ttu-id="f56f1-120">Methods</span><span class="sxs-lookup"><span data-stu-id="f56f1-120">Methods</span></span>
| <span data-ttu-id="f56f1-121">Name</span><span class="sxs-lookup"><span data-stu-id="f56f1-121">Name</span></span> |    <span data-ttu-id="f56f1-122">Description</span><span class="sxs-lookup"><span data-stu-id="f56f1-122">Description</span></span>|
|:---|:---|
| <span data-ttu-id="f56f1-123">GetUserTranslationCounts Method</span><span class="sxs-lookup"><span data-stu-id="f56f1-123">GetUserTranslationCounts Method</span></span> | <span data-ttu-id="f56f1-124">Get counts of the translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="f56f1-124">Get counts of the translations that are created by the user.</span></span> |
| <span data-ttu-id="f56f1-125">GetUserTranslations Method</span><span class="sxs-lookup"><span data-stu-id="f56f1-125">GetUserTranslations Method</span></span> | <span data-ttu-id="f56f1-126">Retrieves the translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="f56f1-126">Retrieves the translations that are created by the user.</span></span> |

<span data-ttu-id="f56f1-127">These methods enable you to:</span><span class="sxs-lookup"><span data-stu-id="f56f1-127">These methods enable you to:</span></span>
* <span data-ttu-id="f56f1-128">Retrieve the complete set of user translations and corrections under your account ID for download.</span><span class="sxs-lookup"><span data-stu-id="f56f1-128">Retrieve the complete set of user translations and corrections under your account ID for download.</span></span>
* <span data-ttu-id="f56f1-129">Obtain the list of the frequent contributors.</span><span class="sxs-lookup"><span data-stu-id="f56f1-129">Obtain the list of the frequent contributors.</span></span> <span data-ttu-id="f56f1-130">Ensure that the correct user name is provided in AddTranslation().</span><span class="sxs-lookup"><span data-stu-id="f56f1-130">Ensure that the correct user name is provided in AddTranslation().</span></span>
* <span data-ttu-id="f56f1-131">Build a user interface (UI) that allows your trusted users to see all available candidates, if necessary restricted to a portion of your site, based on the URI prefix.</span><span class="sxs-lookup"><span data-stu-id="f56f1-131">Build a user interface (UI) that allows your trusted users to see all available candidates, if necessary restricted to a portion of your site, based on the URI prefix.</span></span>

> [!NOTE]
> <span data-ttu-id="f56f1-132">Both the methods are relatively slow and expensive.</span><span class="sxs-lookup"><span data-stu-id="f56f1-132">Both the methods are relatively slow and expensive.</span></span> <span data-ttu-id="f56f1-133">It is recommended to use them sparingly.</span><span class="sxs-lookup"><span data-stu-id="f56f1-133">It is recommended to use them sparingly.</span></span>

## <a name="getusertranslationcounts-method"></a><span data-ttu-id="f56f1-134">GetUserTranslationCounts method</span><span class="sxs-lookup"><span data-stu-id="f56f1-134">GetUserTranslationCounts method</span></span>

<span data-ttu-id="f56f1-135">This method gets the count of translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="f56f1-135">This method gets the count of translations that are created by the user.</span></span> <span data-ttu-id="f56f1-136">It provides the list of translation counts grouped by the uriPrefix, from, to, user, minRating, and maxRating request parameters.</span><span class="sxs-lookup"><span data-stu-id="f56f1-136">It provides the list of translation counts grouped by the uriPrefix, from, to, user, minRating, and maxRating request parameters.</span></span>

<span data-ttu-id="f56f1-137">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f56f1-137">**Syntax**</span></span>

> [!div class="tabbedCodeSnippets"]
```cs
UserTranslationCount[]GetUserTranslationCounts(
           string appId,
           string uriPrefix,
           string from,
           string to,
           int? minRating,
           int? maxRating,
           string user, 
           string category
           DateTime? minDateUtc,
           DateTime? maxDateUtc,
           int? skip,
           int? take);
```

<span data-ttu-id="f56f1-138">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="f56f1-138">**Parameters**</span></span>

| <span data-ttu-id="f56f1-139">Parameter</span><span class="sxs-lookup"><span data-stu-id="f56f1-139">Parameter</span></span> | <span data-ttu-id="f56f1-140">Description</span><span class="sxs-lookup"><span data-stu-id="f56f1-140">Description</span></span> |
|:---|:---|
| <span data-ttu-id="f56f1-141">appId</span><span class="sxs-lookup"><span data-stu-id="f56f1-141">appId</span></span> | <span data-ttu-id="f56f1-142">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span><span class="sxs-lookup"><span data-stu-id="f56f1-142">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span></span>|
| <span data-ttu-id="f56f1-143">uriPrefix</span><span class="sxs-lookup"><span data-stu-id="f56f1-143">uriPrefix</span></span> | <span data-ttu-id="f56f1-144">**Optional** A string containing prefix of URI of the translation.</span><span class="sxs-lookup"><span data-stu-id="f56f1-144">**Optional** A string containing prefix of URI of the translation.</span></span>|
| <span data-ttu-id="f56f1-145">from</span><span class="sxs-lookup"><span data-stu-id="f56f1-145">from</span></span> | <span data-ttu-id="f56f1-146">**Optional** A string representing the language code of the translation text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-146">**Optional** A string representing the language code of the translation text.</span></span> |
| <span data-ttu-id="f56f1-147">to</span><span class="sxs-lookup"><span data-stu-id="f56f1-147">to</span></span> | <span data-ttu-id="f56f1-148">**Optional** A string representing the language code to translate the text into.</span><span class="sxs-lookup"><span data-stu-id="f56f1-148">**Optional** A string representing the language code to translate the text into.</span></span>|
| <span data-ttu-id="f56f1-149">minRating</span><span class="sxs-lookup"><span data-stu-id="f56f1-149">minRating</span></span>| <span data-ttu-id="f56f1-150">**Optional** An integer value representing the minimum quality rating for the translated text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-150">**Optional** An integer value representing the minimum quality rating for the translated text.</span></span> <span data-ttu-id="f56f1-151">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="f56f1-151">The valid value is between -10 and 10.</span></span> <span data-ttu-id="f56f1-152">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="f56f1-152">The default value is 1.</span></span>|
| <span data-ttu-id="f56f1-153">maxRating</span><span class="sxs-lookup"><span data-stu-id="f56f1-153">maxRating</span></span>| <span data-ttu-id="f56f1-154">**Optional** An integer value representing the maximum quality rating for the translated text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-154">**Optional** An integer value representing the maximum quality rating for the translated text.</span></span> <span data-ttu-id="f56f1-155">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="f56f1-155">The valid value is between -10 and 10.</span></span> <span data-ttu-id="f56f1-156">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="f56f1-156">The default value is 1.</span></span>|
| <span data-ttu-id="f56f1-157">user</span><span class="sxs-lookup"><span data-stu-id="f56f1-157">user</span></span> | <span data-ttu-id="f56f1-158">**Optional** A string that is used to filter the result based on the originator of the submission.</span><span class="sxs-lookup"><span data-stu-id="f56f1-158">**Optional** A string that is used to filter the result based on the originator of the submission.</span></span> |
| <span data-ttu-id="f56f1-159">category</span><span class="sxs-lookup"><span data-stu-id="f56f1-159">category</span></span>| <span data-ttu-id="f56f1-160">**Optional** A string containing the category or domain of the translation.</span><span class="sxs-lookup"><span data-stu-id="f56f1-160">**Optional** A string containing the category or domain of the translation.</span></span> <span data-ttu-id="f56f1-161">This parameter supports only the default option general.</span><span class="sxs-lookup"><span data-stu-id="f56f1-161">This parameter supports only the default option general.</span></span>|
| <span data-ttu-id="f56f1-162">minDateUtc</span><span class="sxs-lookup"><span data-stu-id="f56f1-162">minDateUtc</span></span>| <span data-ttu-id="f56f1-163">**Optional** The date from when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="f56f1-163">**Optional** The date from when you want to retrieve the translations.</span></span> <span data-ttu-id="f56f1-164">The date must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="f56f1-164">The date must be in the UTC format.</span></span> |
| <span data-ttu-id="f56f1-165">maxDateUtc</span><span class="sxs-lookup"><span data-stu-id="f56f1-165">maxDateUtc</span></span>| <span data-ttu-id="f56f1-166">**Optional** The date till when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="f56f1-166">**Optional** The date till when you want to retrieve the translations.</span></span> <span data-ttu-id="f56f1-167">The date must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="f56f1-167">The date must be in the UTC format.</span></span> |
| <span data-ttu-id="f56f1-168">skip</span><span class="sxs-lookup"><span data-stu-id="f56f1-168">skip</span></span>| <span data-ttu-id="f56f1-169">**Optional** The number of results that you want to skip on a page.</span><span class="sxs-lookup"><span data-stu-id="f56f1-169">**Optional** The number of results that you want to skip on a page.</span></span> <span data-ttu-id="f56f1-170">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span><span class="sxs-lookup"><span data-stu-id="f56f1-170">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span></span> <span data-ttu-id="f56f1-171">The default value for this parameter is 0.</span><span class="sxs-lookup"><span data-stu-id="f56f1-171">The default value for this parameter is 0.</span></span>|
| <span data-ttu-id="f56f1-172">take</span><span class="sxs-lookup"><span data-stu-id="f56f1-172">take</span></span> | <span data-ttu-id="f56f1-173">**Optional** The number of results that you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="f56f1-173">**Optional** The number of results that you want to retrieve.</span></span> <span data-ttu-id="f56f1-174">The maximum number of each request is 100.</span><span class="sxs-lookup"><span data-stu-id="f56f1-174">The maximum number of each request is 100.</span></span> <span data-ttu-id="f56f1-175">The default is 100.</span><span class="sxs-lookup"><span data-stu-id="f56f1-175">The default is 100.</span></span>|

> [!NOTE]
> <span data-ttu-id="f56f1-176">The skip and take request parameters enable pagination for a large number of result records.</span><span class="sxs-lookup"><span data-stu-id="f56f1-176">The skip and take request parameters enable pagination for a large number of result records.</span></span>

<span data-ttu-id="f56f1-177">**Return value**</span><span class="sxs-lookup"><span data-stu-id="f56f1-177">**Return value**</span></span>

<span data-ttu-id="f56f1-178">The result set contains array of the **UserTranslationCount**.</span><span class="sxs-lookup"><span data-stu-id="f56f1-178">The result set contains array of the **UserTranslationCount**.</span></span> <span data-ttu-id="f56f1-179">Each UserTranslationCount has the following elements:</span><span class="sxs-lookup"><span data-stu-id="f56f1-179">Each UserTranslationCount has the following elements:</span></span>

| <span data-ttu-id="f56f1-180">Field</span><span class="sxs-lookup"><span data-stu-id="f56f1-180">Field</span></span> | <span data-ttu-id="f56f1-181">Description</span><span class="sxs-lookup"><span data-stu-id="f56f1-181">Description</span></span> |
|:---|:---|
| <span data-ttu-id="f56f1-182">Count</span><span class="sxs-lookup"><span data-stu-id="f56f1-182">Count</span></span>| <span data-ttu-id="f56f1-183">The number of results that is retrieved</span><span class="sxs-lookup"><span data-stu-id="f56f1-183">The number of results that is retrieved</span></span>|
| <span data-ttu-id="f56f1-184">From</span><span class="sxs-lookup"><span data-stu-id="f56f1-184">From</span></span> | <span data-ttu-id="f56f1-185">The source language</span><span class="sxs-lookup"><span data-stu-id="f56f1-185">The source language</span></span>|
| <span data-ttu-id="f56f1-186">Rating</span><span class="sxs-lookup"><span data-stu-id="f56f1-186">Rating</span></span>| <span data-ttu-id="f56f1-187">The rating that is applied by the submitter in the AddTranslation() method call</span><span class="sxs-lookup"><span data-stu-id="f56f1-187">The rating that is applied by the submitter in the AddTranslation() method call</span></span>|
| <span data-ttu-id="f56f1-188">To</span><span class="sxs-lookup"><span data-stu-id="f56f1-188">To</span></span>| <span data-ttu-id="f56f1-189">The target language</span><span class="sxs-lookup"><span data-stu-id="f56f1-189">The target language</span></span>|
| <span data-ttu-id="f56f1-190">Uri</span><span class="sxs-lookup"><span data-stu-id="f56f1-190">Uri</span></span>| <span data-ttu-id="f56f1-191">The URI applied in the AddTranslation() method call</span><span class="sxs-lookup"><span data-stu-id="f56f1-191">The URI applied in the AddTranslation() method call</span></span>|
| <span data-ttu-id="f56f1-192">User</span><span class="sxs-lookup"><span data-stu-id="f56f1-192">User</span></span>| <span data-ttu-id="f56f1-193">The user name</span><span class="sxs-lookup"><span data-stu-id="f56f1-193">The user name</span></span>|

<span data-ttu-id="f56f1-194">**Exceptions**</span><span class="sxs-lookup"><span data-stu-id="f56f1-194">**Exceptions**</span></span>

| <span data-ttu-id="f56f1-195">Exception</span><span class="sxs-lookup"><span data-stu-id="f56f1-195">Exception</span></span> | <span data-ttu-id="f56f1-196">Message</span><span class="sxs-lookup"><span data-stu-id="f56f1-196">Message</span></span> | <span data-ttu-id="f56f1-197">Conditions</span><span class="sxs-lookup"><span data-stu-id="f56f1-197">Conditions</span></span> |
|:---|:---|:---|
| <span data-ttu-id="f56f1-198">ArgumentOutOfRangeException</span><span class="sxs-lookup"><span data-stu-id="f56f1-198">ArgumentOutOfRangeException</span></span> | <span data-ttu-id="f56f1-199">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span><span class="sxs-lookup"><span data-stu-id="f56f1-199">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span></span>| <span data-ttu-id="f56f1-200">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span><span class="sxs-lookup"><span data-stu-id="f56f1-200">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span></span>|
| <span data-ttu-id="f56f1-201">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="f56f1-201">TranslateApiException</span></span> | <span data-ttu-id="f56f1-202">IP is over the quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-202">IP is over the quota.</span></span>| <ul><li><span data-ttu-id="f56f1-203">The limit for the number of requests per minute is reached.</span><span class="sxs-lookup"><span data-stu-id="f56f1-203">The limit for the number of requests per minute is reached.</span></span></li><li><span data-ttu-id="f56f1-204">The request size remains limited at 10000 characters.</span><span class="sxs-lookup"><span data-stu-id="f56f1-204">The request size remains limited at 10000 characters.</span></span></li><li><span data-ttu-id="f56f1-205">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span><span class="sxs-lookup"><span data-stu-id="f56f1-205">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span></span></li></ul>|
| <span data-ttu-id="f56f1-206">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="f56f1-206">TranslateApiException</span></span> | <span data-ttu-id="f56f1-207">AppId is over the quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-207">AppId is over the quota.</span></span>| <span data-ttu-id="f56f1-208">The application ID exceeded the hourly or daily quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-208">The application ID exceeded the hourly or daily quota.</span></span>|

> [!NOTE]
> <span data-ttu-id="f56f1-209">The quota will adjust to ensure fairness among all users of the service.</span><span class="sxs-lookup"><span data-stu-id="f56f1-209">The quota will adjust to ensure fairness among all users of the service.</span></span>

<span data-ttu-id="f56f1-210">**View code examples on GitHib**</span><span class="sxs-lookup"><span data-stu-id="f56f1-210">**View code examples on GitHib**</span></span>
* [<span data-ttu-id="f56f1-211">C#</span><span class="sxs-lookup"><span data-stu-id="f56f1-211">C#</span></span>](https://github.com/MicrosoftTranslator/Documentation-Code-TextAPI/blob/master/ctf/ctf-getusertranslationcounts-example-csharp.md)
* [<span data-ttu-id="f56f1-212">PHP</span><span class="sxs-lookup"><span data-stu-id="f56f1-212">PHP</span></span>](https://github.com/MicrosoftTranslator/Documentation-Code-TextAPI/blob/master/ctf/ctf-getusertranslationcounts-example-php.md)

## <a name="getusertranslations-method"></a><span data-ttu-id="f56f1-213">GetUserTranslations method</span><span class="sxs-lookup"><span data-stu-id="f56f1-213">GetUserTranslations method</span></span>

<span data-ttu-id="f56f1-214">This method retrieves the translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="f56f1-214">This method retrieves the translations that are created by the user.</span></span> <span data-ttu-id="f56f1-215">It provides the translations grouped by the uriPrefix, from, to, user, and minRating and maxRating request parameters.</span><span class="sxs-lookup"><span data-stu-id="f56f1-215">It provides the translations grouped by the uriPrefix, from, to, user, and minRating and maxRating request parameters.</span></span>

<span data-ttu-id="f56f1-216">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f56f1-216">**Syntax**</span></span>

> [!div class="tabbedCodeSnippets"]
```cs
UserTranslation[] GetUserTranslations (
            string appId,
            string uriPrefix,
            string from,
            string to,
            int? minRating,
            int? maxRating,
            string user, 
            string category
            DateTime? minDateUtc,
            DateTime? maxDateUtc,
            int? skip,
            int? take); 
```

<span data-ttu-id="f56f1-217">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="f56f1-217">**Parameters**</span></span>

| <span data-ttu-id="f56f1-218">Parameter</span><span class="sxs-lookup"><span data-stu-id="f56f1-218">Parameter</span></span> | <span data-ttu-id="f56f1-219">Description</span><span class="sxs-lookup"><span data-stu-id="f56f1-219">Description</span></span> |
|:---|:---|
| <span data-ttu-id="f56f1-220">appId</span><span class="sxs-lookup"><span data-stu-id="f56f1-220">appId</span></span> | <span data-ttu-id="f56f1-221">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span><span class="sxs-lookup"><span data-stu-id="f56f1-221">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span></span>|
| <span data-ttu-id="f56f1-222">uriPrefix</span><span class="sxs-lookup"><span data-stu-id="f56f1-222">uriPrefix</span></span>| <span data-ttu-id="f56f1-223">**Optional** A string containing prefix of URI of the translation.</span><span class="sxs-lookup"><span data-stu-id="f56f1-223">**Optional** A string containing prefix of URI of the translation.</span></span>|
| <span data-ttu-id="f56f1-224">from</span><span class="sxs-lookup"><span data-stu-id="f56f1-224">from</span></span>| <span data-ttu-id="f56f1-225">**Optional** A string representing the language code of the translation text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-225">**Optional** A string representing the language code of the translation text.</span></span>|
| <span data-ttu-id="f56f1-226">to</span><span class="sxs-lookup"><span data-stu-id="f56f1-226">to</span></span>| <span data-ttu-id="f56f1-227">**Optional** A string representing the language code to translate the text into.</span><span class="sxs-lookup"><span data-stu-id="f56f1-227">**Optional** A string representing the language code to translate the text into.</span></span>|
| <span data-ttu-id="f56f1-228">minRating</span><span class="sxs-lookup"><span data-stu-id="f56f1-228">minRating</span></span>| <span data-ttu-id="f56f1-229">**Optional** An integer value representing the minimum quality rating for the translated text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-229">**Optional** An integer value representing the minimum quality rating for the translated text.</span></span> <span data-ttu-id="f56f1-230">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="f56f1-230">The valid value is between -10 and 10.</span></span> <span data-ttu-id="f56f1-231">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="f56f1-231">The default value is 1.</span></span>|
| <span data-ttu-id="f56f1-232">maxRating</span><span class="sxs-lookup"><span data-stu-id="f56f1-232">maxRating</span></span>| <span data-ttu-id="f56f1-233">**Optional** An integer value representing the maximum quality rating for the translated text.</span><span class="sxs-lookup"><span data-stu-id="f56f1-233">**Optional** An integer value representing the maximum quality rating for the translated text.</span></span> <span data-ttu-id="f56f1-234">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="f56f1-234">The valid value is between -10 and 10.</span></span> <span data-ttu-id="f56f1-235">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="f56f1-235">The default value is 1.</span></span>|
| <span data-ttu-id="f56f1-236">user</span><span class="sxs-lookup"><span data-stu-id="f56f1-236">user</span></span>| <span data-ttu-id="f56f1-237">**Optional. A string that is used to filter the result based on the originator of the submission**</span><span class="sxs-lookup"><span data-stu-id="f56f1-237">**Optional. A string that is used to filter the result based on the originator of the submission**</span></span>|
| <span data-ttu-id="f56f1-238">category</span><span class="sxs-lookup"><span data-stu-id="f56f1-238">category</span></span>| <span data-ttu-id="f56f1-239">**Optional** A string containing the category or domain of the translation.</span><span class="sxs-lookup"><span data-stu-id="f56f1-239">**Optional** A string containing the category or domain of the translation.</span></span> <span data-ttu-id="f56f1-240">This parameter supports only the default option general.</span><span class="sxs-lookup"><span data-stu-id="f56f1-240">This parameter supports only the default option general.</span></span>| 
| <span data-ttu-id="f56f1-241">minDateUtc</span><span class="sxs-lookup"><span data-stu-id="f56f1-241">minDateUtc</span></span>| <span data-ttu-id="f56f1-242">**Optional** The date from when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="f56f1-242">**Optional** The date from when you want to retrieve the translations.</span></span> <span data-ttu-id="f56f1-243">The date must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="f56f1-243">The date must be in the UTC format.</span></span>| 
| <span data-ttu-id="f56f1-244">maxDateUtc</span><span class="sxs-lookup"><span data-stu-id="f56f1-244">maxDateUtc</span></span>| <span data-ttu-id="f56f1-245">**Optional** The date till when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="f56f1-245">**Optional** The date till when you want to retrieve the translations.</span></span> <span data-ttu-id="f56f1-246">The date must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="f56f1-246">The date must be in the UTC format.</span></span>|
| <span data-ttu-id="f56f1-247">skip</span><span class="sxs-lookup"><span data-stu-id="f56f1-247">skip</span></span>| <span data-ttu-id="f56f1-248">**Optional** The number of results that you want to skip on a page.</span><span class="sxs-lookup"><span data-stu-id="f56f1-248">**Optional** The number of results that you want to skip on a page.</span></span> <span data-ttu-id="f56f1-249">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span><span class="sxs-lookup"><span data-stu-id="f56f1-249">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span></span> <span data-ttu-id="f56f1-250">The default value for this parameter is 0.</span><span class="sxs-lookup"><span data-stu-id="f56f1-250">The default value for this parameter is 0.</span></span>|
| <span data-ttu-id="f56f1-251">take</span><span class="sxs-lookup"><span data-stu-id="f56f1-251">take</span></span>| <span data-ttu-id="f56f1-252">**Optional** The number of results that you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="f56f1-252">**Optional** The number of results that you want to retrieve.</span></span> <span data-ttu-id="f56f1-253">The maximum number of each request is 100.</span><span class="sxs-lookup"><span data-stu-id="f56f1-253">The maximum number of each request is 100.</span></span> <span data-ttu-id="f56f1-254">The default is 50.</span><span class="sxs-lookup"><span data-stu-id="f56f1-254">The default is 50.</span></span>|

> [!NOTE]
> <span data-ttu-id="f56f1-255">The skip and take request parameters enable pagination for a large number of result records.</span><span class="sxs-lookup"><span data-stu-id="f56f1-255">The skip and take request parameters enable pagination for a large number of result records.</span></span>

<span data-ttu-id="f56f1-256">**Return value**</span><span class="sxs-lookup"><span data-stu-id="f56f1-256">**Return value**</span></span>

<span data-ttu-id="f56f1-257">The result set contains array of the **UserTranslation**.</span><span class="sxs-lookup"><span data-stu-id="f56f1-257">The result set contains array of the **UserTranslation**.</span></span> <span data-ttu-id="f56f1-258">Each UserTranslation has the following elements:</span><span class="sxs-lookup"><span data-stu-id="f56f1-258">Each UserTranslation has the following elements:</span></span>

| <span data-ttu-id="f56f1-259">Field</span><span class="sxs-lookup"><span data-stu-id="f56f1-259">Field</span></span> | <span data-ttu-id="f56f1-260">Description</span><span class="sxs-lookup"><span data-stu-id="f56f1-260">Description</span></span> |
|:---|:---|
| <span data-ttu-id="f56f1-261">CreatedDateUtc</span><span class="sxs-lookup"><span data-stu-id="f56f1-261">CreatedDateUtc</span></span>| <span data-ttu-id="f56f1-262">The creation date of the entry using AddTranslation()</span><span class="sxs-lookup"><span data-stu-id="f56f1-262">The creation date of the entry using AddTranslation()</span></span>|
| <span data-ttu-id="f56f1-263">From</span><span class="sxs-lookup"><span data-stu-id="f56f1-263">From</span></span>| <span data-ttu-id="f56f1-264">The source language</span><span class="sxs-lookup"><span data-stu-id="f56f1-264">The source language</span></span>|
| <span data-ttu-id="f56f1-265">OriginalText</span><span class="sxs-lookup"><span data-stu-id="f56f1-265">OriginalText</span></span>| <span data-ttu-id="f56f1-266">The source language text that is used when submitting the request</span><span class="sxs-lookup"><span data-stu-id="f56f1-266">The source language text that is used when submitting the request</span></span>|
|<span data-ttu-id="f56f1-267">Rating</span><span class="sxs-lookup"><span data-stu-id="f56f1-267">Rating</span></span> |<span data-ttu-id="f56f1-268">The rating that is applied by the submitter in the AddTranslation() method call</span><span class="sxs-lookup"><span data-stu-id="f56f1-268">The rating that is applied by the submitter in the AddTranslation() method call</span></span>|
|<span data-ttu-id="f56f1-269">To</span><span class="sxs-lookup"><span data-stu-id="f56f1-269">To</span></span>|    <span data-ttu-id="f56f1-270">The target language</span><span class="sxs-lookup"><span data-stu-id="f56f1-270">The target language</span></span>|
|<span data-ttu-id="f56f1-271">TranslatedText</span><span class="sxs-lookup"><span data-stu-id="f56f1-271">TranslatedText</span></span>|    <span data-ttu-id="f56f1-272">The translation as submitted in the AddTranslation() method call</span><span class="sxs-lookup"><span data-stu-id="f56f1-272">The translation as submitted in the AddTranslation() method call</span></span>|
|<span data-ttu-id="f56f1-273">Uri</span><span class="sxs-lookup"><span data-stu-id="f56f1-273">Uri</span></span>|   <span data-ttu-id="f56f1-274">The URI applied in the AddTranslation() method call</span><span class="sxs-lookup"><span data-stu-id="f56f1-274">The URI applied in the AddTranslation() method call</span></span>|
|<span data-ttu-id="f56f1-275">User</span><span class="sxs-lookup"><span data-stu-id="f56f1-275">User</span></span>   |<span data-ttu-id="f56f1-276">The user name</span><span class="sxs-lookup"><span data-stu-id="f56f1-276">The user name</span></span>|

<span data-ttu-id="f56f1-277">**Exceptions**</span><span class="sxs-lookup"><span data-stu-id="f56f1-277">**Exceptions**</span></span>

| <span data-ttu-id="f56f1-278">Exception</span><span class="sxs-lookup"><span data-stu-id="f56f1-278">Exception</span></span> | <span data-ttu-id="f56f1-279">Message</span><span class="sxs-lookup"><span data-stu-id="f56f1-279">Message</span></span> | <span data-ttu-id="f56f1-280">Conditions</span><span class="sxs-lookup"><span data-stu-id="f56f1-280">Conditions</span></span> |
|:---|:---|:---|
| <span data-ttu-id="f56f1-281">ArgumentOutOfRangeException</span><span class="sxs-lookup"><span data-stu-id="f56f1-281">ArgumentOutOfRangeException</span></span> | <span data-ttu-id="f56f1-282">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span><span class="sxs-lookup"><span data-stu-id="f56f1-282">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span></span>| <span data-ttu-id="f56f1-283">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span><span class="sxs-lookup"><span data-stu-id="f56f1-283">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span></span>|
| <span data-ttu-id="f56f1-284">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="f56f1-284">TranslateApiException</span></span> | <span data-ttu-id="f56f1-285">IP is over the quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-285">IP is over the quota.</span></span>| <ul><li><span data-ttu-id="f56f1-286">The limit for the number of requests per minute is reached.</span><span class="sxs-lookup"><span data-stu-id="f56f1-286">The limit for the number of requests per minute is reached.</span></span></li><li><span data-ttu-id="f56f1-287">The request size remains limited at 10000 characters.</span><span class="sxs-lookup"><span data-stu-id="f56f1-287">The request size remains limited at 10000 characters.</span></span></li><li><span data-ttu-id="f56f1-288">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span><span class="sxs-lookup"><span data-stu-id="f56f1-288">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span></span></li></ul>|
| <span data-ttu-id="f56f1-289">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="f56f1-289">TranslateApiException</span></span> | <span data-ttu-id="f56f1-290">AppId is over the quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-290">AppId is over the quota.</span></span>| <span data-ttu-id="f56f1-291">The application ID exceeded the hourly or daily quota.</span><span class="sxs-lookup"><span data-stu-id="f56f1-291">The application ID exceeded the hourly or daily quota.</span></span>|

> [!NOTE]
> <span data-ttu-id="f56f1-292">The quota will adjust to ensure fairness among all users of the service.</span><span class="sxs-lookup"><span data-stu-id="f56f1-292">The quota will adjust to ensure fairness among all users of the service.</span></span>

<span data-ttu-id="f56f1-293">**View code examples on GitHib**</span><span class="sxs-lookup"><span data-stu-id="f56f1-293">**View code examples on GitHib**</span></span>
* [<span data-ttu-id="f56f1-294">C#</span><span class="sxs-lookup"><span data-stu-id="f56f1-294">C#</span></span>](https://github.com/MicrosoftTranslator/Documentation-Code-TextAPI/blob/master/ctf/ctf-getusertranslations-example-csharp.md)
* [<span data-ttu-id="f56f1-295">PHP</span><span class="sxs-lookup"><span data-stu-id="f56f1-295">PHP</span></span>](https://github.com/MicrosoftTranslator/Documentation-Code-TextAPI/blob/master/ctf/ctf-getusertranslations-example-php.md)


















