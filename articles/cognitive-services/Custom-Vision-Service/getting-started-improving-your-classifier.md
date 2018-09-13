---
title: Improve your classifier using Custom Vision Service - Azure Cognitive Services | Microsoft Docs
description: Learn how to improve the quality of your Custom Vision Service classifier.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 07/05/2018
ms.author: nolachar
ms.openlocfilehash: 7c6cbd996d0c35b96fde78daf391bebb36feddce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869411"
---
# <a name="how-to-improve-your-classifier"></a><span data-ttu-id="0c844-103">How to improve your classifier</span><span class="sxs-lookup"><span data-stu-id="0c844-103">How to improve your classifier</span></span>

<span data-ttu-id="0c844-104">Learn how to improve the quality of your Custom Vision Service classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-104">Learn how to improve the quality of your Custom Vision Service classifier.</span></span> <span data-ttu-id="0c844-105">The quality of your classifier is dependent on the amount, quality, and variety of the labeled data you provide to it and how balanced the dataset is.</span><span class="sxs-lookup"><span data-stu-id="0c844-105">The quality of your classifier is dependent on the amount, quality, and variety of the labeled data you provide to it and how balanced the dataset is.</span></span> <span data-ttu-id="0c844-106">A good classifier normally has a balanced training dataset that is representative of what will be submitted to the classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-106">A good classifier normally has a balanced training dataset that is representative of what will be submitted to the classifier.</span></span> <span data-ttu-id="0c844-107">The process of building such a classifier is often iterative.</span><span class="sxs-lookup"><span data-stu-id="0c844-107">The process of building such a classifier is often iterative.</span></span> <span data-ttu-id="0c844-108">It's common to take a few rounds of training to reach expected results.</span><span class="sxs-lookup"><span data-stu-id="0c844-108">It's common to take a few rounds of training to reach expected results.</span></span>

<span data-ttu-id="0c844-109">Here are the common steps taken to improve a classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-109">Here are the common steps taken to improve a classifier.</span></span> <span data-ttu-id="0c844-110">These steps aren't hard and fast rules, but heuristics that will help you build a better classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-110">These steps aren't hard and fast rules, but heuristics that will help you build a better classifier.</span></span>

1. <span data-ttu-id="0c844-111">First-round training</span><span class="sxs-lookup"><span data-stu-id="0c844-111">First-round training</span></span>
1. <span data-ttu-id="0c844-112">Add more images and balance data</span><span class="sxs-lookup"><span data-stu-id="0c844-112">Add more images and balance data</span></span>
1. <span data-ttu-id="0c844-113">Retrain</span><span class="sxs-lookup"><span data-stu-id="0c844-113">Retrain</span></span>
1. <span data-ttu-id="0c844-114">Add images with varying background, lighting, object size, camera angle, and style</span><span class="sxs-lookup"><span data-stu-id="0c844-114">Add images with varying background, lighting, object size, camera angle, and style</span></span>
1. <span data-ttu-id="0c844-115">Retrain & feed in image for prediction</span><span class="sxs-lookup"><span data-stu-id="0c844-115">Retrain & feed in image for prediction</span></span>
1. <span data-ttu-id="0c844-116">Examine prediction results</span><span class="sxs-lookup"><span data-stu-id="0c844-116">Examine prediction results</span></span>
1. <span data-ttu-id="0c844-117">Modify existing training data</span><span class="sxs-lookup"><span data-stu-id="0c844-117">Modify existing training data</span></span>

## <a name="data-quantity-and-data-balance"></a><span data-ttu-id="0c844-118">Data quantity and data balance</span><span class="sxs-lookup"><span data-stu-id="0c844-118">Data quantity and data balance</span></span>

<span data-ttu-id="0c844-119">The most important thing is to upload enough images to train the classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-119">The most important thing is to upload enough images to train the classifier.</span></span> <span data-ttu-id="0c844-120">At least 50 images per label for the training set are recommended as a starting point.</span><span class="sxs-lookup"><span data-stu-id="0c844-120">At least 50 images per label for the training set are recommended as a starting point.</span></span> <span data-ttu-id="0c844-121">With fewer images, there's a strong risk that you're overfitting.</span><span class="sxs-lookup"><span data-stu-id="0c844-121">With fewer images, there's a strong risk that you're overfitting.</span></span> <span data-ttu-id="0c844-122">While your performance numbers may suggest good quality, you may struggle against real world data.</span><span class="sxs-lookup"><span data-stu-id="0c844-122">While your performance numbers may suggest good quality, you may struggle against real world data.</span></span> <span data-ttu-id="0c844-123">Training the classifier with more images will generally increase the accuracy of prediction results.</span><span class="sxs-lookup"><span data-stu-id="0c844-123">Training the classifier with more images will generally increase the accuracy of prediction results.</span></span>

<span data-ttu-id="0c844-124">Another consideration is that you should make sure that your data is balanced.</span><span class="sxs-lookup"><span data-stu-id="0c844-124">Another consideration is that you should make sure that your data is balanced.</span></span> <span data-ttu-id="0c844-125">For instance, having 500 images for one label and 50 images for another label will produce an imbalanced training dataset, causing the model to be more accurate in predicting one label than another.</span><span class="sxs-lookup"><span data-stu-id="0c844-125">For instance, having 500 images for one label and 50 images for another label will produce an imbalanced training dataset, causing the model to be more accurate in predicting one label than another.</span></span> <span data-ttu-id="0c844-126">You're likely to see better results if you maintain at least a 1:2 ratio between the label with the fewest images and the label with the most images.</span><span class="sxs-lookup"><span data-stu-id="0c844-126">You're likely to see better results if you maintain at least a 1:2 ratio between the label with the fewest images and the label with the most images.</span></span> <span data-ttu-id="0c844-127">For example, if the label with the greatest number of images has 500 images, the label with the least images needs to have at least 250 images for training.</span><span class="sxs-lookup"><span data-stu-id="0c844-127">For example, if the label with the greatest number of images has 500 images, the label with the least images needs to have at least 250 images for training.</span></span>

## <a name="train-more-diverse-images"></a><span data-ttu-id="0c844-128">Train more diverse images</span><span class="sxs-lookup"><span data-stu-id="0c844-128">Train more diverse images</span></span>

<span data-ttu-id="0c844-129">Provide images that are representative of what will be submitted to the classifier during normal use.</span><span class="sxs-lookup"><span data-stu-id="0c844-129">Provide images that are representative of what will be submitted to the classifier during normal use.</span></span> <span data-ttu-id="0c844-130">For example, if you're training an “apple” classifier, your classifier might not be as accurate if you only train photos of apples in plates but make predictions on photos of apples on trees.</span><span class="sxs-lookup"><span data-stu-id="0c844-130">For example, if you're training an “apple” classifier, your classifier might not be as accurate if you only train photos of apples in plates but make predictions on photos of apples on trees.</span></span> <span data-ttu-id="0c844-131">Including a variety of images will make sure that your classifier isn't biased and can generalize well.</span><span class="sxs-lookup"><span data-stu-id="0c844-131">Including a variety of images will make sure that your classifier isn't biased and can generalize well.</span></span> <span data-ttu-id="0c844-132">Below are some ways you can make your training set more diverse:</span><span class="sxs-lookup"><span data-stu-id="0c844-132">Below are some ways you can make your training set more diverse:</span></span>

<span data-ttu-id="0c844-133">__Background:__ Provide images of your object in front of different backgrounds (that is, fruit on plate versus fruit in grocery bag).</span><span class="sxs-lookup"><span data-stu-id="0c844-133">__Background:__ Provide images of your object in front of different backgrounds (that is, fruit on plate versus fruit in grocery bag).</span></span> <span data-ttu-id="0c844-134">Photos in context are better than photos in front of neutral backgrounds as they provide more information for the classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-134">Photos in context are better than photos in front of neutral backgrounds as they provide more information for the classifier.</span></span>

![Image of background samples](./media/getting-started-improving-your-classifier/background.png)

<span data-ttu-id="0c844-136">__Lighting:__ Provide images with varied lighting (that is, taken with flash, high exposure, etc.), especially if the images used for prediction have different lighting.</span><span class="sxs-lookup"><span data-stu-id="0c844-136">__Lighting:__ Provide images with varied lighting (that is, taken with flash, high exposure, etc.), especially if the images used for prediction have different lighting.</span></span> <span data-ttu-id="0c844-137">It is also helpful to include images with varied saturation, hue, and brightness.</span><span class="sxs-lookup"><span data-stu-id="0c844-137">It is also helpful to include images with varied saturation, hue, and brightness.</span></span>

![Image of lighting samples](./media/getting-started-improving-your-classifier/lighting.png)

<span data-ttu-id="0c844-139">__Object Size:__ Provide images in which the objects are of varied sizing capturing different parts of the object.</span><span class="sxs-lookup"><span data-stu-id="0c844-139">__Object Size:__ Provide images in which the objects are of varied sizing capturing different parts of the object.</span></span> <span data-ttu-id="0c844-140">For example, a photo of bunches of bananas and a closeup of a single banana.</span><span class="sxs-lookup"><span data-stu-id="0c844-140">For example, a photo of bunches of bananas and a closeup of a single banana.</span></span> <span data-ttu-id="0c844-141">Different sizing helps the classifier generalize better.</span><span class="sxs-lookup"><span data-stu-id="0c844-141">Different sizing helps the classifier generalize better.</span></span>

![Image of size samples](./media/getting-started-improving-your-classifier/size.png)

<span data-ttu-id="0c844-143">__Camera Angle:__ Provide images taken with different camera angles.</span><span class="sxs-lookup"><span data-stu-id="0c844-143">__Camera Angle:__ Provide images taken with different camera angles.</span></span> <span data-ttu-id="0c844-144">If all your photos are taken with a set of fixed cameras (such as surveillance cameras), make sure you assign a different label to every camera even if they capture the same objects to avoid overfitting - modeling unrelated objects (such as lampposts) as the key feature.</span><span class="sxs-lookup"><span data-stu-id="0c844-144">If all your photos are taken with a set of fixed cameras (such as surveillance cameras), make sure you assign a different label to every camera even if they capture the same objects to avoid overfitting - modeling unrelated objects (such as lampposts) as the key feature.</span></span>

![Image of angle samples](./media/getting-started-improving-your-classifier/angle.png)

<span data-ttu-id="0c844-146">__Style:__ Provide images of different styles of the same class (that is, different kinds of citrus).</span><span class="sxs-lookup"><span data-stu-id="0c844-146">__Style:__ Provide images of different styles of the same class (that is, different kinds of citrus).</span></span> <span data-ttu-id="0c844-147">However, if you have images of objects of drastically different styles (that is, Mickey Mouse versus a real-life rat), it is recommended to label them as separate classes to better represent their distinct features.</span><span class="sxs-lookup"><span data-stu-id="0c844-147">However, if you have images of objects of drastically different styles (that is, Mickey Mouse versus a real-life rat), it is recommended to label them as separate classes to better represent their distinct features.</span></span>

![Image of style samples](./media/getting-started-improving-your-classifier/style.png)

## <a name="use-images-submitted-for-prediction"></a><span data-ttu-id="0c844-149">Use images submitted for prediction</span><span class="sxs-lookup"><span data-stu-id="0c844-149">Use images submitted for prediction</span></span>

<span data-ttu-id="0c844-150">The Custom Vision Service stores images submitted to the prediction endpoint.</span><span class="sxs-lookup"><span data-stu-id="0c844-150">The Custom Vision Service stores images submitted to the prediction endpoint.</span></span> <span data-ttu-id="0c844-151">To use these images to improve the classifier, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c844-151">To use these images to improve the classifier, use the following steps:</span></span>

1. <span data-ttu-id="0c844-152">To view images submitted to the classifier, open the [Custom Vision web page](https://customvision.ai), go to your project, and select the __Predictions__ tab. The default view shows images from the current iteration.</span><span class="sxs-lookup"><span data-stu-id="0c844-152">To view images submitted to the classifier, open the [Custom Vision web page](https://customvision.ai), go to your project, and select the __Predictions__ tab. The default view shows images from the current iteration.</span></span> <span data-ttu-id="0c844-153">You can use the __Iteration__ drop down field to view images submitted during previous iterations.</span><span class="sxs-lookup"><span data-stu-id="0c844-153">You can use the __Iteration__ drop down field to view images submitted during previous iterations.</span></span>

    ![Image of the predictions tab](./media/getting-started-improving-your-classifier/predictions.png)

2. <span data-ttu-id="0c844-155">Hover over an image to see the tags that were predicted by the classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-155">Hover over an image to see the tags that were predicted by the classifier.</span></span> <span data-ttu-id="0c844-156">Images are ranked so that the images that can bring the most gains to the classifier are at the top.</span><span class="sxs-lookup"><span data-stu-id="0c844-156">Images are ranked so that the images that can bring the most gains to the classifier are at the top.</span></span> <span data-ttu-id="0c844-157">To select a different sorting, use the __Sort__ section.</span><span class="sxs-lookup"><span data-stu-id="0c844-157">To select a different sorting, use the __Sort__ section.</span></span> <span data-ttu-id="0c844-158">To add an image to your existing training data, select the image, select the correct tag, and click on __Save and close__.</span><span class="sxs-lookup"><span data-stu-id="0c844-158">To add an image to your existing training data, select the image, select the correct tag, and click on __Save and close__.</span></span> <span data-ttu-id="0c844-159">The image will be removed from __Predictions__ and added to the training images.</span><span class="sxs-lookup"><span data-stu-id="0c844-159">The image will be removed from __Predictions__ and added to the training images.</span></span> <span data-ttu-id="0c844-160">You can view it by selecting the __Training Images__ tab.</span><span class="sxs-lookup"><span data-stu-id="0c844-160">You can view it by selecting the __Training Images__ tab.</span></span>

    ![Image of the tagging page](./media/getting-started-improving-your-classifier/tag.png)

3. <span data-ttu-id="0c844-162">Use the __Train__ button to retrain the classifier.</span><span class="sxs-lookup"><span data-stu-id="0c844-162">Use the __Train__ button to retrain the classifier.</span></span>

## <a name="visually-inspect-predictions"></a><span data-ttu-id="0c844-163">Visually inspect predictions</span><span class="sxs-lookup"><span data-stu-id="0c844-163">Visually inspect predictions</span></span>

<span data-ttu-id="0c844-164">To inspect image predictions, select the __Training Images__ tab and then select __Iteration History__.</span><span class="sxs-lookup"><span data-stu-id="0c844-164">To inspect image predictions, select the __Training Images__ tab and then select __Iteration History__.</span></span> <span data-ttu-id="0c844-165">Images that are outlined with a red box were predicted incorrectly.</span><span class="sxs-lookup"><span data-stu-id="0c844-165">Images that are outlined with a red box were predicted incorrectly.</span></span>

![Image of the iteration history](./media/getting-started-improving-your-classifier/iteration.png)

<span data-ttu-id="0c844-167">Sometimes visual inspection can identify patterns that you can then correct by adding additional training data or modifying existing training data.</span><span class="sxs-lookup"><span data-stu-id="0c844-167">Sometimes visual inspection can identify patterns that you can then correct by adding additional training data or modifying existing training data.</span></span> <span data-ttu-id="0c844-168">For example, a classifier for apple vs. lime may incorrectly label all green apples as limes.</span><span class="sxs-lookup"><span data-stu-id="0c844-168">For example, a classifier for apple vs. lime may incorrectly label all green apples as limes.</span></span> <span data-ttu-id="0c844-169">You may be able to correct this problem by adding and providing training data that contains tagged images of green apples.</span><span class="sxs-lookup"><span data-stu-id="0c844-169">You may be able to correct this problem by adding and providing training data that contains tagged images of green apples.</span></span>

## <a name="unexpected-classification"></a><span data-ttu-id="0c844-170">Unexpected classification</span><span class="sxs-lookup"><span data-stu-id="0c844-170">Unexpected classification</span></span>

<span data-ttu-id="0c844-171">Sometimes the classifier incorrectly learns characteristics that your images have in common.</span><span class="sxs-lookup"><span data-stu-id="0c844-171">Sometimes the classifier incorrectly learns characteristics that your images have in common.</span></span> <span data-ttu-id="0c844-172">For example, if you are creating a classifier for apples vs. citrus, and are supplied images of apples in hands and of citrus in white plates, the classifier may train for hands vs. white plates instead of apples vs. citrus.</span><span class="sxs-lookup"><span data-stu-id="0c844-172">For example, if you are creating a classifier for apples vs. citrus, and are supplied images of apples in hands and of citrus in white plates, the classifier may train for hands vs. white plates instead of apples vs. citrus.</span></span>

![Image of unexpected classification](./media/getting-started-improving-your-classifier/unexpected.png)

<span data-ttu-id="0c844-174">To correct this problem, use the above guidance on training with more varied images: provide images with different angles, backgrounds, object size, groups, and other variants.</span><span class="sxs-lookup"><span data-stu-id="0c844-174">To correct this problem, use the above guidance on training with more varied images: provide images with different angles, backgrounds, object size, groups, and other variants.</span></span>

## <a name="negative-image-handling"></a><span data-ttu-id="0c844-175">Negative image handling</span><span class="sxs-lookup"><span data-stu-id="0c844-175">Negative image handling</span></span>

<span data-ttu-id="0c844-176">The Custom Vision Service supports some automatic negative image handling.</span><span class="sxs-lookup"><span data-stu-id="0c844-176">The Custom Vision Service supports some automatic negative image handling.</span></span> <span data-ttu-id="0c844-177">In the case where you are building a grape vs. banana classifier, and submit an image of a shoe for prediction, the classifier should score that image as close to 0% for both grape and banana.</span><span class="sxs-lookup"><span data-stu-id="0c844-177">In the case where you are building a grape vs. banana classifier, and submit an image of a shoe for prediction, the classifier should score that image as close to 0% for both grape and banana.</span></span>

<span data-ttu-id="0c844-178">On the other hand, in cases where the negative images are just a variation of the images used in training, it is likely that the model will classify the negative images as a labeled class due to the great similarities.</span><span class="sxs-lookup"><span data-stu-id="0c844-178">On the other hand, in cases where the negative images are just a variation of the images used in training, it is likely that the model will classify the negative images as a labeled class due to the great similarities.</span></span> <span data-ttu-id="0c844-179">For example, if you have an orange vs. grapefruit classifier, and you feed in an image of a clementine, it may score the clementine as orange.</span><span class="sxs-lookup"><span data-stu-id="0c844-179">For example, if you have an orange vs. grapefruit classifier, and you feed in an image of a clementine, it may score the clementine as orange.</span></span> <span data-ttu-id="0c844-180">This may occur since many features of the clementine (color, shape, texture, natural habitat, etc.) resemble that of oranges.</span><span class="sxs-lookup"><span data-stu-id="0c844-180">This may occur since many features of the clementine (color, shape, texture, natural habitat, etc.) resemble that of oranges.</span></span>  <span data-ttu-id="0c844-181">If your negative images are of this nature, it is recommended to create one or more separate tags ("Other") and label negative images with this tag during training to allow the model to better differentiate between these classes.</span><span class="sxs-lookup"><span data-stu-id="0c844-181">If your negative images are of this nature, it is recommended to create one or more separate tags ("Other") and label negative images with this tag during training to allow the model to better differentiate between these classes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c844-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c844-182">Next steps</span></span>

<span data-ttu-id="0c844-183">Learn how you can test images programmatically by submitting them to the Prediction API.</span><span class="sxs-lookup"><span data-stu-id="0c844-183">Learn how you can test images programmatically by submitting them to the Prediction API.</span></span>

> [!div class="nextstepaction"]
[<span data-ttu-id="0c844-184">Use the prediction API</span><span class="sxs-lookup"><span data-stu-id="0c844-184">Use the prediction API</span></span>](use-prediction-api.md)