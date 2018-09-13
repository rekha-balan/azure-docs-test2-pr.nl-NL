---
title: eCommerce catalog moderation with machine learning and AI with Azure Content Moderator | Microsoft Docs
description: Automatically moderate eCommerce catalogs with machine learning and AI
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/25/2017
ms.author: sajagtap
ms.openlocfilehash: 6177758eaa3e611ad67da0778d889df48b052d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864789"
---
# <a name="ecommerce-catalog-moderation-with-machine-learning"></a><span data-ttu-id="0449f-103">eCommerce catalog moderation with machine learning</span><span class="sxs-lookup"><span data-stu-id="0449f-103">eCommerce catalog moderation with machine learning</span></span>

<span data-ttu-id="0449f-104">In this tutorial, we learn how to implement machine-learning-based intelligent ecommerce catalog moderation by combining machine-assisted AI technologies with human moderation to provide an intelligent catalog system.</span><span class="sxs-lookup"><span data-stu-id="0449f-104">In this tutorial, we learn how to implement machine-learning-based intelligent ecommerce catalog moderation by combining machine-assisted AI technologies with human moderation to provide an intelligent catalog system.</span></span>

![Classified product images](images/tutorial-ecommerce-content-moderator.PNG)

## <a name="business-scenario"></a><span data-ttu-id="0449f-106">Business scenario</span><span class="sxs-lookup"><span data-stu-id="0449f-106">Business scenario</span></span>

<span data-ttu-id="0449f-107">Use machine-assisted technologies to classify and moderate product images in these categories:</span><span class="sxs-lookup"><span data-stu-id="0449f-107">Use machine-assisted technologies to classify and moderate product images in these categories:</span></span>

1. <span data-ttu-id="0449f-108">Adult (Nudity)</span><span class="sxs-lookup"><span data-stu-id="0449f-108">Adult (Nudity)</span></span>
2. <span data-ttu-id="0449f-109">Racy (Suggestive)</span><span class="sxs-lookup"><span data-stu-id="0449f-109">Racy (Suggestive)</span></span>
3. <span data-ttu-id="0449f-110">Celebrities</span><span class="sxs-lookup"><span data-stu-id="0449f-110">Celebrities</span></span>
4. <span data-ttu-id="0449f-111">US Flags</span><span class="sxs-lookup"><span data-stu-id="0449f-111">US Flags</span></span>
5. <span data-ttu-id="0449f-112">Toys</span><span class="sxs-lookup"><span data-stu-id="0449f-112">Toys</span></span>
6. <span data-ttu-id="0449f-113">Pens</span><span class="sxs-lookup"><span data-stu-id="0449f-113">Pens</span></span>

## <a name="tutorial-steps"></a><span data-ttu-id="0449f-114">Tutorial steps</span><span class="sxs-lookup"><span data-stu-id="0449f-114">Tutorial steps</span></span>

<span data-ttu-id="0449f-115">The tutorial guides you through these steps:</span><span class="sxs-lookup"><span data-stu-id="0449f-115">The tutorial guides you through these steps:</span></span>

1. <span data-ttu-id="0449f-116">Sign up and create a Content Moderator team.</span><span class="sxs-lookup"><span data-stu-id="0449f-116">Sign up and create a Content Moderator team.</span></span>
2. <span data-ttu-id="0449f-117">Configure moderation tags (labels) for potential celebrity and flag content.</span><span class="sxs-lookup"><span data-stu-id="0449f-117">Configure moderation tags (labels) for potential celebrity and flag content.</span></span>
3. <span data-ttu-id="0449f-118">Use Content Moderator's image API to scan for potential adult and racy content.</span><span class="sxs-lookup"><span data-stu-id="0449f-118">Use Content Moderator's image API to scan for potential adult and racy content.</span></span>
4. <span data-ttu-id="0449f-119">Use the Computer Vision API to scan for potential celebrities.</span><span class="sxs-lookup"><span data-stu-id="0449f-119">Use the Computer Vision API to scan for potential celebrities.</span></span>
5. <span data-ttu-id="0449f-120">Use the Custom Vision service to scan for possible presence of flags.</span><span class="sxs-lookup"><span data-stu-id="0449f-120">Use the Custom Vision service to scan for possible presence of flags.</span></span>
6. <span data-ttu-id="0449f-121">Present the nuanced scan results for human review and final decision making.</span><span class="sxs-lookup"><span data-stu-id="0449f-121">Present the nuanced scan results for human review and final decision making.</span></span>

## <a name="create-a-team"></a><span data-ttu-id="0449f-122">Create a team</span><span class="sxs-lookup"><span data-stu-id="0449f-122">Create a team</span></span>

<span data-ttu-id="0449f-123">Refer to the [Quickstart](quick-start.md) page to sign up for Content Moderator and create a team.</span><span class="sxs-lookup"><span data-stu-id="0449f-123">Refer to the [Quickstart](quick-start.md) page to sign up for Content Moderator and create a team.</span></span> <span data-ttu-id="0449f-124">Note the **Team ID** from the **Credentials** page.</span><span class="sxs-lookup"><span data-stu-id="0449f-124">Note the **Team ID** from the **Credentials** page.</span></span>


## <a name="define-custom-tags"></a><span data-ttu-id="0449f-125">Define custom tags</span><span class="sxs-lookup"><span data-stu-id="0449f-125">Define custom tags</span></span>

<span data-ttu-id="0449f-126">Refer to the [Tags](https://docs.microsoft.com/azure/cognitive-services/content-moderator/review-tool-user-guide/tags) article to add custom tags.</span><span class="sxs-lookup"><span data-stu-id="0449f-126">Refer to the [Tags](https://docs.microsoft.com/azure/cognitive-services/content-moderator/review-tool-user-guide/tags) article to add custom tags.</span></span> <span data-ttu-id="0449f-127">In addition to the built-in **adult** and **racy** tags, the new tags allow the review tool to display the descriptive names for the tags.</span><span class="sxs-lookup"><span data-stu-id="0449f-127">In addition to the built-in **adult** and **racy** tags, the new tags allow the review tool to display the descriptive names for the tags.</span></span>

<span data-ttu-id="0449f-128">In our case, we define these custom tags (**celebrity**, **flag**, **us**, **toy**, **pen**):</span><span class="sxs-lookup"><span data-stu-id="0449f-128">In our case, we define these custom tags (**celebrity**, **flag**, **us**, **toy**, **pen**):</span></span>

![Configure custom tags](images/tutorial-ecommerce-tags2.PNG)

## <a name="list-your-api-keys-and-endpoints"></a><span data-ttu-id="0449f-130">List your API keys and endpoints</span><span class="sxs-lookup"><span data-stu-id="0449f-130">List your API keys and endpoints</span></span>

1. <span data-ttu-id="0449f-131">The tutorial uses three APIs and the corresponding keys and API end points.</span><span class="sxs-lookup"><span data-stu-id="0449f-131">The tutorial uses three APIs and the corresponding keys and API end points.</span></span>
2. <span data-ttu-id="0449f-132">Your API end points are different based on your subscription regions and the Content Moderator Review Team ID.</span><span class="sxs-lookup"><span data-stu-id="0449f-132">Your API end points are different based on your subscription regions and the Content Moderator Review Team ID.</span></span>

> [!NOTE]
> <span data-ttu-id="0449f-133">The tutorial is designed to use subscription keys in the regions visible in the following endpoints.</span><span class="sxs-lookup"><span data-stu-id="0449f-133">The tutorial is designed to use subscription keys in the regions visible in the following endpoints.</span></span> <span data-ttu-id="0449f-134">Be sure to match your API keys with the region Uris otherwise your keys may not work with the following endpoints:</span><span class="sxs-lookup"><span data-stu-id="0449f-134">Be sure to match your API keys with the region Uris otherwise your keys may not work with the following endpoints:</span></span>

         // Your API keys
        public const string ContentModeratorKey = "XXXXXXXXXXXXXXXXXXXX";
        public const string ComputerVisionKey = "XXXXXXXXXXXXXXXXXXXX";
        public const string CustomVisionKey = "XXXXXXXXXXXXXXXXXXXX";

        // Your end points URLs will look different based on your region and Content Moderator Team ID.
        public const string ImageUri = "https://westus.api.cognitive.microsoft.com/contentmoderator/moderate/v1.0/ProcessImage/Evaluate";
        public const string ReviewUri = "https://westus.api.cognitive.microsoft.com/contentmoderator/review/v1.0/teams/YOURTEAMID/reviews";
        public const string ComputerVisionUri = "https://westcentralus.api.cognitive.microsoft.com/vision/v1.0";
        public const string CustomVisionUri = "https://southcentralus.api.cognitive.microsoft.com/customvision/v1.0/Prediction/XXXXXXXXXXXXXXXXXXXX/url";

## <a name="scan-for-adult-and-racy-content"></a><span data-ttu-id="0449f-135">Scan for adult and racy content</span><span class="sxs-lookup"><span data-stu-id="0449f-135">Scan for adult and racy content</span></span>

1. <span data-ttu-id="0449f-136">The function takes an image URL and an array of key-value pairs as parameters.</span><span class="sxs-lookup"><span data-stu-id="0449f-136">The function takes an image URL and an array of key-value pairs as parameters.</span></span>
2. <span data-ttu-id="0449f-137">It calls the Content Moderator's Image API to get the Adult and Racy scores.</span><span class="sxs-lookup"><span data-stu-id="0449f-137">It calls the Content Moderator's Image API to get the Adult and Racy scores.</span></span>
3. <span data-ttu-id="0449f-138">If the score is greater than 0.4 (range is from 0 to 1), it sets the value in the **ReviewTags** array to **True**.</span><span class="sxs-lookup"><span data-stu-id="0449f-138">If the score is greater than 0.4 (range is from 0 to 1), it sets the value in the **ReviewTags** array to **True**.</span></span>
4. <span data-ttu-id="0449f-139">The **ReviewTags** array is used to highlight the corresponding tag in the review tool.</span><span class="sxs-lookup"><span data-stu-id="0449f-139">The **ReviewTags** array is used to highlight the corresponding tag in the review tool.</span></span>

        public static bool EvaluateAdultRacy(string ImageUrl, ref KeyValuePair[] ReviewTags)
        {
            float AdultScore = 0;
            float RacyScore = 0;

            var File = ImageUrl;
            string Body = $"{{\"DataRepresentation\":\"URL\",\"Value\":\"{File}\"}}";

            HttpResponseMessage response = CallAPI(ImageUri, ContentModeratorKey, CallType.POST,
                                                   "Ocp-Apim-Subscription-Key", "application/json", "", Body);

            if (response.IsSuccessStatusCode)
            {
                // {“answers”:[{“answer”:“Hello”,“questions”:[“Hi”],“score”:100.0}]}
                // Parse the response body. Blocking!
                GetAdultRacyScores(response.Content.ReadAsStringAsync().Result, out AdultScore, out RacyScore);
            }

            ReviewTags[0] = new KeyValuePair();
            ReviewTags[0].Key = "a";
            ReviewTags[0].Value = "false";
            if (AdultScore > 0.4)
            {
                ReviewTags[0].Value = "true";
            }

            ReviewTags[1] = new KeyValuePair();
            ReviewTags[1].Key = "r";
            ReviewTags[1].Value = "false";
            if (RacyScore > 0.3)
            {
                ReviewTags[1].Value = "true";
            }
            return response.IsSuccessStatusCode;
        }

## <a name="scan-for-celebrities"></a><span data-ttu-id="0449f-140">Scan for celebrities</span><span class="sxs-lookup"><span data-stu-id="0449f-140">Scan for celebrities</span></span>

1. <span data-ttu-id="0449f-141">Sign up for a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=computer-vision) of the [Computer Vision API](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span><span class="sxs-lookup"><span data-stu-id="0449f-141">Sign up for a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=computer-vision) of the [Computer Vision API](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span></span>
2. <span data-ttu-id="0449f-142">Click the **Get API Key** button.</span><span class="sxs-lookup"><span data-stu-id="0449f-142">Click the **Get API Key** button.</span></span>
3. <span data-ttu-id="0449f-143">Accept the terms.</span><span class="sxs-lookup"><span data-stu-id="0449f-143">Accept the terms.</span></span>
4. <span data-ttu-id="0449f-144">To login, choose from the list of Internet accounts available.</span><span class="sxs-lookup"><span data-stu-id="0449f-144">To login, choose from the list of Internet accounts available.</span></span>
5. <span data-ttu-id="0449f-145">Note the API keys displayed on your service page.</span><span class="sxs-lookup"><span data-stu-id="0449f-145">Note the API keys displayed on your service page.</span></span>
    
   ![Computer Vision API keys](images/tutorial-computer-vision-keys.PNG)
    
6. <span data-ttu-id="0449f-147">Refer to the project source code for the function that scans the image with the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="0449f-147">Refer to the project source code for the function that scans the image with the Computer Vision API.</span></span>

         public static bool EvaluateComputerVisionTags(string ImageUrl, string ComputerVisionUri, string ComputerVisionKey, ref KeyValuePair[] ReviewTags)
        {
            var File = ImageUrl;
            string Body = $"{{\"URL\":\"{File}\"}}";

            HttpResponseMessage Response = CallAPI(ComputerVisionUri, ComputerVisionKey, CallType.POST,
                                                   "Ocp-Apim-Subscription-Key", "application/json", "", Body);

            if (Response.IsSuccessStatusCode)
            {
                ReviewTags[2] = new KeyValuePair();
                ReviewTags[2].Key = "cb";
                ReviewTags[2].Value = "false";

                ComputerVisionPrediction CVObject = JsonConvert.DeserializeObject<ComputerVisionPrediction>(Response.Content.ReadAsStringAsync().Result);

                if ((CVObject.categories[0].detail != null) && (CVObject.categories[0].detail.celebrities.Count() > 0))
                {                 
                    ReviewTags[2].Value = "true";
                }
            }

            return Response.IsSuccessStatusCode;
        }

## <a name="classify-into-flags-toys-and-pens"></a><span data-ttu-id="0449f-148">Classify into flags, toys, and pens</span><span class="sxs-lookup"><span data-stu-id="0449f-148">Classify into flags, toys, and pens</span></span>

1. <span data-ttu-id="0449f-149">[Sign in](https://azure.microsoft.com/en-us/services/cognitive-services/custom-vision-service/) to the [Custom Vision API preview](https://www.customvision.ai/).</span><span class="sxs-lookup"><span data-stu-id="0449f-149">[Sign in](https://azure.microsoft.com/en-us/services/cognitive-services/custom-vision-service/) to the [Custom Vision API preview](https://www.customvision.ai/).</span></span>
2. <span data-ttu-id="0449f-150">Use the [Quickstart](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) to build your custom classifier to detect the potential presence of flags, toys, and pens.</span><span class="sxs-lookup"><span data-stu-id="0449f-150">Use the [Quickstart](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) to build your custom classifier to detect the potential presence of flags, toys, and pens.</span></span>
   <span data-ttu-id="0449f-151">![Custom Vision Training Images](images/tutorial-ecommerce-custom-vision.PNG)</span><span class="sxs-lookup"><span data-stu-id="0449f-151">![Custom Vision Training Images](images/tutorial-ecommerce-custom-vision.PNG)</span></span>
3. <span data-ttu-id="0449f-152">[Get the prediction endpoint URL](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/use-prediction-api) for your custom classifier.</span><span class="sxs-lookup"><span data-stu-id="0449f-152">[Get the prediction endpoint URL](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/use-prediction-api) for your custom classifier.</span></span>
4. <span data-ttu-id="0449f-153">Refer to the project source code to see the function that calls your custom classifier prediction endpoint to scan your image.</span><span class="sxs-lookup"><span data-stu-id="0449f-153">Refer to the project source code to see the function that calls your custom classifier prediction endpoint to scan your image.</span></span>

        public static bool EvaluateCustomVisionTags(string ImageUrl, string CustomVisionUri, string CustomVisionKey, ref KeyValuePair[] ReviewTags)
        {
            var File = ImageUrl;
            string Body = $"{{\"URL\":\"{File}\"}}";

            HttpResponseMessage response = CallAPI(CustomVisionUri, CustomVisionKey, CallType.POST,
                                                   "Prediction-Key", "application/json", "", Body);

            if (response.IsSuccessStatusCode)
            {
                // Parse the response body. Blocking!
                SaveCustomVisionTags(response.Content.ReadAsStringAsync().Result, ref ReviewTags);
            }
            return response.IsSuccessStatusCode;
        }       
 
## <a name="reviews-for-human-in-the-loop"></a><span data-ttu-id="0449f-154">Reviews for human-in-the-loop</span><span class="sxs-lookup"><span data-stu-id="0449f-154">Reviews for human-in-the-loop</span></span>

1. <span data-ttu-id="0449f-155">In the previous sections, you scanned the incoming images for adult and racy (Content Moderator), celebrities (Computer Vision) and Flags (Custom Vision).</span><span class="sxs-lookup"><span data-stu-id="0449f-155">In the previous sections, you scanned the incoming images for adult and racy (Content Moderator), celebrities (Computer Vision) and Flags (Custom Vision).</span></span>
2. <span data-ttu-id="0449f-156">Based on our match thresholds for each scan, make the nuanced cases available for human review in the review tool.</span><span class="sxs-lookup"><span data-stu-id="0449f-156">Based on our match thresholds for each scan, make the nuanced cases available for human review in the review tool.</span></span>
        <span data-ttu-id="0449f-157">public static bool CreateReview(string ImageUrl, KeyValuePair[] Metadata) {</span><span class="sxs-lookup"><span data-stu-id="0449f-157">public static bool CreateReview(string ImageUrl, KeyValuePair[] Metadata) {</span></span>

            ReviewCreationRequest Review = new ReviewCreationRequest();
            Review.Item[0] = new ReviewItem();
            Review.Item[0].Content = ImageUrl;
            Review.Item[0].Metadata = new KeyValuePair[MAXTAGSCOUNT];
            Metadata.CopyTo(Review.Item[0].Metadata, 0);

            //SortReviewItems(ref Review);

            string Body = JsonConvert.SerializeObject(Review.Item);

            HttpResponseMessage response = CallAPI(ReviewUri, ContentModeratorKey, CallType.POST,
                                                   "Ocp-Apim-Subscription-Key", "application/json", "", Body);

            return response.IsSuccessStatusCode;
        }

## <a name="submit-batch-of-images"></a><span data-ttu-id="0449f-158">Submit batch of images</span><span class="sxs-lookup"><span data-stu-id="0449f-158">Submit batch of images</span></span>

1. <span data-ttu-id="0449f-159">This tutorial assumes a "C:Test" directory with a text file that has a list of image Urls.</span><span class="sxs-lookup"><span data-stu-id="0449f-159">This tutorial assumes a "C:Test" directory with a text file that has a list of image Urls.</span></span>
2. <span data-ttu-id="0449f-160">The following code checks for the existence of the file and reads all Urls into memory.</span><span class="sxs-lookup"><span data-stu-id="0449f-160">The following code checks for the existence of the file and reads all Urls into memory.</span></span>
            <span data-ttu-id="0449f-161">// Check for a test directory for a text file with the list of Image URLs to scan var topdir = @"C:\test\"; var Urlsfile = topdir + "Urls.txt";</span><span class="sxs-lookup"><span data-stu-id="0449f-161">// Check for a test directory for a text file with the list of Image URLs to scan var topdir = @"C:\test\"; var Urlsfile = topdir + "Urls.txt";</span></span>

            if (!Directory.Exists(topdir))
                return;

            if (!File.Exists(Urlsfile))
            {
                return;
            }

            // Read all image URLs in the file
            var Urls = File.ReadLines(Urlsfile);

## <a name="initiate-all-scans"></a><span data-ttu-id="0449f-162">Initiate all scans</span><span class="sxs-lookup"><span data-stu-id="0449f-162">Initiate all scans</span></span>

1. <span data-ttu-id="0449f-163">This top-level function loops through all image URLs in the text file we mentioned earlier.</span><span class="sxs-lookup"><span data-stu-id="0449f-163">This top-level function loops through all image URLs in the text file we mentioned earlier.</span></span>
2. <span data-ttu-id="0449f-164">It scans them with each API and if the match confidence score falls within our criteria, creates a review for human moderators.</span><span class="sxs-lookup"><span data-stu-id="0449f-164">It scans them with each API and if the match confidence score falls within our criteria, creates a review for human moderators.</span></span>
             <span data-ttu-id="0449f-165">// for each image URL in the file... foreach (var Url in Urls) { // Initiatize a new review tags array ReviewTags = new KeyValuePair[MAXTAGSCOUNT];</span><span class="sxs-lookup"><span data-stu-id="0449f-165">// for each image URL in the file... foreach (var Url in Urls) { // Initiatize a new review tags array ReviewTags = new KeyValuePair[MAXTAGSCOUNT];</span></span>

                // Evaluate for potential adult and racy content with Content Moderator API
                EvaluateAdultRacy(Url, ref ReviewTags);

                // Evaluate for potential presence of celebrity (ies) in images with Computer Vision API
                EvaluateComputerVisionTags(Url, ComputerVisionUri, ComputerVisionKey, ref ReviewTags);

                // Evaluate for potential presence of custom categories other than Marijuana
                EvaluateCustomVisionTags(Url, CustomVisionUri, CustomVisionKey, ref ReviewTags);

                // Create review in the Content Moderator review tool
                CreateReview(Url, ReviewTags);
            }

## <a name="license"></a><span data-ttu-id="0449f-166">License</span><span class="sxs-lookup"><span data-stu-id="0449f-166">License</span></span>

<span data-ttu-id="0449f-167">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span><span class="sxs-lookup"><span data-stu-id="0449f-167">All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License.</span></span> <span data-ttu-id="0449f-168">For more details, see [LICENSE](https://microsoft.mit-license.org/).</span><span class="sxs-lookup"><span data-stu-id="0449f-168">For more details, see [LICENSE](https://microsoft.mit-license.org/).</span></span>

## <a name="developer-code-of-conduct"></a><span data-ttu-id="0449f-169">Developer Code of Conduct</span><span class="sxs-lookup"><span data-stu-id="0449f-169">Developer Code of Conduct</span></span>

<span data-ttu-id="0449f-170">Developers using Cognitive Services, including this client library & sample, are expected to follow the “Developer Code of Conduct for Microsoft Cognitive Services”, found at http://go.microsoft.com/fwlink/?LinkId=698895.</span><span class="sxs-lookup"><span data-stu-id="0449f-170">Developers using Cognitive Services, including this client library & sample, are expected to follow the “Developer Code of Conduct for Microsoft Cognitive Services”, found at http://go.microsoft.com/fwlink/?LinkId=698895.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0449f-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="0449f-171">Next steps</span></span>

<span data-ttu-id="0449f-172">Build and extend the tutorial by using the [project source files](https://github.com/MicrosoftContentModerator/samples-eCommerceCatalogModeration) on Github.</span><span class="sxs-lookup"><span data-stu-id="0449f-172">Build and extend the tutorial by using the [project source files](https://github.com/MicrosoftContentModerator/samples-eCommerceCatalogModeration) on Github.</span></span>
