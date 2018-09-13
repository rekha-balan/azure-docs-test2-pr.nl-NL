---
title: Moderate images by using custom lists in Azure Content Moderator | Microsoft Docs
description: Test-drive custom image lists in the Content Moderator API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/05/2017
ms.author: sajagtap
ms.openlocfilehash: 2d714f017be16d978ffbb877a2b7e78e1caf9169
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968026"
---
# <a name="moderate-with-custom-image-lists-in-the-api-console"></a><span data-ttu-id="4fb4c-103">Moderate with custom image lists in the API console</span><span class="sxs-lookup"><span data-stu-id="4fb4c-103">Moderate with custom image lists in the API console</span></span>

<span data-ttu-id="4fb4c-104">You use the [List Management API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672) in Azure Content Moderator to create custom lists of images.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-104">You use the [List Management API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672) in Azure Content Moderator to create custom lists of images.</span></span> <span data-ttu-id="4fb4c-105">Use the custom lists of images with the Image Moderation API.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-105">Use the custom lists of images with the Image Moderation API.</span></span> <span data-ttu-id="4fb4c-106">The image moderation operation evaluates your image.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-106">The image moderation operation evaluates your image.</span></span> <span data-ttu-id="4fb4c-107">If you create custom lists, the operation also compares it to the images in your custom lists.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-107">If you create custom lists, the operation also compares it to the images in your custom lists.</span></span> <span data-ttu-id="4fb4c-108">You can use custom lists to block or allow the image.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-108">You can use custom lists to block or allow the image.</span></span>

> [!NOTE]
> <span data-ttu-id="4fb4c-109">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-109">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span></span>
>

<span data-ttu-id="4fb4c-110">You use the List Management API to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4fb4c-110">You use the List Management API to do the following tasks:</span></span>

- <span data-ttu-id="4fb4c-111">Create a list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-111">Create a list.</span></span>
- <span data-ttu-id="4fb4c-112">Add images to a list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-112">Add images to a list.</span></span>
- <span data-ttu-id="4fb4c-113">Screen images against the images in a list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-113">Screen images against the images in a list.</span></span>
- <span data-ttu-id="4fb4c-114">Delete images from a list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-114">Delete images from a list.</span></span>
- <span data-ttu-id="4fb4c-115">Delete a list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-115">Delete a list.</span></span>
- <span data-ttu-id="4fb4c-116">Edit list information.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-116">Edit list information.</span></span>
- <span data-ttu-id="4fb4c-117">Refresh the index so that changes to the list are included in a new scan.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-117">Refresh the index so that changes to the list are included in a new scan.</span></span>

## <a name="use-the-api-console"></a><span data-ttu-id="4fb4c-118">Use the API console</span><span class="sxs-lookup"><span data-stu-id="4fb4c-118">Use the API console</span></span>
<span data-ttu-id="4fb4c-119">Before you can test-drive the API in the online console, you need your subscription key.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-119">Before you can test-drive the API in the online console, you need your subscription key.</span></span> <span data-ttu-id="4fb4c-120">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-120">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span></span> <span data-ttu-id="4fb4c-121">For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fb4c-121">For more information, see [Overview](overview.md).</span></span>

## <a name="refresh-search-index"></a><span data-ttu-id="4fb4c-122">Refresh search index</span><span class="sxs-lookup"><span data-stu-id="4fb4c-122">Refresh search index</span></span>

<span data-ttu-id="4fb4c-123">After you make changes to an image list, you must refresh its index for changes to be included in future scans.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-123">After you make changes to an image list, you must refresh its index for changes to be included in future scans.</span></span> <span data-ttu-id="4fb4c-124">This step is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-124">This step is similar to how a search engine on your desktop (if enabled) or a web search engine continually refreshes its index to include new files or pages.</span></span>

1.  <span data-ttu-id="4fb4c-125">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image Lists**, and then select **Refresh Search Index**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-125">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image Lists**, and then select **Refresh Search Index**.</span></span>

  <span data-ttu-id="4fb4c-126">The **Image Lists - Refresh Search Index** page opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-126">The **Image Lists - Refresh Search Index** page opens.</span></span>

2. <span data-ttu-id="4fb4c-127">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-127">For **Open API testing console**, select the region that most closely describes your location.</span></span> 
 
    ![Image Lists - Refresh Search Index page region selection](images/test-drive-region.png)

    <span data-ttu-id="4fb4c-129">The **Image Lists - Refresh Search Index** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-129">The **Image Lists - Refresh Search Index** API console opens.</span></span>

3.  <span data-ttu-id="4fb4c-130">In the **listId** box, enter the list ID.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-130">In the **listId** box, enter the list ID.</span></span> <span data-ttu-id="4fb4c-131">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-131">Enter your subscription key, and then select **Send**.</span></span>

  ![Image Lists - Refresh Search Index console Response content box](images/try-image-list-refresh-1.png)


## <a name="create-an-image-list"></a><span data-ttu-id="4fb4c-133">Create an image list</span><span class="sxs-lookup"><span data-stu-id="4fb4c-133">Create an image list</span></span>

1.  <span data-ttu-id="4fb4c-134">Go to the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672).</span><span class="sxs-lookup"><span data-stu-id="4fb4c-134">Go to the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672).</span></span>

  <span data-ttu-id="4fb4c-135">The **Image Lists - Create** page opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-135">The **Image Lists - Create** page opens.</span></span> 

3.  <span data-ttu-id="4fb4c-136">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-136">For **Open API testing console**, select the region that most closely describes your location.</span></span>

    ![Image Lists - Create page region selection](images/test-drive-region.png)

    <span data-ttu-id="4fb4c-138">The **Image Lists - Create** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-138">The **Image Lists - Create** API console opens.</span></span>
 
4.  <span data-ttu-id="4fb4c-139">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-139">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span></span>

5.  <span data-ttu-id="4fb4c-140">In the **Request body** box, enter values for **Name** (for example, MyList) and **Description**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-140">In the **Request body** box, enter values for **Name** (for example, MyList) and **Description**.</span></span>

  ![Image Lists - Create console Request body name and description](images/try-terms-list-create-1.png)

6.  <span data-ttu-id="4fb4c-142">Use key-value pair placeholders to assign more descriptive metadata to your list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-142">Use key-value pair placeholders to assign more descriptive metadata to your list.</span></span>

        {
           "Name": "MyExclusionList",
           "Description": "MyListDescription",
           "Metadata": 
           {
             "Category": "Competitors",
             "Type": "Exclude"
           }
        }

  <span data-ttu-id="4fb4c-143">Add list metadata as key-value pairs, and not the actual images.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-143">Add list metadata as key-value pairs, and not the actual images.</span></span>
 
7.  <span data-ttu-id="4fb4c-144">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-144">Select **Send**.</span></span> <span data-ttu-id="4fb4c-145">Your list is created.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-145">Your list is created.</span></span> <span data-ttu-id="4fb4c-146">Note the **ID** value that is associated with the new list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-146">Note the **ID** value that is associated with the new list.</span></span> <span data-ttu-id="4fb4c-147">You need this ID for other image list management functions.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-147">You need this ID for other image list management functions.</span></span>

  ![Image Lists - Create console Response content box shows the list ID](images/try-terms-list-create-2.png)
 
8.  <span data-ttu-id="4fb4c-149">Next, add images to MyList.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-149">Next, add images to MyList.</span></span> <span data-ttu-id="4fb4c-150">In the left menu, select **Image**, and then select **Add Image**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-150">In the left menu, select **Image**, and then select **Add Image**.</span></span>

  <span data-ttu-id="4fb4c-151">The **Image - Add Image** page opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-151">The **Image - Add Image** page opens.</span></span> 

9. <span data-ttu-id="4fb4c-152">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-152">For **Open API testing console**, select the region that most closely describes your location.</span></span>

  ![Image - Add Image page region selection](images/test-drive-region.png)

  <span data-ttu-id="4fb4c-154">The **Image - Add Image** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-154">The **Image - Add Image** API console opens.</span></span>
 
10. <span data-ttu-id="4fb4c-155">In the **listId** box, enter the list ID that you generated, and then enter the URL of the image that you want to add.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-155">In the **listId** box, enter the list ID that you generated, and then enter the URL of the image that you want to add.</span></span> <span data-ttu-id="4fb4c-156">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-156">Enter your subscription key, and then select **Send**.</span></span>

11. <span data-ttu-id="4fb4c-157">To verify that the image has been added to the list, in the left menu, select **Image**, and then select **Get All Image Ids**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-157">To verify that the image has been added to the list, in the left menu, select **Image**, and then select **Get All Image Ids**.</span></span>

  <span data-ttu-id="4fb4c-158">The **Image - Get All Image Ids** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-158">The **Image - Get All Image Ids** API console opens.</span></span>
  
12. <span data-ttu-id="4fb4c-159">In the **listId** box, enter the list ID, and then enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-159">In the **listId** box, enter the list ID, and then enter your subscription key.</span></span> <span data-ttu-id="4fb4c-160">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-160">Select **Send**.</span></span>

  ![Image - Get All Image Ids console Response content box lists the images that you entered](images/try-image-list-create-11.png)
 
10. <span data-ttu-id="4fb4c-162">Add a few more images.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-162">Add a few more images.</span></span> <span data-ttu-id="4fb4c-163">Now that you have created a custom list of images, try [evaluating images](try-image-api.md) by using the custom image list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-163">Now that you have created a custom list of images, try [evaluating images](try-image-api.md) by using the custom image list.</span></span> 

## <a name="delete-images-and-lists"></a><span data-ttu-id="4fb4c-164">Delete images and lists</span><span class="sxs-lookup"><span data-stu-id="4fb4c-164">Delete images and lists</span></span>

<span data-ttu-id="4fb4c-165">Deleting an image or a list is straightforward.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-165">Deleting an image or a list is straightforward.</span></span> <span data-ttu-id="4fb4c-166">You can use the API to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4fb4c-166">You can use the API to do the following tasks:</span></span>

- <span data-ttu-id="4fb4c-167">Delete an image.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-167">Delete an image.</span></span> <span data-ttu-id="4fb4c-168">(**Image - Delete**)</span><span class="sxs-lookup"><span data-stu-id="4fb4c-168">(**Image - Delete**)</span></span>
- <span data-ttu-id="4fb4c-169">Delete all the images in a list without deleting the list.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-169">Delete all the images in a list without deleting the list.</span></span> <span data-ttu-id="4fb4c-170">(**Image - Delete All Images**)</span><span class="sxs-lookup"><span data-stu-id="4fb4c-170">(**Image - Delete All Images**)</span></span>
- <span data-ttu-id="4fb4c-171">Delete a list and all of its contents.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-171">Delete a list and all of its contents.</span></span> <span data-ttu-id="4fb4c-172">(**Image Lists - Delete**)</span><span class="sxs-lookup"><span data-stu-id="4fb4c-172">(**Image Lists - Delete**)</span></span>

<span data-ttu-id="4fb4c-173">This example deletes a single image:</span><span class="sxs-lookup"><span data-stu-id="4fb4c-173">This example deletes a single image:</span></span>

1. <span data-ttu-id="4fb4c-174">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image**, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-174">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image**, and then select **Delete**.</span></span> 

  <span data-ttu-id="4fb4c-175">The **Image - Delete** page opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-175">The **Image - Delete** page opens.</span></span>

2. <span data-ttu-id="4fb4c-176">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-176">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Image - Delete page region selection](images/test-drive-region.png)
 
  <span data-ttu-id="4fb4c-178">The **Image - Delete** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-178">The **Image - Delete** API console opens.</span></span>
 
3.  <span data-ttu-id="4fb4c-179">In the **listId** box, enter the ID of the list to delete an image from.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-179">In the **listId** box, enter the ID of the list to delete an image from.</span></span>  <span data-ttu-id="4fb4c-180">This is the number returned in the **Image - Get All Image Ids** console for MyList.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-180">This is the number returned in the **Image - Get All Image Ids** console for MyList.</span></span> <span data-ttu-id="4fb4c-181">Then, enter the **ImageId** of the image to delete.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-181">Then, enter the **ImageId** of the image to delete.</span></span> 

<span data-ttu-id="4fb4c-182">In our example, the list ID is **58953**, the value for **ContentSource**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-182">In our example, the list ID is **58953**, the value for **ContentSource**.</span></span> <span data-ttu-id="4fb4c-183">The image ID is **59021**, the value for **ContentIds**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-183">The image ID is **59021**, the value for **ContentIds**.</span></span>

4.  <span data-ttu-id="4fb4c-184">Enter your subscription key, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-184">Enter your subscription key, and then select **Send**.</span></span>

5.  <span data-ttu-id="4fb4c-185">To verify that the image has been deleted, use the **Image - Get All Image Ids** console.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-185">To verify that the image has been deleted, use the **Image - Get All Image Ids** console.</span></span>
 
## <a name="change-list-information"></a><span data-ttu-id="4fb4c-186">Change list information</span><span class="sxs-lookup"><span data-stu-id="4fb4c-186">Change list information</span></span>

<span data-ttu-id="4fb4c-187">You can edit a list’s name and description, and add metadata items.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-187">You can edit a list’s name and description, and add metadata items.</span></span>

1.  <span data-ttu-id="4fb4c-188">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image Lists**, and then select **Update Details**.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-188">In the [Image List Management API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f672), in the left menu, select **Image Lists**, and then select **Update Details**.</span></span> 

  <span data-ttu-id="4fb4c-189">The **Image Lists - Update Details** page opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-189">The **Image Lists - Update Details** page opens.</span></span>

2. <span data-ttu-id="4fb4c-190">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-190">For **Open API testing console**, select the region that most closely describes your location.</span></span>  

    ![Image Lists - Update Details page region selection](images/test-drive-region.png)

    <span data-ttu-id="4fb4c-192">The **Image Lists - Update Details** API console opens.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-192">The **Image Lists - Update Details** API console opens.</span></span>
 
3.  <span data-ttu-id="4fb4c-193">In the **listId** box, enter the list ID, and then enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-193">In the **listId** box, enter the list ID, and then enter your subscription key.</span></span>

4.  <span data-ttu-id="4fb4c-194">In the **Request body** box, make your edits, and then select the **Send** button on the page.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-194">In the **Request body** box, make your edits, and then select the **Send** button on the page.</span></span>

  ![Image Lists - Update Details console Request body edits](images/try-terms-list-change-1.png)
 

## <a name="next-steps"></a><span data-ttu-id="4fb4c-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="4fb4c-196">Next steps</span></span>

<span data-ttu-id="4fb4c-197">Use the REST API in your code or start with the [Image lists .NET quickstart](image-lists-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="4fb4c-197">Use the REST API in your code or start with the [Image lists .NET quickstart](image-lists-quickstart-dotnet.md) to integrate with your application.</span></span>
