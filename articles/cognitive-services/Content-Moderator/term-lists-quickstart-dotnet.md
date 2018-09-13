---
title: Moderate with custom term lists in Azure Content Moderator | Microsoft Docs
description: How to moderate with custom term lists using Azure Content Moderator SDK for .NET.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/10/2018
ms.author: sajagtap
ms.openlocfilehash: d111f4eeea6a7cd630e550b0f57ad1617eb2bcd0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870717"
---
# <a name="moderate-with-custom-term-lists-in-net"></a><span data-ttu-id="7e968-103">Moderate with custom term lists in .NET</span><span class="sxs-lookup"><span data-stu-id="7e968-103">Moderate with custom term lists in .NET</span></span>

<span data-ttu-id="7e968-104">The default global list of terms in Azure Content Moderator is sufficient for most content moderation needs.</span><span class="sxs-lookup"><span data-stu-id="7e968-104">The default global list of terms in Azure Content Moderator is sufficient for most content moderation needs.</span></span> <span data-ttu-id="7e968-105">However, you might need to screen for terms that are specific to your organization.</span><span class="sxs-lookup"><span data-stu-id="7e968-105">However, you might need to screen for terms that are specific to your organization.</span></span> <span data-ttu-id="7e968-106">For example, you might want to tag competitor names for further review.</span><span class="sxs-lookup"><span data-stu-id="7e968-106">For example, you might want to tag competitor names for further review.</span></span> 

<span data-ttu-id="7e968-107">You can use the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to create custom lists of terms to use with the Text Moderation API.</span><span class="sxs-lookup"><span data-stu-id="7e968-107">You can use the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to create custom lists of terms to use with the Text Moderation API.</span></span>

> [!NOTE]
> <span data-ttu-id="7e968-108">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span><span class="sxs-lookup"><span data-stu-id="7e968-108">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span></span>
>

<span data-ttu-id="7e968-109">This article provides information and code samples to help you get started using the Content Moderator SDK for .NET to:</span><span class="sxs-lookup"><span data-stu-id="7e968-109">This article provides information and code samples to help you get started using the Content Moderator SDK for .NET to:</span></span>
- <span data-ttu-id="7e968-110">Create a list.</span><span class="sxs-lookup"><span data-stu-id="7e968-110">Create a list.</span></span>
- <span data-ttu-id="7e968-111">Add terms to a list.</span><span class="sxs-lookup"><span data-stu-id="7e968-111">Add terms to a list.</span></span>
- <span data-ttu-id="7e968-112">Screen terms against the terms in a list.</span><span class="sxs-lookup"><span data-stu-id="7e968-112">Screen terms against the terms in a list.</span></span>
- <span data-ttu-id="7e968-113">Delete terms from a list.</span><span class="sxs-lookup"><span data-stu-id="7e968-113">Delete terms from a list.</span></span>
- <span data-ttu-id="7e968-114">Delete a list.</span><span class="sxs-lookup"><span data-stu-id="7e968-114">Delete a list.</span></span>
- <span data-ttu-id="7e968-115">Edit list information.</span><span class="sxs-lookup"><span data-stu-id="7e968-115">Edit list information.</span></span>
- <span data-ttu-id="7e968-116">Refresh the index so that changes to the list are included in a new scan.</span><span class="sxs-lookup"><span data-stu-id="7e968-116">Refresh the index so that changes to the list are included in a new scan.</span></span>

<span data-ttu-id="7e968-117">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="7e968-117">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator-services"></a><span data-ttu-id="7e968-118">Sign up for Content Moderator services</span><span class="sxs-lookup"><span data-stu-id="7e968-118">Sign up for Content Moderator services</span></span>

<span data-ttu-id="7e968-119">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="7e968-119">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>

<span data-ttu-id="7e968-120">In the Content Moderator Dashboard, you can find your subscription key in **Settings** > **Credentials** > **API** > **Trial Ocp-Apim-Subscription-Key**.</span><span class="sxs-lookup"><span data-stu-id="7e968-120">In the Content Moderator Dashboard, you can find your subscription key in **Settings** > **Credentials** > **API** > **Trial Ocp-Apim-Subscription-Key**.</span></span> <span data-ttu-id="7e968-121">For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e968-121">For more information, see [Overview](overview.md).</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="7e968-122">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="7e968-122">Create your Visual Studio project</span></span>

1. <span data-ttu-id="7e968-123">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="7e968-123">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

1. <span data-ttu-id="7e968-124">Name the project **TermLists**.</span><span class="sxs-lookup"><span data-stu-id="7e968-124">Name the project **TermLists**.</span></span> <span data-ttu-id="7e968-125">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="7e968-125">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="7e968-126">Install required packages</span><span class="sxs-lookup"><span data-stu-id="7e968-126">Install required packages</span></span>

<span data-ttu-id="7e968-127">Install the following NuGet packages for the TermLists project:</span><span class="sxs-lookup"><span data-stu-id="7e968-127">Install the following NuGet packages for the TermLists project:</span></span>

- <span data-ttu-id="7e968-128">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="7e968-128">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="7e968-129">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="7e968-129">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="7e968-130">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="7e968-130">Microsoft.Rest.ClientRuntime.Azure</span></span>
- <span data-ttu-id="7e968-131">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="7e968-131">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="7e968-132">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="7e968-132">Update the program's using statements</span></span>

<span data-ttu-id="7e968-133">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="7e968-133">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="7e968-134">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="7e968-134">Create the Content Moderator client</span></span>

<span data-ttu-id="7e968-135">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7e968-135">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e968-136">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="7e968-136">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>


    /// <summary>
    /// Wraps the creation and configuration of a Content Moderator client.
    /// </summary>
    /// <remarks>This class library contains insecure code. If you adapt this 
    /// code for use in production, use a secure method of storing and using
    /// your Content Moderator subscription key.</remarks>
    public static class Clients
    {
        /// <summary>
        /// The region/location for your Content Moderator account, 
        /// for example, westus.
        /// </summary>
        private static readonly string AzureRegion = "YOUR API REGION";

        /// <summary>
        /// The base URL fragment for Content Moderator calls.
        /// </summary>
        private static readonly string AzureBaseURL =
            $"https://{AzureRegion}.api.cognitive.microsoft.com";

        /// <summary>
        /// Your Content Moderator subscription key.
        /// </summary>
        private static readonly string CMSubscriptionKey = "YOUR API KEY";

        /// <summary>
        /// Returns a new Content Moderator client for your subscription.
        /// </summary>
        /// <returns>The new client.</returns>
        /// <remarks>The <see cref="ContentModeratorClient"/> is disposable.
        /// When you have finished using the client,
        /// you should dispose of it either directly or indirectly. </remarks>
        public static ContentModeratorClient NewClient()
        {
            // Create and initialize an instance of the Content Moderator API wrapper.
            ContentModeratorClient client = new ContentModeratorClient(new ApiKeyServiceClientCredentials(CMSubscriptionKey));

            client.BaseUrl = AzureBaseURL;
            return client;
        }
    }

### <a name="add-private-properties"></a><span data-ttu-id="7e968-137">Add private properties</span><span class="sxs-lookup"><span data-stu-id="7e968-137">Add private properties</span></span>

<span data-ttu-id="7e968-138">Add the following private properties to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-138">Add the following private properties to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// The language of the terms in the term lists.
    /// </summary>
    private const string lang = "eng";

    /// <summary>
    /// The minimum amount of time, in milliseconds, to wait between calls
    /// to the Content Moderator APIs.
    /// </summary>
    private const int throttleRate = 3000;

    /// <summary>
    /// The number of minutes to delay after updating the search index before
    /// performing image match operations against a the list.
    /// </summary>
    private const double latencyDelay = 0.5;

## <a name="create-a-term-list"></a><span data-ttu-id="7e968-139">Create a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-139">Create a term list</span></span>

<span data-ttu-id="7e968-140">You create a term list with **ContentModeratorClient.ListManagementTermLists.Create**.</span><span class="sxs-lookup"><span data-stu-id="7e968-140">You create a term list with **ContentModeratorClient.ListManagementTermLists.Create**.</span></span> <span data-ttu-id="7e968-141">The first parameter to **Create** is a string that contains a MIME type, which should be "application/json".</span><span class="sxs-lookup"><span data-stu-id="7e968-141">The first parameter to **Create** is a string that contains a MIME type, which should be "application/json".</span></span> <span data-ttu-id="7e968-142">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f).</span><span class="sxs-lookup"><span data-stu-id="7e968-142">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f).</span></span> <span data-ttu-id="7e968-143">The second parameter is a **Body** object that contains a name and description for the new term list.</span><span class="sxs-lookup"><span data-stu-id="7e968-143">The second parameter is a **Body** object that contains a name and description for the new term list.</span></span>

<span data-ttu-id="7e968-144">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-144">Add the following method definition to namespace TermLists, class Program.</span></span>

> [!NOTE]
> <span data-ttu-id="7e968-145">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="7e968-145">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="7e968-146">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="7e968-146">A free tier key has a one RPS rate limit.</span></span>

    /// <summary>
    /// Creates a new term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <returns>The term list ID.</returns>
    static string CreateTermList (ContentModeratorClient client)
    {
        Console.WriteLine("Creating term list.");

        Body body = new Body("Term list name", "Term list description");
        TermList list = client.ListManagementTermLists.Create("application/json", body);
        if (false == list.Id.HasValue)
        {
            throw new Exception("TermList.Id value missing.");
        }
        else
        {
            string list_id = list.Id.Value.ToString();
            Console.WriteLine("Term list created. ID: {0}.", list_id);
            Thread.Sleep(throttleRate);
            return list_id;
        }
    }

## <a name="update-term-list-name-and-description"></a><span data-ttu-id="7e968-147">Update term list name and description</span><span class="sxs-lookup"><span data-stu-id="7e968-147">Update term list name and description</span></span>

<span data-ttu-id="7e968-148">You update the term list information with **ContentModeratorClient.ListManagementTermLists.Update**.</span><span class="sxs-lookup"><span data-stu-id="7e968-148">You update the term list information with **ContentModeratorClient.ListManagementTermLists.Update**.</span></span> <span data-ttu-id="7e968-149">The first parameter to **Update** is the term list ID.</span><span class="sxs-lookup"><span data-stu-id="7e968-149">The first parameter to **Update** is the term list ID.</span></span> <span data-ttu-id="7e968-150">The second parameter is a MIME type, which should be "application/json".</span><span class="sxs-lookup"><span data-stu-id="7e968-150">The second parameter is a MIME type, which should be "application/json".</span></span> <span data-ttu-id="7e968-151">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f685).</span><span class="sxs-lookup"><span data-stu-id="7e968-151">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f685).</span></span> <span data-ttu-id="7e968-152">The third parameter is a **Body** object, which contains the new name and description.</span><span class="sxs-lookup"><span data-stu-id="7e968-152">The third parameter is a **Body** object, which contains the new name and description.</span></span>

<span data-ttu-id="7e968-153">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-153">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Update the information for the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list to update.</param>
    /// <param name="name">The new name for the term list.</param>
    /// <param name="description">The new description for the term list.</param>
    static void UpdateTermList (ContentModeratorClient client, string list_id, string name = null, string description = null)
    {
        Console.WriteLine("Updating information for term list with ID {0}.", list_id);
        Body body = new Body(name, description);
        client.ListManagementTermLists.Update(list_id, "application/json", body);
        Thread.Sleep(throttleRate);
    }

## <a name="add-a-term-to-a-term-list"></a><span data-ttu-id="7e968-154">Add a term to a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-154">Add a term to a term list</span></span>

<span data-ttu-id="7e968-155">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-155">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Add a term to the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list to update.</param>
    /// <param name="term">The term to add to the term list.</param>
    static void AddTerm (ContentModeratorClient client, string list_id, string term)
    {
        Console.WriteLine("Adding term \"{0}\" to term list with ID {1}.", term, list_id);
        client.ListManagementTerm.AddTerm(list_id, term, lang);
        Thread.Sleep(throttleRate);
    }

## <a name="get-all-terms-in-a-term-list"></a><span data-ttu-id="7e968-156">Get all terms in a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-156">Get all terms in a term list</span></span>

<span data-ttu-id="7e968-157">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-157">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Get all terms in the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list from which to get all terms.</param>
    static void GetAllTerms(ContentModeratorClient client, string list_id)
    {
        Console.WriteLine("Getting terms in term list with ID {0}.", list_id);
        Terms terms = client.ListManagementTerm.GetAllTerms(list_id, lang);
        TermsData data = terms.Data;
        foreach (TermsInList term in data.Terms)
        {
            Console.WriteLine(term.Term);
        }
        Thread.Sleep(throttleRate);
    }

## <a name="add-code-to-refresh-the-search-index"></a><span data-ttu-id="7e968-158">Add code to refresh the search index</span><span class="sxs-lookup"><span data-stu-id="7e968-158">Add code to refresh the search index</span></span>

<span data-ttu-id="7e968-159">After you make changes to a term list, you refresh its search index for the changes to be included the next time you use the term list to screen text.</span><span class="sxs-lookup"><span data-stu-id="7e968-159">After you make changes to a term list, you refresh its search index for the changes to be included the next time you use the term list to screen text.</span></span> <span data-ttu-id="7e968-160">This is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span><span class="sxs-lookup"><span data-stu-id="7e968-160">This is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span></span>

<span data-ttu-id="7e968-161">You refresh a term list search index with **ContentModeratorClient.ListManagementTermLists.RefreshIndexMethod**.</span><span class="sxs-lookup"><span data-stu-id="7e968-161">You refresh a term list search index with **ContentModeratorClient.ListManagementTermLists.RefreshIndexMethod**.</span></span>

<span data-ttu-id="7e968-162">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-162">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Refresh the search index for the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list to refresh.</param>
    static void RefreshSearchIndex (ContentModeratorClient client, string list_id)
    {
        Console.WriteLine("Refreshing search index for term list with ID {0}.", list_id);
        client.ListManagementTermLists.RefreshIndexMethod(list_id, lang);
        Thread.Sleep((int)(latencyDelay * 60 * 1000));
    }

## <a name="screen-text-using-a-term-list"></a><span data-ttu-id="7e968-163">Screen text using a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-163">Screen text using a term list</span></span>

<span data-ttu-id="7e968-164">You screen text using a term list with **ContentModeratorClient.TextModeration.ScreenText**, which takes the following parameters.</span><span class="sxs-lookup"><span data-stu-id="7e968-164">You screen text using a term list with **ContentModeratorClient.TextModeration.ScreenText**, which takes the following parameters.</span></span>

- <span data-ttu-id="7e968-165">The language of the terms in the term list.</span><span class="sxs-lookup"><span data-stu-id="7e968-165">The language of the terms in the term list.</span></span>
- <span data-ttu-id="7e968-166">A MIME type, which can be "text/html", "text/xml", "text/markdown", or "text/plain".</span><span class="sxs-lookup"><span data-stu-id="7e968-166">A MIME type, which can be "text/html", "text/xml", "text/markdown", or "text/plain".</span></span>
- <span data-ttu-id="7e968-167">The text to screen.</span><span class="sxs-lookup"><span data-stu-id="7e968-167">The text to screen.</span></span>
- <span data-ttu-id="7e968-168">A boolean value.</span><span class="sxs-lookup"><span data-stu-id="7e968-168">A boolean value.</span></span> <span data-ttu-id="7e968-169">Set this field to **true** to autocorrect the text before screening it.</span><span class="sxs-lookup"><span data-stu-id="7e968-169">Set this field to **true** to autocorrect the text before screening it.</span></span>
- <span data-ttu-id="7e968-170">A boolean value.</span><span class="sxs-lookup"><span data-stu-id="7e968-170">A boolean value.</span></span> <span data-ttu-id="7e968-171">Set this field to **true** to detect Personal Identifiable Information (PII) in the text.</span><span class="sxs-lookup"><span data-stu-id="7e968-171">Set this field to **true** to detect Personal Identifiable Information (PII) in the text.</span></span>
- <span data-ttu-id="7e968-172">The term list ID.</span><span class="sxs-lookup"><span data-stu-id="7e968-172">The term list ID.</span></span>

<span data-ttu-id="7e968-173">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f).</span><span class="sxs-lookup"><span data-stu-id="7e968-173">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f).</span></span>

<span data-ttu-id="7e968-174">**ScreenText** returns a **Screen** object, which has a **Terms** property that lists any terms that Content Moderator detected in the screening.</span><span class="sxs-lookup"><span data-stu-id="7e968-174">**ScreenText** returns a **Screen** object, which has a **Terms** property that lists any terms that Content Moderator detected in the screening.</span></span> <span data-ttu-id="7e968-175">Note that if Content Moderator did not detect any terms during the screening, the **Terms** property has value **null**.</span><span class="sxs-lookup"><span data-stu-id="7e968-175">Note that if Content Moderator did not detect any terms during the screening, the **Terms** property has value **null**.</span></span>

<span data-ttu-id="7e968-176">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-176">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Screen the indicated text for terms in the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list to use to screen the text.</param>
    /// <param name="text">The text to screen.</param>
    static void ScreenText (ContentModeratorClient client, string list_id, string text)
    {
        Console.WriteLine("Screening text: \"{0}\" using term list with ID {1}.", text, list_id);
        Screen screen = client.TextModeration.ScreenText(lang, "text/plain", text, false, false, list_id);
        if (null == screen.Terms)
        {
            Console.WriteLine("No terms from the term list were detected in the text.");
        }
        else
        {
            foreach (DetectedTerms term in screen.Terms)
            {
                Console.WriteLine(String.Format("Found term: \"{0}\" from list ID {1} at index {2}.", term.Term, term.ListId, term.Index));
            }
        }
        read.Sleep(throttleRate);
    }

## <a name="delete-terms-and-lists"></a><span data-ttu-id="7e968-177">Delete terms and lists</span><span class="sxs-lookup"><span data-stu-id="7e968-177">Delete terms and lists</span></span>

<span data-ttu-id="7e968-178">Deleting a term or a list is straightforward.</span><span class="sxs-lookup"><span data-stu-id="7e968-178">Deleting a term or a list is straightforward.</span></span> <span data-ttu-id="7e968-179">You use the SDK to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="7e968-179">You use the SDK to do the following tasks:</span></span>

- <span data-ttu-id="7e968-180">Delete a term.</span><span class="sxs-lookup"><span data-stu-id="7e968-180">Delete a term.</span></span> <span data-ttu-id="7e968-181">(**ContentModeratorClient.ListManagementTerm.DeleteTerm**)</span><span class="sxs-lookup"><span data-stu-id="7e968-181">(**ContentModeratorClient.ListManagementTerm.DeleteTerm**)</span></span>
- <span data-ttu-id="7e968-182">Delete all the terms in a list without deleting the list.</span><span class="sxs-lookup"><span data-stu-id="7e968-182">Delete all the terms in a list without deleting the list.</span></span> <span data-ttu-id="7e968-183">(**ContentModeratorClient.ListManagementTerm.DeleteAllTerms**)</span><span class="sxs-lookup"><span data-stu-id="7e968-183">(**ContentModeratorClient.ListManagementTerm.DeleteAllTerms**)</span></span>
- <span data-ttu-id="7e968-184">Delete a list and all of its contents.</span><span class="sxs-lookup"><span data-stu-id="7e968-184">Delete a list and all of its contents.</span></span> <span data-ttu-id="7e968-185">(**ContentModeratorClient.ListManagementTermLists.Delete**)</span><span class="sxs-lookup"><span data-stu-id="7e968-185">(**ContentModeratorClient.ListManagementTermLists.Delete**)</span></span>

### <a name="delete-a-term"></a><span data-ttu-id="7e968-186">Delete a term</span><span class="sxs-lookup"><span data-stu-id="7e968-186">Delete a term</span></span>

<span data-ttu-id="7e968-187">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-187">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Delete a term from the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list from which to delete the term.</param>
    /// <param name="term">The term to delete.</param>
    static void DeleteTerm (ContentModeratorClient client, string list_id, string term)
    {
        Console.WriteLine("Removed term \"{0}\" from term list with ID {1}.", term, list_id);
        client.ListManagementTerm.DeleteTerm(list_id, term, lang);
        Thread.Sleep(throttleRate);
    }

### <a name="delete-all-terms-in-a-term-list"></a><span data-ttu-id="7e968-188">Delete all terms in a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-188">Delete all terms in a term list</span></span>

<span data-ttu-id="7e968-189">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-189">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Delete all terms from the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list from which to delete all terms.</param>
    static void DeleteAllTerms (ContentModeratorClient client, string list_id)
    {
        Console.WriteLine("Removing all terms from term list with ID {0}.", list_id);
        client.ListManagementTerm.DeleteAllTerms(list_id, lang);
        Thread.Sleep(throttleRate);
    }

### <a name="delete-a-term-list"></a><span data-ttu-id="7e968-190">Delete a term list</span><span class="sxs-lookup"><span data-stu-id="7e968-190">Delete a term list</span></span>

<span data-ttu-id="7e968-191">Add the following method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-191">Add the following method definition to namespace TermLists, class Program.</span></span>

    /// <summary>
    /// Delete the indicated term list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="list_id">The ID of the term list to delete.</param>
    static void DeleteTermList (ContentModeratorClient client, string list_id)
    {
        Console.WriteLine("Deleting term list with ID {0}.", list_id);
        client.ListManagementTermLists.Delete(list_id);
        Thread.Sleep(throttleRate);
    }

## <a name="putting-it-all-together"></a><span data-ttu-id="7e968-192">Putting it all together</span><span class="sxs-lookup"><span data-stu-id="7e968-192">Putting it all together</span></span>

<span data-ttu-id="7e968-193">Add the **Main** method definition to namespace TermLists, class Program.</span><span class="sxs-lookup"><span data-stu-id="7e968-193">Add the **Main** method definition to namespace TermLists, class Program.</span></span> <span data-ttu-id="7e968-194">Finally, close the Program class and the TermLists namespace.</span><span class="sxs-lookup"><span data-stu-id="7e968-194">Finally, close the Program class and the TermLists namespace.</span></span>

    static void Main(string[] args)
    {
        using (var client = Clients.NewClient())
        {
            string list_id = CreateTermList(client);

            UpdateTermList(client, list_id, "name", "description");
            AddTerm(client, list_id, "term1");
            AddTerm(client, list_id, "term2");

            GetAllTerms(client, list_id);

            // Always remember to refresh the search index of your list
            RefreshSearchIndex(client, list_id);

            string text = "This text contains the terms \"term1\" and \"term2\".";
            ScreenText(client, list_id, text);

            DeleteTerm(client, list_id, "term1");

            // Always remember to refresh the search index of your list
            RefreshSearchIndex(client, list_id);

            text = "This text contains the terms \"term1\" and \"term2\".";
            ScreenText(client, list_id, text);

            DeleteAllTerms(client, list_id);
            DeleteTermList(client, list_id);

            Console.WriteLine("Press ENTER to close the application.");
            Console.ReadLine();
        }
    }

## <a name="run-the-application-to-see-the-output"></a><span data-ttu-id="7e968-195">Run the application to see the output</span><span class="sxs-lookup"><span data-stu-id="7e968-195">Run the application to see the output</span></span>

<span data-ttu-id="7e968-196">Your output will be on the following lines but the data may vary.</span><span class="sxs-lookup"><span data-stu-id="7e968-196">Your output will be on the following lines but the data may vary.</span></span>

    Creating term list.
    Term list created. ID: 252.
    Updating information for term list with ID 252.
    
    Adding term "term1" to term list with ID 252.
    Adding term "term2" to term list with ID 252.
    
    Getting terms in term list with ID 252.
    term1
    term2
    
    Refreshing search index for term list with ID 252.
    
    Screening text: "This text contains the terms "term1" and "term2"." using term list with ID 252.
    Found term: "term1" from list ID 252 at index 32.
    Found term: "term2" from list ID 252 at index 46.
    
    Removed term "term1" from term list with ID 252.
    
    Refreshing search index for term list with ID 252.
    
    Screening text: "This text contains the terms "term1" and "term2"." using term list with ID 252.
    Found term: "term2" from list ID 252 at index 46.
    
    Removing all terms from term list with ID 252.
    Deleting term list with ID 252.
    Press ENTER to close the application.
    
## <a name="next-steps"></a><span data-ttu-id="7e968-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="7e968-197">Next steps</span></span>

<span data-ttu-id="7e968-198">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="7e968-198">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
