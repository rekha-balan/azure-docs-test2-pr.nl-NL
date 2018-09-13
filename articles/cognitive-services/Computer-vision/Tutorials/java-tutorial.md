---
title: Computer Vision API Java tutorial | Microsoft Docs
description: Explore a basic Java Swing app that uses the Computer Vision API in Microsoft Cognitive Services. Perform OCR, create thumbnails, and work with visual features in an image.
services: cognitive-services
author: KellyDF
ms.author: kefre
ms.date: 09/21/2017
ms.topic: tutorial
ms.service: cognitive-services
ms.devlang: java
manager: corncar
ms.openlocfilehash: e22bbb999cc7d0a07bb20b446ce288b622c5190b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868523"
---
# <a name="computer-vision-api-java-tutorial"></a><span data-ttu-id="45bb9-104">Computer Vision API Java tutorial</span><span class="sxs-lookup"><span data-stu-id="45bb9-104">Computer Vision API Java tutorial</span></span>

<span data-ttu-id="45bb9-105">This tutorial shows the features of the Microsoft Cognitive Services Computer Vision REST API.</span><span class="sxs-lookup"><span data-stu-id="45bb9-105">This tutorial shows the features of the Microsoft Cognitive Services Computer Vision REST API.</span></span>

<span data-ttu-id="45bb9-106">Explore a Java Swing application that uses the Computer Vision REST API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-106">Explore a Java Swing application that uses the Computer Vision REST API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="45bb9-107">This example lets you submit an image URL for analysis or processing.</span><span class="sxs-lookup"><span data-stu-id="45bb9-107">This example lets you submit an image URL for analysis or processing.</span></span> <span data-ttu-id="45bb9-108">You can use this open source example as a template for building your own app in Java to use the Computer Vision REST API.</span><span class="sxs-lookup"><span data-stu-id="45bb9-108">You can use this open source example as a template for building your own app in Java to use the Computer Vision REST API.</span></span>

<span data-ttu-id="45bb9-109">This tutorial will cover how to use Computer Vision to:</span><span class="sxs-lookup"><span data-stu-id="45bb9-109">This tutorial will cover how to use Computer Vision to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45bb9-110">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-110">Analyze an image</span></span>
> * <span data-ttu-id="45bb9-111">Identify a natural or artificial landmark in an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-111">Identify a natural or artificial landmark in an image</span></span>
> * <span data-ttu-id="45bb9-112">Identify a celebrity in an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-112">Identify a celebrity in an image</span></span>
> * <span data-ttu-id="45bb9-113">Create a quality thumbnail from an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-113">Create a quality thumbnail from an image</span></span>
> * <span data-ttu-id="45bb9-114">Read printed text in an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-114">Read printed text in an image</span></span>
> * <span data-ttu-id="45bb9-115">Read handwritten text in an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-115">Read handwritten text in an image</span></span>

<span data-ttu-id="45bb9-116">The Java Swing form application has already been written, but has no functionality.</span><span class="sxs-lookup"><span data-stu-id="45bb9-116">The Java Swing form application has already been written, but has no functionality.</span></span> <span data-ttu-id="45bb9-117">In this tutorial, you add the code specific to the Computer Vision REST API to complete the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="45bb9-117">In this tutorial, you add the code specific to the Computer Vision REST API to complete the application's functionality.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45bb9-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="45bb9-118">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="45bb9-119">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="45bb9-119">Platform requirements</span></span>

<span data-ttu-id="45bb9-120">This tutorial has been developed using the NetBeans IDE.</span><span class="sxs-lookup"><span data-stu-id="45bb9-120">This tutorial has been developed using the NetBeans IDE.</span></span> <span data-ttu-id="45bb9-121">Specifically, the **Java SE** version of NetBeans, which you can [download here](https://netbeans.org/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="45bb9-121">Specifically, the **Java SE** version of NetBeans, which you can [download here](https://netbeans.org/downloads/index.html).</span></span>

### <a name="subscribe-to-computer-vision-api-and-get-a-subscription-key"></a><span data-ttu-id="45bb9-122">Subscribe to Computer Vision API and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="45bb9-122">Subscribe to Computer Vision API and get a subscription key</span></span> 

<span data-ttu-id="45bb9-123">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="45bb9-123">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services.</span></span> <span data-ttu-id="45bb9-124">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="45bb9-124">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="45bb9-125">Both the primary and secondary keys are valid to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="45bb9-125">Both the primary and secondary keys are valid to use in this tutorial.</span></span> 

## <a name="download-the-tutorial-project"></a><span data-ttu-id="45bb9-126">Download the tutorial project</span><span class="sxs-lookup"><span data-stu-id="45bb9-126">Download the tutorial project</span></span>

1. <span data-ttu-id="45bb9-127">Go to the [Cognitive Services Java Computer Vision Tutorial](https://github.com/Azure-Samples/cognitive-services-java-computer-vision-tutorial) repository.</span><span class="sxs-lookup"><span data-stu-id="45bb9-127">Go to the [Cognitive Services Java Computer Vision Tutorial](https://github.com/Azure-Samples/cognitive-services-java-computer-vision-tutorial) repository.</span></span>
1. <span data-ttu-id="45bb9-128">Click the **Clone or download** button.</span><span class="sxs-lookup"><span data-stu-id="45bb9-128">Click the **Clone or download** button.</span></span>
1. <span data-ttu-id="45bb9-129">Click **Download ZIP** to download a .zip file of the tutorial project.</span><span class="sxs-lookup"><span data-stu-id="45bb9-129">Click **Download ZIP** to download a .zip file of the tutorial project.</span></span>

<span data-ttu-id="45bb9-130">There is no need to extract the contents of the .zip file because NetBeans imports the project from the .zip file.</span><span class="sxs-lookup"><span data-stu-id="45bb9-130">There is no need to extract the contents of the .zip file because NetBeans imports the project from the .zip file.</span></span>

## <a name="import-the-tutorial-project"></a><span data-ttu-id="45bb9-131">Import the tutorial project</span><span class="sxs-lookup"><span data-stu-id="45bb9-131">Import the tutorial project</span></span>

<span data-ttu-id="45bb9-132">Import the **cognitive-services-java-computer-vision-tutorial-master.zip** file into NetBeans.</span><span class="sxs-lookup"><span data-stu-id="45bb9-132">Import the **cognitive-services-java-computer-vision-tutorial-master.zip** file into NetBeans.</span></span>

1. <span data-ttu-id="45bb9-133">In NetBeans, click **File** > **Import Project** > **From ZIP...**. The **Import Project(s) from ZIP** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="45bb9-133">In NetBeans, click **File** > **Import Project** > **From ZIP...**. The **Import Project(s) from ZIP** dialog box appears.</span></span>
1. <span data-ttu-id="45bb9-134">In the **ZIP File:** field, click the **Browse** button to locate the **cognitive-services-java-computer-vision-tutorial-master.zip** file, then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-134">In the **ZIP File:** field, click the **Browse** button to locate the **cognitive-services-java-computer-vision-tutorial-master.zip** file, then click **Open**.</span></span>
1. <span data-ttu-id="45bb9-135">Click **Import** from the **Import Project(s) from ZIP** dialog box.</span><span class="sxs-lookup"><span data-stu-id="45bb9-135">Click **Import** from the **Import Project(s) from ZIP** dialog box.</span></span>
1. <span data-ttu-id="45bb9-136">In the **Projects** panel, expand **ComputerVision** > **Source Packages** > **&lt;default package&gt;**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-136">In the **Projects** panel, expand **ComputerVision** > **Source Packages** > **&lt;default package&gt;**.</span></span> 
   <span data-ttu-id="45bb9-137">Some versions of NetBeans use **src** instead of **Source Packages** > **&lt;default package&gt;**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-137">Some versions of NetBeans use **src** instead of **Source Packages** > **&lt;default package&gt;**.</span></span> <span data-ttu-id="45bb9-138">In that case, expand **src**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-138">In that case, expand **src**.</span></span>
1. <span data-ttu-id="45bb9-139">Double-click **MainFrame.java** to load the file into the NetBeans editor.</span><span class="sxs-lookup"><span data-stu-id="45bb9-139">Double-click **MainFrame.java** to load the file into the NetBeans editor.</span></span> <span data-ttu-id="45bb9-140">The **Design** tab of the **MainFrame.java** file appears.</span><span class="sxs-lookup"><span data-stu-id="45bb9-140">The **Design** tab of the **MainFrame.java** file appears.</span></span>
1. <span data-ttu-id="45bb9-141">Click the **Source** tab to view the Java source code.</span><span class="sxs-lookup"><span data-stu-id="45bb9-141">Click the **Source** tab to view the Java source code.</span></span>

## <a name="build-and-run-the-tutorial-project"></a><span data-ttu-id="45bb9-142">Build and run the tutorial project</span><span class="sxs-lookup"><span data-stu-id="45bb9-142">Build and run the tutorial project</span></span>

1. <span data-ttu-id="45bb9-143">Press **F6** to build and run the tutorial application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-143">Press **F6** to build and run the tutorial application.</span></span>

    <span data-ttu-id="45bb9-144">In the tutorial application, click a tab to bring up the pane for that feature.</span><span class="sxs-lookup"><span data-stu-id="45bb9-144">In the tutorial application, click a tab to bring up the pane for that feature.</span></span> <span data-ttu-id="45bb9-145">The buttons have empty methods, so they do nothing.</span><span class="sxs-lookup"><span data-stu-id="45bb9-145">The buttons have empty methods, so they do nothing.</span></span>

    <span data-ttu-id="45bb9-146">At the bottom of the window are the fields **Subscription Key** and **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-146">At the bottom of the window are the fields **Subscription Key** and **Subscription Region**.</span></span> <span data-ttu-id="45bb9-147">These fields must be filled with a valid subscription key and the correct region for that subscription key.</span><span class="sxs-lookup"><span data-stu-id="45bb9-147">These fields must be filled with a valid subscription key and the correct region for that subscription key.</span></span> <span data-ttu-id="45bb9-148">To obtain a subscription key, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="45bb9-148">To obtain a subscription key, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="45bb9-149">If you obtained your subscription key from the free trial at that link, then the default **westcentralus** is the correct region for your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="45bb9-149">If you obtained your subscription key from the free trial at that link, then the default **westcentralus** is the correct region for your subscription keys.</span></span>

1. <span data-ttu-id="45bb9-150">Exit the tutorial application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-150">Exit the tutorial application.</span></span>

## <a name="add-the-tutorial-code"></a><span data-ttu-id="45bb9-151">Add the tutorial code</span><span class="sxs-lookup"><span data-stu-id="45bb9-151">Add the tutorial code</span></span>

<span data-ttu-id="45bb9-152">The Java Swing application is set up with six tabs.</span><span class="sxs-lookup"><span data-stu-id="45bb9-152">The Java Swing application is set up with six tabs.</span></span> <span data-ttu-id="45bb9-153">Each tab demonstrates a different function of Computer Vision (analyze, OCR, etc).</span><span class="sxs-lookup"><span data-stu-id="45bb9-153">Each tab demonstrates a different function of Computer Vision (analyze, OCR, etc).</span></span> <span data-ttu-id="45bb9-154">The six tutorial sections do not have interdependencies, so you can add one section, all six sections, or only a section or two.</span><span class="sxs-lookup"><span data-stu-id="45bb9-154">The six tutorial sections do not have interdependencies, so you can add one section, all six sections, or only a section or two.</span></span> <span data-ttu-id="45bb9-155">And you can add the sections in any order.</span><span class="sxs-lookup"><span data-stu-id="45bb9-155">And you can add the sections in any order.</span></span>

<span data-ttu-id="45bb9-156">Let's get started.</span><span class="sxs-lookup"><span data-stu-id="45bb9-156">Let's get started.</span></span>

## <a name="analyze-an-image"></a><span data-ttu-id="45bb9-157">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="45bb9-157">Analyze an image</span></span>

<span data-ttu-id="45bb9-158">The Analyze feature of Computer Vision analyzes an image for more than 2,000 recognizable objects, living beings, scenery, and actions.</span><span class="sxs-lookup"><span data-stu-id="45bb9-158">The Analyze feature of Computer Vision analyzes an image for more than 2,000 recognizable objects, living beings, scenery, and actions.</span></span> <span data-ttu-id="45bb9-159">Once the analysis is complete, Analyze returns a JSON object that describes the image with descriptive tags, color analysis, captions, and more.</span><span class="sxs-lookup"><span data-stu-id="45bb9-159">Once the analysis is complete, Analyze returns a JSON object that describes the image with descriptive tags, color analysis, captions, and more.</span></span>

<span data-ttu-id="45bb9-160">To complete the Analyze feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-160">To complete the Analyze feature of the tutorial application, perform the following steps:</span></span>

### <a name="analyze-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-161">Analyze step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-161">Analyze step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-162">The **analyzeImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **AnalyzeImage** method to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-162">The **analyzeImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **AnalyzeImage** method to analyze the image.</span></span> <span data-ttu-id="45bb9-163">When **AnalyzeImage** returns, the method displays the formatted JSON response in the **Response** text area, extracts the first caption from the **JSONObject**, and displays the caption and the confidence level that the caption is correct.</span><span class="sxs-lookup"><span data-stu-id="45bb9-163">When **AnalyzeImage** returns, the method displays the formatted JSON response in the **Response** text area, extracts the first caption from the **JSONObject**, and displays the caption and the confidence level that the caption is correct.</span></span>

<span data-ttu-id="45bb9-164">Copy and paste the following code into the **analyzeImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-164">Copy and paste the following code into the **analyzeImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-165">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-165">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-166">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-166">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void analyzeImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL analyzeImageUrl;
        
        // Clear out the previous image, response, and caption, if any.
        analyzeImage.setIcon(new ImageIcon());
        analyzeCaptionLabel.setText("");
        analyzeResponseTextArea.setText("");
        
        // Display the image specified in the text box.
        try {
            analyzeImageUrl = new URL(analyzeImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(analyzeImageUrl);
            scaleAndShowImage(bImage, analyzeImage);
        } catch(IOException e) {
            analyzeResponseTextArea.setText("Error loading Analyze image: " + e.getMessage());
            return;
        }
        
        // Analyze the image.
        JSONObject jsonObj = AnalyzeImage(analyzeImageUrl.toString());
        
        // A return of null indicates failure.
        if (jsonObj == null) {
            return;
        }
        
        // Format and display the JSON response.
        analyzeResponseTextArea.setText(jsonObj.toString(2));
                
        // Extract the text and confidence from the first caption in the description object.
        if (jsonObj.has("description") && jsonObj.getJSONObject("description").has("captions")) {

            JSONObject jsonCaption = jsonObj.getJSONObject("description").getJSONArray("captions").getJSONObject(0);
            
            if (jsonCaption.has("text") && jsonCaption.has("confidence")) {
                
                analyzeCaptionLabel.setText("Caption: " + jsonCaption.getString("text") + 
                        " (confidence: " + jsonCaption.getDouble("confidence") + ").");
            }
        }
    }
```

### <a name="analyze-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-167">Analyze step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-167">Analyze step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-168">The **AnalyzeImage** method wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-168">The **AnalyzeImage** method wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="45bb9-169">The method returns a **JSONObject** describing the image, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-169">The method returns a **JSONObject** describing the image, or **null** if there was an error.</span></span>

<span data-ttu-id="45bb9-170">Copy and paste the **AnalyzeImage** method to just underneath the **analyzeImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-170">Copy and paste the **AnalyzeImage** method to just underneath the **analyzeImageButtonActionPerformed** method.</span></span>

```java
    /**
     * Encapsulates the Microsoft Cognitive Services REST API call to analyze an image.
     * @param imageUrl: The string URL of the image to analyze.
     * @return: A JSONObject describing the image, or null if a runtime error occurs.
     */
    private JSONObject AnalyzeImage(String imageUrl) {
        try (CloseableHttpClient httpclient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call for Analyze Image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseAnalyze;
            URIBuilder builder = new URIBuilder(uriString);

            // Request parameters. All of them are optional.
            builder.setParameter("visualFeatures", "Categories,Description,Color,Adult");
            builder.setParameter("language", "en");

            // Prepare the URI for the REST API call.
            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity reqEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            // If we got a response, parse it and display it.
            if (entity != null)
            {
                // Return the JSONObject.
                String jsonString = EntityUtils.toString(entity);
                return new JSONObject(jsonString);
            } else {
                // No response. Return null.
                return null;
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
            return null;
        }
    }
 ```

### <a name="analyze-step-3-run-the-application"></a><span data-ttu-id="45bb9-171">Analyze step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-171">Analyze step 3: Run the application</span></span>

<span data-ttu-id="45bb9-172">Press **F6** to run the application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-172">Press **F6** to run the application.</span></span> <span data-ttu-id="45bb9-173">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-173">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-174">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-174">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="recognize-a-landmark"></a><span data-ttu-id="45bb9-175">Recognize a landmark</span><span class="sxs-lookup"><span data-stu-id="45bb9-175">Recognize a landmark</span></span>

<span data-ttu-id="45bb9-176">The Landmark feature of Computer Vision analyzes an image for natural and artificial landmarks, such as mountains or famous buildings.</span><span class="sxs-lookup"><span data-stu-id="45bb9-176">The Landmark feature of Computer Vision analyzes an image for natural and artificial landmarks, such as mountains or famous buildings.</span></span> <span data-ttu-id="45bb9-177">Once the analysis is complete, Landmark returns a JSON object that identifies the landmarks found in the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-177">Once the analysis is complete, Landmark returns a JSON object that identifies the landmarks found in the image.</span></span>

<span data-ttu-id="45bb9-178">To complete the Landmark feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-178">To complete the Landmark feature of the tutorial application, perform the following steps:</span></span>

### <a name="landmark-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-179">Landmark step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-179">Landmark step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-180">The **landmarkImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **LandmarkImage** method to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-180">The **landmarkImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **LandmarkImage** method to analyze the image.</span></span> <span data-ttu-id="45bb9-181">When **LandmarkImage** returns, the method displays the formatted JSON response in the **Response** text area, then extracts the first landmark name from the **JSONObject** and displays it on the window along with the confidence level that the landmark was identified correctly.</span><span class="sxs-lookup"><span data-stu-id="45bb9-181">When **LandmarkImage** returns, the method displays the formatted JSON response in the **Response** text area, then extracts the first landmark name from the **JSONObject** and displays it on the window along with the confidence level that the landmark was identified correctly.</span></span>

<span data-ttu-id="45bb9-182">Copy and paste the following code into the **landmarkImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-182">Copy and paste the following code into the **landmarkImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-183">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-183">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-184">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-184">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void landmarkImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL landmarkImageUrl;
        
        // Clear out the previous image, response, and caption, if any.
        landmarkImage.setIcon(new ImageIcon());
        landmarkCaptionLabel.setText("");
        landmarkResponseTextArea.setText("");
        
        // Display the image specified in the text box.
        try {
            landmarkImageUrl = new URL(landmarkImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(landmarkImageUrl);
            scaleAndShowImage(bImage, landmarkImage);
        } catch(IOException e) {
            landmarkResponseTextArea.setText("Error loading Landmark image: " + e.getMessage());
            return;
        }
        
        // Identify the landmark in the image.
        JSONObject jsonObj = LandmarkImage(landmarkImageUrl.toString());
        
        // A return of null indicates failure.
        if (jsonObj == null) {
            return;
        }
        
        // Format and display the JSON response.
        landmarkResponseTextArea.setText(jsonObj.toString(2));
                
        // Extract the text and confidence from the first caption in the description object.
        if (jsonObj.has("result") && jsonObj.getJSONObject("result").has("landmarks")) {

            JSONObject jsonCaption = jsonObj.getJSONObject("result").getJSONArray("landmarks").getJSONObject(0);
            
            if (jsonCaption.has("name") && jsonCaption.has("confidence")) {

                landmarkCaptionLabel.setText("Caption: " + jsonCaption.getString("name") + 
                        " (confidence: " + jsonCaption.getDouble("confidence") + ").");
            }
        }
    }
```

### <a name="landmark-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-185">Landmark step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-185">Landmark step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-186">The **LandmarkImage** method wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-186">The **LandmarkImage** method wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="45bb9-187">The method returns a **JSONObject** describing the landmarks found in the image, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-187">The method returns a **JSONObject** describing the landmarks found in the image, or **null** if there was an error.</span></span>

<span data-ttu-id="45bb9-188">Copy and paste the **LandmarkImage** method to just underneath the **landmarkImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-188">Copy and paste the **LandmarkImage** method to just underneath the **landmarkImageButtonActionPerformed** method.</span></span>

```java
     /**
     * Encapsulates the Microsoft Cognitive Services REST API call to identify a landmark in an image.
     * @param imageUrl: The string URL of the image to process.
     * @return: A JSONObject describing the image, or null if a runtime error occurs.
     */
    private JSONObject LandmarkImage(String imageUrl) {
        try (CloseableHttpClient httpclient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call to identify a Landmark in an image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseLandmark;
            URIBuilder builder = new URIBuilder(uriString);

            // Request parameters. All of them are optional.
            builder.setParameter("visualFeatures", "Categories,Description,Color");
            builder.setParameter("language", "en");

            // Prepare the URI for the REST API call.
            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity reqEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            // If we got a response, parse it and display it.
            if (entity != null)
            {
                // Return the JSONObject.
                String jsonString = EntityUtils.toString(entity);
                return new JSONObject(jsonString);
            } else {
                // No response. Return null.
                return null;
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
            return null;
        }
    }
```

### <a name="landmark-step-3-run-the-application"></a><span data-ttu-id="45bb9-189">Landmark step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-189">Landmark step 3: Run the application</span></span>

<span data-ttu-id="45bb9-190">Press **F6** to run the application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-190">Press **F6** to run the application.</span></span> <span data-ttu-id="45bb9-191">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-191">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-192">Click the **Landmark** tab, enter a URL to an image of a landmark, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-192">Click the **Landmark** tab, enter a URL to an image of a landmark, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="recognize-celebrities"></a><span data-ttu-id="45bb9-193">Recognize celebrities</span><span class="sxs-lookup"><span data-stu-id="45bb9-193">Recognize celebrities</span></span>

<span data-ttu-id="45bb9-194">The Celebrities feature of Computer Vision analyzes an image for famous people.</span><span class="sxs-lookup"><span data-stu-id="45bb9-194">The Celebrities feature of Computer Vision analyzes an image for famous people.</span></span> <span data-ttu-id="45bb9-195">Once the analysis is complete, Celebrities returns a JSON object that identifies the Celebrities found in the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-195">Once the analysis is complete, Celebrities returns a JSON object that identifies the Celebrities found in the image.</span></span>

<span data-ttu-id="45bb9-196">To complete the Celebrities feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-196">To complete the Celebrities feature of the tutorial application, perform the following steps:</span></span>

### <a name="celebrities-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-197">Celebrities step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-197">Celebrities step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-198">The **celebritiesImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **CelebritiesImage** method to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-198">The **celebritiesImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **CelebritiesImage** method to analyze the image.</span></span> <span data-ttu-id="45bb9-199">When **CelebritiesImage** returns, the method displays the formatted JSON response in the **Response** text area, then extracts the first celebrity name from the **JSONObject** and displays the name on the window along with the confidence level that the celebrity was identified correctly.</span><span class="sxs-lookup"><span data-stu-id="45bb9-199">When **CelebritiesImage** returns, the method displays the formatted JSON response in the **Response** text area, then extracts the first celebrity name from the **JSONObject** and displays the name on the window along with the confidence level that the celebrity was identified correctly.</span></span>

<span data-ttu-id="45bb9-200">Copy and paste the following code into the **celebritiesImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-200">Copy and paste the following code into the **celebritiesImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-201">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-201">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-202">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-202">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void celebritiesImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL celebritiesImageUrl;
        
        // Clear out the previous image, response, and caption, if any.
        celebritiesImage.setIcon(new ImageIcon());
        celebritiesCaptionLabel.setText("");
        celebritiesResponseTextArea.setText("");
        
        // Display the image specified in the text box.
        try {
            celebritiesImageUrl = new URL(celebritiesImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(celebritiesImageUrl);
            scaleAndShowImage(bImage, celebritiesImage);
        } catch(IOException e) {
            celebritiesResponseTextArea.setText("Error loading Celebrity image: " + e.getMessage());
            return;
        }
        
        // Identify the celebrities in the image.
        JSONObject jsonObj = CelebritiesImage(celebritiesImageUrl.toString());
        
        // A return of null indicates failure.
        if (jsonObj == null) {
            return;
        }
        
        // Format and display the JSON response.
        celebritiesResponseTextArea.setText(jsonObj.toString(2));
                
        // Extract the text and confidence from the first caption in the description object.
        if (jsonObj.has("result") && jsonObj.getJSONObject("result").has("celebrities")) {

            JSONObject jsonCaption = jsonObj.getJSONObject("result").getJSONArray("celebrities").getJSONObject(0);
            
            if (jsonCaption.has("name") && jsonCaption.has("confidence")) {

                celebritiesCaptionLabel.setText("Caption: " + jsonCaption.getString("name") + 
                        " (confidence: " + jsonCaption.getDouble("confidence") + ").");
            }
        }
    }
```

### <a name="celebrities-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-203">Celebrities step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-203">Celebrities step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-204">The **CelebritiesImage** method wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-204">The **CelebritiesImage** method wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="45bb9-205">The method returns a **JSONObject** describing the celebrities found in the image, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-205">The method returns a **JSONObject** describing the celebrities found in the image, or **null** if there was an error.</span></span>

<span data-ttu-id="45bb9-206">Copy and paste the **CelebritiesImage** method to just underneath the **celebritiesImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-206">Copy and paste the **CelebritiesImage** method to just underneath the **celebritiesImageButtonActionPerformed** method.</span></span>

```java
     /**
     * Encapsulates the Microsoft Cognitive Services REST API call to identify celebrities in an image.
     * @param imageUrl: The string URL of the image to process.
     * @return: A JSONObject describing the image, or null if a runtime error occurs.
     */
    private JSONObject CelebritiesImage(String imageUrl) {
        try (CloseableHttpClient httpclient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call to identify celebrities in an image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseCelebrities;
            URIBuilder builder = new URIBuilder(uriString);

            // Request parameters. All of them are optional.
            builder.setParameter("visualFeatures", "Categories,Description,Color");
            builder.setParameter("language", "en");

            // Prepare the URI for the REST API call.
            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity reqEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            // If we got a response, parse it and display it.
            if (entity != null)
            {
                // Return the JSONObject.
                String jsonString = EntityUtils.toString(entity);
                return new JSONObject(jsonString);
            } else {
                // No response. Return null.
                return null;
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
            return null;
        }
    }
```

### <a name="celebrities-step-3-run-the-application"></a><span data-ttu-id="45bb9-207">Celebrities step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-207">Celebrities step 3: Run the application</span></span>

<span data-ttu-id="45bb9-208">Press **F6** to run the application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-208">Press **F6** to run the application.</span></span> <span data-ttu-id="45bb9-209">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-209">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-210">Click the **Celebrities** tab, enter a URL to an image of a celebrity, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-210">Click the **Celebrities** tab, enter a URL to an image of a celebrity, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="intelligently-generate-a-thumbnail"></a><span data-ttu-id="45bb9-211">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="45bb9-211">Intelligently generate a thumbnail</span></span>

<span data-ttu-id="45bb9-212">The Thumbnail feature of Computer Vision generates a thumnail from an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-212">The Thumbnail feature of Computer Vision generates a thumnail from an image.</span></span> <span data-ttu-id="45bb9-213">By using the **Smart Crop** feature, the Thumbnail feature will identify the area of interest in an image and center the thumnail on this area, to generate more aesthetically pleasing thumbnail images.</span><span class="sxs-lookup"><span data-stu-id="45bb9-213">By using the **Smart Crop** feature, the Thumbnail feature will identify the area of interest in an image and center the thumnail on this area, to generate more aesthetically pleasing thumbnail images.</span></span>

<span data-ttu-id="45bb9-214">To complete the Thumbnail feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-214">To complete the Thumbnail feature of the tutorial application, perform the following steps:</span></span>

### <a name="thumbnail-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-215">Thumbnail step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-215">Thumbnail step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-216">The **thumbnailImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **getThumbnailImage** method to create the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="45bb9-216">The **thumbnailImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **getThumbnailImage** method to create the thumbnail.</span></span> <span data-ttu-id="45bb9-217">When **getThumbnailImage** returns, the method displays the generated thumbnail.</span><span class="sxs-lookup"><span data-stu-id="45bb9-217">When **getThumbnailImage** returns, the method displays the generated thumbnail.</span></span>

<span data-ttu-id="45bb9-218">Copy and paste the following code into the **thumbnailImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-218">Copy and paste the following code into the **thumbnailImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-219">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-219">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-220">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-220">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void thumbnailImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL thumbnailImageUrl;
        JSONObject jsonError[] = new JSONObject[1];
        
        // Clear out the previous image, response, and thumbnail, if any.
        thumbnailSourceImage.setIcon(new ImageIcon());
        thumbnailResponseTextArea.setText("");
        thumbnailImage.setIcon(new ImageIcon());

        // Display the image specified in the text box.
        try {
            thumbnailImageUrl = new URL(thumbnailImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(thumbnailImageUrl);
            scaleAndShowImage(bImage, thumbnailSourceImage);
        } catch(IOException e) {
            thumbnailResponseTextArea.setText("Error loading image to thumbnail: " + e.getMessage());
            return;
        }
        
        // Get the thumbnail for the image.
        BufferedImage thumbnail = getThumbnailImage(thumbnailImageUrl.toString(), jsonError);
        
        // A non-null value indicates error.
        if (jsonError[0] != null) {
            // Format and display the JSON error.
            thumbnailResponseTextArea.setText(jsonError[0].toString(2));
            return;
        }
        
        // Display the thumbnail.
        if (thumbnail != null) {
            scaleAndShowImage(thumbnail, thumbnailImage);
        }
    }
```

### <a name="thumbnail-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-221">Thumbnail step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-221">Thumbnail step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-222">The **getThumbnailImage** method wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-222">The **getThumbnailImage** method wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="45bb9-223">The method returns a **BufferedImage** that contains the thumbnail, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-223">The method returns a **BufferedImage** that contains the thumbnail, or **null** if there was an error.</span></span> <span data-ttu-id="45bb9-224">The error message will be returned in the first element of the **jsonError** string array.</span><span class="sxs-lookup"><span data-stu-id="45bb9-224">The error message will be returned in the first element of the **jsonError** string array.</span></span>

<span data-ttu-id="45bb9-225">Copy and paste the following **getThumbnailImage** method to just underneath the **thumbnailImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-225">Copy and paste the following **getThumbnailImage** method to just underneath the **thumbnailImageButtonActionPerformed** method.</span></span>

```java
     /**
     * Encapsulates the Microsoft Cognitive Services REST API call to create a thumbnail for an image.
     * @param imageUrl: The string URL of the image to process.
     * @return: A BufferedImage containing the thumbnail, or null if a runtime error occurs. In the case
     * of an error, the error message will be returned in the first element of the jsonError string array.
     */
    private BufferedImage getThumbnailImage(String imageUrl, JSONObject[] jsonError) {
        try (CloseableHttpClient httpclient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call to identify celebrities in an image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseThumbnail;
            URIBuilder uriBuilder = new URIBuilder(uriString);

            // Request parameters.
            uriBuilder.setParameter("width", "100");
            uriBuilder.setParameter("height", "150");
            uriBuilder.setParameter("smartCropping", "true");

            // Prepare the URI for the REST API call.
            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity requestEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(requestEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            // Check for success.
            if (response.getStatusLine().getStatusCode() == 200)
            {
                // Return the thumbnail.
                return ImageIO.read(entity.getContent());
            }
            else
            {
                // Format and display the JSON error message.
                String jsonString = EntityUtils.toString(entity);
                jsonError[0] = new JSONObject(jsonString);
                return null;
            }
        }
        catch (Exception e)
        {
            String errorMessage = e.getMessage();
            System.out.println(errorMessage);
            jsonError[0] = new JSONObject(errorMessage);
            return null;
        }
    }
```

### <a name="thumbnail-step-3-run-the-application"></a><span data-ttu-id="45bb9-226">Thumbnail step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-226">Thumbnail step 3: Run the application</span></span>

<span data-ttu-id="45bb9-227">Press **F6** to run the application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-227">Press **F6** to run the application.</span></span> <span data-ttu-id="45bb9-228">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-228">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-229">Click the **Thumbnail** tab, enter a URL to an image, then click the **Generate Thumbnail** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-229">Click the **Thumbnail** tab, enter a URL to an image, then click the **Generate Thumbnail** button to analyze an image and see the result.</span></span>

## <a name="read-printed-text-ocr"></a><span data-ttu-id="45bb9-230">Read printed text (OCR)</span><span class="sxs-lookup"><span data-stu-id="45bb9-230">Read printed text (OCR)</span></span>

<span data-ttu-id="45bb9-231">The Optical Character Recognition (OCR) feature of Computer Vision analyzes an image of printed text.</span><span class="sxs-lookup"><span data-stu-id="45bb9-231">The Optical Character Recognition (OCR) feature of Computer Vision analyzes an image of printed text.</span></span> <span data-ttu-id="45bb9-232">After the analysis is complete, OCR returns a JSON object that contains the text and the location of the text in the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-232">After the analysis is complete, OCR returns a JSON object that contains the text and the location of the text in the image.</span></span>

<span data-ttu-id="45bb9-233">To complete the OCR feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-233">To complete the OCR feature of the tutorial application, perform the following steps:</span></span>

### <a name="ocr-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-234">OCR step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-234">OCR step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-235">The **ocrImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **OcrImage** method to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-235">The **ocrImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **OcrImage** method to analyze the image.</span></span> <span data-ttu-id="45bb9-236">When **OcrImage** returns, the method displays the detected text as formatted JSON in the **Response** text area.</span><span class="sxs-lookup"><span data-stu-id="45bb9-236">When **OcrImage** returns, the method displays the detected text as formatted JSON in the **Response** text area.</span></span>

<span data-ttu-id="45bb9-237">Copy and paste the following code into the **ocrImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-237">Copy and paste the following code into the **ocrImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-238">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-238">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-239">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-239">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void ocrImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL ocrImageUrl;
        
        // Clear out the previous image, response, and caption, if any.
        ocrImage.setIcon(new ImageIcon());
        ocrResponseTextArea.setText("");
        
        // Display the image specified in the text box.
        try {
            ocrImageUrl = new URL(ocrImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(ocrImageUrl);
            scaleAndShowImage(bImage, ocrImage);
        } catch(IOException e) {
            ocrResponseTextArea.setText("Error loading OCR image: " + e.getMessage());
            return;
        }
        
        // Read the text in the image.
        JSONObject jsonObj = OcrImage(ocrImageUrl.toString());
        
        // A return of null indicates failure.
        if (jsonObj == null) {
            return;
        }
        
        // Format and display the JSON response.
        ocrResponseTextArea.setText(jsonObj.toString(2));
    }
```

### <a name="ocr-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-240">OCR step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-240">OCR step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-241">The **OcrImage** method wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-241">The **OcrImage** method wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="45bb9-242">The method returns a **JSONObject** of the JSON data returned from the call, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-242">The method returns a **JSONObject** of the JSON data returned from the call, or **null** if there was an error.</span></span>

<span data-ttu-id="45bb9-243">Copy and paste the following **OcrImage** method to just underneath the **ocrImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-243">Copy and paste the following **OcrImage** method to just underneath the **ocrImageButtonActionPerformed** method.</span></span>

```java
     /**
     * Encapsulates the Microsoft Cognitive Services REST API call to read text in an image.
     * @param imageUrl: The string URL of the image to process.
     * @return: A JSONObject describing the image, or null if a runtime error occurs.
     */
    private JSONObject OcrImage(String imageUrl) {
        try (CloseableHttpClient httpclient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call to read text in an image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseOcr;
            URIBuilder uriBuilder = new URIBuilder(uriString);

            // Request parameters.
            uriBuilder.setParameter("language", "unk");
            uriBuilder.setParameter("detectOrientation ", "true");

            // Prepare the URI for the REST API call.
            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity reqEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            // If we got a response, parse it and display it.
            if (entity != null)
            {
                // Return the JSONObject.
                String jsonString = EntityUtils.toString(entity);
                return new JSONObject(jsonString);
            } else {
                // No response. Return null.
                return null;
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
            return null;
        }
    }
```

### <a name="ocr-step-3-run-the-application"></a><span data-ttu-id="45bb9-244">OCR step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-244">OCR step 3: Run the application</span></span>

<span data-ttu-id="45bb9-245">Press **F6** to run the application.</span><span class="sxs-lookup"><span data-stu-id="45bb9-245">Press **F6** to run the application.</span></span> <span data-ttu-id="45bb9-246">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-246">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-247">Click the **OCR** tab, enter a URL to an image of printed text, then click the **Read Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-247">Click the **OCR** tab, enter a URL to an image of printed text, then click the **Read Image** button to analyze an image and see the result.</span></span>

## <a name="read-handwritten-text-handwriting-recognition"></a><span data-ttu-id="45bb9-248">Read handwritten text (handwriting recognition)</span><span class="sxs-lookup"><span data-stu-id="45bb9-248">Read handwritten text (handwriting recognition)</span></span>

<span data-ttu-id="45bb9-249">The Handwriting Recognition feature of Computer Vision analyzes an image of handwritten text.</span><span class="sxs-lookup"><span data-stu-id="45bb9-249">The Handwriting Recognition feature of Computer Vision analyzes an image of handwritten text.</span></span> <span data-ttu-id="45bb9-250">After the analysis is complete, Handwriting Recognition returns a JSON object that contains the text and the location of the text in the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-250">After the analysis is complete, Handwriting Recognition returns a JSON object that contains the text and the location of the text in the image.</span></span>

<span data-ttu-id="45bb9-251">To complete the Handwriting Recognition feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="45bb9-251">To complete the Handwriting Recognition feature of the tutorial application, perform the following steps:</span></span>

### <a name="handwriting-recognition-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="45bb9-252">Handwriting Recognition step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="45bb9-252">Handwriting Recognition step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="45bb9-253">The **handwritingImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **HandwritingImage** method to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-253">The **handwritingImageButtonActionPerformed** event handler method clears the form, displays the image specified in the URL, then calls the **HandwritingImage** method to analyze the image.</span></span> <span data-ttu-id="45bb9-254">When **HandwritingImage** returns, the method displays the detected text as formatted JSON in the **Response** text area.</span><span class="sxs-lookup"><span data-stu-id="45bb9-254">When **HandwritingImage** returns, the method displays the detected text as formatted JSON in the **Response** text area.</span></span>

<span data-ttu-id="45bb9-255">Copy and paste the following code into the **handwritingImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-255">Copy and paste the following code into the **handwritingImageButtonActionPerformed** method.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb9-256">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-256">NetBeans won't let you paste to the method definition line (```private void```) or to the closing curly brace of that method.</span></span> <span data-ttu-id="45bb9-257">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-257">To copy the code, copy the lines between the method definition and the closing curly brace, and paste them over the contents of the method.</span></span>

```java
    private void handwritingImageButtonActionPerformed(java.awt.event.ActionEvent evt) {
        URL handwritingImageUrl;
        
        // Clear out the previous image, response, and caption, if any.
        handwritingImage.setIcon(new ImageIcon());
        handwritingResponseTextArea.setText("");
        
        // Display the image specified in the text box.
        try {
            handwritingImageUrl = new URL(handwritingImageUriTextBox.getText());
            BufferedImage bImage = ImageIO.read(handwritingImageUrl);
            scaleAndShowImage(bImage, handwritingImage);
        } catch(IOException e) {
            handwritingResponseTextArea.setText("Error loading Handwriting image: " + e.getMessage());
            return;
        }
        
        // Read the text in the image.
        JSONObject jsonObj = HandwritingImage(handwritingImageUrl.toString());
        
        // A return of null indicates failure.
        if (jsonObj == null) {
            return;
        }
        
        // Format and display the JSON response.
        handwritingResponseTextArea.setText(jsonObj.toString(2));
    }
```

### <a name="handwriting-recognition-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="45bb9-258">Handwriting Recognition step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="45bb9-258">Handwriting Recognition step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="45bb9-259">The **HandwritingImage** method wraps the two REST API calls needed to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="45bb9-259">The **HandwritingImage** method wraps the two REST API calls needed to analyze an image.</span></span> <span data-ttu-id="45bb9-260">Because handwriting recognition is a time consuming process, a two step process is used.</span><span class="sxs-lookup"><span data-stu-id="45bb9-260">Because handwriting recognition is a time consuming process, a two step process is used.</span></span> <span data-ttu-id="45bb9-261">The first call submits the image for processing; the second call retrieves the detected text when the processing is complete.</span><span class="sxs-lookup"><span data-stu-id="45bb9-261">The first call submits the image for processing; the second call retrieves the detected text when the processing is complete.</span></span>

<span data-ttu-id="45bb9-262">After the text is retrieved, the **HandwritingImage** method returns a **JSONObject** describing the text and the locations of the text, or **null** if there was an error.</span><span class="sxs-lookup"><span data-stu-id="45bb9-262">After the text is retrieved, the **HandwritingImage** method returns a **JSONObject** describing the text and the locations of the text, or **null** if there was an error.</span></span>

<span data-ttu-id="45bb9-263">Copy and paste the following **HandwritingImage** method to just underneath the **handwritingImageButtonActionPerformed** method.</span><span class="sxs-lookup"><span data-stu-id="45bb9-263">Copy and paste the following **HandwritingImage** method to just underneath the **handwritingImageButtonActionPerformed** method.</span></span>

```java
     /**
     * Encapsulates the Microsoft Cognitive Services REST API call to read handwritten text in an image.
     * @param imageUrl: The string URL of the image to process.
     * @return: A JSONObject describing the image, or null if a runtime error occurs.
     */
    private JSONObject HandwritingImage(String imageUrl) {
        try (CloseableHttpClient textClient = HttpClientBuilder.create().build();
             CloseableHttpClient resultClient = HttpClientBuilder.create().build())
        {
            // Create the URI to access the REST API call to read text in an image.
            String uriString = uriBasePreRegion + 
                    String.valueOf(subscriptionRegionComboBox.getSelectedItem()) + 
                    uriBasePostRegion + uriBaseHandwriting;
            URIBuilder uriBuilder = new URIBuilder(uriString);
            
            // Request parameters.
            uriBuilder.setParameter("handwriting", "true");

            // Prepare the URI for the REST API call.
            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());

            // Request body.
            StringEntity reqEntity = new StringEntity("{\"url\":\"" + imageUrl + "\"}");
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response.
            HttpResponse textResponse = textClient.execute(request);
            
            // Check for success.
            if (textResponse.getStatusLine().getStatusCode() != 202) {
                // An error occured. Return the JSON error message.
                HttpEntity entity = textResponse.getEntity();
                String jsonString = EntityUtils.toString(entity);
                return new JSONObject(jsonString);
            }
            
            String operationLocation = null;

            // The 'Operation-Location' in the response contains the URI to retrieve the recognized text.
            Header[] responseHeaders = textResponse.getAllHeaders();
            for(Header header : responseHeaders) {
                if(header.getName().equals("Operation-Location"))
                {
                    // This string is the URI where you can get the text recognition operation result.
                    operationLocation = header.getValue();
                    break;
                }
            }
            
            // NOTE: The response may not be immediately available. Handwriting recognition is an
            // async operation that can take a variable amount of time depending on the length
            // of the text you want to recognize. You may need to wait or retry this operation.
            //
            // This example checks once per second for ten seconds.
            
            JSONObject responseObj = null;
            int i = 0;
            do {
                // Wait one second.
                Thread.sleep(1000);
                
                // Check to see if the operation completed.
                HttpGet resultRequest = new HttpGet(operationLocation);
                resultRequest.setHeader("Ocp-Apim-Subscription-Key", subscriptionKeyTextField.getText());
                HttpResponse resultResponse = resultClient.execute(resultRequest);
                HttpEntity responseEntity = resultResponse.getEntity();
                if (responseEntity != null)
                {
                    // Get the JSON response.
                    String jsonString = EntityUtils.toString(responseEntity);
                    responseObj = new JSONObject(jsonString);
                }
            }
            while (i < 10 && responseObj != null &&
                    !responseObj.getString("status").equalsIgnoreCase("Succeeded"));
            
            // If the operation completed, return the JSON object.
            if (responseObj != null) {
                return responseObj;
            } else {
                // Return null for timeout error.
                System.out.println("Timeout error.");
                return null;
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
            return null;
        }
    }
```

### <a name="handwriting-recognition-step-3-run-the-application"></a><span data-ttu-id="45bb9-264">Handwriting Recognition step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="45bb9-264">Handwriting Recognition step 3: Run the application</span></span>

<span data-ttu-id="45bb9-265">To run the application, press **F6**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-265">To run the application, press **F6**.</span></span> <span data-ttu-id="45bb9-266">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="45bb9-266">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="45bb9-267">Click the **Read Handwritten Text** tab, enter a URL to an image of handwritten text, then click the **Read Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="45bb9-267">Click the **Read Handwritten Text** tab, enter a URL to an image of handwritten text, then click the **Read Image** button to analyze an image and see the result.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45bb9-268">Next steps</span><span class="sxs-lookup"><span data-stu-id="45bb9-268">Next steps</span></span>

- [<span data-ttu-id="45bb9-269">Computer Vision API C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="45bb9-269">Computer Vision API C&#35; Tutorial</span></span>](CSharpTutorial.md)
- [<span data-ttu-id="45bb9-270">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="45bb9-270">Computer Vision API Python Tutorial</span></span>](PythonTutorial.md)
