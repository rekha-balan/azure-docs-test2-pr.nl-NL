---
title: Add conditional logic and start workflows - Azure Logic Apps | Microsoft Docs
description: Control how workflows run in Azure Logic Apps by adding conditional logic, triggers, actions, and parameters.
author: stepsic-microsoft-com
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: stepsic
ms.openlocfilehash: f92c6dee95f5a8785e788a685aed90ff510fb91d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555086"
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="66c7e-103">Use Logic Apps features</span><span class="sxs-lookup"><span data-stu-id="66c7e-103">Use Logic Apps features</span></span>
<span data-ttu-id="66c7e-104">In the [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span><span class="sxs-lookup"><span data-stu-id="66c7e-104">In the [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="66c7e-105">Now you'll build a fuller process with Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="66c7e-105">Now you'll build a fuller process with Azure Logic Apps.</span></span> <span data-ttu-id="66c7e-106">This topic introduces the following new Azure Logic Apps concepts:</span><span class="sxs-lookup"><span data-stu-id="66c7e-106">This topic introduces the following new Azure Logic Apps concepts:</span></span>

* <span data-ttu-id="66c7e-107">Conditional logic, which executes an action only when a certain condition is met.</span><span class="sxs-lookup"><span data-stu-id="66c7e-107">Conditional logic, which executes an action only when a certain condition is met.</span></span>
* <span data-ttu-id="66c7e-108">Code view to edit an existing logic app.</span><span class="sxs-lookup"><span data-stu-id="66c7e-108">Code view to edit an existing logic app.</span></span>
* <span data-ttu-id="66c7e-109">Options for starting a workflow.</span><span class="sxs-lookup"><span data-stu-id="66c7e-109">Options for starting a workflow.</span></span>

<span data-ttu-id="66c7e-110">Before you complete this topic, you should complete the steps in [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="66c7e-110">Before you complete this topic, you should complete the steps in [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="66c7e-111">In the [Azure portal], browse to your logic app and click **Triggers and Actions** in the summary to edit the logic app definition.</span><span class="sxs-lookup"><span data-stu-id="66c7e-111">In the [Azure portal], browse to your logic app and click **Triggers and Actions** in the summary to edit the logic app definition.</span></span>

## <a name="reference-material"></a><span data-ttu-id="66c7e-112">Reference material</span><span class="sxs-lookup"><span data-stu-id="66c7e-112">Reference material</span></span>
<span data-ttu-id="66c7e-113">You may find the following documents useful:</span><span class="sxs-lookup"><span data-stu-id="66c7e-113">You may find the following documents useful:</span></span>

* <span data-ttu-id="66c7e-114">[Management and runtime REST APIs](https://msdn.microsoft.com/library/azure/mt643787.aspx) - including how to invoke Logic apps directly</span><span class="sxs-lookup"><span data-stu-id="66c7e-114">[Management and runtime REST APIs](https://msdn.microsoft.com/library/azure/mt643787.aspx) - including how to invoke Logic apps directly</span></span>
* <span data-ttu-id="66c7e-115">[Language reference](https://msdn.microsoft.com/library/azure/mt643789.aspx) - a comprehensive list of all supported functions/expressions</span><span class="sxs-lookup"><span data-stu-id="66c7e-115">[Language reference](https://msdn.microsoft.com/library/azure/mt643789.aspx) - a comprehensive list of all supported functions/expressions</span></span>
* <span data-ttu-id="66c7e-116">[Trigger and action types](https://msdn.microsoft.com/library/azure/mt643939.aspx) - the different types of actions and the inputs they take</span><span class="sxs-lookup"><span data-stu-id="66c7e-116">[Trigger and action types](https://msdn.microsoft.com/library/azure/mt643939.aspx) - the different types of actions and the inputs they take</span></span>
* <span data-ttu-id="66c7e-117">[Overview of App Service](../app-service/app-service-value-prop-what-is.md) - description of what components to choose when to build a solution</span><span class="sxs-lookup"><span data-stu-id="66c7e-117">[Overview of App Service](../app-service/app-service-value-prop-what-is.md) - description of what components to choose when to build a solution</span></span>

## <a name="add-conditional-logic-to-your-logic-app"></a><span data-ttu-id="66c7e-118">Add conditional logic to your logic app</span><span class="sxs-lookup"><span data-stu-id="66c7e-118">Add conditional logic to your logic app</span></span>

<span data-ttu-id="66c7e-119">Although your logic app's original flow works, we could improve some areas.</span><span class="sxs-lookup"><span data-stu-id="66c7e-119">Although your logic app's original flow works, we could improve some areas.</span></span>

### <a name="conditional"></a><span data-ttu-id="66c7e-120">Conditional</span><span class="sxs-lookup"><span data-stu-id="66c7e-120">Conditional</span></span>

<span data-ttu-id="66c7e-121">Your first logic app might result in you getting too many emails.</span><span class="sxs-lookup"><span data-stu-id="66c7e-121">Your first logic app might result in you getting too many emails.</span></span> <span data-ttu-id="66c7e-122">The following steps add conditional logic so that you receive email only when the tweet comes from someone with a specific number of followers.</span><span class="sxs-lookup"><span data-stu-id="66c7e-122">The following steps add conditional logic so that you receive email only when the tweet comes from someone with a specific number of followers.</span></span>

0. <span data-ttu-id="66c7e-123">In the Logic App Designer, choose **New Step** (+) > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-123">In the Logic App Designer, choose **New Step** (+) > **Add an action**.</span></span>
0.  <span data-ttu-id="66c7e-124">Find and add the **Get User** action for Twitter.</span><span class="sxs-lookup"><span data-stu-id="66c7e-124">Find and add the **Get User** action for Twitter.</span></span>
0. <span data-ttu-id="66c7e-125">To get the information about the Twitter user, find and add the **Tweeted by** field from the trigger.</span><span class="sxs-lookup"><span data-stu-id="66c7e-125">To get the information about the Twitter user, find and add the **Tweeted by** field from the trigger.</span></span>

    ![Get user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-use-logic-app-features/getuser.png)

0. <span data-ttu-id="66c7e-127">Choose **New Step** (+) > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-127">Choose **New Step** (+) > **Add a condition**.</span></span>
0. <span data-ttu-id="66c7e-128">To filter on the number of followers that users have, under **Object name**, choose **Add dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-128">To filter on the number of followers that users have, under **Object name**, choose **Add dynamic content**.</span></span> 
0.  <span data-ttu-id="66c7e-129">In the search box, find and add the **Followers count** field.</span><span class="sxs-lookup"><span data-stu-id="66c7e-129">In the search box, find and add the **Followers count** field.</span></span>
0. <span data-ttu-id="66c7e-130">Under **Relationship**, select **is greater than**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-130">Under **Relationship**, select **is greater than**.</span></span>
0. <span data-ttu-id="66c7e-131">In the **Value** box, enter the number of followers you want users to have.</span><span class="sxs-lookup"><span data-stu-id="66c7e-131">In the **Value** box, enter the number of followers you want users to have.</span></span>

    ![Conditional](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-use-logic-app-features/conditional.png)

0. <span data-ttu-id="66c7e-133">Finally, drag the **Send email** box into the **If Yes** box.</span><span class="sxs-lookup"><span data-stu-id="66c7e-133">Finally, drag the **Send email** box into the **If Yes** box.</span></span> 

<span data-ttu-id="66c7e-134">Now you get emails only when the follower count meets your condition.</span><span class="sxs-lookup"><span data-stu-id="66c7e-134">Now you get emails only when the follower count meets your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="66c7e-135">Repeat actions over a list with forEach</span><span class="sxs-lookup"><span data-stu-id="66c7e-135">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="66c7e-136">The forEach loop specifies an array to repeat an action over.</span><span class="sxs-lookup"><span data-stu-id="66c7e-136">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="66c7e-137">If it is not an array, the flow fails.</span><span class="sxs-lookup"><span data-stu-id="66c7e-137">If it is not an array, the flow fails.</span></span> <span data-ttu-id="66c7e-138">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="66c7e-138">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="66c7e-139">Edit the code definition for a logic app</span><span class="sxs-lookup"><span data-stu-id="66c7e-139">Edit the code definition for a logic app</span></span>

<span data-ttu-id="66c7e-140">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span><span class="sxs-lookup"><span data-stu-id="66c7e-140">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="66c7e-141">On the command bar, choose **Code view**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-141">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="66c7e-142">A full editor opens and shows the definition you edited.</span><span class="sxs-lookup"><span data-stu-id="66c7e-142">A full editor opens and shows the definition you edited.</span></span>

    ![Code view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="66c7e-144">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span><span class="sxs-lookup"><span data-stu-id="66c7e-144">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="66c7e-145">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span><span class="sxs-lookup"><span data-stu-id="66c7e-145">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="66c7e-146">To save your edits, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-146">To save your edits, choose **Save**.</span></span>

### <a name="parameters"></a><span data-ttu-id="66c7e-147">Parameters</span><span class="sxs-lookup"><span data-stu-id="66c7e-147">Parameters</span></span>

<span data-ttu-id="66c7e-148">Some Logic Apps capabilities are available only in code view, for example, parameters.</span><span class="sxs-lookup"><span data-stu-id="66c7e-148">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="66c7e-149">Parameters make it easy to reuse values throughout your logic app.</span><span class="sxs-lookup"><span data-stu-id="66c7e-149">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="66c7e-150">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span><span class="sxs-lookup"><span data-stu-id="66c7e-150">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="66c7e-151">Parameters are good for pulling out values that you are likely to change a lot.</span><span class="sxs-lookup"><span data-stu-id="66c7e-151">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="66c7e-152">They are especially useful when you need to override parameters in different environments.</span><span class="sxs-lookup"><span data-stu-id="66c7e-152">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="66c7e-153">To learn how to override parameters based on environment, see the [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="66c7e-153">To learn how to override parameters based on environment, see the [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="66c7e-154">This example shows how to update your existing logic app so that you can use parameters for the query term.</span><span class="sxs-lookup"><span data-stu-id="66c7e-154">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="66c7e-155">In code view, find the `parameters : {}` object, and add a topic object:</span><span class="sxs-lookup"><span data-stu-id="66c7e-155">In code view, find the `parameters : {}` object, and add a topic object:</span></span>

        "topic" : {
            "type" : "string",
            "defaultValue" : "MicrosoftAzure"
        }

2. <span data-ttu-id="66c7e-156">Go to the `twitterconnector` action, find the query value, and replace that value with `#@{parameters('topic')}`.</span><span class="sxs-lookup"><span data-stu-id="66c7e-156">Go to the `twitterconnector` action, find the query value, and replace that value with `#@{parameters('topic')}`.</span></span> 

    <span data-ttu-id="66c7e-157">To join two or more strings, you can also use the `concat` function.</span><span class="sxs-lookup"><span data-stu-id="66c7e-157">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="66c7e-158">For example,    `@concat('#',parameters('topic'))` works the same as the above.</span><span class="sxs-lookup"><span data-stu-id="66c7e-158">For example,    `@concat('#',parameters('topic'))` works the same as the above.</span></span>

3.  <span data-ttu-id="66c7e-159">When you're done, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="66c7e-159">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="66c7e-160">Now every hour, you get new tweets that have more than five retweets delivered to a folder called **tweets** in your Dropbox.</span><span class="sxs-lookup"><span data-stu-id="66c7e-160">Now every hour, you get new tweets that have more than five retweets delivered to a folder called **tweets** in your Dropbox.</span></span>

<span data-ttu-id="66c7e-161">To learn more about Logic App definitions, see [author Logic App definitions](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="66c7e-161">To learn more about Logic App definitions, see [author Logic App definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="66c7e-162">Start logic app workflows</span><span class="sxs-lookup"><span data-stu-id="66c7e-162">Start logic app workflows</span></span>

<span data-ttu-id="66c7e-163">You have different options for starting the workflow defined in your logic app.</span><span class="sxs-lookup"><span data-stu-id="66c7e-163">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="66c7e-164">You can always start a workflow on-demand in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="66c7e-164">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="66c7e-165">Recurrence triggers</span><span class="sxs-lookup"><span data-stu-id="66c7e-165">Recurrence triggers</span></span>

<span data-ttu-id="66c7e-166">A recurrence trigger runs at an interval that you specify.</span><span class="sxs-lookup"><span data-stu-id="66c7e-166">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="66c7e-167">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span><span class="sxs-lookup"><span data-stu-id="66c7e-167">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="66c7e-168">A trigger indicates the workflow should run by returning a `200` status code.</span><span class="sxs-lookup"><span data-stu-id="66c7e-168">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="66c7e-169">When the workflow doesn't need to run, the trigger returns a `202` status code.</span><span class="sxs-lookup"><span data-stu-id="66c7e-169">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="66c7e-170">Callback using REST APIs</span><span class="sxs-lookup"><span data-stu-id="66c7e-170">Callback using REST APIs</span></span>

<span data-ttu-id="66c7e-171">To start a workflow, services can call a logic app endpoint.</span><span class="sxs-lookup"><span data-stu-id="66c7e-171">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="66c7e-172">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="66c7e-172">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="66c7e-173">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="66c7e-173">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[Azure portal]: https://portal.azure.com



