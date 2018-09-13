---
title: Learn how Patterns increase prediction accuracy | Microsoft Docs
titleSuffix: Azure
description: Learn how to design patterns to increase intent prediction scores and find entities.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 06/08/2018
ms.author: diberry
ms.openlocfilehash: c08419e3fb5b25284121a0eac30c38c8ba7570f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864511"
---
# <a name="patterns-improve-prediction-accuracy"></a><span data-ttu-id="e2195-103">Patterns improve prediction accuracy</span><span class="sxs-lookup"><span data-stu-id="e2195-103">Patterns improve prediction accuracy</span></span>
<span data-ttu-id="e2195-104">Patterns are designed to improve accuracy when several utterances are very similar.</span><span class="sxs-lookup"><span data-stu-id="e2195-104">Patterns are designed to improve accuracy when several utterances are very similar.</span></span> <span data-ttu-id="e2195-105">By providing a pattern for the utterance, LUIS can have a high confidence in the prediction.</span><span class="sxs-lookup"><span data-stu-id="e2195-105">By providing a pattern for the utterance, LUIS can have a high confidence in the prediction.</span></span> 

## <a name="patterns-solve-low-intent-confidence"></a><span data-ttu-id="e2195-106">Patterns solve low intent confidence</span><span class="sxs-lookup"><span data-stu-id="e2195-106">Patterns solve low intent confidence</span></span>
<span data-ttu-id="e2195-107">Consider a Human Resources app that reports on the organizational chart in relation to an employee.</span><span class="sxs-lookup"><span data-stu-id="e2195-107">Consider a Human Resources app that reports on the organizational chart in relation to an employee.</span></span> <span data-ttu-id="e2195-108">Given an employee's name and relationship, LUIS returns the employees involved.</span><span class="sxs-lookup"><span data-stu-id="e2195-108">Given an employee's name and relationship, LUIS returns the employees involved.</span></span> <span data-ttu-id="e2195-109">Consider an employee, Tom, with a manager name Alice, and a team of subordinates named: Michael, Rebecca, and Carl.</span><span class="sxs-lookup"><span data-stu-id="e2195-109">Consider an employee, Tom, with a manager name Alice, and a team of subordinates named: Michael, Rebecca, and Carl.</span></span>

![Image of Organization chart](./media/luis-concept-patterns/org-chart.png)

|<span data-ttu-id="e2195-111">Utterances</span><span class="sxs-lookup"><span data-stu-id="e2195-111">Utterances</span></span>|<span data-ttu-id="e2195-112">Intent predicted</span><span class="sxs-lookup"><span data-stu-id="e2195-112">Intent predicted</span></span>|<span data-ttu-id="e2195-113">Intent score</span><span class="sxs-lookup"><span data-stu-id="e2195-113">Intent score</span></span>|
|--|--|--|
|<span data-ttu-id="e2195-114">Who is Tom's subordinate?</span><span class="sxs-lookup"><span data-stu-id="e2195-114">Who is Tom's subordinate?</span></span>|<span data-ttu-id="e2195-115">GetOrgChart</span><span class="sxs-lookup"><span data-stu-id="e2195-115">GetOrgChart</span></span>|<span data-ttu-id="e2195-116">.30</span><span class="sxs-lookup"><span data-stu-id="e2195-116">.30</span></span>|
|<span data-ttu-id="e2195-117">Who is the subordinate of Tom?</span><span class="sxs-lookup"><span data-stu-id="e2195-117">Who is the subordinate of Tom?</span></span>|<span data-ttu-id="e2195-118">GetOrgChart</span><span class="sxs-lookup"><span data-stu-id="e2195-118">GetOrgChart</span></span>|<span data-ttu-id="e2195-119">.30</span><span class="sxs-lookup"><span data-stu-id="e2195-119">.30</span></span>|

<span data-ttu-id="e2195-120">If an app has between 10 and 20 utterances with different lengths of sentence, different word order, and even different words (synonyms of "subordinate", "manage", "report"), LUIS may return a low confidence score.</span><span class="sxs-lookup"><span data-stu-id="e2195-120">If an app has between 10 and 20 utterances with different lengths of sentence, different word order, and even different words (synonyms of "subordinate", "manage", "report"), LUIS may return a low confidence score.</span></span> <span data-ttu-id="e2195-121">In order to help LUIS understand the importance of the word order, create a pattern.</span><span class="sxs-lookup"><span data-stu-id="e2195-121">In order to help LUIS understand the importance of the word order, create a pattern.</span></span> 

<span data-ttu-id="e2195-122">Patterns solve the following situations:</span><span class="sxs-lookup"><span data-stu-id="e2195-122">Patterns solve the following situations:</span></span> 

* <span data-ttu-id="e2195-123">When the intent score is low</span><span class="sxs-lookup"><span data-stu-id="e2195-123">When the intent score is low</span></span>
* <span data-ttu-id="e2195-124">When the correct intent is not the top score but too close to the top score.</span><span class="sxs-lookup"><span data-stu-id="e2195-124">When the correct intent is not the top score but too close to the top score.</span></span> 

## <a name="patterns-are-not-a-guarantee-of-intent"></a><span data-ttu-id="e2195-125">Patterns are not a guarantee of intent</span><span class="sxs-lookup"><span data-stu-id="e2195-125">Patterns are not a guarantee of intent</span></span>
<span data-ttu-id="e2195-126">Patterns use a mix of prediction technologies.</span><span class="sxs-lookup"><span data-stu-id="e2195-126">Patterns use a mix of prediction technologies.</span></span> <span data-ttu-id="e2195-127">Setting an intent for a template utterance in a pattern is not a guarantee of the intent prediction but it is a strong signal.</span><span class="sxs-lookup"><span data-stu-id="e2195-127">Setting an intent for a template utterance in a pattern is not a guarantee of the intent prediction but it is a strong signal.</span></span> 

## <a name="patterns-do-not-improve-entity-detection"></a><span data-ttu-id="e2195-128">Patterns do not improve entity detection</span><span class="sxs-lookup"><span data-stu-id="e2195-128">Patterns do not improve entity detection</span></span>
<span data-ttu-id="e2195-129">While patterns require entities, a pattern does not help detect the entity.</span><span class="sxs-lookup"><span data-stu-id="e2195-129">While patterns require entities, a pattern does not help detect the entity.</span></span> <span data-ttu-id="e2195-130">A pattern is only meant to help the prediction with intents and roles.</span><span class="sxs-lookup"><span data-stu-id="e2195-130">A pattern is only meant to help the prediction with intents and roles.</span></span>  

## <a name="patterns-use-entity-roles"></a><span data-ttu-id="e2195-131">Patterns use entity roles</span><span class="sxs-lookup"><span data-stu-id="e2195-131">Patterns use entity roles</span></span>
<span data-ttu-id="e2195-132">If two or more entities in a pattern are contextually related, patterns use entity [roles](luis-concept-roles.md) to extract contextual information about entities.</span><span class="sxs-lookup"><span data-stu-id="e2195-132">If two or more entities in a pattern are contextually related, patterns use entity [roles](luis-concept-roles.md) to extract contextual information about entities.</span></span> <span data-ttu-id="e2195-133">This is equivalent to hierarchical entity children, but is **only** available in patterns.</span><span class="sxs-lookup"><span data-stu-id="e2195-133">This is equivalent to hierarchical entity children, but is **only** available in patterns.</span></span> 

## <a name="prediction-scores-with-and-without-patterns"></a><span data-ttu-id="e2195-134">Prediction scores with and without patterns</span><span class="sxs-lookup"><span data-stu-id="e2195-134">Prediction scores with and without patterns</span></span>
<span data-ttu-id="e2195-135">Given enough example utterances, LUIS would be able to increase prediction confidence without patterns.</span><span class="sxs-lookup"><span data-stu-id="e2195-135">Given enough example utterances, LUIS would be able to increase prediction confidence without patterns.</span></span> <span data-ttu-id="e2195-136">Patterns increase the confidence score without having to provide as many utterances.</span><span class="sxs-lookup"><span data-stu-id="e2195-136">Patterns increase the confidence score without having to provide as many utterances.</span></span>  

## <a name="pattern-matching"></a><span data-ttu-id="e2195-137">Pattern matching</span><span class="sxs-lookup"><span data-stu-id="e2195-137">Pattern matching</span></span>
<span data-ttu-id="e2195-138">A pattern is matched based on detecting the entities inside the pattern first, then validating the rest of the words and word order of the pattern.</span><span class="sxs-lookup"><span data-stu-id="e2195-138">A pattern is matched based on detecting the entities inside the pattern first, then validating the rest of the words and word order of the pattern.</span></span> <span data-ttu-id="e2195-139">Entities are required in the pattern for a pattern to match.</span><span class="sxs-lookup"><span data-stu-id="e2195-139">Entities are required in the pattern for a pattern to match.</span></span> 

## <a name="pattern-syntax"></a><span data-ttu-id="e2195-140">Pattern syntax</span><span class="sxs-lookup"><span data-stu-id="e2195-140">Pattern syntax</span></span>
<span data-ttu-id="e2195-141">Pattern syntax is a template for an utterance.</span><span class="sxs-lookup"><span data-stu-id="e2195-141">Pattern syntax is a template for an utterance.</span></span> <span data-ttu-id="e2195-142">The template should contain words and entities you want to match as well as words and punctuation you want to ignore.</span><span class="sxs-lookup"><span data-stu-id="e2195-142">The template should contain words and entities you want to match as well as words and punctuation you want to ignore.</span></span> <span data-ttu-id="e2195-143">It is **not** a regular expression.</span><span class="sxs-lookup"><span data-stu-id="e2195-143">It is **not** a regular expression.</span></span> 

<span data-ttu-id="e2195-144">Entities in patterns are surrounded by curly brackets, `{}`.</span><span class="sxs-lookup"><span data-stu-id="e2195-144">Entities in patterns are surrounded by curly brackets, `{}`.</span></span> <span data-ttu-id="e2195-145">Patterns can include entities, and entities with roles.</span><span class="sxs-lookup"><span data-stu-id="e2195-145">Patterns can include entities, and entities with roles.</span></span> <span data-ttu-id="e2195-146">Pattern.any is an entity only used in patterns.</span><span class="sxs-lookup"><span data-stu-id="e2195-146">Pattern.any is an entity only used in patterns.</span></span> <span data-ttu-id="e2195-147">The syntax is explained in the following sections.</span><span class="sxs-lookup"><span data-stu-id="e2195-147">The syntax is explained in the following sections.</span></span>

### <a name="syntax-to-add-an-entity-to-a-pattern-template"></a><span data-ttu-id="e2195-148">Syntax to add an entity to a pattern template</span><span class="sxs-lookup"><span data-stu-id="e2195-148">Syntax to add an entity to a pattern template</span></span>
<span data-ttu-id="e2195-149">To add an entity into the pattern template, surround the entity name with curly braces, such as `Who does {Employee} manage?`.</span><span class="sxs-lookup"><span data-stu-id="e2195-149">To add an entity into the pattern template, surround the entity name with curly braces, such as `Who does {Employee} manage?`.</span></span> 

```
Who does {Employee} manage?
```

### <a name="syntax-to-add-an-entity-and-role-to-a-pattern-template"></a><span data-ttu-id="e2195-150">Syntax to add an entity and role to a pattern template</span><span class="sxs-lookup"><span data-stu-id="e2195-150">Syntax to add an entity and role to a pattern template</span></span>
<span data-ttu-id="e2195-151">An entity role is denoted as `{entity:role}` with the entity name followed by a colon, then the role name.</span><span class="sxs-lookup"><span data-stu-id="e2195-151">An entity role is denoted as `{entity:role}` with the entity name followed by a colon, then the role name.</span></span> <span data-ttu-id="e2195-152">To add an entity with a role into the pattern template, surround the entity name and role name with curly braces, such as `Book a ticket from {Location:Origin} to {Location:Destination}`.</span><span class="sxs-lookup"><span data-stu-id="e2195-152">To add an entity with a role into the pattern template, surround the entity name and role name with curly braces, such as `Book a ticket from {Location:Origin} to {Location:Destination}`.</span></span> 

```
Book a ticket from {Location:Origin} to {Location:Destination}
```

### <a name="syntax-to-add-a-patternany-to-pattern-template"></a><span data-ttu-id="e2195-153">Syntax to add a pattern.any to pattern template</span><span class="sxs-lookup"><span data-stu-id="e2195-153">Syntax to add a pattern.any to pattern template</span></span>
<span data-ttu-id="e2195-154">The Pattern.any entity allows you to add an entity of varying length to the pattern.</span><span class="sxs-lookup"><span data-stu-id="e2195-154">The Pattern.any entity allows you to add an entity of varying length to the pattern.</span></span> <span data-ttu-id="e2195-155">As long as the pattern template is followed, the pattern.any can be any length.</span><span class="sxs-lookup"><span data-stu-id="e2195-155">As long as the pattern template is followed, the pattern.any can be any length.</span></span> 

<span data-ttu-id="e2195-156">To add a **Pattern.any** entity into the pattern template, surround the Pattern.any entity with the curly braces, such as `How much does {Booktitle} cost and what format is it available in?`.</span><span class="sxs-lookup"><span data-stu-id="e2195-156">To add a **Pattern.any** entity into the pattern template, surround the Pattern.any entity with the curly braces, such as `How much does {Booktitle} cost and what format is it available in?`.</span></span>  

```
How much does {Booktitle} cost and what format is it available in?
```

|<span data-ttu-id="e2195-157">Book titles in the pattern</span><span class="sxs-lookup"><span data-stu-id="e2195-157">Book titles in the pattern</span></span>|
|--|
|<span data-ttu-id="e2195-158">How much does **steal this book** cost and what format is it available in?</span><span class="sxs-lookup"><span data-stu-id="e2195-158">How much does **steal this book** cost and what format is it available in?</span></span>|
|<span data-ttu-id="e2195-159">How much does **ask** cost and what format is it available in?</span><span class="sxs-lookup"><span data-stu-id="e2195-159">How much does **ask** cost and what format is it available in?</span></span>|
|<span data-ttu-id="e2195-160">How much does **The Curious Incident of the Dog in the Night-Time** cost and what format is it available in?</span><span class="sxs-lookup"><span data-stu-id="e2195-160">How much does **The Curious Incident of the Dog in the Night-Time** cost and what format is it available in?</span></span>| 

<span data-ttu-id="e2195-161">In these book title examples, the contextual words of the book title are not confusing to LUIS.</span><span class="sxs-lookup"><span data-stu-id="e2195-161">In these book title examples, the contextual words of the book title are not confusing to LUIS.</span></span> <span data-ttu-id="e2195-162">LUIS knows where the book title ends because it is in a pattern and marked with a Pattern.any entity.</span><span class="sxs-lookup"><span data-stu-id="e2195-162">LUIS knows where the book title ends because it is in a pattern and marked with a Pattern.any entity.</span></span>

### <a name="explicit-lists"></a><span data-ttu-id="e2195-163">Explicit lists</span><span class="sxs-lookup"><span data-stu-id="e2195-163">Explicit lists</span></span>
<span data-ttu-id="e2195-164">If your pattern contains a Pattern.any, and the pattern syntax allows for the possibility of an incorrect entity extraction based on the utterance, create an [Explicit List](https://aka.ms/ExplicitList) through the authoring API to allow the exception.</span><span class="sxs-lookup"><span data-stu-id="e2195-164">If your pattern contains a Pattern.any, and the pattern syntax allows for the possibility of an incorrect entity extraction based on the utterance, create an [Explicit List](https://aka.ms/ExplicitList) through the authoring API to allow the exception.</span></span> 

<span data-ttu-id="e2195-165">For example, suppose you have a pattern containing both optional syntax, `[]`, and entity syntax, `{}`, combined in a way to extract data incorrectly.</span><span class="sxs-lookup"><span data-stu-id="e2195-165">For example, suppose you have a pattern containing both optional syntax, `[]`, and entity syntax, `{}`, combined in a way to extract data incorrectly.</span></span>

<span data-ttu-id="e2195-166">Consider the pattern \`[find] email about {subject} [from {person}]'.</span><span class="sxs-lookup"><span data-stu-id="e2195-166">Consider the pattern \`[find] email about {subject} [from {person}]'.</span></span> <span data-ttu-id="e2195-167">In the following utterances, the **subject** and **person** entity are extracted correctly and incorrectly:</span><span class="sxs-lookup"><span data-stu-id="e2195-167">In the following utterances, the **subject** and **person** entity are extracted correctly and incorrectly:</span></span>

|<span data-ttu-id="e2195-168">Utterance</span><span class="sxs-lookup"><span data-stu-id="e2195-168">Utterance</span></span>|<span data-ttu-id="e2195-169">Entity</span><span class="sxs-lookup"><span data-stu-id="e2195-169">Entity</span></span>|<span data-ttu-id="e2195-170">Correct extraction</span><span class="sxs-lookup"><span data-stu-id="e2195-170">Correct extraction</span></span>|
|--|--|:--:|
|<span data-ttu-id="e2195-171">email about dogs from Chris</span><span class="sxs-lookup"><span data-stu-id="e2195-171">email about dogs from Chris</span></span>|<span data-ttu-id="e2195-172">subject=dogs</span><span class="sxs-lookup"><span data-stu-id="e2195-172">subject=dogs</span></span><br><span data-ttu-id="e2195-173">person=Chris</span><span class="sxs-lookup"><span data-stu-id="e2195-173">person=Chris</span></span>|<span data-ttu-id="e2195-174">✔</span><span class="sxs-lookup"><span data-stu-id="e2195-174">✔</span></span>|
|<span data-ttu-id="e2195-175">email about the man from La Mancha</span><span class="sxs-lookup"><span data-stu-id="e2195-175">email about the man from La Mancha</span></span>|<span data-ttu-id="e2195-176">subject=the man</span><span class="sxs-lookup"><span data-stu-id="e2195-176">subject=the man</span></span><br><span data-ttu-id="e2195-177">person=La Mancha</span><span class="sxs-lookup"><span data-stu-id="e2195-177">person=La Mancha</span></span>|<span data-ttu-id="e2195-178">X</span><span class="sxs-lookup"><span data-stu-id="e2195-178">X</span></span>|

<span data-ttu-id="e2195-179">In the preceding table, the utterance `email about the man from La Mancha`, the subject should be `the man from La Mancha` (a book title) but because the subject includes the optional word `from`, the title is incorrectly predicted.</span><span class="sxs-lookup"><span data-stu-id="e2195-179">In the preceding table, the utterance `email about the man from La Mancha`, the subject should be `the man from La Mancha` (a book title) but because the subject includes the optional word `from`, the title is incorrectly predicted.</span></span> 

<span data-ttu-id="e2195-180">To fix this exception to the pattern, add `the man from la mancha` as an explicit list match for the {subject} entity using the [authoring API for explicit list](https://aka.ms/ExplicitList).</span><span class="sxs-lookup"><span data-stu-id="e2195-180">To fix this exception to the pattern, add `the man from la mancha` as an explicit list match for the {subject} entity using the [authoring API for explicit list](https://aka.ms/ExplicitList).</span></span>

### <a name="syntax-to-mark-optional-text-in-a-template-utterance"></a><span data-ttu-id="e2195-181">Syntax to mark optional text in a template utterance</span><span class="sxs-lookup"><span data-stu-id="e2195-181">Syntax to mark optional text in a template utterance</span></span>
<span data-ttu-id="e2195-182">Mark optional text in the utterance using the regular expression square bracket syntax, `[]`.</span><span class="sxs-lookup"><span data-stu-id="e2195-182">Mark optional text in the utterance using the regular expression square bracket syntax, `[]`.</span></span> <span data-ttu-id="e2195-183">The optional text can nest square brackets up to two brackets only.</span><span class="sxs-lookup"><span data-stu-id="e2195-183">The optional text can nest square brackets up to two brackets only.</span></span>

```
[find] email about {subject} [from {person}]
```

<span data-ttu-id="e2195-184">Punctuation marks such as `.`, `!`, and `?` can be ignored using the square brackets.</span><span class="sxs-lookup"><span data-stu-id="e2195-184">Punctuation marks such as `.`, `!`, and `?` can be ignored using the square brackets.</span></span> <span data-ttu-id="e2195-185">In order to ignore these marks, each mark must be in a separate pattern.</span><span class="sxs-lookup"><span data-stu-id="e2195-185">In order to ignore these marks, each mark must be in a separate pattern.</span></span> <span data-ttu-id="e2195-186">The optional syntax doesn't currently support ignoring an item in a list of several items.</span><span class="sxs-lookup"><span data-stu-id="e2195-186">The optional syntax doesn't currently support ignoring an item in a list of several items.</span></span>

## <a name="patterns-only"></a><span data-ttu-id="e2195-187">Patterns only</span><span class="sxs-lookup"><span data-stu-id="e2195-187">Patterns only</span></span>
<span data-ttu-id="e2195-188">LUIS allows an app without any example utterances in intent.</span><span class="sxs-lookup"><span data-stu-id="e2195-188">LUIS allows an app without any example utterances in intent.</span></span> <span data-ttu-id="e2195-189">This usage is allowed only if patterns are used.</span><span class="sxs-lookup"><span data-stu-id="e2195-189">This usage is allowed only if patterns are used.</span></span> <span data-ttu-id="e2195-190">Patterns require at least one entity in each pattern.</span><span class="sxs-lookup"><span data-stu-id="e2195-190">Patterns require at least one entity in each pattern.</span></span> <span data-ttu-id="e2195-191">For a pattern-only app, the pattern should not contain machine-learned entities because these do require example utterances.</span><span class="sxs-lookup"><span data-stu-id="e2195-191">For a pattern-only app, the pattern should not contain machine-learned entities because these do require example utterances.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="e2195-192">Best practices</span><span class="sxs-lookup"><span data-stu-id="e2195-192">Best practices</span></span>
<span data-ttu-id="e2195-193">Learn [best practices](luis-concept-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e2195-193">Learn [best practices](luis-concept-best-practices.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2195-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2195-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2195-195">Learn how to implement patterns in this tutorial</span><span class="sxs-lookup"><span data-stu-id="e2195-195">Learn how to implement patterns in this tutorial</span></span>](luis-tutorial-pattern.md)