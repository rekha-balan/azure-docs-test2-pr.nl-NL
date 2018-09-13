---
title: Building a model with the Recommnendations UI | Microsoft Docs
description: Azure Machine Learning Recommendations - Building a model with the Recommendations UI
services: cognitive-services
documentationcenter: ''
author: luiscabrer
manager: jhubbard
editor: cgronlun
ms.assetid: b264fe44-f94e-40ae-9754-60ad7d6cfeb9
ms.service: cognitive-services
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: luisca
ms.openlocfilehash: 488dc9cce5d7ae70aeff1bdb402b8855fbce7f07
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549169"
---
# <a name="building-a-model-with-the-recommendations-ui"></a><span data-ttu-id="26f7a-103">Building a model with the Recommendations UI</span><span class="sxs-lookup"><span data-stu-id="26f7a-103">Building a model with the Recommendations UI</span></span>
<span data-ttu-id="26f7a-104">This document is a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="26f7a-104">This document is a step-by-step guide.</span></span> <span data-ttu-id="26f7a-105">Our objective is to walk you through the steps necessary to train a model using the [Recommendations UI](https://recommendations-portal.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="26f7a-105">Our objective is to walk you through the steps necessary to train a model using the [Recommendations UI](https://recommendations-portal.azurewebsites.net/).</span></span>
<span data-ttu-id="26f7a-106">Going through the exercise allows you to understand the process for building a model before you do it programmatically.</span><span class="sxs-lookup"><span data-stu-id="26f7a-106">Going through the exercise allows you to understand the process for building a model before you do it programmatically.</span></span> <span data-ttu-id="26f7a-107">It also familiarizes you with the UI, which is handy as you start using the service.</span><span class="sxs-lookup"><span data-stu-id="26f7a-107">It also familiarizes you with the UI, which is handy as you start using the service.</span></span>

<span data-ttu-id="26f7a-108">This exercise takes about 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="26f7a-108">This exercise takes about 30 minutes.</span></span>

<a name="Step1"></a>

## <a name="step-1---sign-in-to-the-recommendations-ui"></a><span data-ttu-id="26f7a-109">Step 1 - Sign in to the Recommendations UI</span><span class="sxs-lookup"><span data-stu-id="26f7a-109">Step 1 - Sign in to the Recommendations UI</span></span>
1. <span data-ttu-id="26f7a-110">If you have not done so already, you need to [sign-up](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/Recommendations/pricingtier/S1) for a new [Recommendations API](https://www.microsoft.com/cognitive-services/en-us/recommendations-api) subscription.</span><span class="sxs-lookup"><span data-stu-id="26f7a-110">If you have not done so already, you need to [sign-up](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/Recommendations/pricingtier/S1) for a new [Recommendations API](https://www.microsoft.com/cognitive-services/en-us/recommendations-api) subscription.</span></span> <span data-ttu-id="26f7a-111">You can sign up for the service on **Azure** at [http://portal.azure.com/](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/Recommendations/pricingtier/S1) and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="26f7a-111">You can sign up for the service on **Azure** at [http://portal.azure.com/](https://portal.azure.com/#create/Microsoft.CognitiveServices/apitype/Recommendations/pricingtier/S1) and sign in with your Azure account.</span></span> <span data-ttu-id="26f7a-112">Detailed instructions on the sign up process are provided in *Task 1* of the [Getting Started Guide](cognitive-services-recommendations-quick-start.md)</span><span class="sxs-lookup"><span data-stu-id="26f7a-112">Detailed instructions on the sign up process are provided in *Task 1* of the [Getting Started Guide](cognitive-services-recommendations-quick-start.md)</span></span> 
2. <span data-ttu-id="26f7a-113">Once you have obtained a **Key** for your Recommendations API subscription, go to [Recommendations UI](https://recommendations-portal.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="26f7a-113">Once you have obtained a **Key** for your Recommendations API subscription, go to [Recommendations UI](https://recommendations-portal.azurewebsites.net/).</span></span> 
3. <span data-ttu-id="26f7a-114">Log in to the portal by entering your key in the **Account Key** field, and then click the **Login** button.</span><span class="sxs-lookup"><span data-stu-id="26f7a-114">Log in to the portal by entering your key in the **Account Key** field, and then click the **Login** button.</span></span>
   
    ![Recommendations UI: Sign-in dialog.][reco_signin]

<a name="Step2"></a>

## <a name="step-2---lets-gather-some-training-data"></a><span data-ttu-id="26f7a-116">Step 2 - Let's gather some training data</span><span class="sxs-lookup"><span data-stu-id="26f7a-116">Step 2 - Let's gather some training data</span></span>
<span data-ttu-id="26f7a-117">Before you can create a build, the engine needs two pieces of information: a catalog file and a set of usage files.</span><span class="sxs-lookup"><span data-stu-id="26f7a-117">Before you can create a build, the engine needs two pieces of information: a catalog file and a set of usage files.</span></span> 

<span data-ttu-id="26f7a-118">The catalog file contains information about the items you are offering to your customer.</span><span class="sxs-lookup"><span data-stu-id="26f7a-118">The catalog file contains information about the items you are offering to your customer.</span></span> <span data-ttu-id="26f7a-119">A usage file contains information about how those items are used, or the transactions from your business.</span><span class="sxs-lookup"><span data-stu-id="26f7a-119">A usage file contains information about how those items are used, or the transactions from your business.</span></span>

<span data-ttu-id="26f7a-120">Usually you would query your store database for these pieces of information.</span><span class="sxs-lookup"><span data-stu-id="26f7a-120">Usually you would query your store database for these pieces of information.</span></span> <span data-ttu-id="26f7a-121">Today, we have provided some sample data for you so that you can learn how to use the Recommendations API.</span><span class="sxs-lookup"><span data-stu-id="26f7a-121">Today, we have provided some sample data for you so that you can learn how to use the Recommendations API.</span></span>

<span data-ttu-id="26f7a-122">You can download the data from [http://aka.ms/RecoSampleData](http://aka.ms/RecoSampleData).</span><span class="sxs-lookup"><span data-stu-id="26f7a-122">You can download the data from [http://aka.ms/RecoSampleData](http://aka.ms/RecoSampleData).</span></span> <span data-ttu-id="26f7a-123">Copy and unpack the **Books.Zip** file into a folder on your local machine.</span><span class="sxs-lookup"><span data-stu-id="26f7a-123">Copy and unpack the **Books.Zip** file into a folder on your local machine.</span></span> <span data-ttu-id="26f7a-124">For instance, **c:\data**.</span><span class="sxs-lookup"><span data-stu-id="26f7a-124">For instance, **c:\data**.</span></span>

<span data-ttu-id="26f7a-125">Detailed information on the schema of the catalog and usage files can be found in the [Collecting Data To Train your Model](cognitive-services-recommendations-collecting-data.md) article.</span><span class="sxs-lookup"><span data-stu-id="26f7a-125">Detailed information on the schema of the catalog and usage files can be found in the [Collecting Data To Train your Model](cognitive-services-recommendations-collecting-data.md) article.</span></span>

<span data-ttu-id="26f7a-126">For this exercise, we are going to work with a small file so that you don’t have very to wait too long for training.</span><span class="sxs-lookup"><span data-stu-id="26f7a-126">For this exercise, we are going to work with a small file so that you don’t have very to wait too long for training.</span></span> <span data-ttu-id="26f7a-127">If you want to try a more realistic file, we have also placed **MsStoreData.zip** that contains sample transactions from the Microsoft Store in the [same location](http://aka.ms/RecoSampleData).</span><span class="sxs-lookup"><span data-stu-id="26f7a-127">If you want to try a more realistic file, we have also placed **MsStoreData.zip** that contains sample transactions from the Microsoft Store in the [same location](http://aka.ms/RecoSampleData).</span></span>

<a name="Step3"></a>

## <a name="step-3---create-a-project-and-upload-catalog-and-usage-data"></a><span data-ttu-id="26f7a-128">Step 3 - Create a project and upload catalog and usage data</span><span class="sxs-lookup"><span data-stu-id="26f7a-128">Step 3 - Create a project and upload catalog and usage data</span></span>
<span data-ttu-id="26f7a-129">Upon logging in to the [Recommendations UI](https://recommendations-portal.azurewebsites.net/), you see the Projects Page.</span><span class="sxs-lookup"><span data-stu-id="26f7a-129">Upon logging in to the [Recommendations UI](https://recommendations-portal.azurewebsites.net/), you see the Projects Page.</span></span> <span data-ttu-id="26f7a-130">If you have previously created any projects, you should see them here.</span><span class="sxs-lookup"><span data-stu-id="26f7a-130">If you have previously created any projects, you should see them here.</span></span>
<span data-ttu-id="26f7a-131">A project (also known as *a model* in the API reference) is a container for your catalog and usage data.</span><span class="sxs-lookup"><span data-stu-id="26f7a-131">A project (also known as *a model* in the API reference) is a container for your catalog and usage data.</span></span> <span data-ttu-id="26f7a-132">You can create several *builds* inside the project.</span><span class="sxs-lookup"><span data-stu-id="26f7a-132">You can create several *builds* inside the project.</span></span> <span data-ttu-id="26f7a-133">We will walk you through the process in the next steps.</span><span class="sxs-lookup"><span data-stu-id="26f7a-133">We will walk you through the process in the next steps.</span></span>

1. <span data-ttu-id="26f7a-134">To create a new project, type the name on the text box (Something like “MyFirstModel” would work) and click **Add Project**.</span><span class="sxs-lookup"><span data-stu-id="26f7a-134">To create a new project, type the name on the text box (Something like “MyFirstModel” would work) and click **Add Project**.</span></span>
   
    ![Recommendations UI: Projects Page.][reco_projects]
2. <span data-ttu-id="26f7a-136">Once the project gets created, click the **Browse for File** button on the **Add a Catalog File** section.</span><span class="sxs-lookup"><span data-stu-id="26f7a-136">Once the project gets created, click the **Browse for File** button on the **Add a Catalog File** section.</span></span> 
   <span data-ttu-id="26f7a-137">Upload the catalog you got in step 2.</span><span class="sxs-lookup"><span data-stu-id="26f7a-137">Upload the catalog you got in step 2.</span></span> <span data-ttu-id="26f7a-138">If you saved it at *c:\data*, you need to navigate to that folder.</span><span class="sxs-lookup"><span data-stu-id="26f7a-138">If you saved it at *c:\data*, you need to navigate to that folder.</span></span>
   
     ![Recommendations UI: Adding Data to a Project.][reco_firstmodel]
3. <span data-ttu-id="26f7a-140">After the catalog is uploaded, click the **Browse for File** button on the **Add Usage Files** section.</span><span class="sxs-lookup"><span data-stu-id="26f7a-140">After the catalog is uploaded, click the **Browse for File** button on the **Add Usage Files** section.</span></span> <span data-ttu-id="26f7a-141">Add the usage_large.txt file.</span><span class="sxs-lookup"><span data-stu-id="26f7a-141">Add the usage_large.txt file.</span></span>

> <span data-ttu-id="26f7a-142">**What if I have a large file of usage data?**</span><span class="sxs-lookup"><span data-stu-id="26f7a-142">**What if I have a large file of usage data?**</span></span>
> 
> <span data-ttu-id="26f7a-143">Only usage files smaller than 200-MB  can be uploaded.</span><span class="sxs-lookup"><span data-stu-id="26f7a-143">Only usage files smaller than 200-MB  can be uploaded.</span></span> <span data-ttu-id="26f7a-144">That said, the system can hold up to 2-GB worth of transaction data, so you can upload more than one file if necessary.</span><span class="sxs-lookup"><span data-stu-id="26f7a-144">That said, the system can hold up to 2-GB worth of transaction data, so you can upload more than one file if necessary.</span></span>
> <span data-ttu-id="26f7a-145">You may not need that much data to generate a good model, it’s not just the size of the data that matters, but the quality of the data.</span><span class="sxs-lookup"><span data-stu-id="26f7a-145">You may not need that much data to generate a good model, it’s not just the size of the data that matters, but the quality of the data.</span></span> <span data-ttu-id="26f7a-146">It is common to see usage data where most of the transactions are just on a handful of popular items, and there is “little signal” for other items.</span><span class="sxs-lookup"><span data-stu-id="26f7a-146">It is common to see usage data where most of the transactions are just on a handful of popular items, and there is “little signal” for other items.</span></span>
> 
> 

<a name="Step4"></a>

## <a name="step-4---lets-do-some-training"></a><span data-ttu-id="26f7a-147">Step 4 - Let's do some training!</span><span class="sxs-lookup"><span data-stu-id="26f7a-147">Step 4 - Let's do some training!</span></span>
<span data-ttu-id="26f7a-148">Now that you have uploaded both the catalog and the usage data, we are ready to train the engine so that it can learn patterns from our data.</span><span class="sxs-lookup"><span data-stu-id="26f7a-148">Now that you have uploaded both the catalog and the usage data, we are ready to train the engine so that it can learn patterns from our data.</span></span>

1. <span data-ttu-id="26f7a-149">Click the **New Build** button.</span><span class="sxs-lookup"><span data-stu-id="26f7a-149">Click the **New Build** button.</span></span>
2. <span data-ttu-id="26f7a-150">Select **Recommendations** as the build type.</span><span class="sxs-lookup"><span data-stu-id="26f7a-150">Select **Recommendations** as the build type.</span></span> <span data-ttu-id="26f7a-151">Notice that we support a Ranking Build and an FBT (Frequently Bought Together) build types as well.</span><span class="sxs-lookup"><span data-stu-id="26f7a-151">Notice that we support a Ranking Build and an FBT (Frequently Bought Together) build types as well.</span></span>
   
   ![Recommendations UI: Build Dialog.][reco_build_dialog.png]

    <span data-ttu-id="26f7a-153">An FBT build allows you to identify patterns for products that are usually purchased/consumed in the same transaction.</span><span class="sxs-lookup"><span data-stu-id="26f7a-153">An FBT build allows you to identify patterns for products that are usually purchased/consumed in the same transaction.</span></span>
    <span data-ttu-id="26f7a-154">A ranking build is used to identify features of interest.</span><span class="sxs-lookup"><span data-stu-id="26f7a-154">A ranking build is used to identify features of interest.</span></span> 
    <span data-ttu-id="26f7a-155">We won’t go very deep into FBT or ranking builds in this workshop, but if you are interested you should check out the [Build types and model quality documentation page](cognitive-services-recommendations-buildtypes.md).</span><span class="sxs-lookup"><span data-stu-id="26f7a-155">We won’t go very deep into FBT or ranking builds in this workshop, but if you are interested you should check out the [Build types and model quality documentation page](cognitive-services-recommendations-buildtypes.md).</span></span>

1. <span data-ttu-id="26f7a-156">Click the **Build** button.</span><span class="sxs-lookup"><span data-stu-id="26f7a-156">Click the **Build** button.</span></span> <span data-ttu-id="26f7a-157">The build process takes about five minutes if you are using the Books data.</span><span class="sxs-lookup"><span data-stu-id="26f7a-157">The build process takes about five minutes if you are using the Books data.</span></span> <span data-ttu-id="26f7a-158">It takes longer on larger datasets.</span><span class="sxs-lookup"><span data-stu-id="26f7a-158">It takes longer on larger datasets.</span></span>

<a name="Step5"></a>

## <a name="step-5---lets-find-out-what-the-machine-learned"></a><span data-ttu-id="26f7a-159">Step 5 - Let's find out what the machine learned!</span><span class="sxs-lookup"><span data-stu-id="26f7a-159">Step 5 - Let's find out what the machine learned!</span></span>
<span data-ttu-id="26f7a-160">Once your build is completed, you will notice a new build in the builds list.</span><span class="sxs-lookup"><span data-stu-id="26f7a-160">Once your build is completed, you will notice a new build in the builds list.</span></span> <span data-ttu-id="26f7a-161">This build can be queried for item and user recommendations.</span><span class="sxs-lookup"><span data-stu-id="26f7a-161">This build can be queried for item and user recommendations.</span></span>

1. <span data-ttu-id="26f7a-162">Once your build is completed, click **Score**.</span><span class="sxs-lookup"><span data-stu-id="26f7a-162">Once your build is completed, click **Score**.</span></span> <span data-ttu-id="26f7a-163">This allows you to play with the model and see what items are recommended.</span><span class="sxs-lookup"><span data-stu-id="26f7a-163">This allows you to play with the model and see what items are recommended.</span></span>
   
    ![Recommendations UI: Score button][reco_score_button]
2. <span data-ttu-id="26f7a-165">Select an item to see which items are returned as recommendations for that item.</span><span class="sxs-lookup"><span data-stu-id="26f7a-165">Select an item to see which items are returned as recommendations for that item.</span></span> <span data-ttu-id="26f7a-166">Notice that if there are not enough transactions to predict a recommendation for a particular item, the system will not return any recommendations for that item.</span><span class="sxs-lookup"><span data-stu-id="26f7a-166">Notice that if there are not enough transactions to predict a recommendation for a particular item, the system will not return any recommendations for that item.</span></span>  <span data-ttu-id="26f7a-167">If for some reason you have an item that returns no recommendations, try scoring other items.</span><span class="sxs-lookup"><span data-stu-id="26f7a-167">If for some reason you have an item that returns no recommendations, try scoring other items.</span></span>

<a name="Step6"></a>

## <a name="step-6---next-steps"></a><span data-ttu-id="26f7a-168">Step 6 - Next steps</span><span class="sxs-lookup"><span data-stu-id="26f7a-168">Step 6 - Next steps</span></span>
<span data-ttu-id="26f7a-169">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="26f7a-169">Congratulations!</span></span> <span data-ttu-id="26f7a-170">you have trained a model and then got recommendations from that model.</span><span class="sxs-lookup"><span data-stu-id="26f7a-170">you have trained a model and then got recommendations from that model.</span></span>  <span data-ttu-id="26f7a-171">The Recommendations UI is a useful tool that allows you to see the state of your projects and builds.</span><span class="sxs-lookup"><span data-stu-id="26f7a-171">The Recommendations UI is a useful tool that allows you to see the state of your projects and builds.</span></span> 

<span data-ttu-id="26f7a-172">Now that you have a model, you may want to learn how to do all the steps above programmatically.</span><span class="sxs-lookup"><span data-stu-id="26f7a-172">Now that you have a model, you may want to learn how to do all the steps above programmatically.</span></span> <span data-ttu-id="26f7a-173">In order to do learn to call the API programmatically, we invite you to check the [Recommendations API Reference](http://go.microsoft.com/fwlink/?LinkId=759348) and download the [Recommendations Sample Application](http://go.microsoft.com/fwlink/?LinkID=759344).</span><span class="sxs-lookup"><span data-stu-id="26f7a-173">In order to do learn to call the API programmatically, we invite you to check the [Recommendations API Reference](http://go.microsoft.com/fwlink/?LinkId=759348) and download the [Recommendations Sample Application](http://go.microsoft.com/fwlink/?LinkID=759344).</span></span>

[reco_signin]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/cognitive-services/reco_signin.PNG
[reco_projects]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/cognitive-services/reco_projects.PNG
[reco_firstmodel]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/cognitive-services/reco_firstmodel.png
[reco_build_dialog.png]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/cognitive-services/reco_build_dialog.png
[reco_score_button]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/cognitive-services/reco_score_button.png





