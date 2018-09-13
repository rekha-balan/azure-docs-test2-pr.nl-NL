---
title: Tutorial create a LUIS app to get exact text match listed data - Azure | Microsoft Docs
description: In this tutorial, learn how to create a simple LUIS app using intents and list entities to extract data in this quickstart.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: tutorial
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 04411f415b7cfe07d893c43e758bd2a4a226472a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868629"
---
# <a name="tutorial-4-add-list-entity"></a><span data-ttu-id="97e14-103">Tutorial: 4.</span><span class="sxs-lookup"><span data-stu-id="97e14-103">Tutorial: 4.</span></span> <span data-ttu-id="97e14-104">Add list entity</span><span class="sxs-lookup"><span data-stu-id="97e14-104">Add list entity</span></span>
<span data-ttu-id="97e14-105">In this tutorial, create an app that demonstrates how to get data that matches a predefined list.</span><span class="sxs-lookup"><span data-stu-id="97e14-105">In this tutorial, create an app that demonstrates how to get data that matches a predefined list.</span></span> 

<!-- green checkmark -->
> [!div class="checklist"]
> * <span data-ttu-id="97e14-106">Understand list entities</span><span class="sxs-lookup"><span data-stu-id="97e14-106">Understand list entities</span></span> 
> * <span data-ttu-id="97e14-107">Create new LUIS app for the Human Resources (HR) domain with MoveEmployee intent</span><span class="sxs-lookup"><span data-stu-id="97e14-107">Create new LUIS app for the Human Resources (HR) domain with MoveEmployee intent</span></span>
> * <span data-ttu-id="97e14-108">Add list entity to extract Employee from utterance</span><span class="sxs-lookup"><span data-stu-id="97e14-108">Add list entity to extract Employee from utterance</span></span>
> * <span data-ttu-id="97e14-109">Train, and publish app</span><span class="sxs-lookup"><span data-stu-id="97e14-109">Train, and publish app</span></span>
> * <span data-ttu-id="97e14-110">Query endpoint of app to see LUIS JSON response</span><span class="sxs-lookup"><span data-stu-id="97e14-110">Query endpoint of app to see LUIS JSON response</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="97e14-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="97e14-111">Before you begin</span></span>
<span data-ttu-id="97e14-112">If you don't have the Human Resources app from the [regex entity](luis-quickstart-intents-regex-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="97e14-112">If you don't have the Human Resources app from the [regex entity](luis-quickstart-intents-regex-entity.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="97e14-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-regex-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="97e14-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-regex-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="97e14-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `list`.</span><span class="sxs-lookup"><span data-stu-id="97e14-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `list`.</span></span> <span data-ttu-id="97e14-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="97e14-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

## <a name="purpose-of-the-list-entity"></a><span data-ttu-id="97e14-116">Purpose of the list entity</span><span class="sxs-lookup"><span data-stu-id="97e14-116">Purpose of the list entity</span></span>
<span data-ttu-id="97e14-117">This app predicts utterances about moving an employee from one building to a different building.</span><span class="sxs-lookup"><span data-stu-id="97e14-117">This app predicts utterances about moving an employee from one building to a different building.</span></span> <span data-ttu-id="97e14-118">This app uses a list entity to extract an employee.</span><span class="sxs-lookup"><span data-stu-id="97e14-118">This app uses a list entity to extract an employee.</span></span> <span data-ttu-id="97e14-119">The employee can be referred to using name, phone number, email, or U.S. federal social security number.</span><span class="sxs-lookup"><span data-stu-id="97e14-119">The employee can be referred to using name, phone number, email, or U.S. federal social security number.</span></span> 

<span data-ttu-id="97e14-120">A list entity can hold many items with synonyms for each item.</span><span class="sxs-lookup"><span data-stu-id="97e14-120">A list entity can hold many items with synonyms for each item.</span></span> <span data-ttu-id="97e14-121">For a small to medium size company, the list entity is used to extract the employee information.</span><span class="sxs-lookup"><span data-stu-id="97e14-121">For a small to medium size company, the list entity is used to extract the employee information.</span></span> 

<span data-ttu-id="97e14-122">The canonical name for each item is the employee number.</span><span class="sxs-lookup"><span data-stu-id="97e14-122">The canonical name for each item is the employee number.</span></span> <span data-ttu-id="97e14-123">For this domain, examples of the synonyms are:</span><span class="sxs-lookup"><span data-stu-id="97e14-123">For this domain, examples of the synonyms are:</span></span> 

|<span data-ttu-id="97e14-124">Synonym purpose</span><span class="sxs-lookup"><span data-stu-id="97e14-124">Synonym purpose</span></span>|<span data-ttu-id="97e14-125">Synonym value</span><span class="sxs-lookup"><span data-stu-id="97e14-125">Synonym value</span></span>|
|--|--|
|<span data-ttu-id="97e14-126">Name</span><span class="sxs-lookup"><span data-stu-id="97e14-126">Name</span></span>|<span data-ttu-id="97e14-127">John W. Smith</span><span class="sxs-lookup"><span data-stu-id="97e14-127">John W. Smith</span></span>|
|<span data-ttu-id="97e14-128">Email address</span><span class="sxs-lookup"><span data-stu-id="97e14-128">Email address</span></span>|john.w.smith@mycompany.com|
|<span data-ttu-id="97e14-129">Phone extension</span><span class="sxs-lookup"><span data-stu-id="97e14-129">Phone extension</span></span>|<span data-ttu-id="97e14-130">x12345</span><span class="sxs-lookup"><span data-stu-id="97e14-130">x12345</span></span>|
|<span data-ttu-id="97e14-131">Personal mobile phone number</span><span class="sxs-lookup"><span data-stu-id="97e14-131">Personal mobile phone number</span></span>|<span data-ttu-id="97e14-132">425-555-1212</span><span class="sxs-lookup"><span data-stu-id="97e14-132">425-555-1212</span></span>|
|<span data-ttu-id="97e14-133">U.S. federal social security number</span><span class="sxs-lookup"><span data-stu-id="97e14-133">U.S. federal social security number</span></span>|<span data-ttu-id="97e14-134">123-45-6789</span><span class="sxs-lookup"><span data-stu-id="97e14-134">123-45-6789</span></span>|

<span data-ttu-id="97e14-135">A list entity is a good choice for this type of data when:</span><span class="sxs-lookup"><span data-stu-id="97e14-135">A list entity is a good choice for this type of data when:</span></span>

* <span data-ttu-id="97e14-136">The data values are a known set.</span><span class="sxs-lookup"><span data-stu-id="97e14-136">The data values are a known set.</span></span>
* <span data-ttu-id="97e14-137">The set doesn't exceed the maximum LUIS [boundaries](luis-boundaries.md) for this entity type.</span><span class="sxs-lookup"><span data-stu-id="97e14-137">The set doesn't exceed the maximum LUIS [boundaries](luis-boundaries.md) for this entity type.</span></span>
* <span data-ttu-id="97e14-138">The text in the utterance is an exact match with a synonym.</span><span class="sxs-lookup"><span data-stu-id="97e14-138">The text in the utterance is an exact match with a synonym.</span></span> 

<span data-ttu-id="97e14-139">LUIS extracts the employee in such as way that a standard order to move the employee can be created by the client application.</span><span class="sxs-lookup"><span data-stu-id="97e14-139">LUIS extracts the employee in such as way that a standard order to move the employee can be created by the client application.</span></span>
<!--
## Example utterances
Simple example utterances for a `MoveEmployee` inent:

```
move John W. Smith from B-1234 to H-4452
mv john.w.smith@mycompany from office b-1234 to office h-4452

```
-->

## <a name="add-moveemployee-intent"></a><span data-ttu-id="97e14-140">Add MoveEmployee intent</span><span class="sxs-lookup"><span data-stu-id="97e14-140">Add MoveEmployee intent</span></span>

1. <span data-ttu-id="97e14-141">Make sure your Human Resources app is in the **Build** section of LUIS.</span><span class="sxs-lookup"><span data-stu-id="97e14-141">Make sure your Human Resources app is in the **Build** section of LUIS.</span></span> <span data-ttu-id="97e14-142">You can change to this section by selecting **Build** on the top, right menu bar.</span><span class="sxs-lookup"><span data-stu-id="97e14-142">You can change to this section by selecting **Build** on the top, right menu bar.</span></span> 

2. <span data-ttu-id="97e14-143">Select **Create new intent**.</span><span class="sxs-lookup"><span data-stu-id="97e14-143">Select **Create new intent**.</span></span> 

3. <span data-ttu-id="97e14-144">Enter `MoveEmployee` in the pop-up dialog box then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="97e14-144">Enter `MoveEmployee` in the pop-up dialog box then select **Done**.</span></span> 

    ![Screenshot of create new intent dialog with](./media/luis-quickstart-intent-and-list-entity/hr-create-new-intent-ddl.png)

4. <span data-ttu-id="97e14-146">Add example utterances to the intent.</span><span class="sxs-lookup"><span data-stu-id="97e14-146">Add example utterances to the intent.</span></span>

    |<span data-ttu-id="97e14-147">Example utterances</span><span class="sxs-lookup"><span data-stu-id="97e14-147">Example utterances</span></span>|
    |--|
    |<span data-ttu-id="97e14-148">move John W. Smith from B-1234 to H-4452</span><span class="sxs-lookup"><span data-stu-id="97e14-148">move John W. Smith from B-1234 to H-4452</span></span>|
    |<span data-ttu-id="97e14-149">mv john.w.smith@mycompany.com from office b-1234 to office h-4452</span><span class="sxs-lookup"><span data-stu-id="97e14-149">mv john.w.smith@mycompany.com from office b-1234 to office h-4452</span></span>|
    |<span data-ttu-id="97e14-150">shift x12345 to h-1234 tomorrow</span><span class="sxs-lookup"><span data-stu-id="97e14-150">shift x12345 to h-1234 tomorrow</span></span>|
    |<span data-ttu-id="97e14-151">place 425-555-1212 in HH-2345</span><span class="sxs-lookup"><span data-stu-id="97e14-151">place 425-555-1212 in HH-2345</span></span>|
    |<span data-ttu-id="97e14-152">move 123-45-6789 from A-4321 to J-23456</span><span class="sxs-lookup"><span data-stu-id="97e14-152">move 123-45-6789 from A-4321 to J-23456</span></span>|
    |<span data-ttu-id="97e14-153">mv Jill Jones from D-2345 to J-23456</span><span class="sxs-lookup"><span data-stu-id="97e14-153">mv Jill Jones from D-2345 to J-23456</span></span>|
    |<span data-ttu-id="97e14-154">shift jill-jones@mycompany.com to M-12345</span><span class="sxs-lookup"><span data-stu-id="97e14-154">shift jill-jones@mycompany.com to M-12345</span></span>|
    |<span data-ttu-id="97e14-155">x23456 to M-12345</span><span class="sxs-lookup"><span data-stu-id="97e14-155">x23456 to M-12345</span></span>|
    |<span data-ttu-id="97e14-156">425-555-0000 to h-4452</span><span class="sxs-lookup"><span data-stu-id="97e14-156">425-555-0000 to h-4452</span></span>|
    |<span data-ttu-id="97e14-157">234-56-7891 to hh-2345</span><span class="sxs-lookup"><span data-stu-id="97e14-157">234-56-7891 to hh-2345</span></span>|

    <span data-ttu-id="97e14-158">[ ![Screenshot of Intent page with new utterances highlighted](./media/luis-quickstart-intent-and-list-entity/hr-enter-utterances.png) ](./media/luis-quickstart-intent-and-list-entity/hr-enter-utterances.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="97e14-158">[ ![Screenshot of Intent page with new utterances highlighted](./media/luis-quickstart-intent-and-list-entity/hr-enter-utterances.png) ](./media/luis-quickstart-intent-and-list-entity/hr-enter-utterances.png#lightbox)</span></span>

## <a name="create-an-employee-list-entity"></a><span data-ttu-id="97e14-159">Create an employee list entity</span><span class="sxs-lookup"><span data-stu-id="97e14-159">Create an employee list entity</span></span>
<span data-ttu-id="97e14-160">Now that the **MoveEmployee** intent has utterances, LUIS needs to understand what an employee is.</span><span class="sxs-lookup"><span data-stu-id="97e14-160">Now that the **MoveEmployee** intent has utterances, LUIS needs to understand what an employee is.</span></span> 

1. <span data-ttu-id="97e14-161">Select **Entities** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="97e14-161">Select **Entities** in the left panel.</span></span>

2. <span data-ttu-id="97e14-162">Select **Create new entity**.</span><span class="sxs-lookup"><span data-stu-id="97e14-162">Select **Create new entity**.</span></span>

3. <span data-ttu-id="97e14-163">In the entity pop-up dialog, enter `Employee` for the entity name, and  **List** for entity type.</span><span class="sxs-lookup"><span data-stu-id="97e14-163">In the entity pop-up dialog, enter `Employee` for the entity name, and  **List** for entity type.</span></span> <span data-ttu-id="97e14-164">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="97e14-164">Select **Done**.</span></span>  

    <span data-ttu-id="97e14-165">[![](media/luis-quickstart-intent-and-list-entity/hr-list-entity-ddl.png "Screenshot of creating new entity pop-up dialog")](media/luis-quickstart-intent-and-list-entity/hr-list-entity-ddl.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="97e14-165">[![](media/luis-quickstart-intent-and-list-entity/hr-list-entity-ddl.png "Screenshot of creating new entity pop-up dialog")](media/luis-quickstart-intent-and-list-entity/hr-list-entity-ddl.png#lightbox)</span></span>

4. <span data-ttu-id="97e14-166">On the Employee entity page, enter `Employee-24612` as the new value.</span><span class="sxs-lookup"><span data-stu-id="97e14-166">On the Employee entity page, enter `Employee-24612` as the new value.</span></span>

    <span data-ttu-id="97e14-167">[![](media/luis-quickstart-intent-and-list-entity/hr-emp1-value.png "Screenshot of entering value")](media/luis-quickstart-intent-and-list-entity/hr-emp1-value.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="97e14-167">[![](media/luis-quickstart-intent-and-list-entity/hr-emp1-value.png "Screenshot of entering value")](media/luis-quickstart-intent-and-list-entity/hr-emp1-value.png#lightbox)</span></span>

5. <span data-ttu-id="97e14-168">For Synonyms, add the following values:</span><span class="sxs-lookup"><span data-stu-id="97e14-168">For Synonyms, add the following values:</span></span>

    |<span data-ttu-id="97e14-169">Synonym purpose</span><span class="sxs-lookup"><span data-stu-id="97e14-169">Synonym purpose</span></span>|<span data-ttu-id="97e14-170">Synonym value</span><span class="sxs-lookup"><span data-stu-id="97e14-170">Synonym value</span></span>|
    |--|--|
    |<span data-ttu-id="97e14-171">Name</span><span class="sxs-lookup"><span data-stu-id="97e14-171">Name</span></span>|<span data-ttu-id="97e14-172">John W. Smith</span><span class="sxs-lookup"><span data-stu-id="97e14-172">John W. Smith</span></span>|
    |<span data-ttu-id="97e14-173">Email address</span><span class="sxs-lookup"><span data-stu-id="97e14-173">Email address</span></span>|john.w.smith@mycompany.com|
    |<span data-ttu-id="97e14-174">Phone extension</span><span class="sxs-lookup"><span data-stu-id="97e14-174">Phone extension</span></span>|<span data-ttu-id="97e14-175">x12345</span><span class="sxs-lookup"><span data-stu-id="97e14-175">x12345</span></span>|
    |<span data-ttu-id="97e14-176">Personal mobile phone number</span><span class="sxs-lookup"><span data-stu-id="97e14-176">Personal mobile phone number</span></span>|<span data-ttu-id="97e14-177">425-555-1212</span><span class="sxs-lookup"><span data-stu-id="97e14-177">425-555-1212</span></span>|
    |<span data-ttu-id="97e14-178">U.S. federal social security number</span><span class="sxs-lookup"><span data-stu-id="97e14-178">U.S. federal social security number</span></span>|<span data-ttu-id="97e14-179">123-45-6789</span><span class="sxs-lookup"><span data-stu-id="97e14-179">123-45-6789</span></span>|

    <span data-ttu-id="97e14-180">[![](media/luis-quickstart-intent-and-list-entity/hr-emp1-synonyms.png "Screenshot of entering synonyms")](media/luis-quickstart-intent-and-list-entity/hr-emp1-synonyms.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="97e14-180">[![](media/luis-quickstart-intent-and-list-entity/hr-emp1-synonyms.png "Screenshot of entering synonyms")](media/luis-quickstart-intent-and-list-entity/hr-emp1-synonyms.png#lightbox)</span></span>

6. <span data-ttu-id="97e14-181">Enter the `Employee-45612` as a new value.</span><span class="sxs-lookup"><span data-stu-id="97e14-181">Enter the `Employee-45612` as a new value.</span></span>

7. <span data-ttu-id="97e14-182">For Synonyms, add the following values:</span><span class="sxs-lookup"><span data-stu-id="97e14-182">For Synonyms, add the following values:</span></span>

    |<span data-ttu-id="97e14-183">Synonym purpose</span><span class="sxs-lookup"><span data-stu-id="97e14-183">Synonym purpose</span></span>|<span data-ttu-id="97e14-184">Synonym value</span><span class="sxs-lookup"><span data-stu-id="97e14-184">Synonym value</span></span>|
    |--|--|
    |<span data-ttu-id="97e14-185">Name</span><span class="sxs-lookup"><span data-stu-id="97e14-185">Name</span></span>|<span data-ttu-id="97e14-186">Jill Jones</span><span class="sxs-lookup"><span data-stu-id="97e14-186">Jill Jones</span></span>|
    |<span data-ttu-id="97e14-187">Email address</span><span class="sxs-lookup"><span data-stu-id="97e14-187">Email address</span></span>|jill-jones@mycompany.com|
    |<span data-ttu-id="97e14-188">Phone extension</span><span class="sxs-lookup"><span data-stu-id="97e14-188">Phone extension</span></span>|<span data-ttu-id="97e14-189">x23456</span><span class="sxs-lookup"><span data-stu-id="97e14-189">x23456</span></span>|
    |<span data-ttu-id="97e14-190">Personal mobile phone number</span><span class="sxs-lookup"><span data-stu-id="97e14-190">Personal mobile phone number</span></span>|<span data-ttu-id="97e14-191">425-555-0000</span><span class="sxs-lookup"><span data-stu-id="97e14-191">425-555-0000</span></span>|
    |<span data-ttu-id="97e14-192">U.S. federal social security number</span><span class="sxs-lookup"><span data-stu-id="97e14-192">U.S. federal social security number</span></span>|<span data-ttu-id="97e14-193">234-56-7891</span><span class="sxs-lookup"><span data-stu-id="97e14-193">234-56-7891</span></span>|

## <a name="train-the-luis-app"></a><span data-ttu-id="97e14-194">Train the LUIS app</span><span class="sxs-lookup"><span data-stu-id="97e14-194">Train the LUIS app</span></span>

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a><span data-ttu-id="97e14-195">Publish the app to get the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="97e14-195">Publish the app to get the endpoint URL</span></span>

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-with-a-different-utterance"></a><span data-ttu-id="97e14-196">Query the endpoint with a different utterance</span><span class="sxs-lookup"><span data-stu-id="97e14-196">Query the endpoint with a different utterance</span></span>

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)] 

2. <span data-ttu-id="97e14-197">Go to the end of the URL in the address and enter `shift 123-45-6789 from Z-1242 to T-54672`.</span><span class="sxs-lookup"><span data-stu-id="97e14-197">Go to the end of the URL in the address and enter `shift 123-45-6789 from Z-1242 to T-54672`.</span></span> <span data-ttu-id="97e14-198">The last querystring parameter is `q`, the utterance **q**uery.</span><span class="sxs-lookup"><span data-stu-id="97e14-198">The last querystring parameter is `q`, the utterance **q**uery.</span></span> <span data-ttu-id="97e14-199">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `MoveEmployee` intent with `Employee` extracted.</span><span class="sxs-lookup"><span data-stu-id="97e14-199">This utterance is not the same as any of the labeled utterances so it is a good test and should return the `MoveEmployee` intent with `Employee` extracted.</span></span>

  ```JSON
  {
    "query": "shift 123-45-6789 from Z-1242 to T-54672",
    "topScoringIntent": {
      "intent": "MoveEmployee",
      "score": 0.9882801
    },
    "intents": [
      {
        "intent": "MoveEmployee",
        "score": 0.9882801
      },
      {
        "intent": "FindForm",
        "score": 0.016044287
      },
      {
        "intent": "GetJobInformation",
        "score": 0.007611245
      },
      {
        "intent": "ApplyForJob",
        "score": 0.007063288
      },
      {
        "intent": "Utilities.StartOver",
        "score": 0.00684710965
      },
      {
        "intent": "None",
        "score": 0.00304174074
      },
      {
        "intent": "Utilities.Help",
        "score": 0.002981
      },
      {
        "intent": "Utilities.Confirm",
        "score": 0.00212222221
      },
      {
        "intent": "Utilities.Cancel",
        "score": 0.00191026414
      },
      {
        "intent": "Utilities.Stop",
        "score": 0.0007461446
      }
    ],
    "entities": [
      {
        "entity": "123 - 45 - 6789",
        "type": "Employee",
        "startIndex": 6,
        "endIndex": 16,
        "resolution": {
          "values": [
            "Employee-24612"
          ]
        }
      },
      {
        "entity": "123",
        "type": "builtin.number",
        "startIndex": 6,
        "endIndex": 8,
        "resolution": {
          "value": "123"
        }
      },
      {
        "entity": "45",
        "type": "builtin.number",
        "startIndex": 10,
        "endIndex": 11,
        "resolution": {
          "value": "45"
        }
      },
      {
        "entity": "6789",
        "type": "builtin.number",
        "startIndex": 13,
        "endIndex": 16,
        "resolution": {
          "value": "6789"
        }
      },
      {
        "entity": "-1242",
        "type": "builtin.number",
        "startIndex": 24,
        "endIndex": 28,
        "resolution": {
          "value": "-1242"
        }
      },
      {
        "entity": "-54672",
        "type": "builtin.number",
        "startIndex": 34,
        "endIndex": 39,
        "resolution": {
          "value": "-54672"
        }
      }
    ]
  }
  ```

  <span data-ttu-id="97e14-200">The employee was found and returned as type `Employee` with a resolution value of `Employee-24612`.</span><span class="sxs-lookup"><span data-stu-id="97e14-200">The employee was found and returned as type `Employee` with a resolution value of `Employee-24612`.</span></span>

## <a name="where-is-the-natural-language-processing-in-the-list-entity"></a><span data-ttu-id="97e14-201">Where is the natural language processing in the List entity?</span><span class="sxs-lookup"><span data-stu-id="97e14-201">Where is the natural language processing in the List entity?</span></span> 
<span data-ttu-id="97e14-202">Because the list entity is an exact text match, it doesn't rely on natural language processing (or machine-learning).</span><span class="sxs-lookup"><span data-stu-id="97e14-202">Because the list entity is an exact text match, it doesn't rely on natural language processing (or machine-learning).</span></span> <span data-ttu-id="97e14-203">LUIS does use natural language processing (or machine-learning) to select the correct top-scoring intent.</span><span class="sxs-lookup"><span data-stu-id="97e14-203">LUIS does use natural language processing (or machine-learning) to select the correct top-scoring intent.</span></span> <span data-ttu-id="97e14-204">Additionally, an utterance can be a mix of more than one entity or even more than one type of entity.</span><span class="sxs-lookup"><span data-stu-id="97e14-204">Additionally, an utterance can be a mix of more than one entity or even more than one type of entity.</span></span> <span data-ttu-id="97e14-205">Each utterance is processed for all the entities in the app, including natural language processing (or machine-learned) entities.</span><span class="sxs-lookup"><span data-stu-id="97e14-205">Each utterance is processed for all the entities in the app, including natural language processing (or machine-learned) entities.</span></span>

## <a name="what-has-this-luis-app-accomplished"></a><span data-ttu-id="97e14-206">What has this LUIS app accomplished?</span><span class="sxs-lookup"><span data-stu-id="97e14-206">What has this LUIS app accomplished?</span></span>
<span data-ttu-id="97e14-207">This app, with a list entity, extracted the correct employee.</span><span class="sxs-lookup"><span data-stu-id="97e14-207">This app, with a list entity, extracted the correct employee.</span></span> 

<span data-ttu-id="97e14-208">Your chatbot now has enough information to determine the primary action, `MoveEmployee`, and which employee to move.</span><span class="sxs-lookup"><span data-stu-id="97e14-208">Your chatbot now has enough information to determine the primary action, `MoveEmployee`, and which employee to move.</span></span> 

## <a name="where-is-this-luis-data-used"></a><span data-ttu-id="97e14-209">Where is this LUIS data used?</span><span class="sxs-lookup"><span data-stu-id="97e14-209">Where is this LUIS data used?</span></span> 
<span data-ttu-id="97e14-210">LUIS is done with this request.</span><span class="sxs-lookup"><span data-stu-id="97e14-210">LUIS is done with this request.</span></span> <span data-ttu-id="97e14-211">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span><span class="sxs-lookup"><span data-stu-id="97e14-211">The calling application, such as a chatbot, can take the topScoringIntent result and the data from the entity to take the next step.</span></span> <span data-ttu-id="97e14-212">LUIS doesn't do that programmatic work for the bot or calling application.</span><span class="sxs-lookup"><span data-stu-id="97e14-212">LUIS doesn't do that programmatic work for the bot or calling application.</span></span> <span data-ttu-id="97e14-213">LUIS only determines what the user's intention is.</span><span class="sxs-lookup"><span data-stu-id="97e14-213">LUIS only determines what the user's intention is.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="97e14-214">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="97e14-214">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="97e14-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="97e14-215">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97e14-216">Add a hierarchical entity to the app</span><span class="sxs-lookup"><span data-stu-id="97e14-216">Add a hierarchical entity to the app</span></span>](luis-quickstart-intent-and-hier-entity.md)

