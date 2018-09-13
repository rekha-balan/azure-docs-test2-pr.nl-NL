---
title: Machine Learning - Azure Cognitive Services | Microsoft Docs
description: A tutorial for machine learning in Azure Custom Decision Service, a cloud-based API for contextual decision-making.
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/08/2018
ms.author: slivkins;marcozo;alekh
ms.openlocfilehash: 50814d67ee39c6657954610358462d877843416e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857398"
---
# <a name="machine-learning"></a><span data-ttu-id="ac4ee-103">Machine learning</span><span class="sxs-lookup"><span data-stu-id="ac4ee-103">Machine learning</span></span>

<span data-ttu-id="ac4ee-104">This tutorial addresses the advanced machine learning functionality in Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-104">This tutorial addresses the advanced machine learning functionality in Custom Decision Service.</span></span> <span data-ttu-id="ac4ee-105">The tutorial consists of two parts: [featurization](#featurization-concepts-and-implementation) and [feature specification](#feature-specification-format-and-apis).</span><span class="sxs-lookup"><span data-stu-id="ac4ee-105">The tutorial consists of two parts: [featurization](#featurization-concepts-and-implementation) and [feature specification](#feature-specification-format-and-apis).</span></span> <span data-ttu-id="ac4ee-106">Featurization refers to representing your data as "features" for machine learning.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-106">Featurization refers to representing your data as "features" for machine learning.</span></span> <span data-ttu-id="ac4ee-107">Feature specification covers the JSON format and the ancillary APIs for specifying features.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-107">Feature specification covers the JSON format and the ancillary APIs for specifying features.</span></span>

<span data-ttu-id="ac4ee-108">By default, machine learning in Custom Decision Service is transparent to the customer.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-108">By default, machine learning in Custom Decision Service is transparent to the customer.</span></span> <span data-ttu-id="ac4ee-109">Features are automatically extracted from your content, and a standard reinforcement learning algorithm is used.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-109">Features are automatically extracted from your content, and a standard reinforcement learning algorithm is used.</span></span> <span data-ttu-id="ac4ee-110">Feature extraction leverages several other Azure Cognitive Services: [Entity Linking](../entitylinking/home.md), [Text Analytics](../text-analytics/overview.md), [Emotion](../emotion/home.md), and [Computer Vision](../computer-vision/home.md).</span><span class="sxs-lookup"><span data-stu-id="ac4ee-110">Feature extraction leverages several other Azure Cognitive Services: [Entity Linking](../entitylinking/home.md), [Text Analytics](../text-analytics/overview.md), [Emotion](../emotion/home.md), and [Computer Vision](../computer-vision/home.md).</span></span> <span data-ttu-id="ac4ee-111">This tutorial can be skipped if only the default functionality is used.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-111">This tutorial can be skipped if only the default functionality is used.</span></span>

## <a name="featurization-concepts-and-implementation"></a><span data-ttu-id="ac4ee-112">Featurization: concepts and implementation</span><span class="sxs-lookup"><span data-stu-id="ac4ee-112">Featurization: concepts and implementation</span></span>

<span data-ttu-id="ac4ee-113">Custom Decision Service makes decisions one by one.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-113">Custom Decision Service makes decisions one by one.</span></span> <span data-ttu-id="ac4ee-114">Each decision involves choosing among several alternatives, a.k.a., actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-114">Each decision involves choosing among several alternatives, a.k.a., actions.</span></span> <span data-ttu-id="ac4ee-115">Depending on the application, the decision may choose a single action or a (short) ranked list of actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-115">Depending on the application, the decision may choose a single action or a (short) ranked list of actions.</span></span>

<span data-ttu-id="ac4ee-116">For instance, personalizing the selection of articles on the front page of a website.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-116">For instance, personalizing the selection of articles on the front page of a website.</span></span> <span data-ttu-id="ac4ee-117">Here, actions correspond to articles, and each decision is which articles to show to a given user.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-117">Here, actions correspond to articles, and each decision is which articles to show to a given user.</span></span>

<span data-ttu-id="ac4ee-118">Each action is represented by a vector of properties, henceforth called *features*.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-118">Each action is represented by a vector of properties, henceforth called *features*.</span></span> <span data-ttu-id="ac4ee-119">You can specify new features, in addition to the features extracted automatically.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-119">You can specify new features, in addition to the features extracted automatically.</span></span> <span data-ttu-id="ac4ee-120">You can also instruct Custom Decision Service to log some features, but ignore them for machine learning.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-120">You can also instruct Custom Decision Service to log some features, but ignore them for machine learning.</span></span>

### <a name="native-vs-internal-features"></a><span data-ttu-id="ac4ee-121">Native vs. internal features</span><span class="sxs-lookup"><span data-stu-id="ac4ee-121">Native vs. internal features</span></span>

<span data-ttu-id="ac4ee-122">You can specify features in a format most natural for your application, be it a number, a string, or an array.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-122">You can specify features in a format most natural for your application, be it a number, a string, or an array.</span></span> <span data-ttu-id="ac4ee-123">These features are called "native features."</span><span class="sxs-lookup"><span data-stu-id="ac4ee-123">These features are called "native features."</span></span> <span data-ttu-id="ac4ee-124">Custom Decision Service translates each native feature into one or more numeric features, called "internal features."</span><span class="sxs-lookup"><span data-stu-id="ac4ee-124">Custom Decision Service translates each native feature into one or more numeric features, called "internal features."</span></span>

<span data-ttu-id="ac4ee-125">The translation into internal features is as follows:</span><span class="sxs-lookup"><span data-stu-id="ac4ee-125">The translation into internal features is as follows:</span></span>

- <span data-ttu-id="ac4ee-126">numeric features stay the same.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-126">numeric features stay the same.</span></span>
- <span data-ttu-id="ac4ee-127">a numeric array translates to several numeric features, one for each element of the array.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-127">a numeric array translates to several numeric features, one for each element of the array.</span></span>
- <span data-ttu-id="ac4ee-128">a string-valued feature `"Name":"Value"` is by default translated into a feature with name `"NameValue"` and value 1.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-128">a string-valued feature `"Name":"Value"` is by default translated into a feature with name `"NameValue"` and value 1.</span></span>
- <span data-ttu-id="ac4ee-129">Optionally, a string can be represented as [bag-of-words](https://en.wikipedia.org/wiki/Bag-of-words_model).</span><span class="sxs-lookup"><span data-stu-id="ac4ee-129">Optionally, a string can be represented as [bag-of-words](https://en.wikipedia.org/wiki/Bag-of-words_model).</span></span> <span data-ttu-id="ac4ee-130">Then an internal feature is created for each word in the string, whose value is the number of occurrences of this word.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-130">Then an internal feature is created for each word in the string, whose value is the number of occurrences of this word.</span></span>
- <span data-ttu-id="ac4ee-131">Zero-valued internal features are omitted.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-131">Zero-valued internal features are omitted.</span></span>

### <a name="shared-vs-action-dependent-features"></a><span data-ttu-id="ac4ee-132">Shared vs. action-dependent features</span><span class="sxs-lookup"><span data-stu-id="ac4ee-132">Shared vs. action-dependent features</span></span>

<span data-ttu-id="ac4ee-133">Some features refer to the entire decision, and are the same for all actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-133">Some features refer to the entire decision, and are the same for all actions.</span></span> <span data-ttu-id="ac4ee-134">We call them *shared features*.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-134">We call them *shared features*.</span></span> <span data-ttu-id="ac4ee-135">Some other features are specific to a particular action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-135">Some other features are specific to a particular action.</span></span> <span data-ttu-id="ac4ee-136">We call them *action-dependent features* (ADFs).</span><span class="sxs-lookup"><span data-stu-id="ac4ee-136">We call them *action-dependent features* (ADFs).</span></span>

<span data-ttu-id="ac4ee-137">In the running example, shared features could describe the user and/or the state of the world.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-137">In the running example, shared features could describe the user and/or the state of the world.</span></span> <span data-ttu-id="ac4ee-138">Features like geolocation, age and gender of the user, and which major events are happening right now.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-138">Features like geolocation, age and gender of the user, and which major events are happening right now.</span></span> <span data-ttu-id="ac4ee-139">Action-dependent features could describe the properties of a given article, such as the topics covered by this article.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-139">Action-dependent features could describe the properties of a given article, such as the topics covered by this article.</span></span>

### <a name="interacting-features"></a><span data-ttu-id="ac4ee-140">Interacting features</span><span class="sxs-lookup"><span data-stu-id="ac4ee-140">Interacting features</span></span>

<span data-ttu-id="ac4ee-141">Features often "interact": the effect of one depends on others.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-141">Features often "interact": the effect of one depends on others.</span></span> <span data-ttu-id="ac4ee-142">For example, feature X is whether the user is interested in sports.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-142">For example, feature X is whether the user is interested in sports.</span></span> <span data-ttu-id="ac4ee-143">Feature Y is whether a given article is about sports.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-143">Feature Y is whether a given article is about sports.</span></span> <span data-ttu-id="ac4ee-144">Then the effect of feature Y is highly dependent on feature X.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-144">Then the effect of feature Y is highly dependent on feature X.</span></span>

<span data-ttu-id="ac4ee-145">To account for interaction between features X and Y, create a *quadratic* feature whose value is X\*Y.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-145">To account for interaction between features X and Y, create a *quadratic* feature whose value is X\*Y.</span></span> <span data-ttu-id="ac4ee-146">(We also say, "cross" X and Y.) You can choose which pairs of features are crossed.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-146">(We also say, "cross" X and Y.) You can choose which pairs of features are crossed.</span></span>

> [!TIP]
> <span data-ttu-id="ac4ee-147">A shared feature should be crossed with action-dependent features in order to influence their rank.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-147">A shared feature should be crossed with action-dependent features in order to influence their rank.</span></span> <span data-ttu-id="ac4ee-148">An action-dependent feature should be crossed with shared features in order to contribute to personalization.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-148">An action-dependent feature should be crossed with shared features in order to contribute to personalization.</span></span>

<span data-ttu-id="ac4ee-149">In other words, a shared feature not crossed with any ADFs influences each action in the same way.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-149">In other words, a shared feature not crossed with any ADFs influences each action in the same way.</span></span> <span data-ttu-id="ac4ee-150">An ADF not crossed with any shared feature influences each decision too.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-150">An ADF not crossed with any shared feature influences each decision too.</span></span> <span data-ttu-id="ac4ee-151">These types of features may reduce the variance of reward estimates.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-151">These types of features may reduce the variance of reward estimates.</span></span>

### <a name="implementation-via-namespaces"></a><span data-ttu-id="ac4ee-152">Implementation via namespaces</span><span class="sxs-lookup"><span data-stu-id="ac4ee-152">Implementation via namespaces</span></span>

<span data-ttu-id="ac4ee-153">You can implement crossed features (as well as other featurization concepts) via the "VW command line" on the Portal.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-153">You can implement crossed features (as well as other featurization concepts) via the "VW command line" on the Portal.</span></span> <span data-ttu-id="ac4ee-154">The syntax is based on the [Vowpal Wabbit](http://hunch.net/~vw/) command line.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-154">The syntax is based on the [Vowpal Wabbit](http://hunch.net/~vw/) command line.</span></span>

<span data-ttu-id="ac4ee-155">Central to the implementation is the concept of *namespace*: a named subset of features.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-155">Central to the implementation is the concept of *namespace*: a named subset of features.</span></span> <span data-ttu-id="ac4ee-156">Each feature belongs to exactly one namespace.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-156">Each feature belongs to exactly one namespace.</span></span> <span data-ttu-id="ac4ee-157">The namespace can be specified explicitly when the feature value is provided to Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-157">The namespace can be specified explicitly when the feature value is provided to Custom Decision Service.</span></span> <span data-ttu-id="ac4ee-158">It is the only way to refer to a feature in the VW command line.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-158">It is the only way to refer to a feature in the VW command line.</span></span>

<span data-ttu-id="ac4ee-159">A namespace is either "shared" or "action-dependent": either it consists only of shared features, or it consists only of action-dependent features of the same action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-159">A namespace is either "shared" or "action-dependent": either it consists only of shared features, or it consists only of action-dependent features of the same action.</span></span>

> [!TIP]
> <span data-ttu-id="ac4ee-160">It is a good practice to wrap features in explicitly specified namespaces.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-160">It is a good practice to wrap features in explicitly specified namespaces.</span></span> <span data-ttu-id="ac4ee-161">Group related features in the same namespace.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-161">Group related features in the same namespace.</span></span>

<span data-ttu-id="ac4ee-162">If the namespace is not provided, the feature is automatically assigned to the default namespace.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-162">If the namespace is not provided, the feature is automatically assigned to the default namespace.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac4ee-163">Features and namespaces do not need to be consistent across actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-163">Features and namespaces do not need to be consistent across actions.</span></span> <span data-ttu-id="ac4ee-164">In particular, a namespace can have different features for different actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-164">In particular, a namespace can have different features for different actions.</span></span> <span data-ttu-id="ac4ee-165">Moreover, a given namespace can be defined for some actions and not for some others.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-165">Moreover, a given namespace can be defined for some actions and not for some others.</span></span>

<span data-ttu-id="ac4ee-166">Multiple internal features that came from the same string-valued native feature are grouped into the same namespace.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-166">Multiple internal features that came from the same string-valued native feature are grouped into the same namespace.</span></span> <span data-ttu-id="ac4ee-167">Any two native features that lie in different namespaces are treated as distinct, even if they have the same feature name.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-167">Any two native features that lie in different namespaces are treated as distinct, even if they have the same feature name.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac4ee-168">While long, descriptive namespace IDs are common, the VW command line does not distinguish between namespaces whose id starts with the same letter.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-168">While long, descriptive namespace IDs are common, the VW command line does not distinguish between namespaces whose id starts with the same letter.</span></span> <span data-ttu-id="ac4ee-169">In what follows, namespace IDs are single letters, such as `x` and `y`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-169">In what follows, namespace IDs are single letters, such as `x` and `y`.</span></span>

<span data-ttu-id="ac4ee-170">The implementation details are as follows:</span><span class="sxs-lookup"><span data-stu-id="ac4ee-170">The implementation details are as follows:</span></span>

- <span data-ttu-id="ac4ee-171">To cross namespaces `x` and `y`, write `-q xy` or `--quadratic xy`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-171">To cross namespaces `x` and `y`, write `-q xy` or `--quadratic xy`.</span></span> <span data-ttu-id="ac4ee-172">Then each feature in `x` is crossed with each feature in `y`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-172">Then each feature in `x` is crossed with each feature in `y`.</span></span> <span data-ttu-id="ac4ee-173">Use `-q x:` to cross `x` with every namespace, and `-q ::` to cross all pairs of namespaces.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-173">Use `-q x:` to cross `x` with every namespace, and `-q ::` to cross all pairs of namespaces.</span></span>

- <span data-ttu-id="ac4ee-174">To ignore all features in namespace `x`, write `--ignore x`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-174">To ignore all features in namespace `x`, write `--ignore x`.</span></span>

<span data-ttu-id="ac4ee-175">These commands are applied to each action separately, whenever the namespaces are defined.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-175">These commands are applied to each action separately, whenever the namespaces are defined.</span></span>

### <a name="estimated-average-as-a-feature"></a><span data-ttu-id="ac4ee-176">Estimated average as a feature</span><span class="sxs-lookup"><span data-stu-id="ac4ee-176">Estimated average as a feature</span></span>

<span data-ttu-id="ac4ee-177">As a thought experiment, what would be the average reward of a given action if it were chosen for all decisions?</span><span class="sxs-lookup"><span data-stu-id="ac4ee-177">As a thought experiment, what would be the average reward of a given action if it were chosen for all decisions?</span></span> <span data-ttu-id="ac4ee-178">Such average reward could be used as a measure of the "overall quality" of this action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-178">Such average reward could be used as a measure of the "overall quality" of this action.</span></span> <span data-ttu-id="ac4ee-179">It is not known exactly whenever other actions have been chosen instead in some decisions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-179">It is not known exactly whenever other actions have been chosen instead in some decisions.</span></span> <span data-ttu-id="ac4ee-180">However, it can be estimated via reinforcement learning techniques.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-180">However, it can be estimated via reinforcement learning techniques.</span></span> <span data-ttu-id="ac4ee-181">The quality of this estimate typically improves over time.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-181">The quality of this estimate typically improves over time.</span></span>

<span data-ttu-id="ac4ee-182">You can choose to include this "estimated average reward" as a feature for a given action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-182">You can choose to include this "estimated average reward" as a feature for a given action.</span></span> <span data-ttu-id="ac4ee-183">Then Custom Decision Service would automatically update this estimate as new data arrives.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-183">Then Custom Decision Service would automatically update this estimate as new data arrives.</span></span> <span data-ttu-id="ac4ee-184">This feature is called the *marginal feature* of this action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-184">This feature is called the *marginal feature* of this action.</span></span> <span data-ttu-id="ac4ee-185">Marginal features can be used for machine learning and for audit.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-185">Marginal features can be used for machine learning and for audit.</span></span>

<span data-ttu-id="ac4ee-186">To add marginal features, write `--marginal <namespace>` in the VW command line.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-186">To add marginal features, write `--marginal <namespace>` in the VW command line.</span></span> <span data-ttu-id="ac4ee-187">Define `<namespace>` in JSON as follows:</span><span class="sxs-lookup"><span data-stu-id="ac4ee-187">Define `<namespace>` in JSON as follows:</span></span>

```json
{<namespace>: {"mf_name":1 "action_id":1}
```

<span data-ttu-id="ac4ee-188">Insert this namespace along with other action-dependent features of a given action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-188">Insert this namespace along with other action-dependent features of a given action.</span></span> <span data-ttu-id="ac4ee-189">Provide this definition for each decision, using the same `mf_name` and `action_id` for all decisions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-189">Provide this definition for each decision, using the same `mf_name` and `action_id` for all decisions.</span></span>

<span data-ttu-id="ac4ee-190">The marginal feature is added for each action with `<namespace>`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-190">The marginal feature is added for each action with `<namespace>`.</span></span> <span data-ttu-id="ac4ee-191">The `action_id` can be any feature name that uniquely identifies the action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-191">The `action_id` can be any feature name that uniquely identifies the action.</span></span> <span data-ttu-id="ac4ee-192">The feature name is set to `mf_name`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-192">The feature name is set to `mf_name`.</span></span> <span data-ttu-id="ac4ee-193">In particular, marginal features with different `mf_name` are treated as different features — a different weight is learned for each `mf_name`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-193">In particular, marginal features with different `mf_name` are treated as different features — a different weight is learned for each `mf_name`.</span></span>

<span data-ttu-id="ac4ee-194">The default usage is that `mf_name` is the same for all actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-194">The default usage is that `mf_name` is the same for all actions.</span></span> <span data-ttu-id="ac4ee-195">Then one weight is learned for all marginal features.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-195">Then one weight is learned for all marginal features.</span></span>

<span data-ttu-id="ac4ee-196">You can also specify multiple marginal features for the same action, with same values but different feature names.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-196">You can also specify multiple marginal features for the same action, with same values but different feature names.</span></span>

```json
{<namespace>: {"mf_name1":1 "action_id":1 "mf_name2":1 "action_id":1}}
```

### <a name="1-hot-encoding"></a><span data-ttu-id="ac4ee-197">1-hot encoding</span><span class="sxs-lookup"><span data-stu-id="ac4ee-197">1-hot encoding</span></span>

<span data-ttu-id="ac4ee-198">You can choose to represent some features as bit vectors, where each bit corresponds to a range of possible values.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-198">You can choose to represent some features as bit vectors, where each bit corresponds to a range of possible values.</span></span> <span data-ttu-id="ac4ee-199">This bit is set to 1 if and only if the feature lies in this range.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-199">This bit is set to 1 if and only if the feature lies in this range.</span></span> <span data-ttu-id="ac4ee-200">Thus, there is one "hot" bit that is set to 1, and the others are set to 0.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-200">Thus, there is one "hot" bit that is set to 1, and the others are set to 0.</span></span> <span data-ttu-id="ac4ee-201">This representation is commonly known as *1-hot encoding*.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-201">This representation is commonly known as *1-hot encoding*.</span></span>

<span data-ttu-id="ac4ee-202">The 1-hot encoding is typical for categorical features such as "geographical region" that do not have an inherently meaningful numerical representation.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-202">The 1-hot encoding is typical for categorical features such as "geographical region" that do not have an inherently meaningful numerical representation.</span></span> <span data-ttu-id="ac4ee-203">It is also advisable for numerical features whose influence on the reward is likely to be non-linear.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-203">It is also advisable for numerical features whose influence on the reward is likely to be non-linear.</span></span> <span data-ttu-id="ac4ee-204">For example, a given article could be relevant to a particular age group, and irrelevant to anyone older or younger.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-204">For example, a given article could be relevant to a particular age group, and irrelevant to anyone older or younger.</span></span>

<span data-ttu-id="ac4ee-205">Any string-valued feature is 1-hot encoded by default: a distinct internal feature is created for every possible value.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-205">Any string-valued feature is 1-hot encoded by default: a distinct internal feature is created for every possible value.</span></span> <span data-ttu-id="ac4ee-206">Automatic 1-hot encoding for numerical features and/or with customized ranges are not currently provided.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-206">Automatic 1-hot encoding for numerical features and/or with customized ranges are not currently provided.</span></span>

> [!TIP]
> <span data-ttu-id="ac4ee-207">The machine learning algorithms treat all possible values of a given internal feature in a uniform way: via a common "weight."</span><span class="sxs-lookup"><span data-stu-id="ac4ee-207">The machine learning algorithms treat all possible values of a given internal feature in a uniform way: via a common "weight."</span></span> <span data-ttu-id="ac4ee-208">The 1-hot encoding allows a separate "weight" for each range of values.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-208">The 1-hot encoding allows a separate "weight" for each range of values.</span></span> <span data-ttu-id="ac4ee-209">Making the ranges smaller leads to better rewards once enough data is collected, but may increase the amount of data needed to converge to better rewards.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-209">Making the ranges smaller leads to better rewards once enough data is collected, but may increase the amount of data needed to converge to better rewards.</span></span>

## <a name="feature-specification-format-and-apis"></a><span data-ttu-id="ac4ee-210">Feature specification: format and APIs</span><span class="sxs-lookup"><span data-stu-id="ac4ee-210">Feature specification: format and APIs</span></span>

<span data-ttu-id="ac4ee-211">You can specify features via several ancillary APIs.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-211">You can specify features via several ancillary APIs.</span></span> <span data-ttu-id="ac4ee-212">All APIs use a common JSON format.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-212">All APIs use a common JSON format.</span></span> <span data-ttu-id="ac4ee-213">Below are the APIs and the format on a conceptual level.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-213">Below are the APIs and the format on a conceptual level.</span></span> <span data-ttu-id="ac4ee-214">The specification is complemented by a Swagger schema.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-214">The specification is complemented by a Swagger schema.</span></span>

<span data-ttu-id="ac4ee-215">The basic JSON template for feature specification is as follows:</span><span class="sxs-lookup"><span data-stu-id="ac4ee-215">The basic JSON template for feature specification is as follows:</span></span>

```json
{
"<name>":<value>, "<name>":<value>, ... ,
"namespace1": {"<name>":<value>, ... },
"namespace2": {"<name>":<value>, ... },
...
}
```

<span data-ttu-id="ac4ee-216">Here `<name>` and `<value>` stand for feature name and feature value, respectively.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-216">Here `<name>` and `<value>` stand for feature name and feature value, respectively.</span></span> <span data-ttu-id="ac4ee-217">`<value>` can be a string, an integer, a float, a boolean, or an array.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-217">`<value>` can be a string, an integer, a float, a boolean, or an array.</span></span> <span data-ttu-id="ac4ee-218">A feature not wrapped into a namespace is automatically assigned into the default namespace.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-218">A feature not wrapped into a namespace is automatically assigned into the default namespace.</span></span>

<span data-ttu-id="ac4ee-219">To represent a string as a bag-of-words, use a special syntax `"_text":"string"` instead of `"<name>":<value>`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-219">To represent a string as a bag-of-words, use a special syntax `"_text":"string"` instead of `"<name>":<value>`.</span></span> <span data-ttu-id="ac4ee-220">Effectively, a separate internal feature is created for each word in the string.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-220">Effectively, a separate internal feature is created for each word in the string.</span></span> <span data-ttu-id="ac4ee-221">Its value is the number of occurrences of this word.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-221">Its value is the number of occurrences of this word.</span></span>

<span data-ttu-id="ac4ee-222">If `<name>` starts with "_" (and is not `"_text"`), then the feature is ignored.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-222">If `<name>` starts with "_" (and is not `"_text"`), then the feature is ignored.</span></span>

> [!TIP]
> <span data-ttu-id="ac4ee-223">Sometimes you merge features from multiple JSON sources.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-223">Sometimes you merge features from multiple JSON sources.</span></span> <span data-ttu-id="ac4ee-224">For convenience, you can represent them as follows:</span><span class="sxs-lookup"><span data-stu-id="ac4ee-224">For convenience, you can represent them as follows:</span></span>
>
> ```json
> {
> "source1":<features>,
> "source2":<features>,
> ...
> }
> ```

<span data-ttu-id="ac4ee-225">Here `<features>` refers to the basic feature specification defined previously.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-225">Here `<features>` refers to the basic feature specification defined previously.</span></span> <span data-ttu-id="ac4ee-226">Deeper levels of "nesting" are allowed, too.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-226">Deeper levels of "nesting" are allowed, too.</span></span> <span data-ttu-id="ac4ee-227">Custom Decision Service automatically finds the "deepest" JSON objects that can be interpreted as `<features>`.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-227">Custom Decision Service automatically finds the "deepest" JSON objects that can be interpreted as `<features>`.</span></span>

#### <a name="feature-set-api"></a><span data-ttu-id="ac4ee-228">Feature Set API</span><span class="sxs-lookup"><span data-stu-id="ac4ee-228">Feature Set API</span></span>

<span data-ttu-id="ac4ee-229">Feature Set API returns a list of features in the JSON format described previously.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-229">Feature Set API returns a list of features in the JSON format described previously.</span></span> <span data-ttu-id="ac4ee-230">You can use several Feature Set API endpoints.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-230">You can use several Feature Set API endpoints.</span></span> <span data-ttu-id="ac4ee-231">Each endpoint is identified by feature set id and a URL.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-231">Each endpoint is identified by feature set id and a URL.</span></span> <span data-ttu-id="ac4ee-232">The mapping between feature set IDs and URLs is set on the Portal.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-232">The mapping between feature set IDs and URLs is set on the Portal.</span></span>

<span data-ttu-id="ac4ee-233">Call Feature Set API by inserting the corresponding feature set id in the appropriate place in JSON.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-233">Call Feature Set API by inserting the corresponding feature set id in the appropriate place in JSON.</span></span> <span data-ttu-id="ac4ee-234">For action-dependent features, the call is automatically parameterized by the action id. You can specify several feature set IDs for the same action.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-234">For action-dependent features, the call is automatically parameterized by the action id. You can specify several feature set IDs for the same action.</span></span>

#### <a name="action-set-api-json-version"></a><span data-ttu-id="ac4ee-235">Action Set API (JSON version)</span><span class="sxs-lookup"><span data-stu-id="ac4ee-235">Action Set API (JSON version)</span></span>

<span data-ttu-id="ac4ee-236">Action Set API has a version in which actions and features are specified in JSON.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-236">Action Set API has a version in which actions and features are specified in JSON.</span></span> <span data-ttu-id="ac4ee-237">Features can be specified explicitly and/or via Feature Set APIs.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-237">Features can be specified explicitly and/or via Feature Set APIs.</span></span> <span data-ttu-id="ac4ee-238">Shared features can be specified once for all actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-238">Shared features can be specified once for all actions.</span></span>

#### <a name="ranking-api-http-post-call"></a><span data-ttu-id="ac4ee-239">Ranking API (HTTP POST call)</span><span class="sxs-lookup"><span data-stu-id="ac4ee-239">Ranking API (HTTP POST call)</span></span>

<span data-ttu-id="ac4ee-240">Ranking API has a version that uses HTTP POST call.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-240">Ranking API has a version that uses HTTP POST call.</span></span> <span data-ttu-id="ac4ee-241">The body of this call specifies actions and features via a flexible JSON syntax.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-241">The body of this call specifies actions and features via a flexible JSON syntax.</span></span>

<span data-ttu-id="ac4ee-242">Actions can be specified explicitly and/or via action set IDs.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-242">Actions can be specified explicitly and/or via action set IDs.</span></span> <span data-ttu-id="ac4ee-243">Whenever an action set id is encountered, a call to the corresponding Action Set API endpoint is executed.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-243">Whenever an action set id is encountered, a call to the corresponding Action Set API endpoint is executed.</span></span>

<span data-ttu-id="ac4ee-244">As for Action Set API, features can be specified explicitly and/or via Feature Set APIs.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-244">As for Action Set API, features can be specified explicitly and/or via Feature Set APIs.</span></span> <span data-ttu-id="ac4ee-245">Shared features can be specified once for all actions.</span><span class="sxs-lookup"><span data-stu-id="ac4ee-245">Shared features can be specified once for all actions.</span></span>