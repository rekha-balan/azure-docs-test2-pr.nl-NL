---
title: Moderate text with custom term lists in Azure Content Moderator | Microsoft Docs
description: Test-drive custom term lists in the Content Moderator API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/05/2017
ms.author: sajagtap
ms.openlocfilehash: 2542e4590781879408aafe8d072eceef157e02c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967303"
---
# <a name="moderate-with-custom-term-lists-in-the-api-console"></a><span data-ttu-id="095d6-103">Moderate with custom term lists in the API console</span><span class="sxs-lookup"><span data-stu-id="095d6-103">Moderate with custom term lists in the API console</span></span>

<span data-ttu-id="095d6-104">The default global list of terms in Azure Content Moderator is sufficient for most content moderation needs.</span><span class="sxs-lookup"><span data-stu-id="095d6-104">The default global list of terms in Azure Content Moderator is sufficient for most content moderation needs.</span></span> <span data-ttu-id="095d6-105">However, you might need to screen for terms that are specific to your organization.</span><span class="sxs-lookup"><span data-stu-id="095d6-105">However, you might need to screen for terms that are specific to your organization.</span></span> <span data-ttu-id="095d6-106">For example, you might want to tag competitor names for further review.</span><span class="sxs-lookup"><span data-stu-id="095d6-106">For example, you might want to tag competitor names for further review.</span></span> 

<span data-ttu-id="095d6-107">Use the [List Management API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f) to create custom lists of terms to use with the Text Moderation API.</span><span class="sxs-lookup"><span data-stu-id="095d6-107">Use the [List Management API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f) to create custom lists of terms to use with the Text Moderation API.</span></span> <span data-ttu-id="095d6-108">The **Text - Screen** operation scans your text for profanity, and also compares text against custom and shared blacklists.</span><span class="sxs-lookup"><span data-stu-id="095d6-108">The **Text - Screen** operation scans your text for profanity, and also compares text against custom and shared blacklists.</span></span>

> [!NOTE]
> <span data-ttu-id="095d6-109">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span><span class="sxs-lookup"><span data-stu-id="095d6-109">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span></span>
>

<span data-ttu-id="095d6-110">You can use the List Management API to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="095d6-110">You can use the List Management API to do the following tasks:</span></span>
- <span data-ttu-id="095d6-111">Create a list.</span><span class="sxs-lookup"><span data-stu-id="095d6-111">Create a list.</span></span>
- <span data-ttu-id="095d6-112">Add terms to a list.</span><span class="sxs-lookup"><span data-stu-id="095d6-112">Add terms to a list.</span></span>
- <span data-ttu-id="095d6-113">Screen terms against the terms in a list.</span><span class="sxs-lookup"><span data-stu-id="095d6-113">Screen terms against the terms in a list.</span></span>
- <span data-ttu-id="095d6-114">Delete terms from a list.</span><span class="sxs-lookup"><span data-stu-id="095d6-114">Delete terms from a list.</span></span>
- <span data-ttu-id="095d6-115">Delete a list.</span><span class="sxs-lookup"><span data-stu-id="095d6-115">Delete a list.</span></span>
- <span data-ttu-id="095d6-116">Edit list information.</span><span class="sxs-lookup"><span data-stu-id="095d6-116">Edit list information.</span></span>
- <span data-ttu-id="095d6-117">Refresh the index so that changes to the list are included in a new scan.</span><span class="sxs-lookup"><span data-stu-id="095d6-117">Refresh the index so that changes to the list are included in a new scan.</span></span>

## <a name="use-the-api-console"></a><span data-ttu-id="095d6-118">Use the API console</span><span class="sxs-lookup"><span data-stu-id="095d6-118">Use the API console</span></span>

<span data-ttu-id="095d6-119">Before you can test-drive the API in the online console, you need your subscription key.</span><span class="sxs-lookup"><span data-stu-id="095d6-119">Before you can test-drive the API in the online console, you need your subscription key.</span></span> <span data-ttu-id="095d6-120">This key is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span><span class="sxs-lookup"><span data-stu-id="095d6-120">This key is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span></span> <span data-ttu-id="095d6-121">For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="095d6-121">For more information, see [Overview](overview.md).</span></span>

## <a name="refresh-search-index"></a><span data-ttu-id="095d6-122">Refresh search index</span><span class="sxs-lookup"><span data-stu-id="095d6-122">Refresh search index</span></span>

<span data-ttu-id="095d6-123">After you make changes to a term list, you must refresh its index for changes to be included in future scans.</span><span class="sxs-lookup"><span data-stu-id="095d6-123">After you make changes to a term list, you must refresh its index for changes to be included in future scans.</span></span> <span data-ttu-id="095d6-124">This step is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span><span class="sxs-lookup"><span data-stu-id="095d6-124">This step is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span></span>

1.  <span data-ttu-id="095d6-125">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term Lists**, and then select **Refresh Search Index**.</span><span class="sxs-lookup"><span data-stu-id="095d6-125">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term Lists**, and then select **Refresh Search Index**.</span></span> 

  <span data-ttu-id="095d6-126">The **Term Lists - Refresh Search Index** page opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-126">The **Term Lists - Refresh Search Index** page opens.</span></span>

2. <span data-ttu-id="095d6-127">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="095d6-127">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Term Lists - Refresh Search Index page region selection](images/test-drive-region.png)

  <span data-ttu-id="095d6-129">The **Term Lists - Refresh Search Index** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-129">The **Term Lists - Refresh Search Index** API console opens.</span></span>

3.  <span data-ttu-id="095d6-130">In the **listId** box, enter the list ID.</span><span class="sxs-lookup"><span data-stu-id="095d6-130">In the **listId** box, enter the list ID.</span></span> <span data-ttu-id="095d6-131">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-131">Enter your subscription key, and then select **Send**.</span></span>

  ![Term Lists API - Refresh Search Index console Response content box](images/try-terms-list-refresh-1.png)

## <a name="create-a-term-list"></a><span data-ttu-id="095d6-133">Create a term list</span><span class="sxs-lookup"><span data-stu-id="095d6-133">Create a term list</span></span>
1.  <span data-ttu-id="095d6-134">Go to the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f).</span><span class="sxs-lookup"><span data-stu-id="095d6-134">Go to the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f).</span></span> 

  <span data-ttu-id="095d6-135">The **Term Lists - Create** page opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-135">The **Term Lists - Create** page opens.</span></span>

2.  <span data-ttu-id="095d6-136">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="095d6-136">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Term Lists - Create page region selection](images/test-drive-region.png)

  <span data-ttu-id="095d6-138">The **Term Lists - Create** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-138">The **Term Lists - Create** API console opens.</span></span>
 
3.  <span data-ttu-id="095d6-139">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="095d6-139">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span></span>

4.  <span data-ttu-id="095d6-140">In the **Request body** box, enter values for **Name** (for example, MyList) and **Description**.</span><span class="sxs-lookup"><span data-stu-id="095d6-140">In the **Request body** box, enter values for **Name** (for example, MyList) and **Description**.</span></span>

  ![Term Lists - Create console Request body name and description](images/try-terms-list-create-1.png)

5.  <span data-ttu-id="095d6-142">Use key-value pair placeholders to assign more descriptive metadata to your list.</span><span class="sxs-lookup"><span data-stu-id="095d6-142">Use key-value pair placeholders to assign more descriptive metadata to your list.</span></span>

        {
           "Name": "MyExclusionList",
           "Description": "MyListDescription",
           "Metadata": 
           {
              "Category": "Competitors",
              "Type": "Exclude"
           }
        }

  <span data-ttu-id="095d6-143">Add list metadata as key-value pairs, and not actual terms.</span><span class="sxs-lookup"><span data-stu-id="095d6-143">Add list metadata as key-value pairs, and not actual terms.</span></span>
 
6.  <span data-ttu-id="095d6-144">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-144">Select **Send**.</span></span> <span data-ttu-id="095d6-145">Your list is created.</span><span class="sxs-lookup"><span data-stu-id="095d6-145">Your list is created.</span></span> <span data-ttu-id="095d6-146">Note the **ID** value that is associated with the new list.</span><span class="sxs-lookup"><span data-stu-id="095d6-146">Note the **ID** value that is associated with the new list.</span></span> <span data-ttu-id="095d6-147">You need this ID for other term list management functions.</span><span class="sxs-lookup"><span data-stu-id="095d6-147">You need this ID for other term list management functions.</span></span>

  ![Term Lists - Create console Response content box shows the list ID](images/try-terms-list-create-2.png)
 
7.  <span data-ttu-id="095d6-149">Add terms to MyList.</span><span class="sxs-lookup"><span data-stu-id="095d6-149">Add terms to MyList.</span></span> <span data-ttu-id="095d6-150">In the left menu, under **Term**, select **Add Term**.</span><span class="sxs-lookup"><span data-stu-id="095d6-150">In the left menu, under **Term**, select **Add Term**.</span></span> 

  <span data-ttu-id="095d6-151">The **Term - Add Term** page opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-151">The **Term - Add Term** page opens.</span></span> 

8.  <span data-ttu-id="095d6-152">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="095d6-152">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Term - Add Term page region selection](images/test-drive-region.png)

  <span data-ttu-id="095d6-154">The **Term - Add Term** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-154">The **Term - Add Term** API console opens.</span></span>
 
9.  <span data-ttu-id="095d6-155">In the **listId** box, enter the list ID that you generated, and select a value for **language**.</span><span class="sxs-lookup"><span data-stu-id="095d6-155">In the **listId** box, enter the list ID that you generated, and select a value for **language**.</span></span> <span data-ttu-id="095d6-156">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-156">Enter your subscription key, and then select **Send**.</span></span>

  ![Term - Add Term console query parameters](images/try-terms-list-create-3.png)
 
10. <span data-ttu-id="095d6-158">To verify that the term has been added to the list, in the left menu, select **Term**, and then select **Get All Terms**.</span><span class="sxs-lookup"><span data-stu-id="095d6-158">To verify that the term has been added to the list, in the left menu, select **Term**, and then select **Get All Terms**.</span></span> 

  <span data-ttu-id="095d6-159">The **Term - Get All Terms** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-159">The **Term - Get All Terms** API console opens.</span></span>

11. <span data-ttu-id="095d6-160">In the **listId** box, enter the list ID, and then enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="095d6-160">In the **listId** box, enter the list ID, and then enter your subscription key.</span></span> <span data-ttu-id="095d6-161">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-161">Select **Send**.</span></span>

12. <span data-ttu-id="095d6-162">In the **Response content** box, verify the terms you entered.</span><span class="sxs-lookup"><span data-stu-id="095d6-162">In the **Response content** box, verify the terms you entered.</span></span>

  ![Term - Get All Terms console Response content box lists the terms that you entered](images/try-terms-list-create-4.png)
 
13. <span data-ttu-id="095d6-164">Add a few more terms.</span><span class="sxs-lookup"><span data-stu-id="095d6-164">Add a few more terms.</span></span> <span data-ttu-id="095d6-165">Now that you have created a custom list of terms, try [scanning some text](try-text-api.md) by using the custom term list.</span><span class="sxs-lookup"><span data-stu-id="095d6-165">Now that you have created a custom list of terms, try [scanning some text](try-text-api.md) by using the custom term list.</span></span> 

## <a name="delete-terms-and-lists"></a><span data-ttu-id="095d6-166">Delete terms and lists</span><span class="sxs-lookup"><span data-stu-id="095d6-166">Delete terms and lists</span></span>

<span data-ttu-id="095d6-167">Deleting a term or a list is straightforward.</span><span class="sxs-lookup"><span data-stu-id="095d6-167">Deleting a term or a list is straightforward.</span></span> <span data-ttu-id="095d6-168">You use the API to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="095d6-168">You use the API to do the following tasks:</span></span>

- <span data-ttu-id="095d6-169">Delete a term.</span><span class="sxs-lookup"><span data-stu-id="095d6-169">Delete a term.</span></span> <span data-ttu-id="095d6-170">(**Term - Delete**)</span><span class="sxs-lookup"><span data-stu-id="095d6-170">(**Term - Delete**)</span></span>
- <span data-ttu-id="095d6-171">Delete all the terms in a list without deleting the list.</span><span class="sxs-lookup"><span data-stu-id="095d6-171">Delete all the terms in a list without deleting the list.</span></span> <span data-ttu-id="095d6-172">(**Term - Delete All Terms**)</span><span class="sxs-lookup"><span data-stu-id="095d6-172">(**Term - Delete All Terms**)</span></span>
- <span data-ttu-id="095d6-173">Delete a list and all of its contents.</span><span class="sxs-lookup"><span data-stu-id="095d6-173">Delete a list and all of its contents.</span></span> <span data-ttu-id="095d6-174">(**Term Lists - Delete**)</span><span class="sxs-lookup"><span data-stu-id="095d6-174">(**Term Lists - Delete**)</span></span>

<span data-ttu-id="095d6-175">This example deletes a single term.</span><span class="sxs-lookup"><span data-stu-id="095d6-175">This example deletes a single term.</span></span>

1.  <span data-ttu-id="095d6-176">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term**, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="095d6-176">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term**, and then select **Delete**.</span></span> 

  <span data-ttu-id="095d6-177">The **Term - Delete** opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-177">The **Term - Delete** opens.</span></span>

2. <span data-ttu-id="095d6-178">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="095d6-178">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Term - Delete page region selection](images/test-drive-region.png)

  <span data-ttu-id="095d6-180">The **Term - Delete** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-180">The **Term - Delete** API console opens.</span></span>
  
3.  <span data-ttu-id="095d6-181">In the **listId** box, enter the ID of the list that you want to delete a term from.</span><span class="sxs-lookup"><span data-stu-id="095d6-181">In the **listId** box, enter the ID of the list that you want to delete a term from.</span></span> <span data-ttu-id="095d6-182">This ID is the number (in our example, **122**) that is returned in the **Term Lists - Get Details** console for MyList.</span><span class="sxs-lookup"><span data-stu-id="095d6-182">This ID is the number (in our example, **122**) that is returned in the **Term Lists - Get Details** console for MyList.</span></span> <span data-ttu-id="095d6-183">Enter the term and select a language.</span><span class="sxs-lookup"><span data-stu-id="095d6-183">Enter the term and select a language.</span></span>
 
  ![Term - Delete console query parameters](images/try-terms-list-delete-1.png)

4.  <span data-ttu-id="095d6-185">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-185">Enter your subscription key, and then select **Send**.</span></span>

5.  <span data-ttu-id="095d6-186">To verify that the term has been deleted, use the **Term Lists - Get All** console.</span><span class="sxs-lookup"><span data-stu-id="095d6-186">To verify that the term has been deleted, use the **Term Lists - Get All** console.</span></span>

  ![Term Lists - Get All console Response content box shows that term is deleted](images/try-terms-list-delete-2.png)
 
## <a name="change-list-information"></a><span data-ttu-id="095d6-188">Change list information</span><span class="sxs-lookup"><span data-stu-id="095d6-188">Change list information</span></span>

<span data-ttu-id="095d6-189">You can edit a list’s name and description, and add metadata items.</span><span class="sxs-lookup"><span data-stu-id="095d6-189">You can edit a list’s name and description, and add metadata items.</span></span>

1.  <span data-ttu-id="095d6-190">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term Lists**, and then select **Update Details**.</span><span class="sxs-lookup"><span data-stu-id="095d6-190">In the [Term List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f), in the left menu, select **Term Lists**, and then select **Update Details**.</span></span> 

  <span data-ttu-id="095d6-191">The **Term Lists - Update Details** page opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-191">The **Term Lists - Update Details** page opens.</span></span>

2. <span data-ttu-id="095d6-192">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="095d6-192">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Term Lists - Update Details page region selection](images/test-drive-region.png)

  <span data-ttu-id="095d6-194">The **Term Lists - Update Details** API console opens.</span><span class="sxs-lookup"><span data-stu-id="095d6-194">The **Term Lists - Update Details** API console opens.</span></span>

3.  <span data-ttu-id="095d6-195">In the **listId** box, enter the list ID, and then enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="095d6-195">In the **listId** box, enter the list ID, and then enter your subscription key.</span></span>

4.  <span data-ttu-id="095d6-196">In the **Request body** box, make your edits, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="095d6-196">In the **Request body** box, make your edits, and then select **Send**.</span></span>

  ![Term Lists - Update Details console Request body edits](images/try-terms-list-change-1.png)
 

## <a name="next-steps"></a><span data-ttu-id="095d6-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="095d6-198">Next steps</span></span>

<span data-ttu-id="095d6-199">Use the REST API in your code or start with the [Term lists .NET quickstart](term-lists-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="095d6-199">Use the REST API in your code or start with the [Term lists .NET quickstart](term-lists-quickstart-dotnet.md) to integrate with your application.</span></span>
