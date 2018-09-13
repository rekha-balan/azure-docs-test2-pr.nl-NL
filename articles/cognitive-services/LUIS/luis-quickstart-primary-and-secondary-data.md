---
title: Tutorial creating a LUIS app to extract data - Azure | Microsoft Docs
description: In this tutorial, learn how to create a simple LUIS app using intents and a simple entity to extract machine-learned data.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: a69ea8ea45a02399b7c6ad22f0dc514ad8537e06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864381"
---
# <a name="tutorial-7-add-simple-entity-and-phrase-list"></a><span data-ttu-id="ae534-103">Tutorial: 7.</span><span class="sxs-lookup"><span data-stu-id="ae534-103">Tutorial: 7.</span></span> <span data-ttu-id="ae534-104">Add simple entity and phrase list</span><span class="sxs-lookup"><span data-stu-id="ae534-104">Add simple entity and phrase list</span></span>
<span data-ttu-id="ae534-105">In this tutorial, create an app that demonstrates how to extract machine-learned data from an utterance using the **Simple** entity.</span><span class="sxs-lookup"><span data-stu-id="ae534-105">In this tutorial, create an app that demonstrates how to extract machine-learned data from an utterance using the **Simple** entity.</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="ae534-106">Understand simple entities</span><span class="sxs-lookup"><span data-stu-id="ae534-106">Understand simple entities</span></span> 
> * <span data-ttu-id="ae534-107">Create new LUIS app for the Human Resources (HR) domain</span><span class="sxs-lookup"><span data-stu-id="ae534-107">Create new LUIS app for the Human Resources (HR) domain</span></span> 
> * <span data-ttu-id="ae534-108">Add simple entity to extract jobs from app</span><span class="sxs-lookup"><span data-stu-id="ae534-108">Add simple entity to extract jobs from app</span></span>
> * <span data-ttu-id="ae534-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="ae534-109">Train, and publish app</span></span>
> * <span data-ttu-id="ae534-110">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="ae534-110">Query endpoint of app to see LUIS JSON response</span></span>
> * <span data-ttu-id="ae534-111">Add phrase list to boost signal of job words</span><span class="sxs-lookup"><span data-stu-id="ae534-111">Add phrase list to boost signal of job words</span></span>
> * <span data-ttu-id="ae534-112">Train, publish app, and requery endpoint</span><span class="sxs-lookup"><span data-stu-id="ae534-112">Train, publish app, and requery endpoint</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="ae534-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ae534-113">Before you begin</span></span>
<span data-ttu-id="ae534-114">If you don't have the Human Resources app from the [composite entity](luis-tutorial-composite-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="ae534-114">If you don't have the Human Resources app from the [composite entity](luis-tutorial-composite-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="ae534-115">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-composite-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="ae534-115">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-composite-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="ae534-116">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `simple`.</span><span class="sxs-lookup"><span data-stu-id="ae534-116">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `simple`.</span></span> <span data-ttu-id="ae534-117">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="ae534-117">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span>  

## <a name="purpose-of-the-app"></a><span data-ttu-id="ae534-118">Purpose of the app</span><span class="sxs-lookup"><span data-stu-id="ae534-118">Purpose of the app</span></span>
<span data-ttu-id="ae534-119">This app demonstrates how to pull data out of an utterance.</span><span class="sxs-lookup"><span data-stu-id="ae534-119">This app demonstrates how to pull data out of an utterance.</span></span> <span data-ttu-id="ae534-120">Consider the following utterances from a chatbot:</span><span class="sxs-lookup"><span data-stu-id="ae534-120">Consider the following utterances from a chatbot:</span></span>

|<span data-ttu-id="ae534-121">Utterance</span><span class="sxs-lookup"><span data-stu-id="ae534-121">Utterance</span></span>|<span data-ttu-id="ae534-122">Extractable job name</span><span class="sxs-lookup"><span data-stu-id="ae534-122">Extractable job name</span></span>|
|:--|:--|
|<span data-ttu-id="ae534-123">I want to apply for the new accounting job.</span><span class="sxs-lookup"><span data-stu-id="ae534-123">I want to apply for the new accounting job.</span></span>|<span data-ttu-id="ae534-124">accounting</span><span class="sxs-lookup"><span data-stu-id="ae534-124">accounting</span></span>|
|<span data-ttu-id="ae534-125">Please submit my resume for the engineering position.</span><span class="sxs-lookup"><span data-stu-id="ae534-125">Please submit my resume for the engineering position.</span></span>|<span data-ttu-id="ae534-126">engineering</span><span class="sxs-lookup"><span data-stu-id="ae534-126">engineering</span></span>|
|<span data-ttu-id="ae534-127">Fill out application for job 123456</span><span class="sxs-lookup"><span data-stu-id="ae534-127">Fill out application for job 123456</span></span>|<span data-ttu-id="ae534-128">123456</span><span class="sxs-lookup"><span data-stu-id="ae534-128">123456</span></span>|

<span data-ttu-id="ae534-129">This tutorial adds a new entity to extract the job name.</span><span class="sxs-lookup"><span data-stu-id="ae534-129">This tutorial adds a new entity to extract the job name.</span></span> 

## <a name="purpose-of-the-simple-entity"></a><span data-ttu-id="ae534-130">Purpose of the simple entity</span><span class="sxs-lookup"><span data-stu-id="ae534-130">Purpose of the simple entity</span></span>
<span data-ttu-id="ae534-131">The purpose of the simple entity in this LUIS app is to teach LUIS what a job name is and where it can be found in an utterance.</span><span class="sxs-lookup"><span data-stu-id="ae534-131">The purpose of the simple entity in this LUIS app is to teach LUIS what a job name is and where it can be found in an utterance.</span></span> <span data-ttu-id="ae534-132">The part of the utterance that is the job can change from utterance to utterance based on word choice and utterance length.</span><span class="sxs-lookup"><span data-stu-id="ae534-132">The part of the utterance that is the job can change from utterance to utterance based on word choice and utterance length.</span></span> <span data-ttu-id="ae534-133">LUIS needs examples of jobs in any utterance across all intents.</span><span class="sxs-lookup"><span data-stu-id="ae534-133">LUIS needs examples of jobs in any utterance across all intents.</span></span>  

<span data-ttu-id="ae534-134">The job name is difficult to determine because a name can be a noun, verb, or a phrase of several words.</span><span class="sxs-lookup"><span data-stu-id="ae534-134">The job name is difficult to determine because a name can be a noun, verb, or a phrase of several words.</span></span> <span data-ttu-id="ae534-135">For example:</span><span class="sxs-lookup"><span data-stu-id="ae534-135">For example:</span></span>

|<span data-ttu-id="ae534-136">Jobs</span><span class="sxs-lookup"><span data-stu-id="ae534-136">Jobs</span></span>|
|--|
|<span data-ttu-id="ae534-137">engineer</span><span class="sxs-lookup"><span data-stu-id="ae534-137">engineer</span></span>|
|<span data-ttu-id="ae534-138">software engineer</span><span class="sxs-lookup"><span data-stu-id="ae534-138">software engineer</span></span>|
|<span data-ttu-id="ae534-139">senior software engineer</span><span class="sxs-lookup"><span data-stu-id="ae534-139">senior software engineer</span></span>|
|<span data-ttu-id="ae534-140">engineering team lead</span><span class="sxs-lookup"><span data-stu-id="ae534-140">engineering team lead</span></span> |
|<span data-ttu-id="ae534-141">air traffic controller</span><span class="sxs-lookup"><span data-stu-id="ae534-141">air traffic controller</span></span>|
|<span data-ttu-id="ae534-142">motor vehicle operator</span><span class="sxs-lookup"><span data-stu-id="ae534-142">motor vehicle operator</span></span>|
|<span data-ttu-id="ae534-143">ambulance driver</span><span class="sxs-lookup"><span data-stu-id="ae534-143">ambulance driver</span></span>|
|<span data-ttu-id="ae534-144">tender</span><span class="sxs-lookup"><span data-stu-id="ae534-144">tender</span></span>|
|<span data-ttu-id="ae534-145">extruder</span><span class="sxs-lookup"><span data-stu-id="ae534-145">extruder</span></span>|
|<span data-ttu-id="ae534-146">millwright</span><span class="sxs-lookup"><span data-stu-id="ae534-146">millwright</span></span>|

<span data-ttu-id="ae534-147">This LUIS app has job names in several intents.</span><span class="sxs-lookup"><span data-stu-id="ae534-147">This LUIS app has job names in several intents.</span></span> <span data-ttu-id="ae534-148">By labeling these words in all the intents' utterances, LUIS learns more about what a job is and where it is found in utterances.</span><span class="sxs-lookup"><span data-stu-id="ae534-148">By labeling these words in all the intents' utterances, LUIS learns more about what a job is and where it is found in utterances.</span></span>

## <a name="create-job-simple-entity"></a><span data-ttu-id="ae534-149">Create job simple entity</span><span class="sxs-lookup"><span data-stu-id="ae534-149">Create job simple entity</span></span>

1. <span data-ttu-id="ae534-150">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="ae534-150">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="ae534-151">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="ae534-151">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="ae534-152">On the **Intents** page, select **ApplyForJob** intent.</span><span class="sxs-lookup"><span data-stu-id="ae534-152">On the **Intents** page, select **ApplyForJob** intent.</span></span> 

    <span data-ttu-id="ae534-153">[![](media/luis-quickstart-primary-and-secondary-data/hr-select-applyforjob.png "Screenshot of LUIS with 'ApplyForJob' intent highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-select-applyforjob.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-153">[![](media/luis-quickstart-primary-and-secondary-data/hr-select-applyforjob.png "Screenshot of LUIS with 'ApplyForJob' intent highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-select-applyforjob.png#lightbox)</span></span>

3. <span data-ttu-id="ae534-154">In the utterance, `I want to apply for the new accounting job`, select `accounting`, enter `Job` in the top field of the pop-up menu, then select **Create new entity** in the pop-up menu.</span><span class="sxs-lookup"><span data-stu-id="ae534-154">In the utterance, `I want to apply for the new accounting job`, select `accounting`, enter `Job` in the top field of the pop-up menu, then select **Create new entity** in the pop-up menu.</span></span> 

    <span data-ttu-id="ae534-155">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-entity.png "Screenshot of LUIS with 'ApplyForJob' intent with create entity steps highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-create-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-155">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-entity.png "Screenshot of LUIS with 'ApplyForJob' intent with create entity steps highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-create-entity.png#lightbox)</span></span>

4. <span data-ttu-id="ae534-156">In the pop-up window, verify the entity name and type and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="ae534-156">In the pop-up window, verify the entity name and type and select **Done**.</span></span>

    ![Create simple entity pop-up modal dialog with name of Job and type of simple](media/luis-quickstart-primary-and-secondary-data/hr-create-simple-entity-popup.png)

5. <span data-ttu-id="ae534-158">In the utterance, `Submit resume for engineering position`, label the word `engineering` as a Job entity.</span><span class="sxs-lookup"><span data-stu-id="ae534-158">In the utterance, `Submit resume for engineering position`, label the word `engineering` as a Job entity.</span></span> <span data-ttu-id="ae534-159">Select the word `engineering`, then select **Job** from the pop-up menu.</span><span class="sxs-lookup"><span data-stu-id="ae534-159">Select the word `engineering`, then select **Job** from the pop-up menu.</span></span> 

    <span data-ttu-id="ae534-160">[![](media/luis-quickstart-primary-and-secondary-data/hr-label-simple-entity.png "Screenshot of LUIS labeling job entity highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-label-simple-entity.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-160">[![](media/luis-quickstart-primary-and-secondary-data/hr-label-simple-entity.png "Screenshot of LUIS labeling job entity highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-label-simple-entity.png#lightbox)</span></span>

    <span data-ttu-id="ae534-161">All the utterances are labeled but five utterances aren't enough to teach LUIS about job-related words and phrases.</span><span class="sxs-lookup"><span data-stu-id="ae534-161">All the utterances are labeled but five utterances aren't enough to teach LUIS about job-related words and phrases.</span></span> <span data-ttu-id="ae534-162">The jobs that use the number value do not need more examples because that uses a regular expression entity.</span><span class="sxs-lookup"><span data-stu-id="ae534-162">The jobs that use the number value do not need more examples because that uses a regular expression entity.</span></span> <span data-ttu-id="ae534-163">The jobs that are words or phrases need at least 15 more examples.</span><span class="sxs-lookup"><span data-stu-id="ae534-163">The jobs that are words or phrases need at least 15 more examples.</span></span> 

6. <span data-ttu-id="ae534-164">Add more utterances and mark the job words or phrases as **Job** entity.</span><span class="sxs-lookup"><span data-stu-id="ae534-164">Add more utterances and mark the job words or phrases as **Job** entity.</span></span> <span data-ttu-id="ae534-165">The job types are general across employment for an employment service.</span><span class="sxs-lookup"><span data-stu-id="ae534-165">The job types are general across employment for an employment service.</span></span> <span data-ttu-id="ae534-166">If you wanted jobs related to a specific industry, the job words should reflect that.</span><span class="sxs-lookup"><span data-stu-id="ae534-166">If you wanted jobs related to a specific industry, the job words should reflect that.</span></span> 

    |<span data-ttu-id="ae534-167">Utterance</span><span class="sxs-lookup"><span data-stu-id="ae534-167">Utterance</span></span>|<span data-ttu-id="ae534-168">Job entity</span><span class="sxs-lookup"><span data-stu-id="ae534-168">Job entity</span></span>|
    |:--|:--|
    |<span data-ttu-id="ae534-169">I'm applying for the Program Manager desk in R&D</span><span class="sxs-lookup"><span data-stu-id="ae534-169">I'm applying for the Program Manager desk in R&D</span></span>|<span data-ttu-id="ae534-170">Program Manager</span><span class="sxs-lookup"><span data-stu-id="ae534-170">Program Manager</span></span>|
    |<span data-ttu-id="ae534-171">Here is my line cook application.</span><span class="sxs-lookup"><span data-stu-id="ae534-171">Here is my line cook application.</span></span>|<span data-ttu-id="ae534-172">line cook</span><span class="sxs-lookup"><span data-stu-id="ae534-172">line cook</span></span>|
    |<span data-ttu-id="ae534-173">My resume for camp counselor is attached.</span><span class="sxs-lookup"><span data-stu-id="ae534-173">My resume for camp counselor is attached.</span></span>|<span data-ttu-id="ae534-174">camp counselor</span><span class="sxs-lookup"><span data-stu-id="ae534-174">camp counselor</span></span>|
    |<span data-ttu-id="ae534-175">This is my c.v.</span><span class="sxs-lookup"><span data-stu-id="ae534-175">This is my c.v.</span></span> <span data-ttu-id="ae534-176">for administrative assistant.</span><span class="sxs-lookup"><span data-stu-id="ae534-176">for administrative assistant.</span></span>|<span data-ttu-id="ae534-177">administrative assistant</span><span class="sxs-lookup"><span data-stu-id="ae534-177">administrative assistant</span></span>|
    |<span data-ttu-id="ae534-178">I want to apply for the management job in sales.</span><span class="sxs-lookup"><span data-stu-id="ae534-178">I want to apply for the management job in sales.</span></span>|<span data-ttu-id="ae534-179">management, sales</span><span class="sxs-lookup"><span data-stu-id="ae534-179">management, sales</span></span>|
    |<span data-ttu-id="ae534-180">This is my resume for the new accounting position.</span><span class="sxs-lookup"><span data-stu-id="ae534-180">This is my resume for the new accounting position.</span></span>|<span data-ttu-id="ae534-181">accounting</span><span class="sxs-lookup"><span data-stu-id="ae534-181">accounting</span></span>|
    |<span data-ttu-id="ae534-182">My application for barback is included.</span><span class="sxs-lookup"><span data-stu-id="ae534-182">My application for barback is included.</span></span>|<span data-ttu-id="ae534-183">barback</span><span class="sxs-lookup"><span data-stu-id="ae534-183">barback</span></span>|
    |<span data-ttu-id="ae534-184">I'm submitting my application for roofer and framer.</span><span class="sxs-lookup"><span data-stu-id="ae534-184">I'm submitting my application for roofer and framer.</span></span>|<span data-ttu-id="ae534-185">roofer, framer</span><span class="sxs-lookup"><span data-stu-id="ae534-185">roofer, framer</span></span>|
    |<span data-ttu-id="ae534-186">My c.v.</span><span class="sxs-lookup"><span data-stu-id="ae534-186">My c.v.</span></span> <span data-ttu-id="ae534-187">for bus driver is here.</span><span class="sxs-lookup"><span data-stu-id="ae534-187">for bus driver is here.</span></span>|<span data-ttu-id="ae534-188">bus driver</span><span class="sxs-lookup"><span data-stu-id="ae534-188">bus driver</span></span>|
    |<span data-ttu-id="ae534-189">I'm a registered nurse.</span><span class="sxs-lookup"><span data-stu-id="ae534-189">I'm a registered nurse.</span></span> <span data-ttu-id="ae534-190">Here is my resume.</span><span class="sxs-lookup"><span data-stu-id="ae534-190">Here is my resume.</span></span>|<span data-ttu-id="ae534-191">registered nurse</span><span class="sxs-lookup"><span data-stu-id="ae534-191">registered nurse</span></span>|
    |<span data-ttu-id="ae534-192">I would like to submit my paperwork for the teaching position I saw in the paper.</span><span class="sxs-lookup"><span data-stu-id="ae534-192">I would like to submit my paperwork for the teaching position I saw in the paper.</span></span>|<span data-ttu-id="ae534-193">teaching</span><span class="sxs-lookup"><span data-stu-id="ae534-193">teaching</span></span>|
    |<span data-ttu-id="ae534-194">This is my c.v.</span><span class="sxs-lookup"><span data-stu-id="ae534-194">This is my c.v.</span></span> <span data-ttu-id="ae534-195">for the stocker post in fruits and vegetables.</span><span class="sxs-lookup"><span data-stu-id="ae534-195">for the stocker post in fruits and vegetables.</span></span>|<span data-ttu-id="ae534-196">stocker</span><span class="sxs-lookup"><span data-stu-id="ae534-196">stocker</span></span>|
    |<span data-ttu-id="ae534-197">Apply for tile work.</span><span class="sxs-lookup"><span data-stu-id="ae534-197">Apply for tile work.</span></span>|<span data-ttu-id="ae534-198">tile</span><span class="sxs-lookup"><span data-stu-id="ae534-198">tile</span></span>|
    |<span data-ttu-id="ae534-199">Attached resume for landscape architect.</span><span class="sxs-lookup"><span data-stu-id="ae534-199">Attached resume for landscape architect.</span></span>|<span data-ttu-id="ae534-200">landscape architect</span><span class="sxs-lookup"><span data-stu-id="ae534-200">landscape architect</span></span>|
    |<span data-ttu-id="ae534-201">My curriculum vitae for professor of biology is enclosed.</span><span class="sxs-lookup"><span data-stu-id="ae534-201">My curriculum vitae for professor of biology is enclosed.</span></span>|<span data-ttu-id="ae534-202">professor of biology</span><span class="sxs-lookup"><span data-stu-id="ae534-202">professor of biology</span></span>|
    |<span data-ttu-id="ae534-203">I would like to apply for the position in photography.</span><span class="sxs-lookup"><span data-stu-id="ae534-203">I would like to apply for the position in photography.</span></span>|<span data-ttu-id="ae534-204">photography</span><span class="sxs-lookup"><span data-stu-id="ae534-204">photography</span></span>|<span data-ttu-id="ae534-205">git</span><span class="sxs-lookup"><span data-stu-id="ae534-205">git</span></span> 

## <a name="label-entity-in-example-utterances-for-getjobinformation-intent"></a><span data-ttu-id="ae534-206">Label entity in example utterances for GetJobInformation intent</span><span class="sxs-lookup"><span data-stu-id="ae534-206">Label entity in example utterances for GetJobInformation intent</span></span>
1. <span data-ttu-id="ae534-207">Select **Intents** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="ae534-207">Select **Intents** from the left menu.</span></span>

2. <span data-ttu-id="ae534-208">Select **GetJobInformation** from the list of intents.</span><span class="sxs-lookup"><span data-stu-id="ae534-208">Select **GetJobInformation** from the list of intents.</span></span> 

3. <span data-ttu-id="ae534-209">Label the jobs in the example utterances:</span><span class="sxs-lookup"><span data-stu-id="ae534-209">Label the jobs in the example utterances:</span></span>

    |<span data-ttu-id="ae534-210">Utterance</span><span class="sxs-lookup"><span data-stu-id="ae534-210">Utterance</span></span>|<span data-ttu-id="ae534-211">Job entity</span><span class="sxs-lookup"><span data-stu-id="ae534-211">Job entity</span></span>|
    |:--|:--|
    |<span data-ttu-id="ae534-212">Is there any work in databases?</span><span class="sxs-lookup"><span data-stu-id="ae534-212">Is there any work in databases?</span></span>|<span data-ttu-id="ae534-213">databases</span><span class="sxs-lookup"><span data-stu-id="ae534-213">databases</span></span>|
    |<span data-ttu-id="ae534-214">Looking for a new situation with responsibilities in accounting</span><span class="sxs-lookup"><span data-stu-id="ae534-214">Looking for a new situation with responsibilities in accounting</span></span>|<span data-ttu-id="ae534-215">accounting</span><span class="sxs-lookup"><span data-stu-id="ae534-215">accounting</span></span>|
    |<span data-ttu-id="ae534-216">What positions are available for senior engineers?</span><span class="sxs-lookup"><span data-stu-id="ae534-216">What positions are available for senior engineers?</span></span>|<span data-ttu-id="ae534-217">senior engineers</span><span class="sxs-lookup"><span data-stu-id="ae534-217">senior engineers</span></span>|

    <span data-ttu-id="ae534-218">There are other example utterances but they do not contain job words.</span><span class="sxs-lookup"><span data-stu-id="ae534-218">There are other example utterances but they do not contain job words.</span></span>

## <a name="train-the-luis-app"></a><span data-ttu-id="ae534-219">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="ae534-219">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="ae534-220">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="ae534-220">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-a-different-utterance"></a><span data-ttu-id="ae534-221">Query the endpoint with a different utterance</span><span class="sxs-lookup"><span data-stu-id="ae534-221">Query the endpoint with a different utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)]

2. <span data-ttu-id="ae534-222">Go to the end of the URL in the address and enter `Here is my c.v. for the programmer job`.</span><span class="sxs-lookup"><span data-stu-id="ae534-222">Go to the end of the URL in the address and enter `Here is my c.v. for the programmer job`.</span></span> <span data-ttu-id="ae534-223">The last querystring parameter is `q`, the utterance **query**.</span><span class="sxs-lookup"><span data-stu-id="ae534-223">The last querystring parameter is `q`, the utterance **query**.</span></span> <span data-ttu-id="ae534-224">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `ApplyForJob` utterances.</span><span class="sxs-lookup"><span data-stu-id="ae534-224">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `ApplyForJob` utterances.</span></span>

```JSON
{
  "query": "Here is my c.v. for the programmer job",
  "topScoringIntent": {
    "intent": "ApplyForJob",
    "score": 0.9826467
  },
  "intents": [
    {
      "intent": "ApplyForJob",
      "score": 0.9826467
    },
    {
      "intent": "GetJobInformation",
      "score": 0.0218927357
    },
    {
      "intent": "MoveEmployee",
      "score": 0.007849265
    },
    {
      "intent": "Utilities.StartOver",
      "score": 0.00349470088
    },
    {
      "intent": "Utilities.Confirm",
      "score": 0.00348804821
    },
    {
      "intent": "None",
      "score": 0.00319909188
    },
    {
      "intent": "FindForm",
      "score": 0.00222647213
    },
    {
      "intent": "Utilities.Help",
      "score": 0.00211193133
    },
    {
      "intent": "Utilities.Stop",
      "score": 0.00172086991
    },
    {
      "intent": "Utilities.Cancel",
      "score": 0.00138010911
    }
  ],
  "entities": [
    {
      "entity": "programmer",
      "type": "Job",
      "startIndex": 24,
      "endIndex": 33,
      "score": 0.5230502
    }
  ]
}
```

## <a name="names-are-tricky"></a><span data-ttu-id="ae534-225">Names are tricky</span><span class="sxs-lookup"><span data-stu-id="ae534-225">Names are tricky</span></span>
<span data-ttu-id="ae534-226">The LUIS app found the correct intent with high confidence and it extracted the job name, but names are tricky.</span><span class="sxs-lookup"><span data-stu-id="ae534-226">The LUIS app found the correct intent with high confidence and it extracted the job name, but names are tricky.</span></span> <span data-ttu-id="ae534-227">Try the utterance `This is the lead welder paperwork`.</span><span class="sxs-lookup"><span data-stu-id="ae534-227">Try the utterance `This is the lead welder paperwork`.</span></span>  

<span data-ttu-id="ae534-228">In the following JSON, LUIS responds with the correct intent, `ApplyForJob`, but didn't extract the `lead welder` job name.</span><span class="sxs-lookup"><span data-stu-id="ae534-228">In the following JSON, LUIS responds with the correct intent, `ApplyForJob`, but didn't extract the `lead welder` job name.</span></span> 

```JSON
{
  "query": "This is the lead welder paperwork.",
  "topScoringIntent": {
    "intent": "ApplyForJob",
    "score": 0.468558252
  },
  "intents": [
    {
      "intent": "ApplyForJob",
      "score": 0.468558252
    },
    {
      "intent": "GetJobInformation",
      "score": 0.0102701457
    },
    {
      "intent": "MoveEmployee",
      "score": 0.009442534
    },
    {
      "intent": "Utilities.StartOver",
      "score": 0.00639619166
    },
    {
      "intent": "None",
      "score": 0.005859333
    },
    {
      "intent": "Utilities.Cancel",
      "score": 0.005087704
    },
    {
      "intent": "Utilities.Stop",
      "score": 0.00315379258
    },
    {
      "intent": "Utilities.Help",
      "score": 0.00259344373
    },
    {
      "intent": "FindForm",
      "score": 0.00193389168
    },
    {
      "intent": "Utilities.Confirm",
      "score": 0.000420796918
    }
  ],
  "entities": []
}
```

<span data-ttu-id="ae534-229">Because a name can be anything, LUIS predicts entities more accurately if it has a phrase list of words to boost the signal.</span><span class="sxs-lookup"><span data-stu-id="ae534-229">Because a name can be anything, LUIS predicts entities more accurately if it has a phrase list of words to boost the signal.</span></span>

## <a name="to-boost-signal-add-jobs-phrase-list"></a><span data-ttu-id="ae534-230">To boost signal, add jobs phrase list</span><span class="sxs-lookup"><span data-stu-id="ae534-230">To boost signal, add jobs phrase list</span></span>
<span data-ttu-id="ae534-231">Open the [jobs-phrase-list.csv](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/job-phrase-list.csv) from the LUIS-Samples Github repository.</span><span class="sxs-lookup"><span data-stu-id="ae534-231">Open the [jobs-phrase-list.csv](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/job-phrase-list.csv) from the LUIS-Samples Github repository.</span></span> <span data-ttu-id="ae534-232">The list is over one thousand job words and phrases.</span><span class="sxs-lookup"><span data-stu-id="ae534-232">The list is over one thousand job words and phrases.</span></span> <span data-ttu-id="ae534-233">Look through the list for job words that are meaningful to you.</span><span class="sxs-lookup"><span data-stu-id="ae534-233">Look through the list for job words that are meaningful to you.</span></span> <span data-ttu-id="ae534-234">If your words or phrases are not on the list, add your own.</span><span class="sxs-lookup"><span data-stu-id="ae534-234">If your words or phrases are not on the list, add your own.</span></span>

1. <span data-ttu-id="ae534-235">In the **Build** section of the LUIS app, select **Phrase lists** found under the **Improve app performance** menu.</span><span class="sxs-lookup"><span data-stu-id="ae534-235">In the **Build** section of the LUIS app, select **Phrase lists** found under the **Improve app performance** menu.</span></span>

    <span data-ttu-id="ae534-236">[![](media/luis-quickstart-primary-and-secondary-data/hr-select-phrase-list-left-nav.png "Screenshot of Phrase lists left nav button highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-select-phrase-list-left-nav.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-236">[![](media/luis-quickstart-primary-and-secondary-data/hr-select-phrase-list-left-nav.png "Screenshot of Phrase lists left nav button highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-select-phrase-list-left-nav.png#lightbox)</span></span>

2. <span data-ttu-id="ae534-237">Select **Create new phrase list**.</span><span class="sxs-lookup"><span data-stu-id="ae534-237">Select **Create new phrase list**.</span></span> 

    <span data-ttu-id="ae534-238">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-new-phrase-list.png "Screenshot of create new phrase list button highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-create-new-phrase-list.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-238">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-new-phrase-list.png "Screenshot of create new phrase list button highlighted")](media/luis-quickstart-primary-and-secondary-data/hr-create-new-phrase-list.png#lightbox)</span></span>

3. <span data-ttu-id="ae534-239">Name the new phrase list `Jobs` and copy the list from jobs-phrase-list.csv into the **Values** text box.</span><span class="sxs-lookup"><span data-stu-id="ae534-239">Name the new phrase list `Jobs` and copy the list from jobs-phrase-list.csv into the **Values** text box.</span></span> <span data-ttu-id="ae534-240">Select enter.</span><span class="sxs-lookup"><span data-stu-id="ae534-240">Select enter.</span></span> 

    <span data-ttu-id="ae534-241">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-1.png "Screenshot of create new phrase list dialog pop-up")](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-241">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-1.png "Screenshot of create new phrase list dialog pop-up")](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-1.png#lightbox)</span></span>

    <span data-ttu-id="ae534-242">If you want more words added to the phrase list, review the **Related Values** and add any that are relevant.</span><span class="sxs-lookup"><span data-stu-id="ae534-242">If you want more words added to the phrase list, review the **Related Values** and add any that are relevant.</span></span> 

4. <span data-ttu-id="ae534-243">Select **Save** to activate the phrase list.</span><span class="sxs-lookup"><span data-stu-id="ae534-243">Select **Save** to activate the phrase list.</span></span>

    <span data-ttu-id="ae534-244">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-2.png "Screenshot of create new phrase list dialog pop-up with words in phrase list values box")](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-2.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="ae534-244">[![](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-2.png "Screenshot of create new phrase list dialog pop-up with words in phrase list values box")](media/luis-quickstart-primary-and-secondary-data/hr-create-phrase-list-2.png#lightbox)</span></span>

5. <span data-ttu-id="ae534-245">[Train](#train-the-luis-app) and [publish](#publish-the-app-to-get-the-endpoint-URL) the app again to use phrase list.</span><span class="sxs-lookup"><span data-stu-id="ae534-245">[Train](#train-the-luis-app) and [publish](#publish-the-app-to-get-the-endpoint-URL) the app again to use phrase list.</span></span>

6. <span data-ttu-id="ae534-246">Requery at the endpoint with the same utterance: `This is the lead welder paperwork.`</span><span class="sxs-lookup"><span data-stu-id="ae534-246">Requery at the endpoint with the same utterance: `This is the lead welder paperwork.`</span></span>

    <span data-ttu-id="ae534-247">The JSON response includes the extracted entity:</span><span class="sxs-lookup"><span data-stu-id="ae534-247">The JSON response includes the extracted entity:</span></span>

    ```JSON
    {
        "query": "This is the lead welder paperwork.",
        "topScoringIntent": {
            "intent": "ApplyForJob",
            "score": 0.920025647
        },
        "intents": [
            {
            "intent": "ApplyForJob",
            "score": 0.920025647
            },
            {
            "intent": "GetJobInformation",
            "score": 0.003800706
            },
            {
            "intent": "Utilities.StartOver",
            "score": 0.00299335527
            },
            {
            "intent": "MoveEmployee",
            "score": 0.0027167045
            },
            {
            "intent": "None",
            "score": 0.00259556063
            },
            {
            "intent": "FindForm",
            "score": 0.00224019377
            },
            {
            "intent": "Utilities.Stop",
            "score": 0.00200693542
            },
            {
            "intent": "Utilities.Cancel",
            "score": 0.00195913855
            },
            {
            "intent": "Utilities.Help",
            "score": 0.00162656687
            },
            {
            "intent": "Utilities.Confirm",
            "score": 0.0002851904
            }
        ],
        "entities": [
            {
            "entity": "lead welder",
            "type": "Job",
            "startIndex": 12,
            "endIndex": 22,
            "score": 0.8295959
            }
        ]
    }
    ```

## <a name="phrase-lists"></a><span data-ttu-id="ae534-248">Phrase lists</span><span class="sxs-lookup"><span data-stu-id="ae534-248">Phrase lists</span></span>
<span data-ttu-id="ae534-249">Adding the phrase list boosted the signal of the words in the list but is **not** used as an exact match.</span><span class="sxs-lookup"><span data-stu-id="ae534-249">Adding the phrase list boosted the signal of the words in the list but is **not** used as an exact match.</span></span> <span data-ttu-id="ae534-250">The phrase list has several jobs with the first word of `lead` and also has the job `welder` but does not have the job `lead welder`.</span><span class="sxs-lookup"><span data-stu-id="ae534-250">The phrase list has several jobs with the first word of `lead` and also has the job `welder` but does not have the job `lead welder`.</span></span> <span data-ttu-id="ae534-251">This phrase list for jobs may not be complete.</span><span class="sxs-lookup"><span data-stu-id="ae534-251">This phrase list for jobs may not be complete.</span></span> <span data-ttu-id="ae534-252">As you regularly [review endpoint utterances](luis-how-to-review-endoint-utt.md) and find other job words, add those to your phrase list.</span><span class="sxs-lookup"><span data-stu-id="ae534-252">As you regularly [review endpoint utterances](luis-how-to-review-endoint-utt.md) and find other job words, add those to your phrase list.</span></span> <span data-ttu-id="ae534-253">Then retrain and republish.</span><span class="sxs-lookup"><span data-stu-id="ae534-253">Then retrain and republish.</span></span>

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="ae534-254">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="ae534-254">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="ae534-255">This app, with a simple entity and a phrase list of words, identified a natural language query intention and returned the job data.</span><span class="sxs-lookup"><span data-stu-id="ae534-255">This app, with a simple entity and a phrase list of words, identified a natural language query intention and returned the job data.</span></span> 

<span data-ttu-id="ae534-256">Your chatbot now has enough information to determine the primary action of applying for a job and a parameter of that action, which job is referenced.</span><span class="sxs-lookup"><span data-stu-id="ae534-256">Your chatbot now has enough information to determine the primary action of applying for a job and a parameter of that action, which job is referenced.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="ae534-257">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="ae534-257">Where is this LUIS data used?</span></span> 
<span data-ttu-id="ae534-258">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="ae534-258">LUIS is done with this request.</span></span> <span data-ttu-id="ae534-259">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to use a third-party API to send the job information to a Human Resources representative.</span><span class="sxs-lookup"><span data-stu-id="ae534-259">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to use a third-party API to send the job information to a Human Resources representative.</span></span> <span data-ttu-id="ae534-260">If there are other programmatic options for the bot or calling application, LUIS doesn't do that work.</span><span class="sxs-lookup"><span data-stu-id="ae534-260">If there are other programmatic options for the bot or calling application, LUIS doesn't do that work.</span></span> <span data-ttu-id="ae534-261">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="ae534-261">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="ae534-262">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ae534-262">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="ae534-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae534-263">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae534-264">Add a prebuilt keyphrase entity</span><span class="sxs-lookup"><span data-stu-id="ae534-264">Add a prebuilt keyphrase entity</span></span>](luis-quickstart-intent-and-key-phrase.md)