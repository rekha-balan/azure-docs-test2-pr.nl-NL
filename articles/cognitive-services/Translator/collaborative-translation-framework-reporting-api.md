---
title: Collaborative Translation Framework (CTF) Reporting API | Microsoft Docs
description: Use Collaborative Translation Framework (CTF) Reporting API to return statistics and the actual content in the CTF store.
services: cognitive-services
author: chriswendt1
manager: arulm
ms.service: cognitive-services
ms.technology: translator
ms.topic: article
ms.date: 10/26/2016
ms.author: christw
ms.openlocfilehash: 2ecddb21b3339f4b9299565906a847c3b873095e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553848"
---
# <a name="collaborative-translation-framework-ctf-reporting-api"></a><span data-ttu-id="1ca49-103">Collaborative Translation Framework (CTF) Reporting API</span><span class="sxs-lookup"><span data-stu-id="1ca49-103">Collaborative Translation Framework (CTF) Reporting API</span></span>

<span data-ttu-id="1ca49-104">The Collaborative Translation Framework (CTF) Reporting API returns statistics and the actual content in the CTF store.</span><span class="sxs-lookup"><span data-stu-id="1ca49-104">The Collaborative Translation Framework (CTF) Reporting API returns statistics and the actual content in the CTF store.</span></span> <span data-ttu-id="1ca49-105">This API is different from the GetTranslations() method because it:</span><span class="sxs-lookup"><span data-stu-id="1ca49-105">This API is different from the GetTranslations() method because it:</span></span> 

 * <span data-ttu-id="1ca49-106">Returns the translated content and its total count only from your account (appId or Azure Marketplace account).</span><span class="sxs-lookup"><span data-stu-id="1ca49-106">Returns the translated content and its total count only from your account (appId or Azure Marketplace account).</span></span> 
 * <span data-ttu-id="1ca49-107">Returns the translated content and its total count without requiring a match of the source sentence.</span><span class="sxs-lookup"><span data-stu-id="1ca49-107">Returns the translated content and its total count without requiring a match of the source sentence.</span></span>
 * <span data-ttu-id="1ca49-108">Does not return the automatic translation (machine translation).</span><span class="sxs-lookup"><span data-stu-id="1ca49-108">Does not return the automatic translation (machine translation).</span></span>

<span data-ttu-id="1ca49-109">**Endpoint** The endpoint of the CTF Reporting API is</span><span class="sxs-lookup"><span data-stu-id="1ca49-109">**Endpoint** The endpoint of the CTF Reporting API is</span></span> 

http://api.microsofttranslator.com/v2/beta/ctfreporting.svc

<span data-ttu-id="1ca49-110">**Methods**</span><span class="sxs-lookup"><span data-stu-id="1ca49-110">**Methods**</span></span>

| <span data-ttu-id="1ca49-111">Name</span><span class="sxs-lookup"><span data-stu-id="1ca49-111">Name</span></span>                                                                                      | <span data-ttu-id="1ca49-112">Description</span><span class="sxs-lookup"><span data-stu-id="1ca49-112">Description</span></span>                                                 |
|-------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| <span data-ttu-id="1ca49-113">GetUserTranslationCounts Method</span><span class="sxs-lookup"><span data-stu-id="1ca49-113">GetUserTranslationCounts Method</span></span>                                                           | <span data-ttu-id="1ca49-114">Get counts of the translations that are created by the user</span><span class="sxs-lookup"><span data-stu-id="1ca49-114">Get counts of the translations that are created by the user</span></span> |
| <span data-ttu-id="1ca49-115">GetUserTranslations Method</span><span class="sxs-lookup"><span data-stu-id="1ca49-115">GetUserTranslations Method</span></span>                                                                | <span data-ttu-id="1ca49-116">Retrieves the translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="1ca49-116">Retrieves the translations that are created by the user.</span></span>    |

<span data-ttu-id="1ca49-117">**Remarks** These methods enable you to:</span><span class="sxs-lookup"><span data-stu-id="1ca49-117">**Remarks** These methods enable you to:</span></span> 
 * <span data-ttu-id="1ca49-118">Retrieve the complete set of user translations and corrections under your account ID for download.</span><span class="sxs-lookup"><span data-stu-id="1ca49-118">Retrieve the complete set of user translations and corrections under your account ID for download.</span></span>
 * <span data-ttu-id="1ca49-119">Obtain the list of the frequent contributors.</span><span class="sxs-lookup"><span data-stu-id="1ca49-119">Obtain the list of the frequent contributors.</span></span> <span data-ttu-id="1ca49-120">Ensure that the correct user name is provided in AddTranslation().</span><span class="sxs-lookup"><span data-stu-id="1ca49-120">Ensure that the correct user name is provided in AddTranslation().</span></span>
 * <span data-ttu-id="1ca49-121">Build a user interface (UI) that allows your trusted users to see all available candidates, if necessary restricted to a portion of your site, based on the URI prefix.</span><span class="sxs-lookup"><span data-stu-id="1ca49-121">Build a user interface (UI) that allows your trusted users to see all available candidates, if necessary restricted to a portion of your site, based on the URI prefix.</span></span>
 
>[!NOTE]
><span data-ttu-id="1ca49-122">Both the methods are relatively slow and expensive.</span><span class="sxs-lookup"><span data-stu-id="1ca49-122">Both the methods are relatively slow and expensive.</span></span> <span data-ttu-id="1ca49-123">It is recommended to use them sparingly.</span><span class="sxs-lookup"><span data-stu-id="1ca49-123">It is recommended to use them sparingly.</span></span> 

 
<span data-ttu-id="1ca49-124">**GetUserTranslations Method**</span><span class="sxs-lookup"><span data-stu-id="1ca49-124">**GetUserTranslations Method**</span></span>

<span data-ttu-id="1ca49-125">This method retrieves the translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="1ca49-125">This method retrieves the translations that are created by the user.</span></span> <span data-ttu-id="1ca49-126">It provides the translations grouped by the uriPrefix, from, to, user, and minrating and maxRating request parameters.</span><span class="sxs-lookup"><span data-stu-id="1ca49-126">It provides the translations grouped by the uriPrefix, from, to, user, and minrating and maxRating request parameters.</span></span> 

<span data-ttu-id="1ca49-127">Syntax</span><span class="sxs-lookup"><span data-stu-id="1ca49-127">Syntax</span></span> 

<span data-ttu-id="1ca49-128">**C#**</span><span class="sxs-lookup"><span data-stu-id="1ca49-128">**C#**</span></span>

<span data-ttu-id="1ca49-129">UserTranslation[] GetUserTranslations ( string appId, string uriPrefix, string from, string to, int? minRating, int? maxRating, string user, string category DateTime? minDateUtc, DateTime? maxDateUtc, int? skip, int? take);</span><span class="sxs-lookup"><span data-stu-id="1ca49-129">UserTranslation[] GetUserTranslations ( string appId, string uriPrefix, string from, string to, int? minRating, int? maxRating, string user, string category DateTime? minDateUtc, DateTime? maxDateUtc, int? skip, int? take);</span></span>
            
<span data-ttu-id="1ca49-130">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="1ca49-130">**Parameters**</span></span>

| <span data-ttu-id="1ca49-131">Parameter</span><span class="sxs-lookup"><span data-stu-id="1ca49-131">Parameter</span></span>  | <span data-ttu-id="1ca49-132">Description</span><span class="sxs-lookup"><span data-stu-id="1ca49-132">Description</span></span>                                                                                                                                                                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ca49-133">appId</span><span class="sxs-lookup"><span data-stu-id="1ca49-133">appId</span></span>      | <span data-ttu-id="1ca49-134">**Required**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-134">**Required**.</span></span> <span data-ttu-id="1ca49-135">If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span><span class="sxs-lookup"><span data-stu-id="1ca49-135">If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span></span>                                                                                                          |
| <span data-ttu-id="1ca49-136">uriPrefix</span><span class="sxs-lookup"><span data-stu-id="1ca49-136">uriPrefix</span></span>  | <span data-ttu-id="1ca49-137">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-137">**Optional**.</span></span> <span data-ttu-id="1ca49-138">A string containing prefix of URI of the translation.</span><span class="sxs-lookup"><span data-stu-id="1ca49-138">A string containing prefix of URI of the translation.</span></span>                                                                                                                                                                                     |
| <span data-ttu-id="1ca49-139">from</span><span class="sxs-lookup"><span data-stu-id="1ca49-139">from</span></span>       | <span data-ttu-id="1ca49-140">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-140">**Optional**.</span></span> <span data-ttu-id="1ca49-141">A string representing the language code of the translation text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-141">A string representing the language code of the translation text.</span></span>                                                                                                                                                                          |
| <span data-ttu-id="1ca49-142">to</span><span class="sxs-lookup"><span data-stu-id="1ca49-142">to</span></span>         | <span data-ttu-id="1ca49-143">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-143">**Optional**.</span></span> <span data-ttu-id="1ca49-144">A string representing the language code to translate the text into.</span><span class="sxs-lookup"><span data-stu-id="1ca49-144">A string representing the language code to translate the text into.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="1ca49-145">minRating</span><span class="sxs-lookup"><span data-stu-id="1ca49-145">minRating</span></span>  | <span data-ttu-id="1ca49-146">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-146">**Optional**.</span></span> <span data-ttu-id="1ca49-147">An integer value representing the minimum quality rating for the,translated text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-147">An integer value representing the minimum quality rating for the,translated text.</span></span> <span data-ttu-id="1ca49-148">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="1ca49-148">The valid value is between -10 and 10.</span></span> <span data-ttu-id="1ca49-149">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="1ca49-149">The default value is 1.</span></span>                                                                                          |
| <span data-ttu-id="1ca49-150">maxRating</span><span class="sxs-lookup"><span data-stu-id="1ca49-150">maxRating</span></span>  | <span data-ttu-id="1ca49-151">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-151">**Optional**.</span></span> <span data-ttu-id="1ca49-152">An integer value representing the maximum quality rating for the,translated text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-152">An integer value representing the maximum quality rating for the,translated text.</span></span> <span data-ttu-id="1ca49-153">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="1ca49-153">The valid value is between -10 and 10.</span></span> <span data-ttu-id="1ca49-154">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="1ca49-154">The default value is 1.</span></span>                                                                                          |
| <span data-ttu-id="1ca49-155">user</span><span class="sxs-lookup"><span data-stu-id="1ca49-155">user</span></span>       | <span data-ttu-id="1ca49-156">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-156">**Optional**.</span></span> <span data-ttu-id="1ca49-157">A string that is used to filter the result based on the originator,of the submission.</span><span class="sxs-lookup"><span data-stu-id="1ca49-157">A string that is used to filter the result based on the originator,of the submission.</span></span>                                                                                                                                                     |
| <span data-ttu-id="1ca49-158">category</span><span class="sxs-lookup"><span data-stu-id="1ca49-158">category</span></span>   | <span data-ttu-id="1ca49-159">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-159">**Optional**.</span></span> <span data-ttu-id="1ca49-160">A string containing the category or domain of the translation.,This parameter supports only the default option general.</span><span class="sxs-lookup"><span data-stu-id="1ca49-160">A string containing the category or domain of the translation.,This parameter supports only the default option general.</span></span>                                                                                                                   |
| <span data-ttu-id="1ca49-161">minDateUtc</span><span class="sxs-lookup"><span data-stu-id="1ca49-161">minDateUtc</span></span> | <span data-ttu-id="1ca49-162">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-162">**Optional**.</span></span> <span data-ttu-id="1ca49-163">The date from when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="1ca49-163">The date from when you want to retrieve the translations.</span></span> <span data-ttu-id="1ca49-164">The date,must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="1ca49-164">The date,must be in the UTC format.</span></span>                                                                                                                                             |
| <span data-ttu-id="1ca49-165">maxDateUtc</span><span class="sxs-lookup"><span data-stu-id="1ca49-165">maxDateUtc</span></span> | <span data-ttu-id="1ca49-166">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-166">**Optional**.</span></span> <span data-ttu-id="1ca49-167">The date till when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="1ca49-167">The date till when you want to retrieve the translations.</span></span> <span data-ttu-id="1ca49-168">The date must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="1ca49-168">The date must be in the UTC format.</span></span>                                                                                                                                             |
| <span data-ttu-id="1ca49-169">skip</span><span class="sxs-lookup"><span data-stu-id="1ca49-169">skip</span></span>       | <span data-ttu-id="1ca49-170">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-170">**Optional**.</span></span> <span data-ttu-id="1ca49-171">The number of results that you want to skip on a page.</span><span class="sxs-lookup"><span data-stu-id="1ca49-171">The number of results that you want to skip on a page.</span></span> <span data-ttu-id="1ca49-172">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span><span class="sxs-lookup"><span data-stu-id="1ca49-172">For example, if you want the skip the first 20 rows of the results and view from the 21st result record, specify 20 for this parameter.</span></span> <span data-ttu-id="1ca49-173">The default value for this parameter is 0.</span><span class="sxs-lookup"><span data-stu-id="1ca49-173">The default value for this parameter is 0.</span></span> |
| <span data-ttu-id="1ca49-174">take</span><span class="sxs-lookup"><span data-stu-id="1ca49-174">take</span></span>       | <span data-ttu-id="1ca49-175">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-175">**Optional**.</span></span> <span data-ttu-id="1ca49-176">The number of results that you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="1ca49-176">The number of results that you want to retrieve.</span></span> <span data-ttu-id="1ca49-177">The maximum number of each request is 100.</span><span class="sxs-lookup"><span data-stu-id="1ca49-177">The maximum number of each request is 100.</span></span> <span data-ttu-id="1ca49-178">The default is 50.</span><span class="sxs-lookup"><span data-stu-id="1ca49-178">The default is 50.</span></span>                                                                                                                            |

>[!NOTE]
><span data-ttu-id="1ca49-179">The skip and take request parameters enable pagination for a large number of result records.</span><span class="sxs-lookup"><span data-stu-id="1ca49-179">The skip and take request parameters enable pagination for a large number of result records.</span></span> 

<span data-ttu-id="1ca49-180">**Return Value**</span><span class="sxs-lookup"><span data-stu-id="1ca49-180">**Return Value**</span></span>

<span data-ttu-id="1ca49-181">The result set contains array of the **UserTranslation**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-181">The result set contains array of the **UserTranslation**.</span></span> <span data-ttu-id="1ca49-182">Each UserTranslation has the following elements:</span><span class="sxs-lookup"><span data-stu-id="1ca49-182">Each UserTranslation has the following elements:</span></span> 

| <span data-ttu-id="1ca49-183">Field</span><span class="sxs-lookup"><span data-stu-id="1ca49-183">Field</span></span>          | <span data-ttu-id="1ca49-184">Description</span><span class="sxs-lookup"><span data-stu-id="1ca49-184">Description</span></span>                                                                      |
|----------------|----------------------------------------------------------------------------------|
| <span data-ttu-id="1ca49-185">CreatedDateUtc</span><span class="sxs-lookup"><span data-stu-id="1ca49-185">CreatedDateUtc</span></span> | <span data-ttu-id="1ca49-186">The creation date of the entry using AddTranslation().</span><span class="sxs-lookup"><span data-stu-id="1ca49-186">The creation date of the entry using AddTranslation().</span></span>                           |
| <span data-ttu-id="1ca49-187">From</span><span class="sxs-lookup"><span data-stu-id="1ca49-187">From</span></span>           | <span data-ttu-id="1ca49-188">The source language</span><span class="sxs-lookup"><span data-stu-id="1ca49-188">The source language</span></span>                                                              |
| <span data-ttu-id="1ca49-189">OriginalText</span><span class="sxs-lookup"><span data-stu-id="1ca49-189">OriginalText</span></span>   | <span data-ttu-id="1ca49-190">The source language text that is used when submitting the request.</span><span class="sxs-lookup"><span data-stu-id="1ca49-190">The source language text that is used when submitting the request.</span></span>               |
| <span data-ttu-id="1ca49-191">Rating</span><span class="sxs-lookup"><span data-stu-id="1ca49-191">Rating</span></span>         | <span data-ttu-id="1ca49-192">The rating that is applied by the submitter in the AddTranslation() method call.</span><span class="sxs-lookup"><span data-stu-id="1ca49-192">The rating that is applied by the submitter in the AddTranslation() method call.</span></span> |
| <span data-ttu-id="1ca49-193">To</span><span class="sxs-lookup"><span data-stu-id="1ca49-193">To</span></span>             | <span data-ttu-id="1ca49-194">The target language</span><span class="sxs-lookup"><span data-stu-id="1ca49-194">The target language</span></span>                                                              |
| <span data-ttu-id="1ca49-195">TranslatedText</span><span class="sxs-lookup"><span data-stu-id="1ca49-195">TranslatedText</span></span> | <span data-ttu-id="1ca49-196">The translation as submitted in the AddTranslation() method call.</span><span class="sxs-lookup"><span data-stu-id="1ca49-196">The translation as submitted in the AddTranslation() method call.</span></span>                |
| <span data-ttu-id="1ca49-197">Uri</span><span class="sxs-lookup"><span data-stu-id="1ca49-197">Uri</span></span>            | <span data-ttu-id="1ca49-198">The URI applied in the AddTranslation() method call.</span><span class="sxs-lookup"><span data-stu-id="1ca49-198">The URI applied in the AddTranslation() method call.</span></span>                             |
| <span data-ttu-id="1ca49-199">User</span><span class="sxs-lookup"><span data-stu-id="1ca49-199">User</span></span>           | <span data-ttu-id="1ca49-200">The user name</span><span class="sxs-lookup"><span data-stu-id="1ca49-200">The user name</span></span>                                                                    |

<span data-ttu-id="1ca49-201">**Exceptions**</span><span class="sxs-lookup"><span data-stu-id="1ca49-201">**Exceptions**</span></span>

| <span data-ttu-id="1ca49-202">Exception</span><span class="sxs-lookup"><span data-stu-id="1ca49-202">Exception</span></span>                                                                                                       | <span data-ttu-id="1ca49-203">Message</span><span class="sxs-lookup"><span data-stu-id="1ca49-203">Message</span></span>                                                                           | <span data-ttu-id="1ca49-204">Conditions</span><span class="sxs-lookup"><span data-stu-id="1ca49-204">Conditions</span></span>                                                                                                                                                                                                                       |
|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="1ca49-205">ArgumentOutOfRangeException</span><span class="sxs-lookup"><span data-stu-id="1ca49-205">ArgumentOutOfRangeException</span></span>](https://msdn.microsoft.com/en-us/library/system.argumentoutofrangeexception.aspx) | <span data-ttu-id="1ca49-206">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span><span class="sxs-lookup"><span data-stu-id="1ca49-206">The parameter '**maxDateUtc**' must be greater than or equal to '**minDateUtc**'.</span></span> | <span data-ttu-id="1ca49-207">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-207">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span></span>                                                                                                                              |
| <span data-ttu-id="1ca49-208">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="1ca49-208">TranslateApiException</span></span>                                                                                           | <span data-ttu-id="1ca49-209">IP is over the quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-209">IP is over the quota.</span></span>                                                             |  <span data-ttu-id="1ca49-210">The limit for the number of requests per minute is reached.</span><span class="sxs-lookup"><span data-stu-id="1ca49-210">The limit for the number of requests per minute is reached.</span></span>   <span data-ttu-id="1ca49-211">The request size remains limited at 10000 characters.</span><span class="sxs-lookup"><span data-stu-id="1ca49-211">The request size remains limited at 10000 characters.</span></span>  <span data-ttu-id="1ca49-212">An hourly and a daily quota limit the number of characters that the Microsoft, Translator API will accept.</span><span class="sxs-lookup"><span data-stu-id="1ca49-212">An hourly and a daily quota limit the number of characters that the Microsoft, Translator API will accept.</span></span> |
|                                                                                                                 | <span data-ttu-id="1ca49-213">AppId is over the quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-213">AppId is over the quota.</span></span>                                                          | <span data-ttu-id="1ca49-214">The application ID exceeded the hourly or daily quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-214">The application ID exceeded the hourly or daily quota.</span></span>                                                                                                                                                                           |

>[!NOTE]
><span data-ttu-id="1ca49-215">The quota will adjust to ensure fairness among all users of the service.</span><span class="sxs-lookup"><span data-stu-id="1ca49-215">The quota will adjust to ensure fairness among all users of the service.</span></span> 

<span data-ttu-id="1ca49-216">**Example**
**C#**
**PHP**</span><span class="sxs-lookup"><span data-stu-id="1ca49-216">**Example**
**C#**
**PHP**</span></span>

<span data-ttu-id="1ca49-217">**C#**</span><span class="sxs-lookup"><span data-stu-id="1ca49-217">**C#**</span></span>
```
using System;
using System.IO;
using System.Net;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Json;
using System.Text;
using System.Web;

namespace CtfReporting
{
    class Program
    {
        static void Main(string[] args)
        {
            AdmAccessToken admToken;
            string headerValue;
            //Get Client Id and Client Secret from https://datamarket.azure.com/developer/applications/
            //Refer obtaining AccessToken (http://msdn.microsoft.com/en-us/library/hh454950.aspx) 
            AdmAuthentication admAuth = new AdmAuthentication("clientId", "clientSecret");
            try
            {
                admToken = admAuth.GetAccessToken();
                // Create a header with the access_token property of the returned token
                headerValue = "Bearer " + admToken.access_token;
                Console.WriteLine("User Translations");
                ctfGetUserTranslations(headerValue, 0, 5);
                Console.WriteLine("Press Enter for Next 5 Records");
                if (Console.ReadKey().Key == ConsoleKey.Enter)
                {
                    ctfGetUserTranslations(headerValue, 5, 5);
                    Console.WriteLine("Press any key to exit...");
                    Console.ReadKey(true);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static void ctfGetUserTranslations(string authToken, int skip, int take)
        {
            // Add CtfReportingService as a service reference, Address:http://api.microsofttranslator.com/v2/beta/ctfreporting.svc
            CtfReportingService.CtfReportingServiceClient reportingClient = new CtfReportingService.CtfReportingServiceClient();
            CtfReportingService.UserTranslation[] userTranslations = reportingClient.GetUserTranslations(authToken, "", "es", "en", null, null, "", "general", null, null, skip, take);
            foreach (CtfReportingService.UserTranslation item in userTranslations)
            {
                Console.WriteLine(string.Format("CreatedDateUtc={0},From={1},To={2},Rating={3},Uri={4},User={5},OriginalText={6},TranslatedText={7}", item.CreatedDateUtc, item.From, item.To, item.Rating, item.Uri, item.User, item.OriginalText, item.TranslatedText));
            }
        }


    }
    [DataContract]
    public class AdmAccessToken
    {
        [DataMember]
        public string access_token { get; set; }
        [DataMember]
        public string token_type { get; set; }
        [DataMember]
        public string expires_in { get; set; }
        [DataMember]
        public string scope { get; set; }
    }

    public class AdmAuthentication
    {
        public static readonly string DatamarketAccessUri = "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13";
        private string clientId;
        private string cientSecret;
        private string request;

        public AdmAuthentication(string clientId, string clientSecret)
        {
            this.clientId = clientId;
            this.cientSecret = clientSecret;
            //If clientid or client secret has special characters, encode before sending request
            this.request = string.Format("grant_type=client_credentials&client_id={0}&client_secret={1}&scope=http://api.microsofttranslator.com", HttpUtility.UrlEncode(clientId), HttpUtility.UrlEncode(clientSecret));
        }

        public AdmAccessToken GetAccessToken()
        {
            return HttpPost(DatamarketAccessUri, this.request);
        }

        private AdmAccessToken HttpPost(string DatamarketAccessUri, string requestDetails)
        {
            //Prepare OAuth request 
            WebRequest webRequest = WebRequest.Create(DatamarketAccessUri);
            webRequest.ContentType = "application/x-www-form-urlencoded";
            webRequest.Method = "POST";
            byte[] bytes = Encoding.ASCII.GetBytes(requestDetails);
            webRequest.ContentLength = bytes.Length;
            using (Stream outputStream = webRequest.GetRequestStream())
            {
                outputStream.Write(bytes, 0, bytes.Length);
            }
            using (WebResponse webResponse = webRequest.GetResponse())
            {
                DataContractJsonSerializer serializer = new DataContractJsonSerializer(typeof(AdmAccessToken));
                //Get deserialized object from JSON stream
                AdmAccessToken token = (AdmAccessToken)serializer.ReadObject(webResponse.GetResponseStream());
                return token;
            }
        }
    }
}
``                                            

**PHP**

<?php
```
```
class AccessTokenAuthentication {
    /*
     * Get the access token.
     *
     * @param string $grantType    Grant type.
     * @param string $scopeUrl     Application Scope URL.
     * @param string $clientID     Application client ID.
     * @param string $clientSecret Application client ID.
     * @param string $authUrl      Oauth Url.
     *
     * @return string.
     */
    function getTokens($grantType, $scopeUrl, $clientID, $clientSecret, $authUrl){
        try {
            //Initialize the Curl Session.
            $ch = curl_init();
            //Create the request Array.
            $paramArr = array (
             'grant_type'    => $grantType,
             'scope'         => $scopeUrl,
             'client_id'     => $clientID,
             'client_secret' => $clientSecret
            );
            //Create an Http Query.//
            $paramArr = http_build_query($paramArr);
            //Set the Curl URL.
            curl_setopt($ch, CURLOPT_URL, $authUrl);
            //Set HTTP POST Request.
            curl_setopt($ch, CURLOPT_POST, TRUE);
            //Set data to POST in HTTP "POST" Operation.
            curl_setopt($ch, CURLOPT_POSTFIELDS, $paramArr);
            //CURLOPT_RETURNTRANSFER- TRUE to return the transfer as a string of the return value of curl_exec().
            curl_setopt ($ch, CURLOPT_RETURNTRANSFER, TRUE);
            //CURLOPT_SSL_VERIFYPEER- Set FALSE to stop cURL from verifying the peer's certificate.
            curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
            //Execute the  cURL session.
            $strResponse = curl_exec($ch);
            //Get the Error Code returned by Curl.
            $curlErrno = curl_errno($ch);
            if($curlErrno){
                $curlError = curl_error($ch);
                throw new Exception($curlError);
            }
            //Close the Curl Session.
            curl_close($ch);
            //Decode the returned JSON string.
            $objResponse = json_decode($strResponse);
                
            if ($objResponse->error){
                throw new Exception($objResponse->error_description);
            }
            return $objResponse->access_token;
        } catch (Exception $e) {
            echo "Exception-".$e->getMessage();
        }
    }
}

/*
 * Class:AccessTokenAuthentication
 *
 * Create SOAP Object.
 */
class SOAPMicrosoftTranslator {
    /*
     * Soap Object.
     *
     * @var ObjectArray.
     */
    public $objSoap;
    /*
     * Create the SAOP object.
     *
     * @param string $accessToken Access Token string.
     * @param string $wsdlUrl     WSDL string.
     *
     * @return string.
     */
    public function __construct($accessToken, $wsdlUrl){
        try {
            //Authorization header string.
            $authHeader = "Authorization: Bearer ". $accessToken;
            $contextArr = array(
                'http'   => array(
                    'header' => $authHeader
            )
            );
            //Create a streams context.
            $objContext = stream_context_create($contextArr);
            $optionsArr = array (
                'soap_version'   => 'SOAP_1_2',
                'encoding'          => 'UTF-8',
                'exceptions'      => true,
                'trace'          => true,
                'cache_wsdl'     => 'WSDL_CACHE_NONE',
                'stream_context' => $objContext,
                'user_agent'     => 'PHP-SOAP/'.PHP_VERSION."\r\n".$authHeader    
            );
            //Call Soap Client.
            $this->objSoap = new SoapClient($wsdlUrl, $optionsArr);
        } catch(Exception $e){
            echo "<h2>Exception Error!</h2>";
            echo $e->getMessage();
        }
    }
}


try {
    //Soap WSDL Url.
    $wsdlUrl       = "http://api.microsofttranslator.com/v2/beta/ctfreporting.svc";
    //Client ID of the application.
    $clientID       = "clientid";
    //Client Secret key of the application.
    $clientSecret = "clientsecret";
    //OAuth Url.
    $authUrl      = "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13/";
    //Application Scope Url
    $scopeUrl     = "http://api.microsofttranslator.com";
    //Application grant type
    $grantType    = "client_credentials";

    //Create the Authentication object
    $authObj      = new AccessTokenAuthentication();
    //Get the Access token
    $accessToken  = $authObj->getTokens($grantType, $scopeUrl, $clientID, $clientSecret, $authUrl);
    //Create soap translator Object
    $soapTranslator = new SOAPMicrosoftTranslator($accessToken, $wsdlUrl);

    //Set the Params.
    $from         = '';
    $to         = '';
    $minRating  = 0;
    $maxRating  = 10;
    $takeResult = 10;
    $user         = '';

    //Request argument list.
    $requestArg = array (
        'user'       => $user,
        'from'       => $from,
        'to'           => $to,
        'minRating'  => $minRating,
        'maxRating'  => $maxRating,
        'take'       => $takeResult
    );
    //Call the GetUserTranslations Method.
    $responseObj = $soapTranslator->objSoap->GetUserTranslations($requestArg);
    $translationArr = $responseObj->GetUserTranslationsResult->UserTranslation;
    if(sizeof($translationArr) > 0) {
            echo "<table border=2px>";
            echo "<tr>";
            echo "<td><b>User</b></td><td><b>From</b></td><td><b>To</b></td>
                <td><b>Rating</b></td><td><b>OriginalText</b></td><td><b>OriginalText</b></td>";
            echo "</tr>";
        if(sizeof($translationArr) > 1) {
            $i=1;
            foreach ($translationArr as  $translation) {
                echo "<tr><td>$translation->User</td><td>$translation->From</td>
                    <td>$translation->To</td><td>$translation->Rating</td>
                    <td>$translation->OriginalText</td><td>$translation->TranslatedText</td></tr>";
                $i++;
            }
        } else {
            echo "<tr><td>$translationArr->User</td><td>$translationArr->From</td>
                <td>$translationArr->To</td><td>$translationArr->Rating</td>
                <td>$translationArr->OriginalText</td><td>$translationArr->TranslatedText</td></tr>";
        }
    }
    echo "</table>";    
} catch (Exception $e) {
    echo "Exception: " . $e->getMessage() . PHP_EOL;
}
```                                       


## <a name="getusertranslationcounts-method"></a><span data-ttu-id="1ca49-218">GetUserTranslationCounts Method</span><span class="sxs-lookup"><span data-stu-id="1ca49-218">GetUserTranslationCounts Method</span></span>

<span data-ttu-id="1ca49-219">This method gets the count of translations that are created by the user.</span><span class="sxs-lookup"><span data-stu-id="1ca49-219">This method gets the count of translations that are created by the user.</span></span> <span data-ttu-id="1ca49-220">It provides the list of translation counts grouped by the uriPrefix, from, to, user, minRating, and maxRating request parameters.</span><span class="sxs-lookup"><span data-stu-id="1ca49-220">It provides the list of translation counts grouped by the uriPrefix, from, to, user, minRating, and maxRating request parameters.</span></span> 

<span data-ttu-id="1ca49-221">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="1ca49-221">**Syntax**</span></span>

## <a name="c"></a><span data-ttu-id="1ca49-222">C###</span><span class="sxs-lookup"><span data-stu-id="1ca49-222">C###</span></span>

<span data-ttu-id="1ca49-223">UserTranslationCount[]GetUserTranslationCounts( string appId, string uriPrefix, string from, string to, int? minRating, int? maxRating, string user, string category DateTime? minDateUtc, DateTime? maxDateUtc, int? skip, int? take);</span><span class="sxs-lookup"><span data-stu-id="1ca49-223">UserTranslationCount[]GetUserTranslationCounts( string appId, string uriPrefix, string from, string to, int? minRating, int? maxRating, string user, string category DateTime? minDateUtc, DateTime? maxDateUtc, int? skip, int? take);</span></span>
            
<span data-ttu-id="1ca49-224">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="1ca49-224">**Parameters**</span></span>

| <span data-ttu-id="1ca49-225">Parameter</span><span class="sxs-lookup"><span data-stu-id="1ca49-225">Parameter</span></span>  | <span data-ttu-id="1ca49-226">Description</span><span class="sxs-lookup"><span data-stu-id="1ca49-226">Description</span></span>                                                                                                                                                                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ca49-227">appld</span><span class="sxs-lookup"><span data-stu-id="1ca49-227">appld</span></span>      | <span data-ttu-id="1ca49-228">Required.</span><span class="sxs-lookup"><span data-stu-id="1ca49-228">Required.</span></span> <span data-ttu-id="1ca49-229">If the Authorization header is used, leave the appid field empty,else specify a string containing "Bearer" + " " + access token.</span><span class="sxs-lookup"><span data-stu-id="1ca49-229">If the Authorization header is used, leave the appid field empty,else specify a string containing "Bearer" + " " + access token.</span></span>                                                                                                          |
| <span data-ttu-id="1ca49-230">uriPrefix</span><span class="sxs-lookup"><span data-stu-id="1ca49-230">uriPrefix</span></span>  | <span data-ttu-id="1ca49-231">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-231">Optional.</span></span> <span data-ttu-id="1ca49-232">A string containing prefix of URI of the translation.</span><span class="sxs-lookup"><span data-stu-id="1ca49-232">A string containing prefix of URI of the translation.</span></span>                                                                                                                                                                                     |
| <span data-ttu-id="1ca49-233">from</span><span class="sxs-lookup"><span data-stu-id="1ca49-233">from</span></span>       | <span data-ttu-id="1ca49-234">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-234">Optional.</span></span> <span data-ttu-id="1ca49-235">A string representing the language code of the translation text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-235">A string representing the language code of the translation text.</span></span>                                                                                                                                                                          |
| <span data-ttu-id="1ca49-236">to</span><span class="sxs-lookup"><span data-stu-id="1ca49-236">to</span></span>         | <span data-ttu-id="1ca49-237">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-237">Optional.</span></span> <span data-ttu-id="1ca49-238">A string representing the language code to translate the text into.</span><span class="sxs-lookup"><span data-stu-id="1ca49-238">A string representing the language code to translate the text into.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="1ca49-239">minRating</span><span class="sxs-lookup"><span data-stu-id="1ca49-239">minRating</span></span>  | <span data-ttu-id="1ca49-240">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-240">Optional.</span></span> <span data-ttu-id="1ca49-241">An integer value representing the minimum quality rating for the,translated text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-241">An integer value representing the minimum quality rating for the,translated text.</span></span> <span data-ttu-id="1ca49-242">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="1ca49-242">The valid value is between -10 and 10.</span></span> <span data-ttu-id="1ca49-243">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="1ca49-243">The default value is 1.</span></span>                                                                                          |
| <span data-ttu-id="1ca49-244">maxRating</span><span class="sxs-lookup"><span data-stu-id="1ca49-244">maxRating</span></span>  | <span data-ttu-id="1ca49-245">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-245">Optional.</span></span> <span data-ttu-id="1ca49-246">An integer value representing the maximum quality rating for the,translated text.</span><span class="sxs-lookup"><span data-stu-id="1ca49-246">An integer value representing the maximum quality rating for the,translated text.</span></span> <span data-ttu-id="1ca49-247">The valid value is between -10 and 10.</span><span class="sxs-lookup"><span data-stu-id="1ca49-247">The valid value is between -10 and 10.</span></span> <span data-ttu-id="1ca49-248">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="1ca49-248">The default value is 1.</span></span>                                                                                          |
| <span data-ttu-id="1ca49-249">user</span><span class="sxs-lookup"><span data-stu-id="1ca49-249">user</span></span>       | <span data-ttu-id="1ca49-250">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-250">Optional.</span></span> <span data-ttu-id="1ca49-251">A string that is used to filter the result based on the originator,of the submission.</span><span class="sxs-lookup"><span data-stu-id="1ca49-251">A string that is used to filter the result based on the originator,of the submission.</span></span>                                                                                                                                                     |
| <span data-ttu-id="1ca49-252">category</span><span class="sxs-lookup"><span data-stu-id="1ca49-252">category</span></span>   | <span data-ttu-id="1ca49-253">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-253">Optional.</span></span> <span data-ttu-id="1ca49-254">A string containing the category or domain of the translation.,This parameter supports only the default option general.</span><span class="sxs-lookup"><span data-stu-id="1ca49-254">A string containing the category or domain of the translation.,This parameter supports only the default option general.</span></span>                                                                                                                   |
| <span data-ttu-id="1ca49-255">minDateUtc</span><span class="sxs-lookup"><span data-stu-id="1ca49-255">minDateUtc</span></span> | <span data-ttu-id="1ca49-256">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-256">Optional.</span></span> <span data-ttu-id="1ca49-257">The date from when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="1ca49-257">The date from when you want to retrieve the translations.</span></span> <span data-ttu-id="1ca49-258">The date,must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="1ca49-258">The date,must be in the UTC format.</span></span>                                                                                                                                             |
| <span data-ttu-id="1ca49-259">maxDateUtc</span><span class="sxs-lookup"><span data-stu-id="1ca49-259">maxDateUtc</span></span> | <span data-ttu-id="1ca49-260">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-260">Optional.</span></span> <span data-ttu-id="1ca49-261">The date till when you want to retrieve the translations.</span><span class="sxs-lookup"><span data-stu-id="1ca49-261">The date till when you want to retrieve the translations.</span></span> <span data-ttu-id="1ca49-262">The date,must be in the UTC format.</span><span class="sxs-lookup"><span data-stu-id="1ca49-262">The date,must be in the UTC format.</span></span>                                                                                                                                             |
| <span data-ttu-id="1ca49-263">skip</span><span class="sxs-lookup"><span data-stu-id="1ca49-263">skip</span></span>       | <span data-ttu-id="1ca49-264">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-264">Optional.</span></span> <span data-ttu-id="1ca49-265">The number of results that you want to skip on a page.</span><span class="sxs-lookup"><span data-stu-id="1ca49-265">The number of results that you want to skip on a page.</span></span> <span data-ttu-id="1ca49-266">For example,,if you want the skip the first 20 rows of the results and view from the 21st result,record, specify 20 for this parameter.</span><span class="sxs-lookup"><span data-stu-id="1ca49-266">For example,,if you want the skip the first 20 rows of the results and view from the 21st result,record, specify 20 for this parameter.</span></span> <span data-ttu-id="1ca49-267">The default value for this parameter is 0.</span><span class="sxs-lookup"><span data-stu-id="1ca49-267">The default value for this parameter is 0.</span></span> |
| <span data-ttu-id="1ca49-268">take</span><span class="sxs-lookup"><span data-stu-id="1ca49-268">take</span></span>       | <span data-ttu-id="1ca49-269">Optional.</span><span class="sxs-lookup"><span data-stu-id="1ca49-269">Optional.</span></span> <span data-ttu-id="1ca49-270">The number of results that you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="1ca49-270">The number of results that you want to retrieve.</span></span> <span data-ttu-id="1ca49-271">The maximum number of each request is 100.</span><span class="sxs-lookup"><span data-stu-id="1ca49-271">The maximum number of each request is 100.</span></span> <span data-ttu-id="1ca49-272">The default is 100.</span><span class="sxs-lookup"><span data-stu-id="1ca49-272">The default is 100.</span></span>                                                                                                                           |
><span data-ttu-id="1ca49-273">Note: The skip and take request parameters enable pagination for a large number of result records.</span><span class="sxs-lookup"><span data-stu-id="1ca49-273">Note: The skip and take request parameters enable pagination for a large number of result records.</span></span> 

<span data-ttu-id="1ca49-274">Return value</span><span class="sxs-lookup"><span data-stu-id="1ca49-274">Return value</span></span>

<span data-ttu-id="1ca49-275">The result set contains array of the **UserTranslationCount**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-275">The result set contains array of the **UserTranslationCount**.</span></span> <span data-ttu-id="1ca49-276">Each UserTranslationCount has the following elements:</span><span class="sxs-lookup"><span data-stu-id="1ca49-276">Each UserTranslationCount has the following elements:</span></span> 

| <span data-ttu-id="1ca49-277">Field</span><span class="sxs-lookup"><span data-stu-id="1ca49-277">Field</span></span>  | <span data-ttu-id="1ca49-278">Description</span><span class="sxs-lookup"><span data-stu-id="1ca49-278">Description</span></span>                                                                      |
|--------|----------------------------------------------------------------------------------|
| <span data-ttu-id="1ca49-279">Count</span><span class="sxs-lookup"><span data-stu-id="1ca49-279">Count</span></span>  | <span data-ttu-id="1ca49-280">The number of results that is retrieved.</span><span class="sxs-lookup"><span data-stu-id="1ca49-280">The number of results that is retrieved.</span></span>                                         |
| <span data-ttu-id="1ca49-281">From</span><span class="sxs-lookup"><span data-stu-id="1ca49-281">From</span></span>   | <span data-ttu-id="1ca49-282">The source language</span><span class="sxs-lookup"><span data-stu-id="1ca49-282">The source language</span></span>                                                              |
| <span data-ttu-id="1ca49-283">Rating</span><span class="sxs-lookup"><span data-stu-id="1ca49-283">Rating</span></span> | <span data-ttu-id="1ca49-284">The rating that is applied by the submitter in the AddTranslation() method call.</span><span class="sxs-lookup"><span data-stu-id="1ca49-284">The rating that is applied by the submitter in the AddTranslation() method call.</span></span> |
| <span data-ttu-id="1ca49-285">To</span><span class="sxs-lookup"><span data-stu-id="1ca49-285">To</span></span>     | <span data-ttu-id="1ca49-286">The target language.</span><span class="sxs-lookup"><span data-stu-id="1ca49-286">The target language.</span></span>                                                             |
| <span data-ttu-id="1ca49-287">Uri</span><span class="sxs-lookup"><span data-stu-id="1ca49-287">Uri</span></span>    | <span data-ttu-id="1ca49-288">The URI applied in trhe AddTranslation() method call.</span><span class="sxs-lookup"><span data-stu-id="1ca49-288">The URI applied in trhe AddTranslation() method call.</span></span>                            |
| <span data-ttu-id="1ca49-289">USer</span><span class="sxs-lookup"><span data-stu-id="1ca49-289">USer</span></span>   | <span data-ttu-id="1ca49-290">The user name</span><span class="sxs-lookup"><span data-stu-id="1ca49-290">The user name</span></span>                                                                    |

<span data-ttu-id="1ca49-291">**Exceptions**</span><span class="sxs-lookup"><span data-stu-id="1ca49-291">**Exceptions**</span></span>

| <span data-ttu-id="1ca49-292">Exception</span><span class="sxs-lookup"><span data-stu-id="1ca49-292">Exception</span></span>                                                                                                        | <span data-ttu-id="1ca49-293">Message</span><span class="sxs-lookup"><span data-stu-id="1ca49-293">Message</span></span>                                                                           | <span data-ttu-id="1ca49-294">Conditions</span><span class="sxs-lookup"><span data-stu-id="1ca49-294">Conditions</span></span>                                                                                                                                                                                                                     |
|------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="1ca49-295">ArgumentsOutOfRangeException</span><span class="sxs-lookup"><span data-stu-id="1ca49-295">ArgumentsOutOfRangeException</span></span>](https://msdn.microsoft.com/en-us/library/system.argumentoutofrangeexception.aspx) | <span data-ttu-id="1ca49-296">The parameter **'maxDateUtc'** must be greater than or equal to **'minDateUtc'**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-296">The parameter **'maxDateUtc'** must be greater than or equal to **'minDateUtc'**.</span></span> | <span data-ttu-id="1ca49-297">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span><span class="sxs-lookup"><span data-stu-id="1ca49-297">The value of the parameter **maxDateUtc** is lesser than the value of the parameter **minDateUtc**.</span></span>                                                                                                                            |
| <span data-ttu-id="1ca49-298">TranslateApiException</span><span class="sxs-lookup"><span data-stu-id="1ca49-298">TranslateApiException</span></span>                                                                                            | <span data-ttu-id="1ca49-299">IP is over the quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-299">IP is over the quota.</span></span>                                                             |  <span data-ttu-id="1ca49-300">The limit for the number of requests per minute is reached.</span><span class="sxs-lookup"><span data-stu-id="1ca49-300">The limit for the number of requests per minute is reached.</span></span>   <span data-ttu-id="1ca49-301">The request size remains limited at 10000 characters.</span><span class="sxs-lookup"><span data-stu-id="1ca49-301">The request size remains limited at 10000 characters.</span></span> <span data-ttu-id="1ca49-302">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span><span class="sxs-lookup"><span data-stu-id="1ca49-302">An hourly and a daily quota limit the number of characters that the Microsoft Translator API will accept.</span></span> |
|                                                                                                                  | <span data-ttu-id="1ca49-303">AppId is over the quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-303">AppId is over the quota.</span></span>                                                          | <span data-ttu-id="1ca49-304">The application ID exceeded the hourly or daily quota.</span><span class="sxs-lookup"><span data-stu-id="1ca49-304">The application ID exceeded the hourly or daily quota.</span></span>                                                                                                                                                                         |

>[!NOTE]
><span data-ttu-id="1ca49-305">The quota will adjust to ensure fairness among all users of the service.</span><span class="sxs-lookup"><span data-stu-id="1ca49-305">The quota will adjust to ensure fairness among all users of the service.</span></span>

### <a name="example"></a><span data-ttu-id="1ca49-306">**Example**</span><span class="sxs-lookup"><span data-stu-id="1ca49-306">**Example**</span></span> ###
<span data-ttu-id="1ca49-307">**C# PHP**</span><span class="sxs-lookup"><span data-stu-id="1ca49-307">**C# PHP**</span></span>

<span data-ttu-id="1ca49-308">**C#**</span><span class="sxs-lookup"><span data-stu-id="1ca49-308">**C#**</span></span>
```
using System;
using System.IO;
using System.Net;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Json;
using System.Text;
using System.Web;

namespace CtfReporting
{
    class Program
    {
        static void Main(string[] args)
        {
            AdmAccessToken admToken;
            string headerValue;
            //Get Client Id and Client Secret from https://datamarket.azure.com/developer/applications/
            //Refer obtaining AccessToken (http://msdn.microsoft.com/en-us/library/hh454950.aspx) 
            AdmAuthentication admAuth = new AdmAuthentication("clientId", "clientSecret");
            try
            {
                admToken = admAuth.GetAccessToken();
                // Create a header with the access_token property of the returned token
                headerValue = "Bearer " + admToken.access_token;
                Console.WriteLine("User translations count");
                ctfGetUserTranslationsCount(headerValue, 0, 5);
                Console.WriteLine("Press Enter for Next 5 Records");
                if (Console.ReadKey().Key == ConsoleKey.Enter)
                {
                    ctfGetUserTranslationsCount(headerValue, 5, 5);
                    Console.WriteLine("Press any key to exit...");
                    Console.ReadKey(true);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
                Console.WriteLine("Press any key to exit...");
                Console.ReadKey(true);
            }
        }
        private static void ctfGetUserTranslationsCount(string authToken, int skip, int take)
        {
            // Add CtfReportingService as a service reference, Address:http://api.microsofttranslator.com/v2/beta/ctfreporting.svc
            CtfReportingService.CtfReportingServiceClient reportingClient = new CtfReportingService.CtfReportingServiceClient();
            CtfReportingService.UserTranslationCount[] userTranslationsCount = reportingClient.GetUserTranslationCounts(authToken, "", "es", "en", null, null, "", "general", null, null, skip, take);
            foreach (CtfReportingService.UserTranslationCount item in userTranslationsCount)
            {
                Console.WriteLine(string.Format("Count={0},From={1},To={2},Rating={3},Uri={4},User={5}", item.Count, item.From, item.To, item.Rating, item.Uri, item.User));
            }
        }
    }
    [DataContract]
    public class AdmAccessToken
    {
        [DataMember]
        public string access_token { get; set; }
        [DataMember]
        public string token_type { get; set; }
        [DataMember]
        public string expires_in { get; set; }
        [DataMember]
        public string scope { get; set; }
    }

    public class AdmAuthentication
    {
        public static readonly string DatamarketAccessUri = "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13";
        private string clientId;
        private string cientSecret;
        private string request;

        public AdmAuthentication(string clientId, string clientSecret)
        {
            this.clientId = clientId;
            this.cientSecret = clientSecret;
            //If clientid or client secret has special characters, encode before sending request
            this.request = string.Format("grant_type=client_credentials&client_id={0}&client_secret={1}&scope=http://api.microsofttranslator.com", HttpUtility.UrlEncode(clientId), HttpUtility.UrlEncode(clientSecret));
        }

        public AdmAccessToken GetAccessToken()
        {
            return HttpPost(DatamarketAccessUri, this.request);
        }

        private AdmAccessToken HttpPost(string DatamarketAccessUri, string requestDetails)
        {
            //Prepare OAuth request 
            WebRequest webRequest = WebRequest.Create(DatamarketAccessUri);
            webRequest.ContentType = "application/x-www-form-urlencoded";
            webRequest.Method = "POST";
            byte[] bytes = Encoding.ASCII.GetBytes(requestDetails);
            webRequest.ContentLength = bytes.Length;
            using (Stream outputStream = webRequest.GetRequestStream())
            {
                outputStream.Write(bytes, 0, bytes.Length);
            }
            using (WebResponse webResponse = webRequest.GetResponse())
            {
                DataContractJsonSerializer serializer = new DataContractJsonSerializer(typeof(AdmAccessToken));
                //Get deserialized object from JSON stream
                AdmAccessToken token = (AdmAccessToken)serializer.ReadObject(webResponse.GetResponseStream());
                return token;
            }
        }
    }
}
                                           
**PHP**

<?php

class AccessTokenAuthentication {
    /*
     * Get the access token.
     *
     * @param string $grantType    Grant type.
     * @param string $scopeUrl     Application Scope URL.
     * @param string $clientID     Application client ID.
     * @param string $clientSecret Application client ID.
     * @param string $authUrl      Oauth Url.
     *
     * @return string.
     */
    function getTokens($grantType, $scopeUrl, $clientID, $clientSecret, $authUrl){
        try {
            //Initialize the Curl Session.
            $ch = curl_init();
            //Create the request Array.
            $paramArr = array (
             'grant_type'    => $grantType,
             'scope'         => $scopeUrl,
             'client_id'     => $clientID,
             'client_secret' => $clientSecret
            );
            //Create an Http Query.//
            $paramArr = http_build_query($paramArr);
            //Set the Curl URL.
            curl_setopt($ch, CURLOPT_URL, $authUrl);
            //Set HTTP POST Request.
            curl_setopt($ch, CURLOPT_POST, TRUE);
            //Set data to POST in HTTP "POST" Operation.
            curl_setopt($ch, CURLOPT_POSTFIELDS, $paramArr);
            //CURLOPT_RETURNTRANSFER- TRUE to return the transfer as a string of the return value of curl_exec().
            curl_setopt ($ch, CURLOPT_RETURNTRANSFER, TRUE);
            //CURLOPT_SSL_VERIFYPEER- Set FALSE to stop cURL from verifying the peer's certificate.
            curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
            //Execute the  cURL session.
            $strResponse = curl_exec($ch);
            //Get the Error Code returned by Curl.
            $curlErrno = curl_errno($ch);
            if($curlErrno){
                $curlError = curl_error($ch);
                throw new Exception($curlError);
            }
            //Close the Curl Session.
            curl_close($ch);
            //Decode the returned JSON string.
            $objResponse = json_decode($strResponse);
                
            if ($objResponse->error){
                throw new Exception($objResponse->error_description);
            }
            return $objResponse->access_token;
        } catch (Exception $e) {
            echo "Exception-".$e->getMessage();
        }
    }
}

/*
 * Class:AccessTokenAuthentication
 *
 * Create SOAP Object.
 */
class SOAPMicrosoftTranslator {
    /*
     * Soap Object.
     *
     * @var ObjectArray.
     */
    public $objSoap;
    /*
     * Create the SAOP object.
     *
     * @param string $accessToken Access Token string.
     * @param string $wsdlUrl     WSDL string.
     *
     * @return string.
     */
    public function __construct($accessToken, $wsdlUrl){
        try {
            //Authorization header string.
            $authHeader = "Authorization: Bearer ". $accessToken;
            $contextArr = array(
                'http'   => array(
                    'header' => $authHeader
            )
            );
            //Create a streams context.
            $objContext = stream_context_create($contextArr);
            $optionsArr = array (
                'soap_version'   => 'SOAP_1_2',
                'encoding'          => 'UTF-8',
                'exceptions'      => true,
                'trace'          => true,
                'cache_wsdl'     => 'WSDL_CACHE_NONE',
                'stream_context' => $objContext,
                'user_agent'     => 'PHP-SOAP/'.PHP_VERSION."\r\n".$authHeader    
            );
            //Call Soap Client.
            $this->objSoap = new SoapClient($wsdlUrl, $optionsArr);
        } catch(Exception $e){
            echo "<h2>Exception Error!</h2>";
            echo $e->getMessage();
        }
    }
}

try {
    //Soap WSDL Url.
    $wsdlUrl       = "http://api.microsofttranslator.com/v2/beta/ctfreporting.svc";
    //Client ID of the application.
    $clientID       = "clientId";
    //Client Secret key of the application.
    $clientSecret = "clientSecret";
    //OAuth Url.
    $authUrl      = "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13/";
    //Application Scope Url
    $scopeUrl     = "http://api.microsofttranslator.com";
    //Application grant type
    $grantType    = "client_credentials";

    //Create the Authentication object
    $authObj      = new AccessTokenAuthentication();
    //Get the Access token
    $accessToken  = $authObj->getTokens($grantType, $scopeUrl, $clientID, $clientSecret, $authUrl);
    //Create soap translator Object
    $soapTranslator = new SOAPMicrosoftTranslator($accessToken, $wsdlUrl);
    
    //Set the Params.
    $from         = 'en';
    $to         = 'de';
    $minRating  = 0;
    $maxRating  = 10;
    $takeResult = 100;
    $user         = 'guestUser';
    //Request argument list.
    $requestArg = array (
        'user'       => $user,
        'from'       => $from,
        'to'           => $to,
        'minRating'  => $minRating,
        'maxRating'  => $maxRating,
        'take'       => $takeResult
    );
    //Call GetUserTranslationCount Method.
    $responseObj = $soapTranslator->objSoap->GetUserTranslationCounts($requestArg);
    $translationCountArr = $responseObj->GetUserTranslationCountsResult->UserTranslationCount;
    echo "<table border=2px>";
    echo "<tr>";
    echo "<td><b>User</b></td><td><b>From</b></td><td><b>To</b></td><td><b>rating</b></td><td><b>Count</b></td>";
    echo "</tr>";
    if(sizeof($translationCountArr) > 0) {
        if(sizeof($translationCountArr) > 1) {
            foreach ($translationCountArr as $translationCount) {
                echo "<tr><td>$translationCount->User</td><td>$translationCount->From</td>
                    <td>$translationCount->To</td><td>$translationCount->Rating</td>
                    <td>$translationCount->Count</td></tr>";
            }
        } else {
            echo "<tr><td>$translationCountArr->User</td><td>$translationCountArr->From</td>
                    <td>$translationCountArr->To</td><td>$translationCountArr->Rating</td>
                    <td>$translationCountArr->Count</td></tr>";
        }
    } else {
        echo "<tr><td col='5'>No Record Found.</td></tr>";
    }
    echo "</table>";
    exit;
} catch (Exception $e) {
    echo "Exception: " . $e->getMessage() . PHP_EOL;
}
```                                        
                                          



