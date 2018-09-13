---
title: Test and retrain a model - Custom Vision Service - Azure Cognitive Services | Microsoft Docs
description: Learn how to test an image and then use it to retrain the model.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 05/03/2018
ms.author: anroth
ms.openlocfilehash: 1933b1a45844ac99308baebe59b49687a957abfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968504"
---
# <a name="test-and-retrain-a-model-with-custom-vision-service"></a><span data-ttu-id="0d856-103">Test and retrain a model with Custom Vision Service</span><span class="sxs-lookup"><span data-stu-id="0d856-103">Test and retrain a model with Custom Vision Service</span></span>

<span data-ttu-id="0d856-104">After you train your model, you can quickly test it using a locally stored image or an online image.</span><span class="sxs-lookup"><span data-stu-id="0d856-104">After you train your model, you can quickly test it using a locally stored image or an online image.</span></span> <span data-ttu-id="0d856-105">The test uses the most recently trained iteration.</span><span class="sxs-lookup"><span data-stu-id="0d856-105">The test uses the most recently trained iteration.</span></span>

## <a name="test-your-model"></a><span data-ttu-id="0d856-106">Test your model</span><span class="sxs-lookup"><span data-stu-id="0d856-106">Test your model</span></span>

1. <span data-ttu-id="0d856-107">From the [Custom Vision web page](https://customvision.ai), select your project.</span><span class="sxs-lookup"><span data-stu-id="0d856-107">From the [Custom Vision web page](https://customvision.ai), select your project.</span></span> <span data-ttu-id="0d856-108">Select **Quick Test** on the right of the top menu bar.</span><span class="sxs-lookup"><span data-stu-id="0d856-108">Select **Quick Test** on the right of the top menu bar.</span></span> <span data-ttu-id="0d856-109">This action opens a window labeled **Quick Test**.</span><span class="sxs-lookup"><span data-stu-id="0d856-109">This action opens a window labeled **Quick Test**.</span></span>

    ![The Quick Test button is shown in the upper right corner of the window.](./media/test-your-model/quick-test-button.png)

2. <span data-ttu-id="0d856-111">In the **Quick Test** window, click in the **Submit Image** field and enter the URL of the image you want to use for your test.</span><span class="sxs-lookup"><span data-stu-id="0d856-111">In the **Quick Test** window, click in the **Submit Image** field and enter the URL of the image you want to use for your test.</span></span> <span data-ttu-id="0d856-112">If you want to use a locally stored image instead, click the **Browse local files** button and select a local image file.</span><span class="sxs-lookup"><span data-stu-id="0d856-112">If you want to use a locally stored image instead, click the **Browse local files** button and select a local image file.</span></span>

    ![Image of the submit image page](./media/test-your-model/submit-image.png)

<span data-ttu-id="0d856-114">The image you select appears in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="0d856-114">The image you select appears in the middle of the page.</span></span> <span data-ttu-id="0d856-115">Then the results appear below the image in the form of a table with two columns, labeled **Tags** and **Confidence**.</span><span class="sxs-lookup"><span data-stu-id="0d856-115">Then the results appear below the image in the form of a table with two columns, labeled **Tags** and **Confidence**.</span></span> <span data-ttu-id="0d856-116">After you view the results, you may close the **Quick Test** window.</span><span class="sxs-lookup"><span data-stu-id="0d856-116">After you view the results, you may close the **Quick Test** window.</span></span>

<span data-ttu-id="0d856-117">You can now add this test image to your model and then retrain your model.</span><span class="sxs-lookup"><span data-stu-id="0d856-117">You can now add this test image to your model and then retrain your model.</span></span>

## <a name="use-the-predicted-image-for-training"></a><span data-ttu-id="0d856-118">Use the predicted image for training.</span><span class="sxs-lookup"><span data-stu-id="0d856-118">Use the predicted image for training.</span></span>

<span data-ttu-id="0d856-119">To use the image submitted previously for training, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="0d856-119">To use the image submitted previously for training, use the following steps:</span></span>

1. <span data-ttu-id="0d856-120">To view images submitted to the classifier, open the [Custom Vision web page](https://customvision.ai) and select the __Predictions__ tab.</span><span class="sxs-lookup"><span data-stu-id="0d856-120">To view images submitted to the classifier, open the [Custom Vision web page](https://customvision.ai) and select the __Predictions__ tab.</span></span>

    ![Image of the predictions tab](./media/test-your-model/predictions-tab.png)

    > [!TIP]
    > <span data-ttu-id="0d856-122">The default view shows images from the current iteration.</span><span class="sxs-lookup"><span data-stu-id="0d856-122">The default view shows images from the current iteration.</span></span> <span data-ttu-id="0d856-123">You can use the __Iteration__ drop down field to view images submitted during previous iterations.</span><span class="sxs-lookup"><span data-stu-id="0d856-123">You can use the __Iteration__ drop down field to view images submitted during previous iterations.</span></span>

2. <span data-ttu-id="0d856-124">Hover over an image to see the tags that were predicted by the classifier.</span><span class="sxs-lookup"><span data-stu-id="0d856-124">Hover over an image to see the tags that were predicted by the classifier.</span></span>

    > [!TIP]
    > <span data-ttu-id="0d856-125">Images are ranked, so that the images that can bring the most gains to the classifier are at the top.</span><span class="sxs-lookup"><span data-stu-id="0d856-125">Images are ranked, so that the images that can bring the most gains to the classifier are at the top.</span></span> <span data-ttu-id="0d856-126">To select a different sorting, use the __Sort__ section.</span><span class="sxs-lookup"><span data-stu-id="0d856-126">To select a different sorting, use the __Sort__ section.</span></span>

    <span data-ttu-id="0d856-127">To add an image to your training data, select the image, select the tag, and then select __Save and close__.</span><span class="sxs-lookup"><span data-stu-id="0d856-127">To add an image to your training data, select the image, select the tag, and then select __Save and close__.</span></span> <span data-ttu-id="0d856-128">The image is removed from __Predictions__ and added to the training images.</span><span class="sxs-lookup"><span data-stu-id="0d856-128">The image is removed from __Predictions__ and added to the training images.</span></span> <span data-ttu-id="0d856-129">You can view it by selecting the __Training Images__ tab.</span><span class="sxs-lookup"><span data-stu-id="0d856-129">You can view it by selecting the __Training Images__ tab.</span></span>

    ![Image of the tagging page](./media/test-your-model/tag-image.png)

3. <span data-ttu-id="0d856-131">Use the __Train__ button to retrain the classifier.</span><span class="sxs-lookup"><span data-stu-id="0d856-131">Use the __Train__ button to retrain the classifier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d856-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d856-132">Next steps</span></span>

[<span data-ttu-id="0d856-133">Improve your classifier</span><span class="sxs-lookup"><span data-stu-id="0d856-133">Improve your classifier</span></span>](getting-started-improving-your-classifier.md)